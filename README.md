# StayBnB — React Frontend

The frontend for **StayBnB**, a room booking platform. Built with React 18, Vite, TypeScript, Tailwind CSS, and shadcn/ui.

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Framework | React 18 |
| Build Tool | Vite |
| Language | TypeScript |
| Styling | Tailwind CSS v4 |
| UI Components | shadcn/ui (Radix UI) |
| Routing | Wouter |
| Data Fetching | TanStack Query (React Query) |
| Forms | React Hook Form + Zod |
| Animations | Framer Motion |
| Icons | Lucide React + React Icons |
| Package Manager | pnpm |

---

## Project Structure

```
stay_bnb_frontend/
├── src/
│   ├── App.tsx                  # Root component with routing
│   ├── main.tsx                 # Entry point
│   ├── index.css                # Global styles + Tailwind
│   ├── components/
│   │   ├── Navbar.tsx           # Top navigation bar
│   │   ├── RoomCard.tsx         # Room listing card
│   │   ├── RoomSkeleton.tsx     # Loading skeleton
│   │   └── ui/                  # shadcn/ui component library
│   ├── context/
│   │   └── AuthContext.tsx      # Authentication state & JWT management
│   ├── hooks/
│   │   ├── use-mobile.tsx       # Responsive breakpoint hook
│   │   └── use-toast.ts         # Toast notification hook
│   ├── lib/
│   │   └── utils.ts             # cn() and utility helpers
│   └── pages/
│       ├── Home.tsx             # Landing page
│       ├── Rooms.tsx            # Browse all rooms
│       ├── RoomDetail.tsx       # Room detail + booking form
│       ├── Login.tsx            # Login page
│       ├── Register.tsx         # Register page
│       ├── Dashboard.tsx        # Guest bookings dashboard
│       ├── HostDashboard.tsx    # Host room management
│       ├── AdminPanel.tsx       # Admin user/room management
│       └── not-found.tsx        # 404 page
├── lib/
│   └── api-client-react/        # Generated API client (TanStack Query hooks)
│       └── src/
│           ├── index.ts
│           ├── custom-fetch.ts
│           └── generated/
│               ├── api.ts       # API hooks (useGetRooms, useCreateBooking, etc.)
│               └── api.schemas.ts
├── public/
│   └── favicon.svg
├── index.html
├── vite.config.ts
├── tsconfig.json
├── components.json              # shadcn/ui config
└── pnpm-workspace.yaml
```

---

## Prerequisites

- **Node.js 18+** — [Download](https://nodejs.org/)
- **pnpm 9+** — Install with `npm install -g pnpm`
- **Backend API running** — Either the [Node.js API server](https://github.com/khushi1218ahuja/staybnb) or the [Spring Boot backend](https://github.com/khushi1218ahuja/stay_bnb_java)

---

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/khushi1218ahuja/stay_bnb_frontend.git
cd stay_bnb_frontend
```

### 2. Install dependencies

```bash
pnpm install
```

> This installs dependencies for both the frontend app and the `lib/api-client-react` package in one command.

### 3. Set environment variables

Create a `.env` file in the project root:

```env
PORT=3000
BASE_PATH=/
VITE_API_URL=http://localhost:8081
```

| Variable | Description | Default |
|----------|-------------|---------|
| `PORT` | Port for the Vite dev server | **Required** |
| `BASE_PATH` | Base URL path for the app (use `/` locally) | **Required** |
| `VITE_API_URL` | URL of the backend API | `http://localhost:8081` |

### 4. Configure the API base URL

Open `lib/api-client-react/src/custom-fetch.ts` and make sure the base URL points to your running backend:

```ts
// It reads from VITE_API_URL at runtime — set it in your .env
```

### 5. Start the development server

```bash
pnpm dev
```

The app will be available at: `http://localhost:3000`

---

## Available Scripts

Run these from the project root:

| Command | Description |
|---------|-------------|
| `pnpm dev` | Start development server with hot reload |
| `pnpm build` | Build for production |
| `pnpm serve` | Preview the production build |
| `pnpm typecheck` | Run TypeScript type checking |

---

## Pages & Routes

| Route | Page | Access |
|-------|------|--------|
| `/` | Home — landing page | Public |
| `/rooms` | Browse all available rooms | Public |
| `/rooms/:id` | Room details + booking form | Public |
| `/login` | Login | Public |
| `/register` | Register | Public |
| `/dashboard` | Guest booking history | Authenticated |
| `/host` | Host room management | Host only |
| `/admin` | Admin panel | Admin only |

---

## Authentication

- On login/register, a JWT token is stored in `localStorage`
- The `AuthContext` provides `user`, `token`, `login()`, and `logout()` across the app
- Protected routes redirect unauthenticated users to `/login`
- The API client automatically attaches the token to all requests via the `Authorization: Bearer` header

---

## Connecting to the Backend

This frontend works with two backend options:

### Option A — Node.js API Server
Clone and run the full monorepo:
```bash
git clone https://github.com/khushi1218ahuja/staybnb.git
```
Set `VITE_API_URL=http://localhost:3001` (or whichever port the Node API runs on).

### Option B — Spring Boot Backend
Clone and run the Java backend:
```bash
git clone https://github.com/khushi1218ahuja/stay_bnb_java.git
```
Set `VITE_API_URL=http://localhost:8081` in your `.env`.

---

## Building for Production

```bash
pnpm build
```

Output will be in the `dist/public/` directory. You can serve it with any static file server:

```bash
npx serve dist/public
```

---

## License

This project is open-source and available under the [MIT License](LICENSE).