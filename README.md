# AI Article Summarizer Automation

This project is an automation workflow that fetches a webpage, extracts the article text, summarizes it using an AI model, and stores the results in a Google Sheet.

The workflow is built using **Make.com** and integrates **Groq's LLM API** for fast AI inference.

*You can see the workflow here:* [Automation Workflow on Make.com](https://eu1.make.com/public/shared-scenario/hwViYPTtECR/automation-make-com)

---

## 🚀 Overview

The system takes an article URL as input and automatically generates a concise summary.

Workflow pipeline:

```
Webhook
   ↓
HTTP Request (Fetch Webpage)
   ↓
HTML → Text Parsing
   ↓
Groq AI API (Generate Summary)
   ↓
Google Sheets (Store Result)
```

---

## 🧠 Features

* Fetches webpage content from a URL
* Converts raw HTML into readable text
* Uses AI to generate a structured summary
* Automatically stores results in Google Sheets
* Handles long articles by truncating text to avoid token limits

---

## 🛠️ Tech Stack

Automation Platform

* Make.com

AI Model

* Groq API (llama-3.1-8b-instant)

Storage

* Google Sheets

Processing

* HTML to text parsing
* Text truncation and formatting

---

## 📂 Workflow Architecture

### 1. Webhook Trigger

Receives a request containing an article URL.

Example payload:

```json
{
  "url": "https://example.com/article"
}
```

---

### 2. HTTP Request (Fetch Webpage)

Fetches the webpage HTML content.

---

### 3. Text Parsing

Converts the raw HTML into clean text by removing:

* HTML tags
* scripts
* styles
* unnecessary formatting

---

### 4. AI Summarization

The cleaned article text is sent to the Groq API.

Example request body:

```json
{
  "model": "llama-3.1-8b-instant",
  "messages": [
    {
      "role": "user",
      "content": "Summarize the following article in 5 bullet points."
    }
  ]
}
```

To avoid token limit issues, the article text is truncated:

```
substring(text, 0, 3000)
```

---

### 5. Store Results

The generated summary is saved to Google Sheets.

Example sheet structure:

| Article URL         | AI Summary           | Timestamp  |
| ------------------- | -------------------- | ---------- |
| example.com/article | Bullet point summary | 2026-03-10 |

---

## ⚠️ Token Limit Handling

Groq models enforce token limits.
To avoid exceeding limits, the article text is truncated before sending to the AI.

Example logic:

```
substring(article_text, 0, 3000)
```

This ensures the request stays within the API token constraints.

---

## ▶️ Running the Automation

1. Trigger the webhook with an article URL.
2. The system fetches and processes the webpage.
3. AI generates the summary.
4. The result is stored automatically in Google Sheets.

---

## 📌 Example Output

Input URL:

```
https://en.wikipedia.org/wiki/Machine_learning
```

Output summary:

```
• Machine learning is a subset of artificial intelligence.
• It allows systems to learn from data without explicit programming.
• Common techniques include supervised, unsupervised, and reinforcement learning.
• It is widely used in recommendation systems, vision, and NLP.
• Large datasets and computing power drive modern ML progress.
```

---

## 🔮 Possible Improvements

* Automatically extract article titles
* Handle long articles using chunking
* Generate social media posts from summaries
* Add sentiment or key insight extraction
* Store results in a database instead of spreadsheets

