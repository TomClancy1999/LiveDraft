# LiveDraft

A realtime collaborative markdown workspace built with React, TypeScript, WebSocket, Yjs, and PostgreSQL.

LiveDraft enables multiple users to edit markdown documents simultaneously with low-latency synchronization, live cursor presence, inline comments, and persistent document storage.

---

## Motivation

Modern collaborative tools such as Notion and Google Docs provide seamless real-time editing experiences, but building these systems requires solving challenges around concurrent editing, synchronization, persistence, and responsiveness.

LiveDraft was created to explore the design and implementation of collaborative applications using CRDT-based synchronization and modern web technologies.

---

## Features

### Realtime Collaboration

- Multi-user collaborative editing
- Conflict-free synchronization using Yjs CRDT
- Low-latency updates over WebSocket
- Automatic synchronization across connected clients

### Live Presence

- Cursor presence visualization
- Active user awareness
- Session synchronization

### Document Management

- Markdown document editing
- Automatic persistence
- Snapshot-based recovery
- Document history tracking

### Collaboration Workflows

- Inline comments
- Shared document sessions
- Real-time update propagation

---

## Architecture

```text
React Client
    │
    ▼
WebSocket Layer
    │
    ▼
Hocuspocus Server
    │
    ▼
Yjs CRDT Engine
    │
    ▼
PostgreSQL
```

### Frontend

- React
- TypeScript
- Tiptap
- Yjs Client

### Backend

- Node.js
- Hocuspocus
- WebSocket

### Storage

- PostgreSQL

---

## Design Decisions

### Why Yjs?

Concurrent edits from multiple users can create synchronization conflicts.

LiveDraft uses Yjs, a CRDT framework, to merge updates automatically while maintaining consistency across connected clients.

### Why WebSocket?

Collaborative editing requires low-latency bidirectional communication.

WebSocket enables efficient propagation of document updates, cursor movements, and collaboration events.

### Why Snapshot-Based Persistence?

Writing every keystroke directly to the database creates excessive write traffic.

LiveDraft periodically stores document snapshots and batches updates to reduce database overhead during high-frequency editing sessions.

### Why PostgreSQL?

PostgreSQL provides reliable persistence for:

- User metadata
- Documents
- Comments
- Snapshots

while collaborative state remains synchronized through Yjs.

---

## Performance Optimizations

### Update Batching

Multiple document updates are grouped together before synchronization to reduce network overhead.

### Debounced Persistence

Document changes are persisted periodically instead of after every edit, reducing redundant database writes during active editing sessions.

### Incremental Synchronization

Only document updates are transmitted rather than full document states, improving responsiveness and reducing bandwidth usage.

---

## Future Improvements

- Role-based permissions
- Shareable links
- Offline editing support
- Version history
- AI-assisted writing workflows
- Rich-text collaboration

---

## Tech Stack

### Frontend

- React
- TypeScript
- Tiptap

### Backend

- Node.js
- Hocuspocus
- WebSocket

### Database

- PostgreSQL

### Collaboration

- Yjs
- CRDT
