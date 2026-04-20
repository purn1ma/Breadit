# Breadit

A full-stack Reddit-like web application where users can create communities, post content, and engage through comments and votes.

## Live Demo

[Coming soon — deploying on Vercel]

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

## Architecture Overview

```
src/
├── app/                  # Next.js App Router pages and API routes
│   ├── api/              # Backend API endpoints (posts, votes, comments, auth)
│   └── r/                # Community pages and post pages
├── components/           # Reusable UI components
├── hooks/                # Custom React hooks
├── lib/                  # Utility functions, db client, auth config
└── types/                # TypeScript type definitions

prisma/
└── schema.prisma         # Database schema (User, Post, Comment, Vote, Subreddit)
```

## Database Schema

The app uses 7 models:
- **User** — stores profile, linked accounts, sessions
- **Subreddit** — a community with a name and creator
- **Subscription** — links users to communities they've joined
- **Post** — belongs to a subreddit and author, stores rich text content as JSON
- **Comment** — supports nested replies via self-referential relation
- **Vote / CommentVote** — tracks upvotes/downvotes per user per post/comment

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