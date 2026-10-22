# CalcPro — Standard & Scientific Calculator

**A modern, responsive calculator with a complete scientific toolkit — built as one HTML file.**

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](https://developer.mozilla.org/docs/Web/HTML)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-38BDF8?style=flat-square&logo=tailwindcss&logoColor=white)](https://tailwindcss.com)
[![JavaScript](https://img.shields.io/badge/Vanilla_JS-F7DF1E?style=flat-square&logo=javascript&logoColor=111111)](https://developer.mozilla.org/docs/Web/JavaScript)
[![Single file](https://img.shields.io/badge/Single_file-index.html-22D3EE?style=flat-square)](#project-structure)
[![Responsive](https://img.shields.io/badge/Responsive-320px%2B-6366F1?style=flat-square)](#browser-support)
[![MIT License](https://img.shields.io/badge/License-MIT-34D399?style=flat-square)](LICENSE)

[Live Demo](https://maryammumtaz-piaic.github.io/calcpro-calculator/) · [Features](#features) · [Usage](#usage) · [Supported functions](#supported-functions) · [Run locally](#run-locally) · [License](#license)

---

## Overview

**CalcPro** is a fast, private, dependency-free calculator that lives in a single `index.html` file. It combines an everyday **Standard** keypad with a full **Scientific** workspace: trigonometry with DEG/RAD support, powers, roots, logarithms, factorials, constants, memory, and a persistent history panel.

The math is powered by a purpose-built tokenizer and recursive-descent parser — **no `eval()` and no third-party math library** — so operator precedence, parentheses, implicit multiplication, percentages, and domain errors behave correctly.

The same file is also a responsive landing page, making it easy to publish, embed, or use as a starting point for your own project.

> हर गणना, एक ही जगह — सटीक, तेज़ और हर स्क्रीन के लिए।

---

## Features

- **Two calculators in one** — switch between Standard and Scientific without losing your expression.
- **Full scientific toolkit** — trig and inverse trig, powers, square/cube roots, natural and base-10 logarithms, arbitrary-base logs, factorial, absolute value, `exp`, `10^x`, `e^x`, `π`, `e`, and `Ans`.
- **Correct math engine** — tokenizer + recursive-descent parser with proper precedence, right-associative powers, unary operators, implicit multiplication, and smart percentages.
- **DEG / RAD toggle** — affects all trigonometric and inverse-trigonometric functions. The active unit is always visible.
- **Clear display states** — expression line, live result preview, error messages, mode label, angle badge, and memory indicator.
- **Memory controls** — `MC`, `MR`, `M+`, `M−`, `MS` with toast feedback.
- **History** — the last 50 calculations are saved locally; click any entry to restore its expression.
- **Keyboard-first support** — type the whole expression, press `Enter` to solve, `Backspace` to fix, `Esc` to clear, `↑` to recall history.
- **Smart percentages** — `50 + 10% = 55` and `200 − 10% = 180`; elsewhere `10%` is `0.10`.
- **Auto-closing parentheses** — unmatched opening parentheses are closed automatically when you press `=`.
- **Precision-aware display** — up to 12 significant digits, exponential notation for extreme values, and no floating-point noise (`0.1 + 0.2` shows `0.3`).
- **100% local & private** — no backend, no analytics, no network calls for calculations. Memory and history stay in `localStorage`.
- **Responsive and accessible** — works from 320 px phones to desktops; semantic buttons, ARIA labels, focus rings, live-region announcements, and reduced-motion support.
- **Reusable engine** — `window.CalcPro` exposes `evaluate()`, `format()`, `setAngleMode()`, and `getAngleMode()` for use in your own scripts.
- **Zero build step** — no framework, no bundler, no package install.

---

## Live demo

**https://maryammumtaz-piaic.github.io/calcpro-calculator/**

The demo is deployed from the `main` branch with GitHub Pages.

---

## Supported functions

### Core operators

| Syntax | Meaning | Example |
| --- | --- | --- |
| `+` `−` `×` `÷` | Addition, subtraction, multiplication, division | `12 ÷ 4 = 3` |
| `^` | Power (right-associative) | `2^10 = 1024` |
| `( )` | Grouping / precedence | `(2 + 3) × 4 = 20` |
| `!` | Factorial (non-negative integers, up to 170) | `5! = 120` |
| `%` | Percent; smart in `+` / `−` | `50 + 10% = 55` |
| `mod` | Modulo | `10 mod 3 = 1` |
| `1/x` | Reciprocal | `1/x` on `8` → `0.125` |

### Trigonometry

| Function | Description | Example (DEG) |
| --- | --- | --- |
| `sin(x)` | Sine | `sin(30) = 0.5` |
| `cos(x)` | Cosine | `cos(60) = 0.5` |
| `tan(x)` | Tangent | `tan(45) = 1` |
| `asin(x)` | Inverse sine | `asin(0.5) = 30` |
| `acos(x)` | Inverse cosine | `acos(0.5) = 60` |
| `atan(x)` | Inverse tangent | `atan(1) = 45` |
| `sinh`, `cosh`, `tanh` | Hyperbolic functions | `sinh(0) = 0` |
| `asinh`, `acosh`, `atanh` | Inverse hyperbolic functions | `asinh(0) = 0` |

Switch to **RAD** for radian input: `sin(π ÷ 2) = 1`.

### Powers, roots and logarithms

| Function | Description | Example |
| --- | --- | --- |
| `x²` | Square | `9² = 81` |
| `√(x)` / `sqrt(x)` | Square root | `√(144) = 12` |
| `∛(x)` / `cbrt(x)` | Cube root | `∛(27) = 3` |
| `ln(x)` | Natural logarithm | `ln(e) = 1` |
| `log(x)` | Base-10 logarithm | `log(1000) = 3` |
| `log(base, x)` | Logarithm with any base | `log(2, 8) = 3` |
| `10^x` | Power of ten | `10^3 = 1000` |
| `e^x` / `exp(x)` | Exponential | `e^1 = 2.71828182846` |

### Constants and helpers

| Syntax | Meaning |
| --- | --- |
| `π` / `pi` | Pi (3.14159265359…) |
| `e` | Euler's number (2.71828182846…) |
| `tau` | 2π |
| `ans` | Previous committed answer |
| `abs(x)` | Absolute value |
| `floor(x)`, `ceil(x)`, `round(x)`, `sign(x)` | Rounding and sign helpers |
| `1.5E3` | Scientific notation (`1500`) |

### Implicit multiplication

These all work without typing `×`:

```text
2π                 → 6.28318530718
3(4 + 1)           → 15
(1 + 2)(3 + 4)     → 21
2sin(30)           → 1        (DEG)
sin(30)cos(60)     → 0.25     (DEG)
```

---

## Run locally

### Option 1 — open the file

Download or clone the repository, then open `index.html` in any modern browser.

```bash
git clone https://github.com/MaryamMumtaz-piaic/calcpro-calculator.git
cd calcpro-calculator
```

### Option 2 — serve it (recommended)

A local server keeps `localStorage` and the Clipboard API in a normal secure context.

```bash
# Python
python -m http.server 8000

# or Node.js
npx serve .
```

Then visit **http://localhost:8000**.

> An internet connection is needed the first time the page loads Tailwind CSS and Google Fonts from their CDNs. All calculator logic runs locally.

---

## Usage

1. Choose **Standard** or **Scientific** at the top of the calculator.
2. Select **DEG** or **RAD** before using trigonometry.
3. Build an expression with the keypad or your keyboard — the result previews live.
4. Press **=** / **Enter** to commit the result. It is added to history.
5. Click a history row to load that expression again, or click the result to copy it.

### Keyboard shortcuts

| Key | Action |
| --- | --- |
| `0`–`9`, `.` | Enter numbers and decimals |
| `+` `-` `*` `/` | Basic operators |
| `^` `%` `!` | Power, percent, factorial |
| `(` `)` | Parentheses |
| `Enter` or `=` | Evaluate |
| `Backspace` | Delete the last input (whole function names such as `sin(` are removed together) |
| `Esc` or `Delete` | Clear everything |
| `↑` | Load the most recent history item |

### Memory

| Button | Action |
| --- | --- |
| `MS` | Store the current value |
| `MR` | Recall the stored value into the expression |
| `M+` | Add the current value to memory |
| `M−` | Subtract the current value from memory |
| `MC` | Clear memory |

### History and privacy

History, memory, the selected mode, and the angle unit are stored in your browser under the `calcpro:v1` key. Nothing is uploaded. Clearing browser site data resets the calculator.

---

## How it works

The calculator does **not** evaluate strings as JavaScript.

1. **Tokenize** — the input is normalized (`×`→`*`, `÷`→`/`, `−`→`-`, `π`→`pi`, `√`→`sqrt`, `∛`→`cbrt`) and split into numbers, identifiers, operators, parentheses, and commas.
2. **Parse** — a recursive-descent parser builds an AST with the precedence hierarchy `+ −` → `* / mod` → unary → `^` (right-associative) → postfix `! %`.
3. **Evaluate** — the AST is walked with domain checks, degree/radian conversion, factorial handling, and smart-percentage logic.
4. **Format** — results are rounded to 12 significant digits for display; extreme values use exponential notation.

This architecture makes the engine easy to test, extend, and reuse independently of the UI:

```js
CalcPro.setAngleMode('DEG');
CalcPro.format(CalcPro.evaluate('sin(30) + log(2, 8)')); // "3.5"
CalcPro.format(CalcPro.evaluate('2^10'));                // "1024"
CalcPro.evaluate('1 / 0');                               // throws: Division by zero
```

### Why `Ans` does not change during preview

Live previews call the engine with `{ commit: false }`, so typing `ans + 1` shows a preview without overwriting the previous answer. `Ans` updates only when you press `=`.

---

## Project structure

```text
calcpro-calculator/
├── index.html      # The entire application: markup, Tailwind config, CSS, math engine and UI
├── README.md       # This document
├── PROMPT.md       # Reusable AI coding-agent prompt used to build the project
├── LICENSE         # MIT license
└── .gitignore      # OS, editor, log and dependency ignores
```

---

## Customization

Everything is in `index.html`:

- **Brand and links** — search for `CalcPro`, `MaryamMumtaz-piaic`, and the GitHub URLs.
- **Colors and fonts** — edit the `tailwind.config` block in `<head>` and the custom properties/classes in `<style>`.
- **Default mode and angle** — change `mode: 'scientific'` and `angle: 'DEG'` in the `state` object.
- **History limit** — change the `slice(0, 50)` calls in the UI controller.
- **Storage key** — change `const STORAGE_KEY = 'calcpro:v1'`.
- **Math engine** — the engine is a self-contained section at the top of the main script. It can be extracted into its own module if you outgrow the single-file constraint.

### Deploying to GitHub Pages

1. Push the repository to GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**.
4. Select `main` and `/ (root)`, then save.
5. The site is published at `https://<username>.github.io/<repository>/`.

---

## Browser support

CalcPro targets modern evergreen browsers:

- Chrome / Edge 90+
- Firefox 90+
- Safari 15+

It uses modern JavaScript (`??`, optional chaining, `Object.freeze`) and CSS (`backdrop-filter`, `mask-image`, CSS grid). Older browsers degrade gracefully but may lose some visual polish.

---

## Contributing

Contributions are welcome. To keep the project true to its purpose:

1. Fork the repository and create a feature branch.
2. Keep the app in a **single `index.html`** file — no build step, no frameworks.
3. Do not introduce `eval()` or a math library.
4. Verify the expressions in [Supported functions](#supported-functions) still produce the documented results.
5. Open a pull request describing the change and the reasoning behind it.

Bug reports and feature requests are welcome in [Issues](https://github.com/MaryamMumtaz-piaic/calcpro-calculator/issues).

---

## License

Released under the [MIT License](LICENSE).

```text
MIT © 2026 Maryam Mumtaz
```

You are free to use, modify, and distribute this project, including commercially, provided the copyright notice and permission notice are retained.

---

## Acknowledgements

- [Tailwind CSS](https://tailwindcss.com) — utility-first styling.
- [Google Fonts](https://fonts.google.com) — Inter and JetBrains Mono.
- [Shields.io](https://shields.io) — README badges.
- Built from the reusable prompt in [`PROMPT.md`](PROMPT.md).

---

**If CalcPro is useful to you, consider giving the repository a star.**
