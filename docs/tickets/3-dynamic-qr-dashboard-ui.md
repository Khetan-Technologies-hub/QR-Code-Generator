# Ticket: Dynamic QR Dashboard UI Implementation

**Brief:** #2

## Story/Why
Registered users need a professional "Command Center" to manage their Dynamic QR codes. This dashboard transforms the technical redirection engine into a user-facing product, allowing marketers to monitor scan counts and update target URLs effortlessly. The goal is to provide total control and confidence over their physical marketing assets.

## Context
This ticket implements the frontend screens for the Dynamic QR Dashboard across both Android (Jetpack Compose) and Web (React/TS). It builds upon the logic implemented in the "Dynamic QR Redirection & Analytics Logic" ticket.

The UI must be a high-fidelity implementation of the provided Figma designs, following the KTech theme and `ui-ux-pro-max` dashboard standards.

## 🔑 Access & prerequisites
- **Design Assets**: Developer must request the Figma/Mockup links from the Manager at `/start-ticket`.
- **API Integration**: The backend "Dynamic QR Engine" (Cloud Functions) must be deployed and accessible.
- **Theme**: KTech theme tokens must be available in `ui.theme` (Android) and the React theme config.

## Scope

### 1. The Dynamic QR Inventory (List View)
Implement a professional data table/grid across both platforms:
- **Columns**:
    - **QR Preview**: A small, clear thumbnail of the generated QR.
    - **Target URL**: The current destination (with smart truncation for long URLs).
    - **Scan Count**: A real-time counter of total scans.
    - **Date Created**: Formatted date string.
    - **Actions**: "Edit" and "Download" buttons.
- **Behavior**:
    - Sortable columns (especially by Scan Count and Date).
    - Empty state handling (when the user has no Dynamic QRs).
    - Loading states with appropriate skeletons.

### 2. The Edit Destination Flow
Implement a side-panel or modal interaction for updating the QR:
- **Input**: A validated text field for the new destination URL.
- **Validation**: Real-time URL format check (must be a valid `http/https` link).
- **Confirmation**: Immediate visual feedback (Toast/Snackbar) upon successful update.

### 3. Asset Download Trigger
- **Action**: "Download" button that triggers the download of the QR image in the user's original chosen format (SVG/PNG/etc.).

## Acceptance Criteria
- [ ] The UI matches the provided Figma designs **exactly** (pixel-perfect).
- [ ] The Inventory list loads data from Firestore and displays it in the data table format.
- [ ] Updating a destination URL via the modal successfully updates the Firestore record.
- [ ] "Download" button correctly fetches and saves the QR asset.
- [ ] The dashboard is fully responsive (Mobile $\rightarrow$ Tablet $\rightarrow$ Desktop).
- [ ] Full Light and Dark mode support is verified.
- [ ] All user-facing strings are routed through i18n/string resources.

## Out of scope
- Advanced analytics charts (handled in future tickets).
- Bulk editing of multiple QRs.
- Managing the "Custom Domain" settings from the UI.

## 🖼️ UI standards
### Design fidelity
- [ ] **Reproduce the provided design exactly.** Match spacing, sizing, color, type, hierarchy, and every state faithfully.
- [ ] **Request design assets** from the PM at `/start-ticket` before building.
- [ ] Pull from **design-system tokens**; no hardcoded colors or sizes.

### Theming & Native Components
- [ ] Ship **both light and dark themes**; verify in both modes.
- [ ] Use **native platform components** (Material 3 for Android, native web equivalents).

### Layout & Responsiveness
- [ ] **Edge-to-edge layout** on Android; content kept out of unsafe areas (notch, nav bar).
- [ ] **Responsive** across phone, tablet, and desktop (reflow layout).
- [ ] Text **ellipsizes** cleanly; no clipping or overlapping.

### Input & Feedback
- [ ] **Right keyboard per field** (URL keyboard for destination links).
- [ ] **Focused fields remain visible** above the keyboard.
- [ ] Define and implement **loading, empty, and error states**.

### Accessibility & Quality
- [ ] **Accessible labels** and content descriptions on all interactive elements.
- [ ] **Min touch target: 44x44px**; Contrast ratio $\ge$ 4.5:1.
- [ ] Honor **dynamic type/font scaling**.

## References
- **Brief #2**: Dynamic QR Dashboard.
- **CLAUDE.md**: For architectural and UI rules.
- **ui-ux-pro-max**: For data-dense dashboard layout guidance.

**Kickoff:** `/start-ticket <#>`
