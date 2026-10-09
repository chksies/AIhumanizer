# AI Humanizer

A single-page tool that rewrites AI-sounding text so it reads like a person wrote it. Paste text in, get a cleaned-up version back, streamed live. It runs entirely in your browser and calls the Anthropic API directly.

## Features

- **Streaming rewrite** of pasted text, with a Stop button.
- **Tone:** natural, casual, professional, or academic.
- **Rewrite strength:** light (fix tells only), medium, or heavy (restructure freely).
- **Double-check pass (optional):** a second call compares the draft with your original, restores any fact that drifted, and fixes remaining AI tells. It roughly doubles cost and time per run.
- **Show changes:** a word-level diff of your input against the result.
- **Meaning preserved:** the prompt tells the model to keep every fact, number, name, quote and URL, and not to invent anything.
- Input is wrapped in tags, so pasted questions or commands are rewritten instead of answered.
- Word and character counts, copy button, and Ctrl+Enter (Cmd+Enter on Mac) to run.

## Usage

1. Open `humanizer.html` in a browser. No build step or install.
2. Paste your Anthropic API key into the key field. Get one at [console.anthropic.com](https://console.anthropic.com).
3. Paste your text, pick a tone and strength, and click **Humanize**.
4. Click **Show changes** to see what was edited, then **Copy result**.

Opening the file directly works. If your browser blocks something on `file://`, serve the folder instead:

```bash
python -m http.server 8000
```

Then visit `http://localhost:8000/humanizer.html`.

## API key and privacy

- The key is stored in your browser's `localStorage` and sent only to `api.anthropic.com`.
- Because the key lives in the page, use this tool yourself. Do not host it publicly with your key, and do not share a browser profile that has it saved.
- Your text is sent to the Anthropic API for processing. Do not paste anything you are not comfortable sending there.

## Limits

- Output is capped at 8192 tokens (roughly 6,000 words). If a result hits the cap, the page says it is incomplete. Split long documents into parts.
- The diff is skipped for very long texts.
- No rewriter can guarantee a pass on AI detectors. This tool aims for clearer, more natural writing, not for detector evasion.

## Configuration

Edit the top of the script in `humanizer.html`:

- `SYSTEM_PROMPT`: the editing rules.
- `TONES` and `STRENGTHS`: the dropdown instructions.
- `AUDIT_ADDENDUM`: the second-pass instructions.
- `MODEL`: the Claude model used for both passes.
