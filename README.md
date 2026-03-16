# 🧠 CampusX ML Quiz

> AI-graded, two-player quiz app for **CampusX 100 Days of ML**.  
> Built with vanilla HTML/CSS/JS — no framework, no build step, just open and play.

## ✨ Features

- **Mixed question types** — MCQ, True/False, and Short Answer
- **AI grading** — Short answers graded by Claude for conceptual understanding, not keyword matching. Good reasoning = full marks.
- **Answer locking** — Once selected, answers are final. No going back.
- **Two-player mode** — Both players take the quiz independently, then share a result code for a head-to-head scoreboard
- **Persistent leaderboard** — All scores saved to Supabase Postgres, visible to both players across sessions
- **Weak topic analysis** — Day-by-day performance breakdown, individually and across all attempts
- **Quiz Report export** — Downloads a `.txt` file with full review + AI feedback, ready to upload to any AI tool for personalised revision

---

## 🚀 Live Demo

**[stranger4uu.github.io/campusx-ml-quiz](https://stranger4uu.github.io/campusx-ml-quiz/)**

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | Vanilla HTML / CSS / JavaScript |
| Database | Supabase (Postgres via REST API) |
| AI Grading | Anthropic Claude (`claude-sonnet-4-20250514`) |
| Hosting | GitHub Pages |

---

## ⚙️ Self-Host Setup (~15 min)

### 1. Fork this repo

### 2. Create a Supabase project

Go to [supabase.com](https://supabase.com) → New project → open **SQL Editor** → run:

```sql
CREATE TABLE quiz_results (
  id           uuid DEFAULT gen_random_uuid() PRIMARY KEY,
  player_name  text NOT NULL,
  score        integer NOT NULL,
  max_score    integer NOT NULL,
  percentage   numeric NOT NULL,
  mcq_score    integer,
  tf_score     integer,
  short_score  integer,
  details      jsonb,
  quiz_date    timestamptz DEFAULT now(),
  quiz_label   text
);

ALTER TABLE quiz_results ENABLE ROW LEVEL SECURITY;

CREATE POLICY "allow insert" ON quiz_results FOR INSERT WITH CHECK (true);
CREATE POLICY "allow read"   ON quiz_results FOR SELECT USING (true);
```

### 3. Add your credentials

In `index.html`, replace the first two lines:

```js
const SUPABASE_URL = 'https://your-project-id.supabase.co';
const SUPABASE_KEY = 'sb_publishable_your_key_here';
```

Get these from: Supabase dashboard → **Settings → API Keys**

### 4. Enable GitHub Pages

**Settings → Pages → Source: main branch → / (root) → Save**

Your quiz goes live at `https://yourusername.github.io/campusx-ml-quiz/` in ~1 minute.

---

## 🎮 Two-Player Flow

```
Player 1                        Player 2
─────────────────────────────   ─────────────────────────────
1. Open the quiz URL            1. Open the same URL
2. Enter name + quiz label      2. Enter name
3. Take the quiz                3. Take the quiz
4. Copy Result Code  ────────►  4. Paste code → see scoreboard
5. Download .txt report         5. Download .txt report
6. Upload to Claude/ChatGPT     6. Upload to Claude/ChatGPT
   for revision feedback           for revision feedback
```

---

## 📄 Quiz Report

The downloaded `.txt` report includes score breakdown, topic analysis, per-question review with AI feedback, and this ready-made prompt:

```
Here is my ML quiz report. Please:
1. Identify my biggest knowledge gaps
2. Explain the topics I got wrong in simple terms
3. Give me 3 practice questions on my weak areas
4. Suggest what I should revise before the next quiz
```

---

## 🗂️ Project Structure

```
campusx-ml-quiz/
├── index.html   # Entire app — self-contained single file
└── README.md
```

---

## 🤝 Contributing

Adding questions for later CampusX days? PRs are welcome.

1. Fork → add questions to the `QS` array in `index.html`
2. Follow the existing `{id, type, day, pts, q, opts, ans}` format
3. Open a PR with the day number in the title

---

## 👤 Author

**Stranger4uu** — BTech AI/ML Student  
GitHub: [@Stranger4uu](https://github.com/Stranger4uu)

---

## 📜 License

MIT — free to use, fork, and build on.

---

<div align="center">
  <sub>Built during CampusX 100 Days of ML · Powered by Claude AI · Hosted on GitHub Pages</sub>
</div>
