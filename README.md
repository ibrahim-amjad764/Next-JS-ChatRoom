#  Realtime Chat Application

A modern, real-time chat application built with **Next.js 16**, **Socket.IO**, **TypeORM**, and **Firebase Authentication**. Features include chat rooms, instant messaging with database persistence, typing indicators, and online user status.



##  Features

-  **Firebase Authentication** - Secure user login/signup
-  **Realtime Messaging** - Instant message delivery via Socket.IO
-  **Chat Rooms** - Create and join multiple chat rooms
-  **Database Persistence** - Messages stored in PostgreSQL/SQLite via TypeORM
-  **Online Users** - See who's online in real-time
-  **Typing Indicators** - See when someone is typing
-  **Responsive Design** - Works on desktop and mobile
-  **Optimistic UI** - Instant feedback before server confirmation
-  **State Management** - Zustand for client-side state

##  Project Structure

```
my-apps/
├── 📁 app/                          # Next.js App Router
│   ├── 📁 api/                      # API Routes
│   │   ├── 📁 rooms/                # Room management API
│   │   │   ├── 📁 [roomId]/
│   │   │   │   ├── 📁 join/         # Join room endpoint
│   │   │   │   └── 📁 messages/     # Messages API (GET/POST)
│   │   │   └── route.js             # Rooms CRUD
│   │   └── 📁 users/                # User management API
│   │       ├── 📁 [uid]/
│   │       │   └── 📁 rooms/        # User-specific rooms
│   │       └── route.js             # User sync endpoint
│   ├── 📁 chat/
│   │   └── 📁 [roomId]/             # Chat room page
│   │       └── page.jsx
│   ├── 📁 home/                     # Home dashboard
│   │   └── page.jsx
│   ├── 📄 layout.jsx                # Root layout
│   └── 📄 page.jsx                  # Landing page
│
├── 📁 components/                   # React Components
│   ├── 📄 ChatWindow.jsx            # Main chat interface
│   ├── 📄 MessageBubble.jsx         # Individual message display
│   ├── 📄 RoomList.jsx              # Chat rooms sidebar
│   ├── 📄 OnlineUsers.jsx           # Online users list
│   └── 📄 CreateRoomModal.jsx       # Room creation modal
│
├── 📁 services/                     # External services
│   ├── 📄 firebase.js               # Firebase auth config
│   └── 📄 socket.js                 # Socket.IO client service
│
├── 📁 store/                        # Zustand state management
│   ├── 📄 useAuthStore.js           # Authentication state
│   └── 📄 useChatStore.js           # Chat state (rooms, messages)
│
├── 📁 server/                       # Socket.IO Server
│   └── 📄 server.js                 # Real-time server with DB integration
│
├── 📁 database/                     # TypeORM configuration
│   ├── 📄 data-source.ts            # Database connection config
│   ├── 📄 migrate.ts                # Migration runner
│   └── 📁 migrations/               # Database migrations
│       ├── 📄 001_CreateUsers.ts
│       ├── 📄 002_CreateRooms.ts
│       ├── 📄 003_CreateRoomMembers.ts
│       └── 📄 004_CreateMessages.ts
│
├── 📁 entities-schema/              # TypeORM Entities
│   ├── 📄 user.ts                   # User entity
│   ├── 📄 room.ts                   # Room entity
│   ├── 📄 room_member.ts            # Room membership entity
│   └── 📄 message.ts                # Message entity
│
├── 📁 lib/                          # Utilities
│   └── 📄 db.js                     # Database initialization helper
│
├── 📁 utils/                        # Helper functions
│   └── 📄 helpers.js
│
├── 📄 package.json                  # Dependencies & scripts
├── 📄 next.config.ts                # Next.js configuration
├── 📄 tailwind.config.js            # Tailwind CSS config
├── 📄 tsconfig.json                # TypeScript configuration
└── 📄 .env                          # Environment variables
```

##  Getting Started

### Prerequisites

