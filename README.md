# Desk Signal

Support triage powered by [Pollinations Jev](https://pollinations.ai), built for quest [#15722](https://github.com/pollinations/pollinations/issues/15722).

Paste a support report and supply your own Pollinations API key. One direct `POST /alpha/decisions` call picks the support team and estimates the probability of immediate urgency. The app's code changes the routing card, highlights the selected team's probabilities, chooses the team's checklist, and adds an on-call escalation at urgency >= 70%. Team confidence below 65%, or a `needs_info` route, requires human review.

## Run locally

```sh
python -m http.server 8765 --directory dist
```

Open http://localhost:8765. No dependencies or build are required. Host `dist/` on any static HTTPS host for deployment.

## Keys and Pollen

Each visitor pays with their own Pollen. Get a key from https://enter.pollinations.ai/keys; allow Jev. Paste it into the password field or load a local `.txt` file containing only the key. The file is read locally, not uploaded. The key is kept only in page memory and sent solely to `https://gen.pollinations.ai` as a bearer token. It is never included in a URL, logged, stored in browser storage, or embedded in this repository. Clear it with **Clear** or close the page. The app does not create or revoke keys.

This app calls the built-in Jev model directly. It does not need public access to the author's separate, privately registered Support Desk agent.

## Verification

Live browser tests of the actual UI against Jev:

- Production HTTP 500 outage: **Technical / IMMEDIATE**, 100% team confidence, 97% urgency; three checklist items including alerting on-call; 504 input tokens.
- Duplicate payment and feature request use the supplied sample buttons. All displayed probabilities come from Jev; the app contains no precomputed result fixtures.

The companion agent's same decision questions were also exercised with five live support reports, producing billing, technical, security, product and needs_info routes, and with ten unit tests. Request errors remain visible and do not trigger paid retries.

AI probabilities are judgments, not verified facts. The app suggests actions; it does not assign tickets, send messages, issue refunds, or change accounts. Avoid pasting credentials or personal customer data into support reports.

Created by GitHub user **MetaMysteries8** with **Codex AI assistance**. MIT licensed.
