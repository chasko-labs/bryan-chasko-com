---
title: "design system v2 — prototypes"
date: 2026-04-27
draft: false
tags: ["design", "frontend", "prototypes"]
description: "six chromatic shadow + surface depth explorations adapted from cloud-del-norte structural patterns into the nebula violet/indigo/orange palette. review surface before any site-wide lift."
---

<style>
/* ── demo well — showcase container ──────────────────── */
.demo-well {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 360px;
  padding: var(--space-2xl, 3rem);
  margin: var(--space-xl, 2rem) 0;
  border: 1px solid var(--color-border);
  border-radius: var(--radius-xl);
  background: color-mix(in srgb, var(--color-background) 92%, var(--brand-purple) 8%);
  box-shadow: inset 0 1px 4px rgba(0, 0, 0, 0.06);
}

[data-theme="dark"] .demo-well {
  background: color-mix(in srgb, var(--color-background) 85%, var(--brand-lavender) 15%);
  box-shadow: inset 0 1px 4px rgba(0, 0, 0, 0.20);
}

/* ── chromatic shadow comparison row inside a demo well */
.demo-well-compare {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: var(--space-xl, 2rem);
  width: 100%;
  align-items: start;
  justify-items: center;
}

/* ── section heading accent rule ─────────────────────── */
.proto-section-heading {
  font-size: clamp(1.75rem, 4vw, 2.5rem);
  font-weight: 700;
  line-height: 1.1;
  color: var(--color-text);
  margin-bottom: var(--space-xs, 0.5rem);
  padding-bottom: var(--space-sm, 0.75rem);
  border-bottom: 2px solid var(--brand-purple);
}

.proto-section-subtitle {
  font-size: var(--font-size-sm);
  color: var(--color-text-secondary);
  margin-bottom: 0;
  margin-top: 0;
}

/* ── details / summary collapse ──────────────────────── */
.proto-details {
  margin-top: var(--space-md, 1rem);
}

.proto-details summary {
  font-family: var(--font-mono);
  font-size: var(--font-size-xs);
  color: var(--color-text-secondary);
  letter-spacing: 0.04em;
  cursor: pointer;
  user-select: none;
}

.proto-details summary:hover {
  color: var(--color-text);
}

.proto-details .proto-details-body {
  margin-top: var(--space-sm, 0.75rem);
  font-size: var(--font-size-sm);
  color: var(--color-text-secondary);
  line-height: var(--line-height-base);
}

/* ── section gap ──────────────────────────────────────── */
.proto-section {
  margin-bottom: var(--space-3xl, 4rem);
}

/* ── prototype layout helpers ─────────────────────── */
.proto-compare-row {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: var(--space-xl);
  margin-bottom: var(--space-xl);
}

.proto-single-row {
  display: flex;
  flex-wrap: wrap;
  gap: var(--space-md);
  margin-bottom: var(--space-xl);
}

.proto-figure {
  display: flex;
  flex-direction: column;
  gap: var(--space-md);
  margin: 0;
}

.proto-label {
  font-family: var(--font-mono);
  font-size: var(--font-size-xs);
  color: var(--color-text-secondary);
  letter-spacing: 0.04em;
}

.proto-label code {
  background: transparent;
  padding: 0;
  color: var(--nebula-lavender);
  font-size: inherit;
}

/* ── base card shell — shared ─────────────────────── */
.proto-card {
  max-width: 380px;
  padding: var(--space-lg);
  border-radius: var(--radius-xl);
  border: 1px solid var(--color-border);
  display: flex;
  flex-direction: column;
  gap: var(--space-sm);
  position: relative;
  overflow: hidden;
}

.proto-card strong {
  font-size: var(--font-size-lg);
  color: var(--color-text);
}

.proto-card p {
  font-size: var(--font-size-sm);
  color: var(--color-text-secondary);
  line-height: var(--line-height-base);
  margin: 0;
}

.proto-card .proto-card-link {
  font-family: var(--font-mono);
  font-size: var(--font-size-sm);
  color: var(--nebula-lavender);
  text-decoration: none;
  margin-top: var(--space-xs);
}

