# PRD: QR Code Generator

## Overview & Vision
The QR Code Generator is a professional-grade platform designed for small business owners and marketers who require high-fidelity, branded QR codes. Unlike generic generators, this tool focuses on **Unmatched Design Control**, allowing users to create "artistic" QR codes with custom logos, gradients, and unique shapes without sacrificing scannability.

**Winning State**: The industry standard for "Designer QR Codes"—providing the most advanced styling options for free while maintaining a professional, KTech-branded experience.

## Goals & Non-Goals
### Goals
- **Design Supremacy**: Provide the most advanced styling options (logos, gradients, custom shapes).
- **Multi-Platform Presence**: Seamless experience across Android (Kotlin/Compose) and Web (React/TS).
- **Professional Output**: High-resolution exports in SVG, PDF, and Raster formats.
- **Future-Proofing**: Support for Dynamic QRs (updatable destination links).

### Non-Goals
- **Social Networking**: No community sharing or "QR galleries."
- **Enterprise Management**: No complex organization-level permission systems for v1.
- **Payment Processing**: While "Premium" features may be planned, v1 is focused on the free utility.

## Target Users & Roles
| Role | Description | Permissions |
| :--- | :--- | :--- |
| **Guest** | Anonymous user wanting a quick QR code. | Generate static QRs, Basic/Advanced styling, Export. |
| **Registered User** | User with an account (via OAuth). | All Guest permissions + Save customizations, QR history, Manage Dynamic QRs. |

## System Architecture

### High-Level Flow
`Android App` $\leftrightarrow$ `Centralized API` $\leftrightarrow$ `Database/Storage`
`Website` $\leftrightarrow$ `Centralized API` $\leftrightarrow$ `Database/Storage`

### Tech Stack
- **Android**: Kotlin, Jetpack Compose.
- **Website**: React, TypeScript.
- **Backend**: Centralized API (Server-side generation).
- **Authentication**: Social Auth (OAuth - Google/Apple/GitHub).
- **Design System**: KTech Theme + `ui-ux-pro-max` guidelines.

### Key Technical Decisions
- **Server-Side Generation**: All QR rendering is handled by the API. This enables Dynamic QRs and consistent output across platforms.
- **Dynamic QR Logic**: The API generates a unique "short-link" QR. The server maps this link to the final destination, allowing the destination to be updated in the database without changing the QR image.

## Feature Spec

### 1. QR Generation Engine
- **Input Types**:
    - Basic: Plain Text, URLs, Email.
    - Advanced: WiFi (SSID/Pass), VCards, Calendar events.
- **Styling Options**:
    - **Colors**: Foreground/Background (solid & gradients).
    - **Shapes**: Customizable pixel shapes (dots, rounded, etc.) and "Eye" (finder pattern) styles.
    - **Branding**: Center logo overlay with auto-scaling for scannability.
- **Export Formats**: SVG (Vector), PDF, PNG, and JPG.

### 2. Account & Management
- **OAuth Integration**: One-click login via social providers.
- **Local History**: Cache of recently generated QRs for Guests.
- **Cloud History**: Persistent storage of QR configurations for Registered Users.
- **Dynamic QR Dashboard**: Interface to update destination URLs for previously generated Dynamic QRs.

### 3. UI/UX (KTech Theme)
- **Fidelity**: Pixel-perfect match to approved Figma/Mockups.
- **Responsiveness**: Adaptive layout for Mobile $\rightarrow$ Tablet $\rightarrow$ Desktop.
- **Theming**: Full Light and Dark mode support.

## Non-Functional Requirements
- **Scannability**: Every stylized QR must be verified for scannability across major OS (iOS/Android) before export.
- **Performance**: API response time for QR generation $\le$ 500ms.
- **Accessibility**: WCAG AA compliance (Contrast $\ge$ 4.5:1, accessible labels).
- **Security**: No hardcoded secrets; secure handling of OAuth tokens.

## Open Decisions
- **Backend Language**: Specific language for the Centralized API (e.g., Node.js, Python, or Go) to be decided during architecture phase.
- **Storage**: Choice of database for Dynamic QR mapping (e.g., PostgreSQL vs MongoDB).

## Decision Log
| Date | Decision | Rationale |
| :--- | :--- | :--- |
| 2026-09-24 | Design-First Vision | Focus on "Unmatched Design Control" to differentiate from competitors. |
| 2026-09-24 | Server-Side Generation | Necessary to support Dynamic QRs and maintain consistency. |
| 2026-09-24 | Centralized API | Avoids duplicating logic across Android and Web. |
| 2026-09-24 | Social Auth | Reduces friction for the "Optional Accounts" feature. |
| 2026-09-24 | Dynamic QR Support | Adds high-value utility for marketers (change link after print). |
