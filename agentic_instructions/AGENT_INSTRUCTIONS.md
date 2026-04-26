# Agent Instructions: WebGL, CSS, Build & Deploy

Focused technical guide for AI agents working on WebGL effects, CSS architecture, and deployment workflows.

---

## 🎯 Core Principles

1. **Diagnostic First**: Use MCP tools (`file_search`, `grep_search`, `get_errors`, `read_file`) before making changes
2. **Test-Driven**: All WebGL changes must pass visual regression tests (`npm test`) before deployment
3. **No Hardcoding**: Never hardcode AWS credentials, ARNs, bucket names, or distribution IDs
4. **Cache-Aware**: Browser cache is the most common cause of "code not working" — always consider hard refresh

---

## 🌐 WebGL Architecture

### Scene Hierarchy

```
BaseScene.js (foundation)
├── OrbitScene.js       → Builder card animation (3 orbits, teal/green)
├── TransitionScene.js  → Page navigation fade (noise shader)
├── RippleScene.js      → Blog card interaction (ready for integration)
└── SkillsNetworkScene.js → Force-directed graph (ready for integration)

SceneInitializer.js (orchestrator) → Auto-detects data-* attributes and initializes scenes
```

### File Locations

| Purpose | Path |
|---------|------|
| WebGL Source (canonical) | `themes/bryan-chasko-theme/assets/js/webgl-scenes/` |
| WebGL Static (build output) | `themes/bryan-chasko-theme/static/js/webgl-scenes/` |
| Constellation (standalone) | `themes/bryan-chasko-theme/static/js/constellation.js` |
| CSS Variables | `themes/bryan-chasko-theme/assets/css/core/variables.css` |
| Extended Styles | `themes/bryan-chasko-theme/assets/css/extended/nebula.css` |

### DOM Integration Pattern

Each scene uses `data-*` attributes for auto-detection:

```html
<!-- Constellation (home hero) -->
<div class="constellation-hero" data-constellation aria-hidden="true"></div>

<!-- Orbit (builder card) -->
<div class="builder-card" data-orbit-scene></div>

<!-- Skills Network (future) -->
<div class="skills-container" data-skills-network></div>

<!-- Ripple (future) -->
<article class="post-entry" data-ripple></article>
```

### WebGL Color System

Scenes consume CSS variables via `BaseScene.getThemeColor()`:

```javascript
// In scene code
const tealColor = this.getThemeColor('--cosmic-teal');  // Returns RGB object
```

**Active Palette** (defined in `nebula.css`):

```css
--cosmic-teal: #00CED1;      /* Orbit particles */
--cosmic-energy: #00FA9A;    /* Center node */
--cosmic-primary: #5E41A2;   /* Deep purple */
--cosmic-accent: #FF9900;    /* Orange highlights */
```

### ⚠️ Critical: Asset Sync Workflow

Hugo assets pipeline requires manual sync for WebGL changes:

```bash
# 1. Edit ONLY the source (assets/)
nano themes/bryan-chasko-theme/assets/js/webgl-scenes/OrbitScene.js

# 2. Copy to static (required for fast render mode)
cp themes/bryan-chasko-theme/assets/js/webgl-scenes/*.js \
   themes/bryan-chasko-theme/static/js/webgl-scenes/

# 3. Rebuild Hugo
hugo --minify

# 4. Hard refresh browser
# macOS: Cmd+Shift+R | Windows/Linux: Ctrl+Shift+R

# 5. Verify with tests
npm test
```

**Never edit** `static/js/webgl-scenes/` directly — changes are overwritten by Hugo.

### Resize Handling

All scenes support responsive sizing via `onResize()` override:

```javascript
// In OrbitScene.js
onResize() {
  // Recalculate center when canvas dimensions change
  this.centerX = this.options.width / 2;
  this.centerY = this.options.height / 2;
}
```

The resize event flow:

```
window.resize → BaseScene.handleResize() → Update options.width/height → Call this.onResize()
```

---

## 🎨 CSS Architecture

### Directory Structure

```
themes/bryan-chasko-theme/assets/css/
├── core/           # Foundation
│   ├── variables.css    # CSS custom properties (colors, spacing, typography)
│   ├── reset.css        # Browser normalization
│   ├── typography.css   # Font scales, line heights
│   └── utilities.css    # Helper classes
├── common/         # Shared components
│   └── header.css       # Navigation, logo, theme toggle
├── components/     # Reusable elements
│   ├── cards.css        # Post cards, service cards
│   ├── home.css         # Home page layout, builder card, terminal
│   └── social-feed.css  # Social profile heroes, activity feed
├── extended/       # Site-wide overrides
│   ├── nebula.css       # Animated backgrounds, WebGL palettes
│   └── help.css         # Service pages
└── layouts/        # Page-specific styles
```

### Color Variables (3-Palette System)

**1. Core Brand** (identity):

```css
--nebula-purple: #5E41A2;
--nebula-lavender: #8169C5;
--nebula-orange: #FF9900;
```

**2. Vibrant Cosmic** (WebGL):