.proto-card .proto-card-link:hover {
  color: var(--nebula-orange);
}

/* ── prototype a — current black shadow ───────────── */
.proto-card-black-shadow {
  background: var(--color-background-secondary);
  box-shadow: var(--shadow-md);
}

/* ── prototype a — chromatic violet 3-layer shadow ── */
.proto-card-chromatic {
  background: var(--color-background-secondary);
  box-shadow:
    0 1px 2px rgba(94, 65, 162, 0.06),
    0 8px 24px rgba(94, 65, 162, 0.10),
    0 2px 6px rgba(0, 0, 0, 0.04);
}

[data-theme="dark"] .proto-card-chromatic {
  box-shadow:
    0 1px 2px rgba(129, 105, 197, 0.10),
    0 8px 24px rgba(129, 105, 197, 0.18),
    0 2px 6px rgba(0, 0, 0, 0.20);
}

/* ── prototype b — multi-layer gradient surface ───── */
.proto-card-gradient-surface {
  background: linear-gradient(
    135deg,
    var(--color-background-secondary) 0%,
    color-mix(in srgb, var(--color-background-secondary) 92%, var(--brand-purple) 8%) 50%,
    var(--color-background-secondary) 100%
  );
  box-shadow:
    0 1px 2px rgba(94, 65, 162, 0.06),
    0 8px 24px rgba(94, 65, 162, 0.10),
    0 2px 6px rgba(0, 0, 0, 0.04);
}

[data-theme="dark"] .proto-card-gradient-surface {
  background: linear-gradient(
    135deg,
    var(--color-background-secondary) 0%,
    color-mix(in srgb, var(--color-background-secondary) 90%, var(--brand-lavender) 10%) 50%,
    var(--color-background-secondary) 100%
  );
  box-shadow:
    0 1px 2px rgba(129, 105, 197, 0.10),
    0 8px 24px rgba(129, 105, 197, 0.18),
    0 2px 6px rgba(0, 0, 0, 0.20);
}

/* ── prototype c — spring-hover lift ─────────────── */
.proto-card-spring {
  background: var(--color-background-secondary);
  box-shadow:
    0 1px 2px rgba(94, 65, 162, 0.06),
    0 8px 24px rgba(94, 65, 162, 0.10),
    0 2px 6px rgba(0, 0, 0, 0.04);
}

[data-theme="dark"] .proto-card-spring {
  box-shadow:
    0 1px 2px rgba(129, 105, 197, 0.10),
    0 8px 24px rgba(129, 105, 197, 0.18),
    0 2px 6px rgba(0, 0, 0, 0.20);
}

@media (prefers-reduced-motion: no-preference) {
  .proto-card-spring {
    transition:
      transform var(--duration-base) cubic-bezier(0.22, 1, 0.36, 1),
      box-shadow var(--duration-base) var(--ease-out);
  }

  .proto-card-spring:hover {
    transform: translateY(-3px);
    box-shadow:
      0 2px 4px rgba(94, 65, 162, 0.08),
      0 16px 40px rgba(94, 65, 162, 0.16),
      0 4px 12px rgba(0, 0, 0, 0.06);
  }

  [data-theme="dark"] .proto-card-spring:hover {
    box-shadow:
      0 2px 4px rgba(129, 105, 197, 0.14),
      0 16px 40px rgba(129, 105, 197, 0.26),
      0 4px 12px rgba(0, 0, 0, 0.30);
  }
}

/* ── prototype d — conic-gradient accent edge ─────── */
.proto-card-conic-edge {
  background: var(--color-background-secondary);
  box-shadow:
    0 1px 2px rgba(94, 65, 162, 0.06),
    0 8px 24px rgba(94, 65, 162, 0.10),
    0 2px 6px rgba(0, 0, 0, 0.04);
}

[data-theme="dark"] .proto-card-conic-edge {
  box-shadow:
    0 1px 2px rgba(129, 105, 197, 0.10),
    0 8px 24px rgba(129, 105, 197, 0.18),
    0 2px 6px rgba(0, 0, 0, 0.20);
}

