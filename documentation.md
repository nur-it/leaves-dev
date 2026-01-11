# LEAVES Project Documentation

## 1. Table of Contents

- [Project Overview](#2-project-overview)
- [Current File Structure Analysis](#3-current-file-structure-analysis)
- [Roadmap to Dynamic Implementation](#4-roadmap-to-dynamic-implementation)
- [Folder Structure Recommendations](#5-folder-structure-recommendations-for-the-dynamic-build)
- [Maintenance & Deployment](#6-maintenance--deployment)

## 2. Project Overview

This project, LEAVES, is a digital legacy platform designed to preserve and share family memories. It functions as a digital archive for life stories, a timeline of significant events, a map of personal history, and a repository for important documents and letters.

The current technology stack consists of:

- **HTML5** for structuring the content.
- **Tailwind CSS** for styling the user interface.
- **Vanilla JavaScript** for interactive elements.

## 3. Current File Structure Analysis

The project is composed of the following HTML files:

- **`index.html`**:
  - **Purpose**: The main dashboard and entry point of the application, providing an overview of the platform's features.
- **`times-of-my-life.html`**:
  - **Purpose**: Contains the interface for recording and organizing life stories.
- **`personas.html`**:
  - **Purpose**: Implements the "Forever Voice™" feature, allowing users to capture audio memories and personal narratives.
- **`life-map.html`**:
  - **Purpose**: Displays an interactive map to visualize important locations and journeys from a person's life.
- **`life-timeline.html`**:
  - **Purpose**: Provides a chronological visualization of life events.
- **`document-archive.html`**:
  - **Purpose**: A secure storage space for important documents.
- **`legacy-letters.html`**:
  - **Purpose**: An interface for writing and storing letters to be delivered in the future.
- **`media-library.html`**:
  - **Purpose**: A gallery for organizing and displaying photos and videos.
- **`marketing.html`**:
  - **Purpose**: The public-facing marketing and informational page that describes the Leaves Family Heritage Hub™ and its suite of applications. It serves as the primary entry point for new users to understand the product's value.

## 4. Roadmap to Dynamic Implementation

To transition this static project into a dynamic, content-manageable platform, we recommend the following phased approach:

### Phase A: Data Modeling (The "Brain")

The first step is to define the structure of the data that will be stored and managed. Based on the existing HTML files, we propose the following schemas:

- **For `legacy-letters.html`**:

  - `title`: String
  - `date`: Date
  - `recipient`: String
  - `bodyText`: Text
  - `scannedImage_URL`: String (URL to an image of a physical letter)

- **For `life-timeline.html`**:

  - `year`: Number
  - `eventTitle`: String
  - `description`: Text
  - `category`: String (e.g., "Career", "Family", "Travel")

- **For `life-map.html`**:
  - `latitude`: Number
  - `longitude`: Number
  - `locationName`: String
  - `memoryDescription`: Text

### Phase B: Recommended Tech Stack for Dynamic Version

We suggest two potential technology stacks for making the LEAVES platform dynamic:

1. **Low Code / CMS (e.g., Sanity.io or Strapi with Next.js)**:

   - **Best for**: Ease of content editing and rapid development. A headless CMS would allow for a user-friendly interface for managing content without requiring technical expertise.
   - **Implementation**: The frontend would be built with a modern framework like Next.js, which would fetch data from the CMS via an API.

2. **Custom Stack (e.g., Node.js/Express + MongoDB)**:
   - **Best for**: Full control and scalability. This option provides the most flexibility for custom features and integrations.
   - **Implementation**: A custom backend would be developed with Node.js and Express, connected to a NoSQL database like MongoDB. The frontend could be built with a framework like React or Vue.js.

### Phase C: Integration Steps

1. **Extract Hardcoded Content**: The static content from the HTML files will be migrated to the chosen database or CMS.
2. **Create API Endpoints**: The backend will expose API endpoints to create, read, update, and delete data.
3. **Replace Static HTML with Dynamic Components**: The frontend will be rebuilt with a modern framework to fetch data from the API and render it dynamically. For example, a `map` function would be used to loop through a list of legacy letters and display them on the page.

## 5. Folder Structure Recommendations (For the Dynamic Build)

For a more scalable and maintainable dynamic application, we recommend the following folder structure:

- **`/components`**: Reusable UI components (e.g., buttons, modals, navigation bars).
- **`/pages`**: The main pages of the application, corresponding to the existing HTML files.
- **`/assets`**: Static assets such as images, fonts, and global CSS files.
- **`/lib`**: Helper functions, API clients, and other utility modules.

## 6. Maintenance & Deployment

- **Current Maintenance**: To update content in the current static version, the HTML files must be manually edited and re-uploaded to the server.
- **Dynamic Version Maintenance**: With a dynamic implementation, content can be updated through a user-friendly CMS or a custom admin panel, without requiring any code changes.

- **Deployment**:
  - **Current**: The static files can be hosted on any simple web server or a service like Netlify or Vercel.
  - **Dynamic**: The application would be deployed as a full-stack project, with the backend and frontend hosted on a platform like Vercel, Heroku, or AWS.