```css
--cosmic-teal: #00CED1;
--cosmic-energy: #00FA9A;
--cosmic-primary: #5E41A2;
```

**3. Semantic Mappings** (theme-aware):

```css
/* Light mode */
--color-background: var(--white);
--color-text: var(--gray-900);
--color-link: var(--nebula-purple);

/* Dark mode */
[data-theme="dark"] {
  --color-background: var(--nebula-dark-navy);
  --color-text: var(--gray-100);
}
```

### Protected CSS Rules

These rules use `!important` and should not be modified without testing:

| File | Rule | Purpose |
|------|------|---------|
| `header.css` | `.logo img, .logo svg` | Logo sizing (26px height) |
| `header.css` | Mobile nav `@media` | Single-line navigation on mobile |

### Adding New Styles

1. **Component styles** → Create in `components/` directory
2. **Page-specific** → Create in `layouts/` directory
3. **WebGL-related** → Add to `extended/nebula.css`
4. **New CSS variables** → Add to `core/variables.css`

---

## 🔧 Build Process

### Development Server

```bash
hugo server --config hugo.toml
# Runs on http://localhost:1313
# Hot-reloads content/layouts but NOT WebGL assets
```

### Production Build

```bash
hugo --minify
# Outputs to public/ directory
# Minifies HTML, CSS, JS
```

### Build Verification Checklist

```bash
# Check Hugo version (must be 0.152.2+ Extended)
hugo version

# Check Node version (must be 18.0.0+)
node --version

# Verify theme submodule
git submodule status

# Build and verify output
hugo --minify
ls -la public/ | head -20
```

### Common Build Issues

| Issue | Solution |
|-------|----------|
| `module "PaperMod" not found` | Run `git submodule update --init --recursive` |
| CSS not updating | Check `themes/bryan-chasko-theme/assets/css/` and rebuild |
| WebGL not updating | Copy assets→static, rebuild, hard refresh |
| `Raw HTML omitted` warning | Expected behavior (site allows raw HTML in markdown) |

---

## 🚀 Deploy Process

### Deploy Script Location

```bash
scripts/deploy.pl  # Perl script with test gate
```

### Deploy Pipeline Order

```
1. Hugo Build (hugo --minify)
2. WebGL Test Gate (npm test) ← BLOCKS on failure
3. S3 Sync (public/ → bucket)
4. Wait 5 seconds (S3 propagation)
5. CloudFront Invalidation (/* path)
6. Baseline Update (main branch only)
```

### Standard Deploy

```bash
# With test gate (recommended)
perl scripts/deploy.pl --profile websites-bryanchasko --verbose

# Dry run (no AWS calls)
perl scripts/deploy.pl --dry-run --verbose

# Emergency bypass (skip tests - NOT recommended)
perl scripts/deploy.pl --skip-tests --profile websites-bryanchasko
```

### Configuration Priority

The deploy script reads configuration in this order:

1. **Command-line arguments**: `--bucket`, `--domain`, `--distribution-id`
2. **Environment variables**: `SITE_BUCKET`, `SITE_DOMAIN`, `SITE_DISTRIBUTION_ID`
3. **External config file**: `~/.bcc-site/config.json`
4. **AWS Parameter Store**: `/sites/bryanchasko.com/*`
5. **Hugo config inference**: `baseURL` from `hugo.toml`

### AWS Parameter Store Setup

```bash
# Store config in SSM (one-time)
aws ssm put-parameter --name /sites/bryanchasko.com/s3_bucket \
  --type String --value bryanchasko.com --profile websites-bryanchasko

aws ssm put-parameter --name /sites/bryanchasko.com/domain \
  --type String --value bryanchasko.com --profile websites-bryanchasko

aws ssm put-parameter --name /sites/bryanchasko.com/cloudfront_distribution_id \
  --type String --value [YOUR-DISTRIBUTION-ID] --profile websites-bryanchasko

# Deploy using SSM
perl scripts/deploy.pl --profile websites-bryanchasko --param-path /sites/bryanchasko.com
```

---

## 🧪 Testing Infrastructure

### Test Commands

```bash
# Full test suite (all browsers)
npm test

# Single browser
npm run test:chrome
npm run test:firefox
npm run test:webkit

# Update baselines after intentional changes
npm run test:update-baselines

# Debug mode (step through tests)
npm run test:debug
```

### Test Coverage

| Test Type | File | Validates |
|-----------|------|-----------|
| Visual Regression | `tests/webgl/orbit-scene.spec.js` | Screenshot comparison (5% tolerance) |
| Pixel Validation | `tests/webgl/orbit-scene.spec.js` | RGB color extraction from canvas |
| Performance | `tests/webgl/performance.spec.js` | Init time <150ms, FPS >50, memory <200MB |
| Cross-browser | All specs | Chrome, Firefox, Safari consistency |

### Performance Budgets

| Metric | Target | Hardware Baseline |
|--------|--------|-------------------|
| Orbit Init | <150ms | Intel UHD 620 (2020) |
| Steady FPS | >50 fps | Intel UHD 620 (2020) |
| WebGL Memory | <200MB | 8GB RAM system |

