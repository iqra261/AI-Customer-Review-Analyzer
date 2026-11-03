# 💬 AI Customer Review Analyzer

Upload a CSV of product reviews and instantly see what customers think: sentiment charts,
common complaints, what people praise, and optional AI-written insights.

## What it does
- Reads a CSV and lets you pick the review text, rating, date and product columns.
- Sentiment (Positive / Neutral / Negative) with a score from -1 to +1, using VADER. **No API key needed.**
- Dashboard: metrics, sentiment and rating charts, trend over time, sentiment by product, frequent words.
- Complaint and praise themes (quality, price, shipping, service, fit, performance, packaging...).
- Sidebar filters for sentiment, product, rating and date.
- Optional **AI Insights** with Groq: summary, top complaints/positives, suggested actions, follow-up chat.
- Download the results as CSV.

Your uploaded file is only kept in your browser session. It is never stored permanently.

## Files
| File | Purpose |
|---|---|
| `app.py` | The whole Streamlit app |
| `requirements.txt` | Python packages |
| `sample_reviews.csv` | 40 sample reviews to try |
| `.gitignore` | Keeps secrets and private data out of GitHub |

## Run it on your computer (optional)
```
pip install -r requirements.txt
streamlit run app.py
```

## Adding the Groq key (optional)
The app works without it; only the AI Insights tab needs a key.
1. Get a free key at https://console.groq.com
2. **On Streamlit Community Cloud:** open your app → **Settings → Secrets** and paste one line (straight quotes):
   ```
   GROQ_API_KEY = "your-key-here"
   ```
   Save, then **Reboot app**.
3. **On your own computer:** create `.streamlit/secrets.toml` with the same line. This file is in `.gitignore`, so it is never uploaded.

Never put your key inside `app.py`.

## Storage note
The app needs no database because it analyses whatever file you upload. If you later want to save past
analyses, use a free hosted database such as **Neon PostgreSQL**. Streamlit Community Cloud erases local
files (including SQLite) whenever the app restarts, so local files are not permanent storage there.

## Common problems
- **ModuleNotFoundError**: a package is missing from `requirements.txt`.
- **File not found / app won't start**: check the main file is `app.py` and the file names have no `.txt` on the end.
- **AI tab says no key**: the secret must be named exactly `GROQ_API_KEY`; reboot after saving.
- **Odd characters in the CSV**: the app tries UTF-8 then Latin-1; re-saving as "CSV UTF-8" in Excel also helps.
- **AI model unavailable**: change `GROQ_MODEL` near the top of `app.py`.
