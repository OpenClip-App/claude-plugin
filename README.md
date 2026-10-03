# OpenClip for Claude

Find the moments worth sharing, then turn them into captioned clips. Use [OpenClip](https://openclip.app) in Claude to preview clips from podcasts, interviews, and webinars, choose your exports, and write posts from the original transcript.

## Connect and make your first request

1. [Create a free OpenClip account](https://openclip.app/register), or use your existing account.
2. Connect OpenClip from the plugin's **Connectors** tab and sign in. In Claude Code, open `/mcp` to connect. OAuth handles sign-in; you don't need an API key.
3. Choose one task below and provide a video link, an existing OpenClip video, or a file this session can upload.

Clipping your own videos requires a trial or paid plan with credits. Creating an account alone does not grant processing credits. Captioning short videos and media utilities have separate allowances, described below.

## Choose the result you need

- **Find clips to share.** "Find short clips from this video and show me the previews." Share a supported public video link. After reviewing the results, ask Claude to export your chosen clip with captions.
- **Caption a finished short video.** "Caption this video in the Chase style." Use a video up to 3 minutes long. Claude can list the available styles if you want to choose.
- **Find a quote or draft a post.** "Find where my interview covers pricing and draft a LinkedIn post from that passage." Claude uses the processed video's transcript and timestamps. For transcription alone: "Transcribe this audio file and give me an SRT file."
- **Prepare existing media.** "Resize this cover image to 1080 by 1080." You can also trim, crop, resize, or compress video, convert formats, extract audio, and save thumbnail frames.
- **Reuse your brand settings.** "Use my saved brand settings to clip this video link." Claude can find saved processing agents, or save caption styles, composition settings, and a logo you ask it to reuse.

Claude checks processing progress, then returns previews or the finished file. Supported Claude apps show playable clip previews; Claude Code provides preview links. You choose what to export and where to share it.

## Accounts and credits

- **Clipping:** one processing credit per minute of source video, with enough credits and an active trial or paid plan. Reading existing videos, clips, and transcripts uses no processing credits.
- **Quick Captions:** no processing credits. Free accounts can export two captioned videos per month; once that allowance is used, further exports, including re-exports, wait until the next month. Paid plans are unlimited.
- **Media utilities:** an account is enough. Transcription, media edits, conversion, and thumbnail extraction use no processing credits, but file and daily limits apply. On free accounts, edited or converted videos, edited images, and GIFs carry an OpenClip watermark; transcripts, extracted audio, and thumbnail frames do not.

The current [published trial offer](https://openclip.app/docs/getting-started/credits-and-plans) is 3 days with 60 processing credits for eligible accounts. It requires a card and costs $0 today; a temporary card authorization may appear. The selected plan is charged when the trial ends unless canceled. Clips rendered during the trial include an OpenClip watermark. See the linked documentation for current terms.

## Video links and file uploads

For clipping, share a public YouTube, Vimeo, Google Drive, Dropbox, OneDrive, Rumble, or direct video link. For local video, audio, or images, the Claude session must be able to read your authorized file and upload its bytes. Otherwise, upload through the matching tool at openclip.app and ask Claude to use that file.

For clients that transfer files, `create_upload` returns `uploaded: false`, a `video` id, and a presigned PUT URL. The id identifies any uploaded media, including an image. PUT the actual bytes before processing. Creating an upload alone starts no processing.

- For clipping a local video with a trial or paid plan, call `complete_upload` after the PUT.
- For whole-video captions up to 3 minutes, call `caption_video` without `complete_upload`.
- For utilities, call `transcribe`, `edit_video`, `convert_media`, `extract_thumbnails`, or `edit_image`, then poll `get_tool_job_status` until completed or failed. Use the `outputs` only after completion. These operations use no processing credits but enforce account/file/daily limits.
- For a logo, call `create_agent_logo_upload`, PUT a JPEG/PNG/GIF under 2 MB, then call `set_agent_logo`. Replacing an existing logo or changing shared agent settings requires the user's request or approval.

Use `list_agents` to find a saved agent and pass its id to `submit_video`. Before setting advanced fields, call `describe_agent_settings`. Uploaded-video clipping through `complete_upload` uses defaults. Use `get_account` to check the connection, plan, and credit balance; `get_usage` shows credit activity.

## What's included

The plugin connects to `https://openclip.app/mcp/claude` with 27 tools and three workflow skills: [clip-video](skills/clip-video/SKILL.md), [caption-video](skills/caption-video/SKILL.md), and [repurpose-clips](skills/repurpose-clips/SKILL.md). It works with your existing media. AI UGC generation and background removal are outside this connector.

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