.proto-card-conic-edge::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 3px;
  background: conic-gradient(
    from 90deg at 50% 50%,
    var(--brand-purple),
    var(--brand-orange),
    var(--brand-lavender),
    var(--brand-purple)
  );
  border-radius: var(--radius-xl) var(--radius-xl) 0 0;
}

/* ── prototype e — perspective tilt ──────────────── */
.proto-card-perspective {
  background: var(--color-background-secondary);
  box-shadow:
    0 1px 2px rgba(94, 65, 162, 0.06),
    0 8px 24px rgba(94, 65, 162, 0.10),
    0 2px 6px rgba(0, 0, 0, 0.04);
  transform: perspective(1000px) rotateX(0deg);
}

[data-theme="dark"] .proto-card-perspective {
  box-shadow:
    0 1px 2px rgba(129, 105, 197, 0.10),
    0 8px 24px rgba(129, 105, 197, 0.18),
    0 2px 6px rgba(0, 0, 0, 0.20);
}

@media (prefers-reduced-motion: no-preference) {
  .proto-card-perspective {
    transition:
      transform var(--duration-base) cubic-bezier(0.22, 1, 0.36, 1),
      box-shadow var(--duration-base) var(--ease-out);
  }

  .proto-card-perspective:hover {
    transform: perspective(1000px) rotateX(2deg);
    box-shadow:
      0 2px 4px rgba(94, 65, 162, 0.08),
      0 12px 32px rgba(94, 65, 162, 0.14),
      0 4px 12px rgba(0, 0, 0, 0.06);
  }

  [data-theme="dark"] .proto-card-perspective:hover {
    box-shadow:
      0 2px 4px rgba(129, 105, 197, 0.14),
      0 12px 32px rgba(129, 105, 197, 0.22),
      0 4px 12px rgba(0, 0, 0, 0.30);
  }
}

/* ── prototype f — inset highlight buttons ────────── */
.proto-btn-row {
  display: flex;
  flex-wrap: wrap;
  gap: var(--space-md);
  align-items: center;
  padding: var(--space-lg);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-lg);
  background: var(--color-background-secondary);
  margin-bottom: var(--space-md);
}

.proto-btn-inset {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: var(--space-sm) var(--space-lg);
  font-family: var(--font-body);
  font-size: var(--font-size-sm);
  font-weight: 600;
  border-radius: var(--radius-md);
  cursor: pointer;
  border: none;
  background: var(--brand-purple);
  color: #ffffff;
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.15),
    0 2px 8px rgba(94, 65, 162, 0.20);
}

[data-theme="dark"] .proto-btn-inset {
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.04),
    0 2px 8px rgba(129, 105, 197, 0.30);
}

@media (prefers-reduced-motion: no-preference) {
  .proto-btn-inset {
    transition:
      transform var(--duration-fast) var(--ease-out),
      box-shadow var(--duration-fast) var(--ease-out),
      background var(--duration-fast) var(--ease-out);
  }

  .proto-btn-inset:hover {
    background: var(--brand-lavender);
    transform: translateY(-1px);
    box-shadow:
      inset 0 1px 0 rgba(255, 255, 255, 0.20),
      0 4px 16px rgba(94, 65, 162, 0.30);
  }

  [data-theme="dark"] .proto-btn-inset:hover {
    box-shadow:
      inset 0 1px 0 rgba(255, 255, 255, 0.08),
      0 4px 16px rgba(129, 105, 197, 0.40);
  }
}

.proto-btn-inset:focus-visible {
  outline: var(--focus-ring);
  outline-offset: 3px;
}

.proto-btn-inset-secondary {
  background: var(--color-background-secondary);
  color: var(--brand-purple);
  border: 1px solid rgba(94, 65, 162, 0.25);
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.60),
    0 2px 8px rgba(94, 65, 162, 0.12);
}

[data-theme="dark"] .proto-btn-inset-secondary {
  color: var(--brand-lavender);
  border-color: rgba(129, 105, 197, 0.30);
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.04),
    0 2px 8px rgba(129, 105, 197, 0.20);
}

