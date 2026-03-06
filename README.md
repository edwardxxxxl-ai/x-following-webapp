# X Following Exporter

Local web app for exporting an X account's following list as Markdown by reusing your logged-in Arc session.

## Run

```bash
cd /Users/yankuan/x-following-webapp
npm start
```

Then open `http://127.0.0.1:4321`.

## Requirements

- Arc must be installed on this Mac.
- Arc must be open.
- You must already be logged into X inside Arc.
- The app temporarily reuses the active Arc tab, then restores the previous URL.

## Notes

- Input should be a plain X handle, for example `odysseyml` or `@odysseyml`.
- Output is generated as Markdown and can be copied or downloaded from the page.
- This workflow depends on X's current web endpoints and Arc's AppleScript support.
