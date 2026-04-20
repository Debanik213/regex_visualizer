# MathLab: Regular Languages

> An interactive, visual teaching tool for the theory of regular languages — built for students and educators studying formal language theory, automata, and compiler design.

---

## Overview

MathLab is a three-page static web app that makes abstract concepts from formal language theory tangible and explorable. No server, no build step, no dependencies beyond a CDN — just open an HTML file and start learning.

It covers three core areas:

| Page | Purpose |
|---|---|
| `index.html` | Theory reference — alphabets, REs, DFAs/NFAs, Kleene's theorem, and the equivalence verification pipeline |
| `regex.html` | Regex Builder — construct expressions with a palette, generate matching sample strings, and see a live railroad syntax diagram |
| `equivalncechecker.html` | Equivalence Checker — test whether two regular expressions define the same language |

---

## Features

### Theory Page (`index.html`)
- Structured walkthrough of formal definitions: alphabets (Σ), strings, and languages
- Base cases and inductive steps for regular expression construction
- DFA 5-tuple definition and NFA comparison with ε-transition diagram
- Kleene's Theorem statement and explanation
- Four-phase equivalence verification pipeline: Thompson's Construction → Subset Construction → Hopcroft's Algorithm → Structural Isomorphism

### Regex Builder (`regex.html`)
- **Construction palette** — clickable buttons for literals (`a`, `b`, `c`), quantifiers (`*`, `+`, `?`), union (`|`), grouping (`(`, `)`, `[]`), and epsilon (`ε`)
- **Live railroad diagram** — a custom SVG syntax diagram that updates in real-time as you type, showing the structure of your expression with standard railroad notation (terminals, alternation branches, repetition loops)
- **Sample string generator** — generates up to 50 matching strings up to a configurable max length using random sampling against the compiled regex
- Copy-to-clipboard for generated samples

### Equivalence Checker (`equivalncechecker.html`)
- Input two regular expressions and check if they define the same language
- Uses brute-force string enumeration up to a configurable max length over the derived alphabet
- Returns a counterexample string if a difference is found, or confirms equivalence within the checked bounds
- Supports standard regex operators plus math notation (`+` for union, `ε` for empty string)

---

## Railroad Diagram Engine

The railroad diagram renderer in `regex.html` is fully self-contained — no external library required. It works in three stages:

1. **Recursive-descent parser** — reads the regex and builds an AST with node types: `lit`, `class`, `seq`, `alt`, `rep`
2. **Layout pass** — measures width, height, and rail centerline for each subtree bottom-up
3. **SVG draw pass** — emits inline SVG with styled shapes, rail lines, and arcs

Supported constructs in the diagram:

| Construct | Rendering |
|---|---|
| Literal (`a`, `\d`) | Pill-shaped terminal box |
| Character class (`[a-z]`) | Rounded teal box |
| Sequence (`ab`) | Boxes chained on a horizontal rail |
| Alternation (`a\|b`) | Vertically branching rails |
| Kleene star (`r*`) | Dashed loop-back arc + skip-over arc |
| Kleene plus (`r+`) | Dashed loop-back arc |
| Optional (`r?`) | Dashed loop-back arc + skip-over arc |

---

## Getting Started

No installation needed. Clone the repo and open any HTML file directly in a browser.

```bash
git clone https://github.com/your-username/mathlab-regular-languages.git
cd mathlab-regular-languages
open index.html   # or just double-click in your file manager
```

All three pages link to each other via relative hrefs, so navigation works out of the box.

### Dependencies (loaded from CDN)

- [Tailwind CSS](https://tailwindcss.com/) — utility styling
- [GSAP 3](https://greensock.com/gsap/) — entrance animations, cursor spring, magnetic buttons, tilt cards
- [Google Fonts — Plus Jakarta Sans](https://fonts.google.com/specimen/Plus+Jakarta+Sans) — display and body font
- [Google Material Symbols](https://fonts.google.com/icons) — icon set

No npm, no bundler, no framework.

---

## Usage Examples

### Regex Builder

Type `(a|b)*abb` into the input field. The railroad diagram updates live, showing:
- A `*`-repeated alternation group `(a|b)` with a loop arc
- Three literal terminals `a`, `b`, `b` in sequence

Click **Generate** to produce matching sample strings like `abb`, `aabb`, `babb`, `abababb`, etc.

### Equivalence Checker

| RE1 | RE2 | Result |
|---|---|---|
| `(a+b)*` | `(a*b*)*` | ✅ Equivalent — both accept all strings over {a, b} |
| `a*b*` | `(a\|b)*` | ❌ Not equivalent — `ba` is accepted by RE2 only |
| `(ab)+` | `ab(ab)*` | ✅ Equivalent — one or more `ab` repetitions |

Set **Max Check Length** higher to increase confidence (at the cost of more enumeration). The hard cap is length 10 to prevent exponential blowups on large alphabets.

---

## Project Structure

```
mathlab-regular-languages/
├── index.html               # Theory reference page
├── regex.html               # Regex Builder + Railroad Diagram
├── equivalncechecker.html   # Equivalence Checker
└── README.md
```

All logic is inline JavaScript within each HTML file. There are no external `.js` or `.css` files.

---

## Design

The UI follows a warm editorial aesthetic built on a custom Material You-inspired token palette:

- **Primary:** `#9b4500` (burnt orange)
- **Secondary:** `#006b5f` (deep teal)
- **Tertiary:** `#705d00` (golden olive)
- **Background:** `#fef8f1` (warm cream)

Interactive details include a custom CSS cursor with GSAP spring tracking, 3D tilt on cards, magnetic button physics, a grain overlay, and a large background marquee text element — all implemented without any UI component library.

---

## Limitations

- The equivalence checker uses **finite string enumeration**, not a true DFA minimization algorithm. It can confirm equivalence for all strings up to the chosen length, but cannot prove equivalence for unbounded languages with certainty. For a guaranteed decision procedure, implement full Hopcroft + isomorphism checking.
- The railroad diagram parser handles the most common regex constructs but does not support lookaheads, backreferences, or complex PCRE features — it is scoped to the regular language subset.
- No dark mode is implemented despite the Tailwind `dark:` classes being present in the markup; adding `class="dark"` to `<html>` will activate partial dark styling.

---

## License

MIT — free to use, adapt, and redistribute for educational purposes.
