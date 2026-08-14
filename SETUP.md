# Setup Guide

## Workshop https://agent-foundations-globant-bwsdt7z5t.vercel.app/docs
## Vercel deployment
- https://vercel.com/globant-agent-foundations-workshop/my-agent2
- https://vercel.com/martinaguila-4137s-projects/vercel-agent-foundations-certification

This repository contains two applications:
1. **Next.js Storefront** (Ship It Shop) - runs on port 3000
2. **Eve Agent** (AI agent) - runs on port 2000


## Prerequisites

- **Node.js**: v24.19.0 or later
- **pnpm**: v11.21.0 or later (this project uses pnpm)
- **Git**: For version control

## Project Structure

```
vercel-agent-foundations-certification/
├── app/                    # Next.js app routes
├── components/             # React components
├── lib/                    # Utilities, API client, types
├── my-agent/              # Eve AI agent (separate app)
│   ├── agent/             # Agent configuration
│   │   ├── agent.ts       # Agent definition
│   │   ├── instructions.md # Agent instructions
│   │   └── channels/      # Communication channels
│   └── package.json       # Eve dependencies
├── .env.local             # Next.js environment variables
└── package.json           # Next.js dependencies
```

---

## 🚀 Starting the Next.js Storefront (Port 3000)

### 1. Install Dependencies

```bash
# From project root
pnpm install
```

### 2. Configure Environment Variables

Create `.env.local` in the project root:

```bash
# Required for API access
VERCEL_PROTECTION_BYPASS_SECRET=your_bypass_secret_here

# Optional - defaults to Vercel's API
API_BASE_URL=https://vercel-agentic-swag-store-api.vercel.app/api
```

**Important:** Get your `VERCEL_PROTECTION_BYPASS_SECRET` from the Vercel dashboard or instructor.

### 3. Start the Development Server

```bash
pnpm dev
```

The app will be available at: **http://localhost:3000**

### 4. Verify the Setup

- Navigate to http://localhost:3000
- You should see the Ship It Shop storefront
- Browse products, add to cart, etc.

### Build for Production

```bash
pnpm build    # Create production build
pnpm start    # Serve production build
```

---

## 🤖 Starting the Eve Agent (Port 2000)

### 1. Navigate to the Agent Directory

```bash
cd my-agent
```

### 2. Install Agent Dependencies

```bash
pnpm install
```

### 3. Configure Environment (Optional)

Create `.env.local` in the `my-agent/` directory if you need custom configuration:

```bash
# Optional: AI Gateway API Key
AI_GATEWAY_API_KEY=your_api_key_here
```

**Note:** For local development, the agent uses `localDev()` auth and works without credentials.

### 4. Start the Eve Dev Server

```bash
pnpm dev
```

The agent will be available at: **http://127.0.0.1:2000/**

You should see:
```
☰eve  v0.37.0
[DEV] server listening at http://127.0.0.1:2000/
```

### 5. Interact with the Agent

**Option A: Use the eve CLI**
```bash
# In the my-agent directory
pnpm exec eve chat
```

**Option B: Use HTTP requests**
Send POST requests to http://127.0.0.1:2000/

### Agent Configuration

- **Model**: `zai/glm-5.2`
- **Instructions**: Located in `agent/instructions.md`
- **Channels**: Configured in `agent/channels/eve.ts`

---

## 🔄 Running Both Apps Simultaneously

To run both the storefront and the agent at the same time:

### Terminal 1: Next.js App
```bash
# From project root
pnpm dev
```
**Runs on:** http://localhost:3000

### Terminal 2: Eve Agent
```bash
# From project root
cd my-agent
pnpm dev
```
**Runs on:** http://127.0.0.1:2000

---

## 📝 Common Commands

### Next.js Storefront
```bash
pnpm dev          # Start dev server (port 3000)
pnpm build        # Build for production
pnpm start        # Serve production build
pnpm lint         # Run linter (currently not configured)
```

### Eve Agent
```bash
cd my-agent
pnpm dev          # Start eve dev server (port 2000)
pnpm build        # Build agent
pnpm start        # Start production agent
pnpm exec eve chat    # Interactive chat with agent
```

---

## 🐛 Troubleshooting

### Next.js App Issues

**Port 3000 already in use:**
```bash
# Kill the process using port 3000
lsof -ti:3000 | xargs kill -9
# Or use a different port
PORT=3001 pnpm dev
```

**Missing VERCEL_PROTECTION_BYPASS_SECRET:**
- Error: API calls fail with 403
- Solution: Add the secret to `.env.local`

**Images not loading:**
- Check `next.config.mjs` has correct image domains whitelisted
- Verify API is returning valid image URLs

### Eve Agent Issues

**Port 2000 already in use:**
```bash
# Kill the process using port 2000
lsof -ti:2000 | xargs kill -9
```

**AI Gateway authentication failed:**
- For local dev, this shouldn't happen (uses `localDev()` auth)
- If it does, run: `eve link` or set `AI_GATEWAY_API_KEY` in `.env.local`

**Model not responding:**
- Verify the model `zai/glm-5.2` is available
- Check eve logs in `my-agent/.eve/logs/`

---

## 🔐 Security Notes

- **Never commit `.env.local`** - it's already in `.gitignore`
- **Never commit secrets** - use environment variables
- The `VERCEL_PROTECTION_BYPASS_SECRET` must remain server-side
- The `my-agent/` folder is gitignored to avoid committing runtime artifacts

---

## 📚 Additional Resources

- **Next.js Documentation**: https://nextjs.org/docs
- **Eve Framework**: https://eve.dev/docs
- **Project Instructions**: See `CLAUDE.md` in project root
- **Agent Instructions**: See `my-agent/AGENTS.md`

---

## 🎯 Quick Start Checklist

- [ ] Install pnpm (`npm install -g pnpm`)
- [ ] Clone repository
- [ ] Install Next.js dependencies (`pnpm install`)
- [ ] Create `.env.local` with `VERCEL_PROTECTION_BYPASS_SECRET`
- [ ] Start Next.js app (`pnpm dev`)
- [ ] Install eve agent dependencies (`cd my-agent && pnpm install`)
- [ ] Start eve agent (`pnpm dev` from my-agent directory)
- [ ] Test both apps are running

---

**Last Updated:** 2026-08-13  
**Next.js Version:** 16  
**Eve Version:** 0.37.0