@media (prefers-reduced-motion: no-preference) {
  .proto-btn-inset-secondary:hover {
    background: var(--color-background);
    border-color: rgba(94, 65, 162, 0.40);
    transform: translateY(-1px);
    box-shadow:
      inset 0 1px 0 rgba(255, 255, 255, 0.70),
      0 4px 16px rgba(94, 65, 162, 0.18);
  }

  [data-theme="dark"] .proto-btn-inset-secondary:hover {
    border-color: rgba(129, 105, 197, 0.50);
    box-shadow:
      inset 0 1px 0 rgba(255, 255, 255, 0.06),
      0 4px 16px rgba(129, 105, 197, 0.30);
  }
}
</style>

these are the patterns from the cloud-del-norte / sumerian-hosts research synthesis. evaluate each in both modes before deciding which to lift site-wide. six prototypes — chromatic shadows, gradient surfaces, spring motion, conic edges, perspective tilt, inset buttons.

---

<div class="proto-section">

## chromatic shadow card

<p class="proto-section-subtitle">side-by-side: current black-channel shadow vs 3-layer violet shadow — does the color channel read as depth or just tint?</p>

<div class="demo-well">
  <div class="demo-well-compare">
    <figure class="proto-figure">
      <figcaption class="proto-label">current — <code>--shadow-md</code></figcaption>
      <article class="proto-card proto-card-black-shadow">
        <strong>service card</strong>
        <p>black-channel shadow — lifts but reads cool/flat against nebula backgrounds</p>
        <a href="#chromatic-shadow-card" class="proto-card-link">learn more →</a>
      </article>
    </figure>
    <figure class="proto-figure">
      <figcaption class="proto-label">prototype — chromatic violet shadow</figcaption>
      <article class="proto-card proto-card-chromatic">
        <strong>service card</strong>
        <p>warm violet channels: ambient diffuse + mid shadow + ambient base. reads as depth rather than silhouette</p>
        <a href="#chromatic-shadow-card" class="proto-card-link">learn more →</a>
      </article>
    </figure>
  </div>
</div>

<details class="proto-details">
  <summary>see notes</summary>
  <div class="proto-details-body">
    3-layer pattern: <code>rgba(94,65,162,0.06)</code> ambient diffuse + <code>rgba(94,65,162,0.10)</code> mid shadow + <code>rgba(0,0,0,0.04)</code> ambient base. dark mode bumps all opacity values — <code>rgba(129,105,197,...)</code> at 0.10 / 0.18 / 0.20. the demo well bg must differ from the card surface for the shadow to read — if they match, the shadow disappears.
  </div>
</details>

</div>

---

<div class="proto-section">

## multi-layer gradient surface

<p class="proto-section-subtitle">color-mix tints the card background with brand-purple at 8% — perceived surface variation without new token declarations</p>

<div class="demo-well">
  <article class="proto-card proto-card-gradient-surface">
    <strong>gradient surface card</strong>
    <p>135deg diagonal — secondary bg to purple-tinted midpoint and back. the tint is subtle in light mode, slightly stronger in dark</p>
    <a href="#multi-layer-gradient-surface" class="proto-card-link">learn more →</a>
  </article>
</div>

<details class="proto-details">
  <summary>see notes</summary>
  <div class="proto-details-body">
    light mode: <code>color-mix(in srgb, var(--color-background-secondary) 92%, var(--brand-purple) 8%)</code> at the 50% stop. dark mode: same pattern with <code>var(--brand-lavender)</code> at 10%. no new token declarations — only existing tokens composed differently. pair with chromatic shadow for maximum surface read.
  </div>
</details>

</div>

---

<div class="proto-section">

## spring-hover lift

<p class="proto-section-subtitle">cubic-bezier(0.22, 1, 0.36, 1) gives physical overshoot on hover — shadow expands as the card lifts</p>

