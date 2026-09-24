# Feature Brief: Dynamic QR Dashboard

## Problem & Outcome
Users who print QR codes on physical materials (flyers, business cards) face a critical risk: if the destination URL changes, the printed material becomes obsolete. 

The **Dynamic QR Dashboard** solves this by providing a centralized command center where registered users can manage their "Smart" QR codes. "Done" feels like a professional management suite where a user can update a link in seconds, knowing the change is instant and global.

## Who it's for
**Registered Users (Marketers & Business Owners)** who have deployed Dynamic QRs in the real world and need to maintain them or track their effectiveness.

## Capabilities
- **Dynamic QR Inventory**: A professional list of all Dynamic QRs owned by the user, displaying:
    - A small visual preview of the QR.
    - The current destination URL.
    - Creation date.
    - **Real-time Scan Count**: Total number of times the QR has been scanned.
- **Instant Destination Update**: Ability to edit the target URL of any Dynamic QR, updating the redirection logic in Firestore immediately.
- **Asset Retrieval**: One-click download of the QR image in the original chosen format (SVG/PNG/etc.).
- **Scan Analytics (v1)**: Basic aggregate counting of scans per QR code.

## What "Good" Looks Like
- **Efficiency**: Updating a destination URL is a low-friction process (Select $\rightarrow$ Edit $\rightarrow$ Save).
- **Confidence**: The user receives immediate confirmation that the link has been updated.
- **Professionalism**: The dashboard reflects a "Control Panel" aesthetic—clean, high-density but not cluttered, adhering to the KTech Theme.
- **Reliability**: Zero downtime during the redirection update.

## Non-Negotiables
- **Strict Ownership**: Only the authenticated creator of the QR can see or edit it (Firebase Security Rules).
- **URL Integrity**: Mandatory validation of new destination URLs to prevent broken links.
- **Performance**: The dashboard must load the list of QRs efficiently, using pagination or lazy loading if the list grows large.

## Technical Steers
- `[hard]` **Firebase Cloud Functions**: The redirection logic must increment the scan count in Firestore *before* redirecting the user.
- `[preference]` **Real-time Updates**: Use Firestore snapshots to update scan counts on the dashboard in real-time without requiring a page refresh.

## References
- **PRD**: Section "Account & Management" $\rightarrow$ Dynamic QR Dashboard.
- **Design**: Provided by the PO (Figma/Mockups to be requested at `/start-ticket`).
- **UI Standard**: `ui-ux-pro-max` for data-dense dashboard layout.
