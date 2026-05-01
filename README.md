# NoteAppAssignment

A React Native note-taking application with local persistence, cloud sync, and real-time connectivity.

## Features

- Create, read, update, and delete notes
- Input validation for note title/content
- Favorite and unfavorite notes
- Local persistence using AsyncStorage
- Cloud connectivity with REST API (Express + SQLite)
- Real-time status updates using Socket.IO
- Multi-level navigation using Drawer + Stack + Bottom Tabs

## App Modules

- `App.tsx` - app entry point and navigation container
- `navigation/` - app navigators (`DrawerNavigator`, `StackNavigator`, `TabNavigator`)
- `screens/` - UI screens (Notes, Favorites, Cloud, Add/Edit, Profile, Settings)
- `components/` - reusable UI components (`CustomButton`, `CustomInput`, `NoteCard`)
- `storage/noteStorage.ts` - local note persistence logic
- `services/api.ts` - REST and WebSocket client service
- `server.js` - backend API server and Socket.IO setup

## Data Model

Each note stores:

- `id`
- `title`
- `content`
- `isFavorite`
- `updatedAt`
- `syncStatus` (`pending`, `synced`, `failed`)

## Data Persistence

AsyncStorage keys used in the project:

- `NOTES` - notes list
- `USER_PROFILE` - profile data
- `APP_SETTINGS` - app settings (auto sync, sync badge visibility)

## Cloud Connectivity

### REST API Endpoints

- `GET /api/notes`
- `GET /api/notes/:id`
- `POST /api/notes`
- `PUT /api/notes/:id`
- `DELETE /api/notes/:id`

### WebSocket

- Namespace: `/notes`
- Events used:
  - Client -> Server: `client_connected`, `client_send`
  - Server -> Client: `server_send`

## Setup

### 1) Start backend server

```bash
node server.js
```

Server runs on port `5000`.

### 2) Base URL note

Current mobile API base URL in `services/api.ts` is:

`http://10.0.2.2:5000`

This is for Android emulator access to host localhost.

- Android emulator: use `10.0.2.2`
- Physical device: replace with your PC LAN IP
- iOS simulator: usually `http://localhost:5000`

### 3) Run the app

Use your usual React Native command, for example:

```bash
npx react-native run-android
```

## Sync Behavior

- New/updated/favorited notes are marked `pending`
- Cloud sync uploads pending notes
- Successful upload sets status to `synced`
- Failed upload sets status to `failed`
- Cloud screen shows WebSocket status and activity logs

## Authors

- Name: Charles Tiong Jung Zhi, Cheng Jun Yan, Justin Yii Zhu Yong, Lee San Hung
- Student ID: 2305101,
- Course: UECS3253 Wireless Application Development
