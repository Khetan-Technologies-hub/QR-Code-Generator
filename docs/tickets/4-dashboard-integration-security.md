# Ticket: Dashboard Integration & Security Hardening

**Brief:** #2

## Story/Why
A feature is only as good as its security and polish. Now that the Engine (Ticket #3) and the UI (Ticket #4) are built, we must ensure the system is "production-ready." This means locking down the data so users can only edit their own QRs and adding the "magic" of real-time updates so scan counts tick up live on the dashboard without page refreshes.

## Context
This is the final ticket for the Dynamic QR feature set. It closes the loop between the Frontend and the Firebase Backend, transforming a functional prototype into a secure, polished product.

## 🔑 Access & prerequisites
- **Firebase Console Access**: Developer needs access to Firestore "Rules" and "Indexes" tabs.
- **Existing Build**: Both the Dynamic QR Engine (Cloud Functions) and Dashboard UI must be deployed in a development environment.
- **Auth**: Firebase Social Auth must be fully operational.

## Scope

### 1. Security Lockdown (Firebase Rules)
Implement strict **Firestore Security Rules** to enforce ownership:
- **Read Access**: Users can read a Dynamic QR's mapping if they are the `userId` associated with it.
- **Write Access**: Users can only update the `destinationUrl` of a QR if they are the authenticated owner.
- **Admin Access**: Ensure a system admin role (if defined) can manage all records for support purposes.
- **Validation**: Use Firestore rules to ensure `destinationUrl` is not empty and follows basic URL formatting.

### 2. Real-time Analytics Integration
Upgrade the Dashboard from static fetching to real-time synchronization:
- **Firestore Snapshots**: Implement `onSnapshot` (Web) and `snapshots()` (Android) for the Dynamic QR list.
- **UI Reaction**: Ensure the **Scan Count** column updates instantly as the Cloud Function increments the value in the background.
- **Performance**: Optimize the snapshot listener to avoid unnecessary re-renders of the entire table.

### 3. Final End-to-End Validation
Perform a "Hardening Pass" to verify the following:
- **Ownership Breach Test**: Attempt to update a QR using a different authenticated account (must be rejected by Firestore).
- **Unauthorized Access Test**: Attempt to update a QR without being logged in (must be rejected).
- **Race Condition Test**: Verify that multiple simultaneous scans of the same QR are all correctly counted.
- **Latency Check**: Ensure the "Real-time" update doesn't introduce lag to the rest of the dashboard UI.

## Acceptance Criteria
- [ ] Firebase Security Rules successfully block all unauthorized read/write attempts to `dynamic_qrs`.
- [ ] Scan counts on the Dashboard update in real-time without manual refresh.
- [ ] All Dynamic QR operations (Create $\rightarrow$ Scan $\rightarrow$ Update $\rightarrow$ Re-scan) work seamlessly across Android and Web.
- [ ] No sensitive data (user IDs, etc.) is exposed in the public redirection URL.
- [ ] System survives "stress tests" with multiple simultaneous redirects.

## Out of scope
- Implementing a full-scale analytics dashboard with graphs (handled in future features).
- User account deletion/GDPR "right to be forgotten" logic (general account ticket).

## Dependencies
- Completion of Ticket #3 (Engine) and Ticket #4 (UI).
- Firebase Auth project configuration.

## References
- **Brief #2**: Dynamic QR Dashboard.
- **CLAUDE.md**: For Firebase "Principle of Least Privilege" rules.
- **PRD**: Non-Functional Requirements $\rightarrow$ Security & Performance.

**Kickoff:** `/start-ticket <#>`
