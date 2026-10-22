# AI Coding Agent Prompt — Build a Single-File Scientific Calculator Website

This is the reusable, production-grade prompt used to build **CalcPro**. Copy everything between the two markers below and paste it into your AI coding agent (Claude, GPT, Gemini, Cursor, Copilot, etc.). Replace the bracketed placeholders if you want a different brand or repository.

---

## ✂️ Prompt starts here

**Role**

You are a senior frontend engineer and product designer. You care about correct mathematics, clean interaction design, accessibility, and code that another developer can read and reuse. You ship working software — not a mockup.

**Mission**

Build a polished, modern, fully responsive calculator website called **CalcPro**. It must have two modes — a **Standard calculator** and a **Scientific calculator** — and it must be delivered as exactly **one self-contained `index.html` file**. The page should work as a landing page, with the calculator as the centerpiece.

**Non-negotiable constraints**

1. Exactly one application file: `index.html`. All HTML, Tailwind CSS configuration, custom CSS, and JavaScript live inside that file.
2. Use **HTML5**, **Tailwind CSS** (CDN is allowed), and **vanilla JavaScript**. No React, Vue, Svelte, jQuery, math libraries, build tools, or package installation.
3. Do **not** use `eval()`, `new Function()`, or `setTimeout("string")`. Build a real expression tokenizer and parser.
4. The page must work when opened directly from disk and when hosted on GitHub Pages.
5. External requests are limited to the Tailwind CDN and Google Fonts. Everything else must be inline.
6. The layout must be responsive from **320 px** upward, with touch targets of at least **40 × 40 px**.
7. The calculator must be reusable: keep the math engine separate from the DOM controller and expose a small public API (`window.CalcPro`) with `evaluate`, `format`, `setAngleMode`, and `getAngleMode`.
8. No placeholder buttons, no dead controls, no broken states. Every visible control must work.

**Landing page requirements**

Create a cohesive, modern page with:

- A fixed, translucent navigation bar with a logo, section links (Calculator, Features, Guide), a GitHub link, and a clear call to action.
- A hero section with a short value proposition, a one-line secondary tagline, two CTAs (“Start calculating” and “View source”), and 3–4 compact stats (modes, functions, responsive, files).
- A calculator section (`id="calculator"`) with a section heading and the working calculator.
- A features section (`id="features"`) with 6 cards, each with an icon, title, and one-sentence benefit.
- A help/guide section (`id="guide"`) that explains how to use the calculator, lists keyboard shortcuts, shows worked examples, and documents the supported syntax.
- A closing CTA and a footer with the license, GitHub, docs, and issues links.
- Decorative background: subtle grid pattern, gradient glow blobs, glassmorphism cards. Keep it tasteful and readable.
- Dark theme with strong contrast and a distinctive two-color accent (for example cyan + indigo). Use a geometric sans font (Inter) and a monospace font (JetBrains Mono) for numbers.
- Smooth scrolling, `scroll-mt` offsets for the fixed header, and a `prefers-reduced-motion` fallback.

**Calculator UI requirements**

- A tabbed mode switcher: **Standard** and **Scientific**. Preserve the current expression when switching.
- A **DEG/RAD** angle toggle that affects every trigonometric function (including inverse trig). Show the active unit in the display and persist it.
- A display area with:
  - the current expression, right-aligned and horizontally scrollable;
  - a large live result preview;
  - a clear error line (for example “Division by zero”);
  - an `M` memory indicator, an angle badge, and the current mode label.
- An **AC** (all clear) key, a **DEL** (backspace) key that removes whole function names such as `sin(`, a **±** sign toggle, a decimal key, and a tall **=** key.
- A memory row: **MC, MR, M+, M−, MS**, with sensible feedback when recalled or stored.
- A history panel showing the last 50 calculations. Clicking an entry restores its expression. Include a clear-history action. Persist history in `localStorage`.
- Keyboard support: digits, `.`, `+`, `-`, `*`, `/`, `^`, `%`, `!`, `(`, `)`; **Enter** or `=` evaluates; **Backspace** deletes; **Esc** clears; **↑** loads the most recent history item. Do not hijack keys when the user is typing in a form control.
- After `=`, pressing an operator should continue from the result; pressing a digit or a new function should start a new expression.
- Auto-close unmatched parentheses when the user evaluates. Show a helpful error for unmatched `)`.
- Toast feedback for copy, memory, and history actions. Clicking the result copies it when the Clipboard API is available.
- Persist memory, history, mode, and angle unit locally. Never send data to a server.

**Scientific function requirements**

Every function below must work correctly and be reachable from the UI (some may also be typed):

- Basic: `+`, `−`, `×`, `÷`, decimals, unary minus, parentheses, `%`, `mod`.
- Powers and roots: `^` (right-associative), square (`x²`), cube, square root (`√`), cube root (`∛`), reciprocal (`1/x`).
- Trigonometry: `sin`, `cos`, `tan` with DEG/RAD handling, plus `sin⁻¹`, `cos⁻¹`, `tan⁻¹`.
- Logarithms: `ln`, `log` (base 10), and `log(base, value)` for any base.
- Other: factorial (`n!`, non-negative integers up to 170), absolute value, `exp`, `10^x`, `e^x`, constants `π` and `e`, and `Ans` for the previous answer.
- Also support typed-only helpers where sensible: `sinh`, `cosh`, `tanh`, `asinh`, `acosh`, `atanh`, `floor`, `ceil`, `round`, `sign`, `tau`, and scientific notation such as `1.5E3`.

