# Breadit

A full-stack Reddit-like web application where users can create communities, post content, and engage through comments and votes.

## Live Demo

[breadit-theta-liart.vercel.app](https://breadit-theta-liart.vercel.app)

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Next.js 14 (App Router) |
| Language | TypeScript |
| Database | PostgreSQL (Neon) |
| ORM | Prisma |
| Authentication | NextAuth.js (Google OAuth) |
| Caching / Rate Limiting | Upstash Redis |
| File Uploads | Uploadthing |
| UI | Tailwind CSS, Radix UI |
| State Management | TanStack React Query |

## Features

- **Authentication** — Sign in with Google via NextAuth
- **Communities** — Create and join topic-based communities (subreddits)
- **Posts** — Rich text post editor powered by EditorJS (supports headings, images, code blocks, embeds)
- **Voting** — Upvote and downvote posts and comments with rate limiting via Redis
- **Comments** — Nested comment threads with reply support
- **Search** — Real-time community search with debouncing
- **Infinite Scroll** — Feed loads more posts as you scroll
- **Image Uploads** — Post images via Uploadthing

## Getting Started

### Prerequisites
- Node.js 18+
- A PostgreSQL database (e.g. [Neon](https://neon.tech))
- Google OAuth credentials
- [Uploadthing](https://uploadthing.com) account
- [Upstash](https://upstash.com) Redis database

### Setup

```bash
git clone https://github.com/purn1ma/Breadit.git
cd Breadit
npm install
```

Copy the example env file and fill in your values:

```bash
cp .env.example .env
```

Required environment variables:

```env
DATABASE_URL=        # PostgreSQL connection string
NEXTAUTH_SECRET=     # Random secret (generate with: openssl rand -base64 32)
GOOGLE_CLIENT_ID=    # From Google Cloud Console
GOOGLE_CLIENT_SECRET=
UPLOADTHING_SECRET=  # From uploadthing.com
UPLOADTHING_APP_ID=
REDIS_URL=           # From Upstash console
REDIS_SECRET=
```

Push the database schema:

```bash
npx prisma db push
```

Run the development server:

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000)

## Known Issues Fixed

- Downgraded `@editorjs/editorjs` from `2.27.0` to `2.26.5` to fix a `containsNode` runtime crash on post creation pages

## License

MIT