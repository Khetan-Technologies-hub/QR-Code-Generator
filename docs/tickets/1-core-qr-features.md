# Ticket: Core QR Generation Engine & UI Implementation

**Brief:** N/A (Core Foundation)

## Story/Why
As a user, I want to be able to convert various types of data (URLs, WiFi, Contacts, etc.) into highly customized QR codes that I can export in multiple professional formats, so that I can use them for both digital and print branding.

## Context
This ticket establishes the foundational QR generation capabilities for both the Android (Kotlin/Compose) and Website (React/TS) platforms. We are using a library-based approach to ensure stability and standards compliance while layering high-level customization on top.

The UI must match the existing approved designs exactly. The developer is required to request the Figma/Mockup assets from the manager during `/start-ticket`.

## 🔑 Access & prerequisites
- **Design Assets**: Developer must request Figma/Mockup links from the Manager at `/start-ticket`.
- **Dependencies**:
    - Android: Research and integrate a stable QR library (e.g., ZXing).
    - Web: Research and integrate a stable QR library (e.g., qrcode.react).
- **KTech Theme**: Ensure `ui.theme` (Android) and the React theme config are initialized.

## Scope

### 1. Input Support
Implement generators for the following data types:
- **Basic**: Plain Text, URLs, Email.
- **Advanced**: WiFi networks (SSID, Password, Encryption), VCards (Contact info), and Calendar events.

### 2. Customization Engine
Implement the ability to modify the following visual properties:
- **Basic Styling**: 
    - Foreground (pixel) color.
    - Background color.
    - Finder pattern ('eye') styles.
- **Advanced Styling**:
    - Center logo overlay (image upload/selection).
    - Pixel shape (e.g., rounded corners vs. square).
    - Gradient fills for pixels.

### 3. Export System
Allow users to download/save the generated QR in:
- **Raster**: PNG and JPG.
- **Vector**: SVG.
- **Document**: PDF.

## Acceptance Criteria
- [ ] All listed input types generate valid, scannable QR codes.
- [ ] All styling options (colors, eyes, logos, gradients, shapes) apply correctly to the rendered QR.
- [ ] Exported files (PNG, JPG, SVG, PDF) are high-resolution and maintain the chosen customizations.
- [ ] The UI matches the provided designs **exactly** (pixel-perfect).
- [ ] The implementation follows the `CLAUDE.md` architecture (ViewModel/State driven, no business logic in UI).
- [ ] Both Light and Dark themes are fully implemented and verified.
- [ ] All user-facing strings are routed through i18n/string resources.

## Out of scope
- User accounts/cloud saving of QR codes.
- Advanced QR analytics/tracking (Dynamic QRs).
- API integration for third-party QR services.

## Dependencies
- Project initialization of Android and Website folders.
- KTech Theme tokens availability.

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
- [ ] **Right keyboard per field** (e.g., numeric for PINs/OTP).
- [ ] **Focused fields remain visible** above the keyboard.
- [ ] Define and implement **loading, empty, and error states**.

### Accessibility & Quality
- [ ] **Accessible labels** and content descriptions on all interactive elements.
- [ ] **Min touch target: 44x44px**; Contrast ratio $\ge$ 4.5:1.
- [ ] Honor **dynamic type/font scaling**.

## References
- **CLAUDE.md**: For architectural rules.
- **ui-ux-pro-max**: For UX quality control.

**Kickoff:** `/start-ticket <#>`