**Math engine requirements**

1. Tokenize the input into numbers, identifiers, operators, parentheses, and commas.
2. Normalize display symbols: `×`→`*`, `÷`→`/`, `−`→`-`, `π`→`pi`, `√`→`sqrt`, `∛`→`cbrt`.
3. Parse with recursive descent and correct precedence:
   - `+`/`-` lowest;
   - `*`, `/`, `mod` next;
   - unary `+`/`-`;
   - `^` right-associative;
   - postfix `!` and `%` highest.
4. Support implicit multiplication: `2π`, `3(4+1)`, `(1+2)(3+4)`, `2sin(30)`, `sin(30)cos(60)`.
5. Support smart percentages in addition and subtraction: `50 + 10% = 55`, `200 − 10% = 180`; elsewhere `10%` means `0.10`.
6. Validate domains and produce human-readable errors:
   - division or modulo by zero;
   - `sqrt` of a negative number;
   - `ln`/`log` of non-positive values;
   - `asin`/`acos` outside `[-1, 1]`;
   - `tan` at 90° + k·180° (DEG) or π/2 + k·π (RAD);
   - factorial of a negative or non-integer value;
   - overflow/non-finite results.
7. Round floating-point noise before display: `0.1 + 0.2` must show `0.3`, `sin(30°)` must show `0.5`, and `log(2, 8)` must show `3`. Keep up to 12 significant digits, switch to exponential notation for very large or small values, and never show `NaN`.
8. Cover edge cases: `2^3^2 = 512`, `-2^2 = -4`, `2^-2 = 0.25`, `0! = 1`, `170!` is finite, `171!` errors.
9. Do not mutate `Ans` during live preview. Commit it only when the user presses `=`.

**Acceptance tests**

The finished app must satisfy all of these:

| Expression | Mode | Expected |
| --- | --- | --- |
| `2 + 3 × 4` | any | `14` |
| `(2 + 3) × 4` | any | `20` |
| `10 ÷ 4` | any | `2.5` |
| `0.1 + 0.2` | any | `0.3` |
| `2^10` | any | `1024` |
| `2^3^2` | any | `512` |
| `-2^2` | any | `-4` |
| `√(144)` | any | `12` |
| `∛(27)` | any | `3` |
| `log(1000)` | any | `3` |
| `log(2, 8)` | any | `3` |
| `ln(e)` | any | `1` |
| `sin(30)` | DEG | `0.5` |
| `cos(60)` | DEG | `0.5` |
| `tan(45)` | DEG | `1` |
| `sin⁻¹(0.5)` | DEG | `30` |
| `sin(π ÷ 2)` | RAD | `1` |
| `5!` | any | `120` |
| `50 + 10%` | any | `55` |
| `200 − 10%` | any | `180` |
| `2π` | any | `6.28318530718` |
| `3(4 + 1)` | any | `15` |
| `1 ÷ 0` | any | error, not `Infinity` |
| `√(-1)` | any | error |
| `tan(90)` | DEG | error |
| `log(0)` | any | error |

**Accessibility and quality**

- Use semantic landmarks, real `<button>` elements, `aria-label` on icon-only or symbolic keys, `aria-pressed` on toggles, and `role="tablist"`/`role="tab"` with `aria-selected`.
- Provide visible focus rings and an `aria-live` announcement for results and errors.
- Use `title` or visually hidden text where a symbol is ambiguous.
- Avoid layout shift: reserve space for the expression, result, and error line.
- Keep the console free of errors and warnings from your own code.
- Add `noscript` messaging.
- Ensure the app still looks intentional on a 360 px phone, a tablet, and a desktop.

**Documentation deliverables**

In addition to `index.html`, create:

- `README.md` — project description, live demo link, feature list, supported functions/syntax, quick start, usage, keyboard shortcuts, how the parser works, project structure, customization notes, browser support, contributing, license, and acknowledgements. Use GitHub-flavored Markdown and shields.io badges.
- `LICENSE` — the MIT license with the copyright holder and year.
- `.gitignore` — ignore OS files, editor folders, logs, and dependencies.
- Optionally keep this prompt as `PROMPT.md` so the build is reproducible.

**Definition of done**

The task is complete only when:

- every acceptance test above passes;
- all controls work and no button is decorative;
- the page is responsive at 360 px, 768 px, and 1440 px;
- the code is one `index.html` with no `eval`;
- README, LICENSE, and the repository description are complete;
- the project is committed and pushed to GitHub, and the README explains how to run and deploy it.

## ✂️ Prompt ends here

---

### How to use this prompt

1. Paste the section above into your agent as the task.
2. Tell the agent your repository name and GitHub username if you want it to create and push the repo.
3. Ask it to verify the acceptance tests before committing.
4. Review the diff, then publish. For GitHub Pages: **Settings → Pages → Deploy from a branch → `main` → `/ (root)`**.

The reference implementation of this prompt is this repository's [`index.html`](index.html).
