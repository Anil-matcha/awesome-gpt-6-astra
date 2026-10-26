<p align="center">
  <img src="https://img.shields.io/badge/open%20source-MIT-4f46e5?style=flat-square" alt="MIT license">
  <img src="https://img.shields.io/badge/Next.js-16-black?style=flat-square&logo=next.js" alt="Next.js 16">
  <a href="https://github.com/Anil-matcha/Postiz-cheap/stargazers"><img src="https://img.shields.io/github/stars/Anil-matcha/Postiz-cheap?style=flat-square" alt="GitHub stars"></a>
</p>

<h1 align="center">Postiz-cheap</h1>

<p align="center">
  A self-hostable, open-source social media scheduler for creators who want a simpler, lower-cost alternative to Postiz.
</p>

Postiz-cheap brings a content calendar, post composer, AI writing assistant, and social publishing into one Next.js app. Run it on your own infrastructure and keep control of your workflow. The app is MIT licensed; usage of external AI, hosting, and social publishing services may still cost money.

## What you can do

- Plan and edit posts in a calendar, then publish now or schedule them.
- Draft platform-specific copy with the AI post writer or the conversational social marketing agent.
- Connect social accounts and manage posts from one workspace.
- Preview copy for different platforms before publishing.
- Track scheduled, processing, published, and failed posts.
- Use publishing integrations wired for YouTube, TikTok, Instagram, Facebook, X, LinkedIn, Threads, and Pinterest.

## Cost and provider requirements

The scheduler itself has no required monthly subscription when you self-host it. It currently uses MuAPI for AI features, account connections, media uploads, and publishing, so you need a MuAPI API key and provider usage charges may apply. You also cover hosting, database, and any fees charged by social networks or other providers.

This repository contains the self-hosted application. It does not include a hosted Postiz-cheap service. Postiz-cheap is an independent project and is not affiliated with or endorsed by Postiz.

## How it works

- **App:** Next.js 16 with the App Router
- **Database:** PostgreSQL with Prisma
- **Sign-in:** Google OAuth through NextAuth
- **AI and social publishing:** MuAPI
- **Optional credit checkout:** Stripe

Scheduled posts are stored in PostgreSQL and submitted through the app's post-processing route. The current project does not include a separate always-on job worker; review the scheduling flow and hosting setup before relying on unattended production publishing.

## Run it locally

### Requirements

- Node.js and npm
- A PostgreSQL database
- Google OAuth credentials
- A MuAPI API key for AI and social publishing

### 1. Clone and install

```bash
git clone https://github.com/Anil-matcha/Postiz-cheap.git
cd Postiz-cheap
npm install
cp .env.example .env
```

### 2. Configure environment variables

Set the required database, authentication, Google OAuth, and MuAPI values in `.env`:

```env
DATABASE_URL="postgresql://user:password@host:5432/postiz_cheap?pgbouncer=true"
DIRECT_URL="postgresql://user:password@host:5432/postiz_cheap"

NEXTAUTH_URL="http://localhost:3000"
NEXTAUTH_SECRET="replace_with_a_long_random_secret"

GOOGLE_CLIENT_ID="your_google_client_id"
GOOGLE_CLIENT_SECRET="your_google_client_secret"

MUAPIAPP_API_KEY="your_muapi_api_key"
WEBHOOK_URL="http://localhost:3000"
```

In Google Cloud, add `http://localhost:3000/api/auth/callback/google` as an authorized redirect URI. Stripe variables in `.env.example` are only needed if you want to enable credit checkout on your own deployment.

### 3. Prepare the database and start

```bash
npx prisma db push
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

## Project structure

```text
src/app/          Next.js pages and API routes
src/components/   Calendar, composer, navigation, and agent UI
src/lib/          Auth, database, billing, and integration services
prisma/           PostgreSQL schema
```

## Contributing

Issues and pull requests are welcome. Keep provider credentials out of commits, and describe which social platform or workflow your change affects.

## License

MIT. See [LICENSE](LICENSE).
