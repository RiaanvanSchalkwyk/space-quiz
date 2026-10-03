# Copilot instructions

## Project shape and commands

- This is a static, dependency-free web quiz. The complete app lives in `index.html`: semantic markup, theme tokens and responsive CSS, quiz data, and interaction logic are all in that file. There is no package manifest, build step, configured test runner, or linter.
- Open `index.html` directly in a browser to run it; no server is required. There is no single-test command. For a focused smoke check, load the page, choose one correct answer and one incorrect answer, advance to the results, and verify the score and feedback.

## How the app works

- The `questions` array is the quiz's source of truth. Each entry contains a prompt, four answers, the zero-based correct-answer index, and an explanatory fact.
- `renderQuestion()` builds answer buttons from the current array entry. `chooseAnswer()` locks the question after one selection, updates score and progress, marks the correct/wrong choices, and reveals the fact. `showResults()` selects the end-screen reaction from the final score. The restart control resets the state and renders question one.
- Progress is shown both as text and as an ARIA progressbar; its visual fill is transformed in proportion to completed questions. Answer and next-question controls are native buttons, with focus moved to feedback progression and the next prompt.

## Codebase conventions

- Keep the app self-contained in `index.html`; do not add a framework, package setup, or external asset dependency without a project requirement.
- Keep light and dark theme values paired in `:root` and `@media (prefers-color-scheme: light)`. Reuse the existing CSS custom properties for surfaces, text, signals, and correct/incorrect feedback.
- Preserve native keyboard-operable buttons, visible `:focus-visible` styling, accessible progress and feedback announcements, and the `prefers-reduced-motion` override when changing interactions or animation.
- When changing quiz content, update each question's prompt, four answer choices, correct index, and fact together. `correct` is zero-based and must point to the intended answer.
