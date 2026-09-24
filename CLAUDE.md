# CLAUDE.md — QR Code Generator

A professional, high-customization QR code generation platform allowing users to create stylized, colorful, and branded QR codes for free. The project consists of a native Android application and a responsive web application.

## Architecture

### Tech Stack
- **Android App**: Kotlin, Jetpack Compose (Modern declarative UI).
- **Website**: React, TypeScript.
- **Backend**: Firebase (Cloud Functions, Firestore, Auth).
- **Design System**: KTech Theme (Professional, consistent visual language).
- **UI/UX Guidance**: `ui-ux-pro-max` (Accessibility, Touch, Performance).

### Layout & Layers
- `/App`: Android project root.
    - `com.khetantechnologies.qrcodegenerator`: Main package.
    - `ui.theme`: Centralized styling (Color, Type, Theme).
- `/Website`: React project root.
- **Backend (Firebase)**:
    - **Cloud Functions**: Handles server-side QR generation and Dynamic QR redirection.
    - **Firestore**: Stores QR configurations, User profiles, and Dynamic QR mappings.
    - **Firebase Auth**: Manages Social OAuth (Google, Apple, GitHub).

### Data Flow & Rules
- **Input $\rightarrow$ QR**: Support for various input types (URLs, Text, VCards, WiFi, etc.).
- **Dynamic QR Flow**: 
    1. UI $\rightarrow$ Cloud Function $\rightarrow$ Generates unique short-link QR $\rightarrow$ Saves mapping in Firestore $\rightarrow$ Returns QR.
    2. Scanner $\rightarrow$ Short-link $\rightarrow$ Cloud Function $\rightarrow$ Resolves destination from Firestore $\rightarrow$ Redirects user.
- **Customization $\rightarrow$ Rendering**: Customization settings (colors, styles, formats) must be processed by the Firebase Cloud Function to generate the final image/SVG.
- **UI Consistency**: All components must strictly adhere to the KTech theme and the `ui-ux-pro-max` guidelines.

## Key rules

### Coding Conventions
- **Kotlin/Compose**: Use State Hoisting, follow Material 3 guidelines, and maintain a clear separation between business logic and UI.
- **React/TS**: Use functional components, strict typing for all props/state, and modular CSS/Styling.
- **Firebase**: Use the Firebase SDK for client-side interactions (Auth, Firestore) and follow the principle of least privilege in Firestore Security Rules.
- **UI/UX**: 
    - Min touch target: 44x44px.
    - Contrast ratio: $\ge$ 4.5:1.
    - No horizontal scroll on mobile.
    - SVG icons only (no emojis as functional icons).

### Security & Non-Negotiables
- **No Hardcoded Secrets**: API keys or sensitive configs must live in environment variables, `local.properties` (Android), `.env` (Web), or Firebase Secret Manager.
- **Input Validation**: Sanitize all user inputs before processing into QR codes to prevent injection or malformed data.
- **Performance**: Implement lazy loading for images and minimize re-renders in Compose/React. Use Firebase indexing to ensure fast Firestore queries.

## How we work (ticket workflow)
> Full playbook for managers and new joiners: **`docs/PROCESS.md`**.
- **Managers draft tickets** with **`/draft-ticket <what to build>`** — it interviews the manager on the decisions a developer would otherwise have to chase, then produces a ready-to-create issue.
- **Always `git checkout main && git pull` before starting a ticket**, so every `ticket-N` branch builds on the latest merged work. (`/start-ticket` handles this for you.)
- A developer opens a ticket with **`/start-ticket <#>`** — it reads the ticket + this file + the spec, gives a plain-language walkthrough, offers a Q&A (training mode), then **plans and confirms before writing any code.**
- When done, run **`/handoff <#>`** to write `handoffs/ticket-<#>.md` from the **real diff**, then open a PR (the PR template links the handoff).
- The manager reviews with **`/manager-review <PR#>`**.
- If a ticket clashes with this file or the spec, **stop and ask** — don't guess.

## References
- **UI/UX Standard**: `ui-ux-pro-max` skill.
- **Brand Guidelines**: KTech Theme.
- **PRD**: `docs/PRD.md`.