<div class="demo-well">
  <article class="proto-card proto-card-spring">
    <strong>spring lift card</strong>
    <p>hover this card — chromatic shadow expands as the card rises. both light + dark get tuned opacity values</p>
    <a href="#spring-hover-lift" class="proto-card-link">learn more →</a>
  </article>
</div>

<details class="proto-details">
  <summary>see notes</summary>
  <div class="proto-details-body">
    <code>transform: translateY(-3px)</code> on hover. shadow grows from mid-level to <code>0 16px 40px rgba(94,65,162,0.16)</code>. guarded by <code>@media (prefers-reduced-motion: no-preference)</code> — no motion fires for reduced-motion users. dark mode uses the 129,105,197 violet channel at higher opacity to maintain legibility.
  </div>
</details>

</div>

---

<div class="proto-section">

## conic-gradient accent edge

<p class="proto-section-subtitle">3px ::before pseudo on the top edge — purple → orange → lavender → purple loop using existing brand tokens only</p>

<div class="demo-well">
  <article class="proto-card proto-card-conic-edge">
    <strong>accent edge card</strong>
    <p>most portable cloud-del-norte signature adapted to nebula palette. the gradient loops — no hard stops, no new color values</p>
    <a href="#conic-gradient-accent-edge" class="proto-card-link">learn more →</a>
  </article>
</div>

<details class="proto-details">
  <summary>see notes</summary>
  <div class="proto-details-body">
    <code>::before</code> pseudo, <code>height: 3px</code>, <code>position: absolute; top: 0</code>. conic-gradient from 90deg — <code>var(--brand-purple)</code> → <code>var(--brand-orange)</code> → <code>var(--brand-lavender)</code> → <code>var(--brand-purple)</code>. card must have <code>overflow: hidden</code> and matching border-radius on the pseudo. no light/dark override needed — the gradient is always visible regardless of mode.
  </div>
</details>

</div>

---

<div class="proto-section">

## perspective tilt

<p class="proto-section-subtitle">rotateX(2deg) at perspective(1000px) on hover — lightest-touch 3D feel, no babylon.js dependency</p>

<div class="demo-well">
  <article class="proto-card proto-card-perspective">
    <strong>perspective tilt card</strong>
    <p>hover to see the tilt. works in every browser. combines well with chromatic shadow expansion</p>
    <a href="#perspective-tilt" class="proto-card-link">learn more →</a>
  </article>
</div>

<details class="proto-details">
  <summary>see notes</summary>
  <div class="proto-details-body">
    <code>transform: perspective(1000px) rotateX(0deg)</code> on rest state — declares the perspective context. hover applies <code>rotateX(2deg)</code>. 2deg is the minimum perceptible tilt; more reads as novelty rather than depth. guarded by <code>prefers-reduced-motion</code>. shadow stays chromatic on hover — same 3-layer pattern as prototype a, lighter opacity values.
  </div>
</details>

</div>

---

<div class="proto-section">

## inset highlight button

<p class="proto-section-subtitle">inset top-edge shadow catches the light-source reading — both primary (solid purple) and secondary (ghost with border) variants</p>

<div class="demo-well">
  <div>
    <div class="proto-btn-row">
      <button type="button" class="proto-btn-inset">primary action</button>
      <button type="button" class="proto-btn-inset proto-btn-inset-secondary">secondary action</button>
    </div>
  </div>
</div>

<details class="proto-details">
  <summary>see notes</summary>
  <div class="proto-details-body">
    primary: <code>inset 0 1px 0 rgba(255,255,255,0.15)</code> catches light from above. dark mode drops inset to <code>rgba(255,255,255,0.04)</code> — barely perceptible, shadow below carries the depth read. secondary variant: ghost background with <code>rgba(94,65,162,0.25)</code> border + high inset highlight (<code>rgba(255,255,255,0.60)</code> in light mode). hover shifts primary bg from <code>--brand-purple</code> to <code>--brand-lavender</code>. focus-visible ring via <code>var(--focus-ring)</code> with 3px offset.
  </div>
</details>

</div>

---

switch the theme toggle in the nav to compare both modes — the demo-well backgrounds shift between modes, so the contrast read changes for each prototype.
