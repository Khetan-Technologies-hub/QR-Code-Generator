# Ticket: Dynamic QR Redirection & Analytics Logic

**Brief:** #2

## Story/Why
To support "Dynamic" QR codes, we cannot encode the final destination URL directly into the QR image. Instead, we must encode a unique short-link that points to our own server. When a user scans the QR, our server identifies the QR ID, increments a scan counter, and then redirects the user to the current target URL. This allows the destination to be updated in the database without changing the physical QR code.

## Context
This is the first ticket of the Dynamic QR feature set. We are implementing the "Engine" that powers both the Android and Web platforms. The logic will be hosted as a Firebase Cloud Function and use Firestore for the mapping and analytics.

The short-links will use a custom domain (e.g., `qr.ktech.link/{id}`).

## 🔑 Access & prerequisites
- **Firebase Project Access**: Developer needs "Editor" or "Owner" access to the project to deploy Cloud Functions.
- **Domain Configuration**: The custom domain must be mapped to the Firebase project in the Firebase Console.
- **Firestore Setup**: A `dynamic_qrs` collection must be created with the following suggested schema:
    - `id` (String, Document ID)
    - `userId` (String, owner of the QR)
    - `destinationUrl` (String, the current target)
    - `scanCount` (Number, total scans)
    - `createdAt` (Timestamp)

## Scope

### 1. The Redirection Function (The "Engine")
Implement a single Firebase Cloud Function (monolithic) that handles the following:
- **Request Handling**: Listen for requests at the custom domain endpoint (e.g., `/qr/{id}`).
- **Lookup**: Fetch the `destinationUrl` from the `dynamic_qrs` collection using the `{id}`.
- **Analytics**: Increment the `scanCount` field in the Firestore document using an atomic increment (`FieldValue.increment(1)`).
- **Redirection**: Perform a 302 (Found) redirect to the `destinationUrl`.
- **Error Handling**: Redirect to a fallback "Not Found" page or the project homepage if the ID does not exist.

### 2. The Creation Logic
Within the same function or as a separate endpoint:
- **Unique ID Generation**: Create a short, collision-resistant ID for new Dynamic QRs.
- **Mapping Storage**: Save the initial `destinationUrl` and `userId` to Firestore.

## Acceptance Criteria
- [ ] Scanning a Dynamic QR successfully redirects the user to the target URL.
- [ ] Every successful redirect increments the `scanCount` in Firestore by exactly 1.
- [ ] The redirection happens with minimal latency (verified via network logs).
- [ ] Requests for non-existent IDs are handled gracefully with a redirect to a fallback page.
- [ ] The system uses a custom domain for the short-links.
- [ ] All Firestore writes are atomic to prevent scan count race conditions.

## Out of scope
- Advanced analytics (device type, geo-location).
- Frontend UI for creating or managing the QRs (covered in subsequent tickets).
- Customizing the redirection page (e.g., interstitial ads).

## Dependencies
- Firebase project initialization.
- Custom domain DNS configuration.

## References
- **Brief #2**: Dynamic QR Dashboard.
- **CLAUDE.md**: For Firebase architecture rules.
- **PRD**: System Architecture section.

**Kickoff:** `/start-ticket <#>`
