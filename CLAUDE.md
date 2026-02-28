# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project
Healthspan Concierge Medicine — static website built as a single `index.html` with inline Tailwind CSS.

**Google Drive source:** `GoogleDrive-peter@r12consulting.io/My Drive/Healthspan Concierge Medicine Website/`
Brand assets and reference files live there; copy into `brand_assets/` as needed.

## Always Do First
- Invoke the `frontend-design` skill before writing any frontend code, every session.

## Reference Images
- If a reference image is provided: match layout, spacing, typography, and color exactly. Swap in placeholder content. Do not improve or add to the design.
- If no reference image: design from scratch using the guardrails below.
- Screenshot your output, compare against reference, fix mismatches, re-screenshot. Do at least 2 rounds. Stop only when no visible differences remain or user says so.

## Local Server
- Always serve on localhost — never screenshot a `file:///` URL.
- Start the dev server: `node serve.mjs` (serves project root at `http://localhost:3000`)
- `serve.mjs` lives in the project root. Start it in the background before taking screenshots.
- If the server is already running, do not start a second instance.

## Screenshot Workflow
- `node screenshot.mjs http://localhost:3000` → saves to `./temporary screenshots/screenshot-N.png` (auto-incremented)
- Optional label: `node screenshot.mjs http://localhost:3000 label` → `screenshot-N-label.png`
- After screenshotting, read the PNG with the Read tool to analyze visually.
- Be specific when comparing: "heading is 32px but reference shows ~24px", "card gap is 16px but should be 24px"
- Check: spacing/padding, font size/weight/line-height, colors (exact hex), alignment, border-radius, shadows, image sizing

## Output Defaults
- Single `index.html`, all styles inline unless told otherwise
- Tailwind CSS via CDN: `<script src="https://cdn.tailwindcss.com"></script>`
- Placeholder images: `https://placehold.co/WIDTHxHEIGHT`
- Mobile-first responsive

## Brand Assets
- Check `brand_assets/` before designing. May contain logos, color guides, style guides, or images.
- Use real assets if present — do not use placeholders where real assets exist.
- If a color palette is defined, use those exact values. Do not invent brand colors.

## Anti-Generic Design Guardrails
- **Colors:** Never use default Tailwind palette (no indigo-500, blue-600, etc.). Derive from brand color.
- **Shadows:** Never flat `shadow-md`. Use layered, color-tinted shadows with low opacity.
- **Typography:** Different fonts for headings vs body. Pair display/serif with clean sans. Tight tracking (`-0.03em`) on large headings, generous line-height (`1.7`) on body.
- **Gradients:** Layer multiple radial gradients. Add grain/texture via SVG noise filter for depth.
- **Animations:** Only animate `transform` and `opacity`. Never `transition-all`. Spring-style easing.
- **Interactive states:** Every clickable element needs hover, focus-visible, and active states.
- **Images:** Gradient overlay (`bg-gradient-to-t from-black/60`) + color treatment with `mix-blend-multiply`.
- **Spacing:** Intentional, consistent spacing tokens — not random Tailwind steps.
- **Depth:** Layering system (base → elevated → floating) — not everything at the same z-plane.

## Hard Rules
- Do not add sections, features, or content not in the reference
- Do not "improve" a reference design — match it
- Do not stop after one screenshot pass
- Do not use `transition-all`
- Do not use default Tailwind blue/indigo as primary color