- **Node.js** v18+ 
- **npm** or **yarn**
- **PostgreSQL** (or SQLite for development)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/realtime-chat.git
   cd realtime-chat
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Environment Setup**
   Create `.env` file in root:
   ```env
   # Database
   DB_HOST=localhost
   DB_PORT=5432
   DB_USER=postgres
   DB_PASSWORD=yourpassword
   DB_NAME=chat_app
   DB_TYPE=postgres  # or 'sqlite' for dev

   # Firebase
   NEXT_PUBLIC_FIREBASE_API_KEY=your_api_key
   NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
   NEXT_PUBLIC_FIREBASE_PROJECT_ID=your_project
   NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=your_project.appspot.com
   NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=123456789
   NEXT_PUBLIC_FIREBASE_APP_ID=1:123456789:web:abcdef

   # Socket Server
   SOCKET_PORT=4000
   NEXT_PUBLIC_SOCKET_URL=http://localhost:4000
   ```

4. **Database Setup**
   ```bash
   # Run migrations
   npm run migration:run
   
   # Or sync schema directly
   npm run schema:sync
   ```

5. **Start Development Servers**
   
   Terminal 1 - Next.js:
   ```bash
   npm run dev
   ```
   
   Terminal 2 - Socket Server:
   ```bash
   npm run server
   ```

6. **Open browser**
   Navigate to `http://localhost:3000`

##  Available Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start Next.js dev server (port 3000) |
| `npm run server` | Start Socket.IO server (port 4000) |
| `npm run build` | Build production app |
| `npm run start` | Start production server |
| `npm run lint` | Run ESLint |
| `npm run migration:generate` | Generate TypeORM migration |
| `npm run migration:run` | Run pending migrations |
| `npm run migration:revert` | Revert last migration |
| `npm run schema:sync` | Sync database schema |

## 🔌 API Endpoints

### Rooms
- `GET /api/rooms` - Get all rooms
- `POST /api/rooms` - Create new room
- `POST /api/rooms/:roomId/join` - Join a room

### Messages
- `GET /api/rooms/:roomId/messages` - Get room messages
- `POST /api/rooms/:roomId/messages` - Send message

### Users
- `POST /api/users` - Sync user with database
- `GET /api/users/:uid/rooms` - Get user's rooms

##  Tech Stack

| Category | Technology |
|----------|------------|
| **Framework** | Next.js 16 (App Router) |
| **UI** | React 19, TailwindCSS 4 |
| **State** | Zustand (with persistence) |
| **Auth** | Firebase Authentication |
| **Realtime** | Socket.IO 4 |
| **Database** | PostgreSQL / SQLite |
| **ORM** | TypeORM 0.3 |
| **Server** | Node.js + tsx |

##  Key Features Explained

### Real-time Architecture
```
┌─────────────┐     Socket.IO     ┌─────────────┐
│   Browser   │ ◄───────────────► │   Server    │
│  (Client)   │                   │  (Port 4000)│
└─────────────┘                   └──────┬──────┘
      │                                  │
      │ HTTP API                         │ TypeORM
      ▼                                  ▼
┌─────────────┐                   ┌─────────────┐
│  Next.js    │                   │  Database   │
│  API Routes │                   │ PostgreSQL  │
└─────────────┘                   └─────────────┘
```

### Message Flow
1. User sends message → Optimistic UI update (Zustand)
2. Socket.IO broadcasts to room members
3. API saves to database (TypeORM)
4. API response updates message with real ID

##  Troubleshooting

### Socket connection issues
```bash
# Check if server is running
curl http://localhost:4000/socket.io/
```

### Database connection errors
```bash
# Verify DB credentials in .env
# Check PostgreSQL is running
pg_isready -h localhost -p 5432
```

### Migration errors
```bash
# Reset database
npm run schema:drop
npm run migration:run
```

##  License

MIT License - feel free to use this project for personal or commercial purposes.

##  Author

**Ibrahim Amjad** - [@ibrahim-amjad764](https://github.com/ibrahim-amjad764)

---

 Star this repo if you found it helpful!
