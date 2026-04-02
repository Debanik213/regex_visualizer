# MathLab: Regular Languages Interactive Tool

A zero-dependency, client-side web application designed to help users explore, build, and verify the mathematics behind Regular Expressions and Formal Languages.

This project was built as an academic assignment and runs entirely in the browser without the need for a backend server or external mathematical libraries.

## 🚀 Features

The application is divided into three core modules:

### 1. The Theory Module (`index.html`)
An educational hub that breaks down the theoretical foundations of regular languages. It covers:
* Formal definitions of Alphabets (Σ), Strings (w), and Languages (L).
* The inductive steps of Regular Expressions (Union, Concatenation, Kleene Star).
* The computational models of Finite Automata (DFA & NFA) and Kleene's Theorem.

### 2. Regex Builder & Generator (`regex.html`)
An interactive testing ground for building regular expressions.
* **Construction Palette:** A click-to-insert UI for adding common regex operators (Kleene Star, Union, Capture Groups, etc.) without memorizing syntax.
* **String Generator:** Uses a custom client-side algorithm to derive the alphabet from the user's input and generate bounded random strings. It strictly verifies these strings against the browser's native `RegExp` engine, outputting valid matches directly to the UI.

### 3. Equivalence Verification (`equivalncechecker.html`)
A testing laboratory to mathematically verify if two distinct regular expressions generate the same language: `L(R1) ≡ L(R2)`.
* **Bounded Universe Algorithm:** Instead of implementing a heavy NFA-to-DFA minimization algorithm, this tool dynamically generates a "universe" of all possible strings based on the combined alphabets of both inputs up to a user-defined maximum length.
* It tests every single string in that bounded universe. If a string is accepted by one expression but rejected by the other, it instantly flags the counterexample.

## 🛠️ Tech Stack

* **Frontend:** HTML5, Vanilla JavaScript.
* **Styling:** Tailwind CSS (via CDN) with custom glassmorphism and "schematic" design elements.
* **Dependencies:** None. Everything runs natively in the browser.

## ⚙️ How to Run Locally

Because this project relies entirely on client-side JavaScript, setup is instant. 

1. Clone this repository or extract the ZIP file.
2. Open the project folder.
3. Double-click the `index.html` file to open it in your default web browser (Chrome, Firefox, Safari, Edge).
4. Navigate between the modules using the side or bottom navigation bars.

## 📝 Assignment Details

* **Submission Deadline:** April 10, 2026
* **Student Name:** [Your Name Here]
* **Roll Number:** [Your Roll Number Here]
