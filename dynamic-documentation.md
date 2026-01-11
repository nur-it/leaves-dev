# LEAVES Platform: Dynamic Conversion Documentation

This document outlines the requirements for converting the static HTML pages of the LEAVES project into a dynamic web application. It covers data models, API endpoints, and component-based architecture for each page.

## General Architecture

The application will be refactored to use a modern frontend framework (e.g., React, Vue, or Svelte) to manage state and render dynamic content. A backend API will serve data from a database.

### Key UI Components

- **Header**: The main navigation header is consistent across all pages. It should be a reusable component that fetches user information and notification data.
- **Custom Scrollbar**: The custom scrollbar styles should be applied globally.
- **Tailwind CSS Configuration**: The existing `tailwind.config.js` defines the color palette and custom styles, which should be integrated into the new frontend project.

### API Design Philosophy

All API endpoints should be RESTful and return data in JSON format. Authentication and authorization should be handled for all endpoints that deal with user-specific data.

## Table of Contents

1.  [`index.html` - Dashboard](#1-indexhtml---dashboard)
2.  [`legacy-letters.html` - Legacy Letters](#2-legacy-lettershtml---legacy-letters)
3.  [`life-map.html` - Life Map](#3-life-maphtml---life-map)
4.  [`life-timeline.html` - Life Timeline](#4-life-timelinehtml---life-timeline)
5.  [`media-library.html` - Media Library](#5-media-libraryhtml---media-library)
6.  [`personas.html` - Forever Voice™](#6-personashtml---forever-voice)
    7s. [`times-of-my-life.html` - Times of My Life](#7-times-of-my-lifehtml---times-of-my-life)
7.  [`document-archive.html` - Document Archive](#8-document-archivehtml---document-archive)

## Page-Specific Documentation

### 1. `index.html` - Dashboard

The main dashboard provides a summary of recent activities and upcoming events.

#### Data Models

- **User**:

  - `userId`: String (or Integer)
  - `name`: String
  - `profileImageUrl`: String

- **Activity**:

  - `activityId`: String (or Integer)
  - `type`: String (e.g., "New Memory", "Photo Uploaded", "Letter Written")
  - `description`: String
  - `timestamp`: DateTime
  - `user`: User (a reference to the user who performed the activity)

- **Event**:
  - `eventId`: String (or Integer)
  - `title`: String
  - `date`: DateTime
  - `location`: String (optional)

#### API Endpoints

- `GET /api/user/me`: Fetches the current user's information.
- `GET /api/activities/recent`: Fetches a list of recent activities.
- `GET /api/events/upcoming`: Fetches a list of upcoming events.

#### Components

- **WelcomeMessage**: Displays "Welcome back, [User Name]!".
  - Props: `userName: String`
- **RecentActivityFeed**: A list of `ActivityItem` components.
  - Props: `activities: Array<Activity>`
- **UpcomingEvents**: A list of `EventItem` components.
  - Props: `events: Array<Event>`

### 2. `legacy-letters.html` - Legacy Letters

This page allows users to write, view, and manage their legacy letters.

#### Data Models

- **Letter**:
  - `letterId`: String (or Integer)
  - `title`: String
  - `content`: String (rich text)
  - `recipient`: String
  - `status`: String (e.g., "Draft", "Scheduled", "Sent")
  - `scheduledAt`: DateTime (optional)
  - `createdAt`: DateTime
  - `updatedAt`: DateTime

#### API Endpoints

- `GET /api/letters`: Fetches all letters for the current user.
- `GET /api/letters/:letterId`: Fetches a single letter by its ID.
- `POST /api/letters`: Creates a new letter.
- `PUT /api/letters/:letterId`: Updates an existing letter.
- `DELETE /api/letters/:letterId`: Deletes a letter.

#### Components

- **LetterList**: Displays a list of letters with their title, recipient, and status.
  - Props: `letters: Array<Letter>`
- **LetterEditor**: A rich text editor for writing and editing letters.
  - Props: `letter: Letter`, `onSave: Function`
- **LetterView**: Displays a single letter.
  - Props: `letter: Letter`

### 3. `life-map.html` - Life Map

This page displays an interactive map with pins marking significant locations in the user's life.

#### Data Models

- **Location**:

  - `locationId`: String (or Integer)
  - `name`: String
  - `description`: String
  - `latitude`: Float
  - `longitude`: Float
  - `date`: DateTime
  - `media`: Array of Media objects (images, videos) associated with this location.

- **Media**:
  - `mediaId`: String (or Integer)
  - `type`: String ("image", "video")
  - `url`: String
  - `caption`: String

#### API Endpoints

- `GET /api/locations`: Fetches all locations for the current user.
- `POST /api/locations`: Adds a new location.
- `PUT /api/locations/:locationId`: Updates a location's details.
- `DELETE /api/locations/:locationId`: Removes a location.

#### Components

- **LifeMap**: The main map component (e.g., using Leaflet or Google Maps) that renders location pins.
  - Props: `locations: Array<Location>`
- **LocationPin**: A clickable pin on the map.
  - Props: `location: Location`, `onClick: Function`
- **LocationDetails**: A modal or sidebar that displays information about a selected location, including its media gallery.
  - Props: `location: Location`

### 4. `life-timeline.html` - Life Timeline

This page presents a chronological timeline of the user's life events.

#### Data Models

- **TimelineEvent**:
  - `eventId`: String (or Integer)
  - `title`: String
  - `description`: String
  - `date`: DateTime
  - `type`: String (e.g., "Birth", "Education", "Career", "Family")
  - `media`: Array of Media objects associated with this event.

#### API Endpoints

- `GET /api/timeline/events`: Fetches all timeline events for the current user.
- `POST /api/timeline/events`: Adds a new event to the timeline.
- `PUT /api/timeline/events/:eventId`: Updates a timeline event.
- `DELETE /api/timeline/events/:eventId`: Removes an event from the timeline.

#### Components

- **TimelineBoard**: The main component that renders the timeline and its events.
  - Props: `events: Array<TimelineEvent>`
- **TimelineEventMarker**: A clickable marker on the timeline.
  - Props: `event: TimelineEvent`, `onClick: Function`
- **EventDetails**: A modal or sidebar that displays information about a selected event.
  - Props: `event: TimelineEvent`

### 5. `media-library.html` - Media Library

This page provides a gallery view of all the user's uploaded media.

#### Data Models

- **Media**: (Same as the one defined in `life-map.html`)
  - `mediaId`: String (or Integer)
  - `type`: String ("image", "video", "audio")
  - `url`: String
  - `thumbnailUrl`: String (for videos)
  - `caption`: String
  - `tags`: Array of Strings
  - `uploadedAt`: DateTime

#### API Endpoints

- `GET /api/media`: Fetches all media for the current user, with filtering and sorting options (e.g., by tag, date).
- `POST /api/media/upload`: Uploads a new media file.
- `PUT /api/media/:mediaId`: Updates media metadata (caption, tags).
- `DELETE /api/media/:mediaId`: Deletes a media file.

#### Components

- **MediaGrid**: A grid or list view of media items.
  - Props: `media: Array<Media>`
- **MediaFilter**: Controls for filtering and sorting the media library.
- **MediaUploader**: A component for uploading new files.
- **MediaViewer**: A modal or separate view to display a single media item in full size, with its details.
  - Props: `media: Media`

### 6. `personas.html` - Forever Voice™

This page contains the "Forever Voice™" feature, an AI-powered chat interface that allows users to interact with a digital persona.

#### Data Models

- **Persona**:

  - `personaId`: String (or Integer)
  - `name`: String
  - `avatarUrl`: String
  - `description`: String

- **ChatMessage**:

  - `messageId`: String (or Integer)
  - `text`: String
  - `sender`: String ("user" or "persona")
  - `timestamp`: DateTime

- **ChatSession**:
  - `sessionId`: String (or Integer)
  - `persona`: Persona
  - `messages`: Array of ChatMessage objects

#### API Endpoints

- `GET /api/personas`: Fetches the available personas for the user.
- `GET /api/chat/sessions/:personaId`: Retrieves or creates a chat session with a specific persona.
- `POST /api/chat/sessions/:sessionId/messages`: Sends a user's message and receives the persona's response. This endpoint will interact with a language model service.

#### Components

- **PersonaSelector**: Allows the user to choose which persona to talk to.
  - Props: `personas: Array<Persona>`, `onSelect: Function`
- **ChatWindow**: The main chat interface that displays the conversation.
  - Props: `session: ChatSession`
- **MessageBubble**: Renders a single chat message, with different styles for the user and the persona.
  - Props: `message: ChatMessage`
- **ChatInput**: The input field for the user to type and send messages.
  - Props: `onSendMessage: Function`

### 7. `times-of-my-life.html` - Times of My Life

This page allows users to record and browse stories from different periods of their life.

#### Data Models

- **LifePeriod**:

  - `periodId`: String (or Integer)
  - `title`: String (e.g., "Childhood", "Teenage Years", "Early Adulthood")
  - `description`: String

- **Story**:
  - `storyId`: String (or Integer)
  - `title`: String
  - `content`: String (rich text)
  - `period`: LifePeriod
  - `createdAt`: DateTime
  - `updatedAt`: DateTime

#### API Endpoints

- `GET /api/life-periods`: Fetches all life periods.
- `GET /api/stories?period=:periodId`: Fetches all stories for a given life period.
- `POST /api/stories`: Creates a new story.
- `PUT /api/stories/:storyId`: Updates a story.
- `DELETE /api/stories/:storyId`: Deletes a story.

#### Components

- **LifePeriodTabs**: Tabs to switch between different life periods.
  - Props: `periods: Array<LifePeriod>`, `onSelect: Function`
- **StoryList**: Displays a list of stories for the selected period.
  - Props: `stories: Array<Story>`
- **StoryEditor**: A rich text editor for writing and editing stories.
  - Props: `story: Story`, `onSave: Function`
- **StoryView**: Displays a single story.
  - Props: `story: Story`

### 8. `document-archive.html` - Document Archive

This page allows users to upload, categorize, and view important documents.

#### Data Models

- **Document**:
  - `documentId`: String (or Integer)
  - `title`: String
  - `description`: String
  - `fileUrl`: String
  - `thumbnailUrl`: String (for generating previews)
  - `category`: String (e.g., "Financial", "Legal", "Personal")
  - `uploadedAt`: DateTime

#### API Endpoints

- `GET /api/documents`: Fetches all documents for the current user, with filtering by category.
- `POST /api/documents/upload`: Uploads a new document.
- `PUT /api/documents/:documentId`: Updates document metadata.
- `DELETE /api/documents/:documentId`: Deletes a document.

#### Components

- **DocumentGrid**: A grid or list view of documents.
  - Props: `documents: Array<Document>`
- **DocumentFilter**: Controls for filtering documents by category.
- **DocumentUploader**: A component for uploading new documents.
- **DocumentViewer**: A modal or view to display a document preview.
  - Props: `document: Document`