### S3 Baseline Storage

- **Bucket**: `bryanchasko-com-webgl-baselines`
- **Region**: `us-west-2`
- **Lifecycle**: 180-day expiration
- **Versioning**: Enabled

### Troubleshooting Tests

**Tests pass locally but fail in CI:**

```javascript
// Relax budget for slower CI runners
const budget = process.env.CI ? 200 : 150;
```

**"No baseline found" error:**

```bash
npm run test:update-baselines
```

**Colors wrong after code change:**

```bash
# Run test to capture actual pixels (ground truth)
npm test -- tests/webgl/orbit-scene.spec.js

# Test output shows actual RGB values
# If test shows wrong colors but browser shows right → code bug
# If test shows right colors but browser shows wrong → cache issue
```

---

## 🔄 GitHub Actions Workflows

### WebGL Tests Workflow

**File**: `.github/workflows/webgl-tests.yml`

**Triggers**: PR to main, push to main, manual dispatch

**Matrix**: Chrome, Firefox, Safari

**Steps**:

1. Checkout code
2. Scan for secrets (security gate)
3. Install Node.js + dependencies
4. Install Playwright browsers
5. Configure AWS credentials
6. Run visual regression tests
7. Upload artifacts (reports, diffs)

### Deploy Workflow

**File**: `.github/workflows/deploy.yml`

**Triggers**: Push to main, manual dispatch

**Steps**:

1. Checkout code
2. Scan for secrets (security gate)
3. Setup Hugo + Node.js
4. Install Playwright browsers
5. **Test Gate** (npm test - blocks on failure)
6. Hugo build
7. S3 sync
8. CloudFront invalidation
9. Baseline update

### Required GitHub Secrets

```
AWS_ACCESS_KEY_ID          # IAM user for S3 access
AWS_SECRET_ACCESS_KEY      # IAM user secret key
```

---

## 🐛 Common Debugging Workflows

### WebGL Scene Not Rendering

```bash
# 1. Check console for initialization logs
# Look for: [SceneInitializer], [OrbitScene], [WebGL]

# 2. Verify DOM hook exists
grep -r "data-orbit-scene" themes/bryan-chasko-theme/layouts/

# 3. Check for WebGL errors
# Browser console → filter for "WebGL" or "shader"

# 4. Verify scene files are loaded
# Network tab → check for OrbitScene.js, BaseScene.js
```

### Colors Wrong in WebGL

```bash
# 1. Verify CSS variable definition
grep "cosmic-teal" themes/bryan-chasko-theme/assets/css/extended/nebula.css

# 2. Check if scene is reading variable
grep "getThemeColor" themes/bryan-chasko-theme/assets/js/webgl-scenes/OrbitScene.js

# 3. Run test to extract actual pixels
npm test -- tests/webgl/orbit-scene.spec.js

# 4. If test passes but browser wrong → hard refresh (cache issue)
```

### CSS Changes Not Appearing

```bash
# 1. Rebuild Hugo
hugo --minify

# 2. Hard refresh browser
# macOS: Cmd+Shift+R | Windows/Linux: Ctrl+Shift+R

# 3. Check file is in correct directory
ls themes/bryan-chasko-theme/assets/css/components/

# 4. Verify import chain
grep -r "home.css" themes/bryan-chasko-theme/
```

### Deploy Failing

```bash
# 1. Check test gate
npm test

# 2. Verify AWS credentials
aws sts get-caller-identity --profile websites-bryanchasko

# 3. Dry run deploy
perl scripts/deploy.pl --dry-run --verbose

# 4. Check CloudFront distribution
aws cloudfront list-distributions --profile websites-bryanchasko
```

---

## 📋 Quick Reference Commands

```bash
# Development
hugo server --config hugo.toml          # Start dev server
hugo --minify                           # Production build

# Testing
npm test                                # Full test suite
npm run test:update-baselines           # Update visual baselines
npm run test:chrome                     # Chrome only

# Deploy
perl scripts/deploy.pl --dry-run --verbose              # Preview
perl scripts/deploy.pl --profile websites-bryanchasko      # Deploy

# WebGL Asset Sync
cp themes/bryan-chasko-theme/assets/js/webgl-scenes/*.js \
   themes/bryan-chasko-theme/static/js/webgl-scenes/

# Submodule Update
git submodule update --init --recursive
```

---

## 📚 Related Documentation

| Document | Purpose |
|----------|---------|
| [WEBGL_ARCHITECTURE.md](WEBGL_ARCHITECTURE.md) | Scene integration, DOM patterns, lifecycle |
| [TESTING.md](TESTING.md) | Test setup, baseline management, CI/CD |
| [RESPONSIVE_ORBIT_FIX.md](RESPONSIVE_ORBIT_FIX.md) | Responsive canvas sizing case study |
| [.github/copilot-instructions.md](.github/copilot-instructions.md) | Full project context |
| [DEPLOYMENT.md](DEPLOYMENT.md) | Deployment workflow, rollback procedures |
| [CI_CD_SETUP.md](CI_CD_SETUP.md) | GitHub Actions configuration |
