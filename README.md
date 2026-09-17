# Reading Lab

Interactive reading-comprehension lessons built from real news articles, each covering pre-reading discussion, guided reading with tap-to-define vocabulary, and a set of post-reading practice games and a comprehension quiz.

## Files

| File | What it is |
|---|---|
| `index.html` | The landing page. Lists every lesson as a numbered ring on a vertical path; links out to each lesson file. |
| `mango-founder.html` | Lesson: *Son of Mango Founder Steps Down* (business & crime). |
| `hot-drink.html` | Lesson: *Does a Hot Drink Really Cool You Down?* (health & science). |
| `template.html` | Blank starting point for a new lesson. Same engine as the lessons above, with placeholder content and instructions instead of a real article. |

All files are static HTML — no build step, no dependencies beyond Google Fonts and Font Awesome (loaded from a CDN). Drop them all in the same folder on Netlify (or anywhere else) and `index.html`'s links will work, since they point to the other files by relative filename.

## How each lesson file works

Every lesson file (`mango-founder.html`, `hot-drink.html`, and `template.html`) is self-contained: one HTML file with all its CSS and JavaScript inline. The entire content of the lesson — every question, paragraph, definition, and quiz answer — lives in a single JavaScript object near the top of the `<script>` block, called `LESSON`. Everything below that object (the styling, the games, the scoring, the navigation) is the shared "engine" and doesn't need to change between lessons.

A lesson has three stages, shown as tabs at the top: **Before**, **While**, and **Post**.

- **Before** — a short opinion survey (`LESSON.survey`) to get the learner thinking about the topic before they read.
- **While** — the article itself (`LESSON.paragraphs`), shown either one paragraph at a time or as full text (a toggle switch lets the learner choose). Words wrapped in `<vw>...</vw>` tags are tap-to-define, using the definitions in `LESSON.vocabulary`.
- **Post** — ten practice activities, each pulling from a different part of `LESSON`:
  - **Match** — terms to definitions (`vocabulary`)
  - **Synonyms** — advanced word to simple synonym (`synonyms`)
  - **Quick-Fire** — rapid-fire multiple choice on vocabulary (`vocabulary`)
  - **Word Order** — rebuild a scrambled sentence (`reorderSentences`)
  - **Story Order** — put paragraphs back in order (`paragraphs`)
  - **Fill Gaps** — cloze exercise with a word bank (`cloze`)
  - **True/False** — True / False / Not Given statements (`trueFalseNotGiven`)
  - **Fact/Opinion** — sort statements into fact or opinion (`factOpinion`)
  - **Agree/Disagree** — swipe-style opinion prompts (`agreeDisagree`)
  - **Quiz** — the graded comprehension test (`quiz`)

Points are awarded throughout and shown in a running score at the top and bottom of the page. Finishing the quiz shows a completion screen with the final score, quiz accuracy, and the lesson's key takeaways (`LESSON.takeaways`).

## Adding a new lesson

1. Copy `template.html` and rename it (e.g. `my-new-article.html`).
2. Open it and fill in the `LESSON` object — the comment block at the top of the file walks through every field, one at a time.
3. Open `index.html` and copy one of the existing `<a class="node left">` or `<a class="node right">` blocks, then update its `href`, `--rim` color, category tag, and title to match the new lesson. Row placement on the path is handled automatically — no need to renumber anything.
4. Upload the new lesson file alongside the others.

## A note on shared styling

Because each lesson file carries its own full copy of the CSS and JavaScript, a design change (like the read-mode toggle or the tooltip fix) currently has to be made in every lesson file individually. This is fine for a handful of lessons. If the library grows past ~10, it may be worth factoring the shared engine out into its own file that every lesson includes, so a single change updates all lessons at once — worth keeping in mind, not an immediate concern.
