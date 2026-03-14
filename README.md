![OneCut Demo](OneCut.gif)

# OneCut

OneCut is an AI-powered, browser-based video editor built to transform long-form recordings into high-impact highlights. It combines intelligent clip detection, a professional timeline editor, and scalable export workflows so creators can publish faster without sacrificing quality.

## Why OneCut

- Reduce hours of manual editing with AI-assisted highlight generation.
- Keep full creative control with a multi-track timeline and precision tools.
- Produce platform-ready videos for YouTube, TikTok, Instagram, and more.
- Run a modern full-stack architecture designed for real-time media workflows.

## Core Features

### AI Editing Engine
- Smart highlight detection for interviews, tutorials, podcasts, and similar formats.
- Configurable prompt-based instructions for tailored output.
- Short-form and long-form clip generation modes.
- Scene-aware analysis pipeline for better content segmentation.

### Professional Web Editor
- Multi-track timeline with drag-and-drop interactions.
- Frame-level trimming and clip splitting.
- Playback speed controls and aspect-ratio presets (`16:9`, `9:16`, `1:1`).
- Text, stickers, transitions, and visual effects.

### Captions, Audio, and Voice
- Automatic caption generation with timing synchronization.
- Caption style presets for different publishing formats.
- AI voiceover support and music layering.
- Audio cleanup and volume balancing workflows.

### Export and Delivery
- Hybrid rendering pipeline with FFmpeg and browser rendering.
- Progress-tracked export jobs with real-time updates.
- Optimized output profiles for major social/video platforms.

## Product Workflow

1. **Upload** source footage to your project.
2. **Analyze** content with AI to generate initial highlight candidates.
3. **Edit** in the timeline (captions, cuts, transitions, overlays, audio).
4. **Export** a final render in your preferred platform format.

## Tech Stack

### Frontend (`client`)
- `Next.js 15`
- `React 18`
- `Tailwind CSS 4`
- `FFmpeg.wasm`
- `Socket.IO Client`

### Backend (`server`)
- `Node.js` + `Express`
- `TypeScript`
- `Supabase` (Auth + PostgreSQL)
- `Google Cloud Storage`
- `Google Vertex AI` / `Google GenAI`
- `FFmpeg` + `Puppeteer` (hybrid export)

## Repository Structure

```text
OneCut/
├── client/                 # Next.js app (UI/editor)
├── server/                 # Express API + media/AI processing
├── _db/                    # SQL schema and migrations
├── render.yaml             # Deployment config
└── README.md
```

## Getting Started

### Prerequisites

- Node.js `18+`
- npm
- Supabase project
- Google Cloud project with required APIs (Storage, Vertex AI, Video Transcoder)
- ElevenLabs API key (if using voiceover features)

### 1) Clone and install

```bash
git clone <your-repo-url>
cd OneCut
npm install
cd client && npm install
cd ../server && npm install
```

### 2) Configure environment variables

Create `client/.env.local`:

```env
NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
NEXT_PUBLIC_API_URL=http://localhost:3001
```

Create `server/.env`:

```env
SUPABASE_URL=your_supabase_url
SUPABASE_SERVICE_KEY=your_supabase_service_key
GOOGLE_CLOUD_STORAGE_BUCKET=your_bucket_name
GOOGLE_APPLICATION_CREDENTIALS=path/to/service-account.json
VERTEX_AI_PROJECT_ID=your_project_id
VERTEX_AI_LOCATION=us-central1
ELEVENLABS_API_KEY=your_elevenlabs_api_key
PORT=3001
```

### 3) Apply database schema

Run SQL files inside `_db/` against your Supabase/PostgreSQL instance (for example: `users.sql`, `projects.sql`, `assets.sql`, `clips.sql`, `tracks.sql`, etc.).

### 4) Start development servers

Backend:

```bash
cd server
npm run dev
```

Frontend (new terminal):

```bash
cd client
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

## API Overview

All protected endpoints require a Supabase JWT:

```http
Authorization: Bearer <access_token>
```

Representative endpoints:

- `POST /api/projects` - create project
- `POST /api/assets/upload-to-gcs` - upload source media
- `POST /api/quickclips/start` - trigger AI clip generation
- `GET /api/timeline/:projectId` - fetch timeline data
- `POST /api/export/start` - start export
- `GET /api/export/status/:jobId` - export progress/status

## Architecture Notes

- **Hybrid render system**: FFmpeg handles media operations while browser rendering preserves rich visual fidelity.
- **Real-time job updates**: Socket-based status updates for processing and export stages.
- **AI pipeline**: Analysis, transcription, scene understanding, and clip proposal generation.

## Development

Client build:

```bash
cd client
npm run build
```

Server build:

```bash
cd server
npm run build
```

## Contributing

Contributions are welcome. Recommended flow:

1. Fork the repository.
2. Create a feature branch.
3. Implement and test your changes.
4. Open a pull request with a clear description and test notes.

## Security

Do not commit secrets, service-account files, or production API keys. Use local environment files and your deployment secret manager.

## License

Add your project license here (for example, MIT, Apache-2.0, or proprietary/internal use).

## Support

For bug reports and feature requests, open a GitHub issue with reproduction steps and environment details.

---

OneCut is built to make professional, AI-assisted editing faster, more accessible, and production-ready.
