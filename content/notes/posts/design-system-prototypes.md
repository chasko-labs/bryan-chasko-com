---
title: "design system v2 — prototypes"
date: 2026-04-27
draft: false
tags: ["design", "frontend", "prototypes"]
description: "six chromatic shadow + surface depth explorations adapted from cloud-del-norte structural patterns into the nebula violet/indigo/orange palette. review surface before any site-wide lift."
ShowToc: true
---

<style>
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

six chromatic shadow + surface depth explorations adapted from cloud-del-norte structural patterns into the nebula violet/indigo/orange palette. intent: find out what reads as depth vs silhouette against dark backgrounds before any site-wide lift into nebula.css

---

## a — chromatic shadow card

side-by-side: current `--shadow-md` (black channel) vs a 3-layer violet shadow. violet channels read as warmth rather than silhouette — the card sits in the plane instead of floating above it

<div class="proto-compare-row">
  <figure class="proto-figure">
    <figcaption class="proto-label">current — <code>--shadow-md</code> (black shadow)</figcaption>
    <article class="proto-card proto-card-black-shadow">
      <strong>service card</strong>
      <p>black-channel shadow — visually lifts but reads cool/flat against nebula backgrounds</p>
      <a href="#a----chromatic-shadow-card" class="proto-card-link">learn more →</a>
    </article>
  </figure>
  <figure class="proto-figure">
    <figcaption class="proto-label">prototype a — chromatic violet shadow (3-layer)</figcaption>
    <article class="proto-card proto-card-chromatic">
      <strong>service card</strong>
      <p>warm violet channels: ambient diffuse + mid shadow + ambient base. reads as depth rather than silhouette. dark mode uses higher opacity rgba values on the same hue</p>
      <a href="#a----chromatic-shadow-card" class="proto-card-link">learn more →</a>
    </article>
  </figure>
</div>

---

## b — multi-layer gradient surface

`color-mix` tints the secondary background with `--brand-purple` at 8% in light mode, `--brand-lavender` at 10% in dark. perceived surface variation without new token values — just existing tokens composed differently

<div class="proto-single-row">
  <article class="proto-card proto-card-gradient-surface">
    <strong>gradient surface card</strong>
    <p>background uses <code>color-mix</code> to tint the secondary background with brand-purple at 8%, creating perceived surface variation without introducing new token values</p>
    <a href="#b----multi-layer-gradient-surface" class="proto-card-link">learn more →</a>
  </article>
</div>

---

## c — spring-hover lift

`cubic-bezier(0.22, 1, 0.36, 1)` gives a physical overshoot feel on hover. the shadow expands as the card lifts. both light + dark get tuned opacity values. guarded by `prefers-reduced-motion`

<div class="proto-single-row">
  <article class="proto-card proto-card-spring">
    <strong>spring lift card</strong>
    <p>hover this card — <code>cubic-bezier(0.22, 1, 0.36, 1)</code> gives a physical overshoot bounce on translate. chromatic shadow expands on lift</p>
    <a href="#c----spring-hover-lift" class="proto-card-link">learn more →</a>
  </article>
</div>

---

## d — conic-gradient accent edge

3px `::before` pseudo on the top edge — purple → orange → lavender → purple loop. portable CDN signature pattern adapted to nebula palette. color-stops are all existing brand tokens, no new values needed

<div class="proto-single-row">
  <article class="proto-card proto-card-conic-edge">
    <strong>accent edge card</strong>
    <p>3px <code>::before</code> conic gradient on top edge — purple → orange → lavender → purple loop. most portable CDN signature adapted to nebula palette</p>
    <a href="#d----conic-gradient-accent-edge" class="proto-card-link">learn more →</a>
  </article>
</div>

---

## e — perspective tilt (featured card)

hover to see `rotateX(2deg)` at `perspective(1000px)`. lightest-touch 3D feel, no babylon.js dependency, universal browser support. guarded by `prefers-reduced-motion`

<div class="proto-single-row">
  <article class="proto-card proto-card-perspective">
    <strong>perspective tilt card</strong>
    <p>hover to see <code>rotateX(2deg)</code> tilt at <code>perspective(1000px)</code> — lightest-touch 3D feel without babylon.js weight. works in every browser</p>
    <a href="#e----perspective-tilt-featured-card" class="proto-card-link">learn more →</a>
  </article>
</div>

---

## f — inset highlight button (light catch)

inset top-edge shadow catches the "light source" reading. chromatic violet shadow below. dark mode drops the inset opacity to `rgba(255,255,255,0.04)` — barely perceptible, but the shadow below does the heavy lifting. both variants: primary (solid purple) + secondary (ghost with border)

<div class="proto-btn-row">
  <button type="button" class="proto-btn-inset">primary action</button>
  <button type="button" class="proto-btn-inset proto-btn-inset-secondary">secondary action</button>
</div>

inset top edge catches "light". chromatic violet shadow below. dark mode uses `rgba(255,255,255,0.04)` inset — barely visible, shadow carries the depth read

---

_self-contained — every rule in this post's inline `<style>` block. ready to lift into nebula.css site-wide once any prototype clears review_
