# X Following Exporter

Local web app that exports an X account's following list as Markdown by reusing your logged-in Arc session on macOS.

## What It Does

- Input any X handle, such as `@odysseyml`
- Reuse your active Arc login session for X
- Fetch that account's following list
- Generate Markdown output
- Copy or download the result as a `.md` file

## How It Works

This project does not use official X API credentials.

Instead, it:

1. Runs a local Node server
2. Temporarily switches the active Arc tab to `x.com/home`
3. Executes a small in-page script through Arc AppleScript support
4. Reads the following list through X's current web endpoints
5. Returns the result to the local web app as Markdown

This means the tool is simple to run locally, but it is tightly coupled to:

- Arc being installed
- Arc AppleScript behavior
- Your existing X login session in Arc
- X's current web endpoint behavior

## Requirements

- macOS
- Arc browser installed
- Arc open on the machine
- Logged into X inside Arc
- Node.js installed

## Run Locally

```bash
git clone https://github.com/edwardxxxxl-ai/x-following-webapp.git
cd x-following-webapp
npm start
```

Then open:

```bash
http://127.0.0.1:4321
```

## Input

Accepted input examples:

- `odysseyml`
- `@odysseyml`

## Output Format

Example output:

```md
# X Following

Source: @odysseyml
Exported at: 2026-03-06T03:08:15.471Z
Total: 5

- @HuangRenee3
- @JonathanSadeghi
- @BreezeChai
```

## Project Structure

```text
server.js           Local HTTP server and Arc/X export logic
public/index.html   Single-page UI
public/styles.css   Frontend styling
```

## Limitations

- This is a local automation workflow, not a hosted SaaS app
- It currently depends on Arc, not Chrome or Safari
- X may change internal endpoints at any time
- If Arc blocks AppleScript or X changes page behavior, the exporter may break
- The app temporarily reuses the active Arc tab and then restores its URL

## Safety Notes

- The app runs locally on your machine
- It does not require storing X credentials in this repo
- It relies on your already authenticated Arc browser session

You should still treat it as browser automation tooling and review the code before using it with any sensitive account.

## License

MIT
