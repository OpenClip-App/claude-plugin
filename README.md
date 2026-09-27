# OpenClip for Claude

Turn long videos into short vertical clips without leaving the conversation. Share a YouTube, Vimeo, Google Drive, Dropbox, OneDrive, Rumble, or direct video link, and Claude sends it to [OpenClip](https://openclip.app), which finds the moments most likely to work as shorts and scores each one. Preview the clips inline, render captioned finals, and write posts grounded in the video's transcript.

## What's included

- **OpenClip connector**: the hosted OpenClip MCP server at `https://openclip.app/mcp/claude`. It submits videos, reports processing and render status, lists clips, renders captioned clips, and returns time-coded transcripts. In Claude on the web, desktop, and mobile, clip results appear as an interactive card with playable previews.
- **clip-video skill**: the submit, poll, preview, and render workflow, including how to read each processing status and pick the highest-scoring clip.
- **repurpose-clips skill**: writes quotes, captions, social posts, and summaries from a processed video's transcript, tied to the clips' timestamps.

## Requirements

- An OpenClip account. Sign in when you connect the OpenClip connector from the plugin's **Connectors** tab (Claude Code prompts you through `/mcp`).
- Processing new videos needs an active OpenClip plan with credits: one credit per minute of source video. Reading existing videos, clips, and transcripts doesn't use credits.

## Try it

- "Turn https://www.youtube.com/watch?v=... into short clips."
- "Which clip from my last OpenClip video scored highest? Render it with captions."
- "Write a LinkedIn post from the top clip of my podcast episode, quoting what was said."
- "Where in my webinar do they talk about pricing?"

## Data and privacy

The plugin itself stores nothing and runs no local code. It connects Claude to OpenClip's server at `openclip.app`, which receives:

- the video links you ask Claude to process, plus optional titles
- the ids of videos and clips you ask about, and your render choices, such as a caption style

OpenClip downloads and processes those videos in your OpenClip account and returns clips, scores, and transcripts to Claude. Sign-in uses OAuth, so Claude never sees your OpenClip password. OpenClip doesn't read your Claude conversations. How OpenClip collects, uses, stores, and retains data is described in the [OpenClip privacy policy](https://openclip.app/privacy), and use of the service is covered by the [terms of service](https://openclip.app/terms).

## Support

Email [support@openclip.app](mailto:support@openclip.app) or read the [OpenClip MCP documentation](https://openclip.app/docs/developers/mcp).

## License

[MIT](LICENSE)
