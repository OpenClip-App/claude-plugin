# OpenClip for Claude

Turn long videos into short vertical clips without leaving the conversation. Share a YouTube, Vimeo, Google Drive, Dropbox, OneDrive, Rumble, or direct video link, and Claude sends it to [OpenClip](https://openclip.app), which finds the moments most likely to work as shorts and scores each one. Preview the clips inline, render captioned finals, and write posts grounded in the video's transcript.

## What you can do

The connector exposes 27 tools. In addition to clipping and captions, Claude can transcribe video/audio, trim/crop/resize/compress video, convert video formats or extract audio, extract thumbnail frames, and crop/resize/compress images. It can show detailed credit usage and create or update saved processing agents, including caption/composition settings and a logo watermark. It edits your existing media; AI UGC generation and background removal are outside this connector.

## What's included

- **OpenClip connector**: the hosted OpenClip MCP server at `https://openclip.app/mcp/claude`. It submits videos, reports processing and render status, lists clips, renders captioned clips, captions short videos you upload, returns time-coded transcripts, edits existing media, and manages saved processing agents. In Claude on the web, desktop, and mobile, clip results appear as an interactive card with playable previews.
- **clip-video skill**: the submit, poll, preview, and render workflow, including how to read each processing status and pick the highest-scoring clip.
- **caption-video skill**: uploads a short video (up to 3 minutes) you already have and renders it with animated captions in the style you pick.
- **repurpose-clips skill**: writes quotes, captions, social posts, and summaries from a processed video's transcript, tied to the clips' timestamps.

## Requirements

- An OpenClip account. [Create a free account](https://openclip.app/register) if you need one, then sign in when you connect OpenClip from the plugin's **Connectors** tab (Claude Code prompts you through `/mcp`).
- Clipping your own videos needs a trial or paid plan with enough credits: one credit per minute of source video. Reading existing videos, clips, and transcripts doesn't use credits. Media utilities need only an account, subject to file and daily limits. Quick Captions uses no processing credits and follows the account's export allowance.

The current [published trial offer](https://openclip.app/docs/getting-started/credits-and-plans) is 3 days with 60 processing credits for eligible accounts. It requires a card and costs $0 today; a temporary card authorization may appear. The selected plan is charged when the trial ends unless canceled. Trial renders include an OpenClip watermark. Signing up alone does not grant processing credits. See the linked documentation for current terms.

## Try it

- "Check my OpenClip connection and tell me my plan and remaining credits."
- "Turn https://www.youtube.com/watch?v=... into short clips."
- "Which clip from my last OpenClip video scored highest? Render it with captions."
- "Write a LinkedIn post from the top clip of my podcast episode, quoting what was said."
- "Where in my webinar do they talk about pricing?"
- "Caption ./reel.mp4 in the Chase style."
- "Transcribe ./interview.wav and give me an SRT file."
- "Resize ./cover.png to 1080 by 1080."
- "Save a brand agent with the default caption style and use it for my next video."

## Uploads and media jobs

`create_upload` accepts video, audio, and image files and returns `uploaded: false`, a `video` id, and a presigned PUT URL. The id identifies any uploaded media, including an image. In Claude Code or a client with authorized local-file access, PUT the actual bytes before processing. The upload itself starts no processing. Claude apps without file transfer use existing OpenClip media or upload through the matching tool at openclip.app.

- For paid clipping of a local video, call `complete_upload` after the PUT.
- For whole-video captions up to 3 minutes, call `caption_video` without `complete_upload`.
- For utilities, call `transcribe`, `edit_video`, `convert_media`, `extract_thumbnails`, or `edit_image`, then poll `get_tool_job_status` until completed or failed. Use the `outputs` only after completion. These operations use no processing credits but enforce account/file/daily limits.
- For a logo, call `create_agent_logo_upload`, PUT a JPEG/PNG/GIF under 2 MB, then call `set_agent_logo`. Replacing an existing logo or changing shared agent settings requires the user's request or approval.

Use `list_agents` to find a saved agent and pass its id to `submit_video`. Before setting advanced fields, call `describe_agent_settings`. Uploaded-video clipping through `complete_upload` uses defaults.

## Data and privacy

The plugin itself stores nothing and runs no local code. It connects Claude to OpenClip's server at `openclip.app`, which receives:

- the video links you ask Claude to process, plus optional titles
- video, audio, and image files you explicitly upload to your OpenClip account for processing
- agent settings and logo images you ask to save or replace
- the ids of videos and clips you ask about, and your render choices, such as a caption style

OpenClip downloads and processes that media in your OpenClip account and returns clips, scores, and transcripts to Claude. Sign-in uses OAuth, so Claude never sees your OpenClip password. OpenClip doesn't read your Claude conversations. How OpenClip collects, uses, stores, and retains data is described in the [OpenClip privacy policy](https://openclip.app/privacy), and use of the service is covered by the [terms of service](https://openclip.app/terms).

## Support

Email [support@openclip.app](mailto:support@openclip.app) or read the [OpenClip MCP documentation](https://openclip.app/docs/developers/mcp).

## License

[MIT](LICENSE)
