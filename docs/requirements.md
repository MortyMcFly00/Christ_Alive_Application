Roles:
  Guest - Not signed in
  Member - Signed in as standard user
  Leadership - Moderator and Admin (Permissioned Roles)

Functional Requirements:

  System requirements
    (Must)
    1. System must support user authentication (sign up, sign in, and sign out)
    2. System must support role-based access control for Guest, Member, Moderator, and Admin.
    3. System must enforce authorization so only permitted roles can perform restricted actions.
    4. System must provide live Services via an embedded third-party source.
    5. System must provice a Tithing experience vian and embedded third-party source.
    6. System must provide a video library of prior services and Bible studies via embeddeed video sources.
    7. System must allow users to filter the video library content based on defined filter options.
    8. System must provide an event calander visible to members.
    9. System must allow members to volunteer for events.
    10. System must provide an announcement board visible to members.
    11. System must allow any user to submit a prayer request.
    12. Prayer request must offer an anonymous option.
    13. System must deliver prayer requests to the church email.
    14. System must detect when the live service broadast begins and send a push notification to subscribed users.
    15. System must send at most one "Live has begun" notification per broadcast (no duplicates).
    16. System must allow users to opt in/ opt out of "live started" push notification.

     (Research action logging, sanitation, supabase ping to keep free teir from going inactive, etc.)
    
    (Should)
    1. System should provide user-friendly fallback when embed fails (Blocked or failed load), including external link to open content.
    2. System should include basic spam protection for prayer requests (rate limiting/ basic CAPTCHA).
    3. System shpuld prevent duplicate volunteering signups by the same member for the same event.
    4. System should display confirmation feedback after prayer request submission and after volunteering.
   
    (Could)
    1. System could allow users to subscribe to additional notification categories (events, announcements).
    2. System could support bookmarking/ favoriting videos or saving filter presets.
    3. System could show event volunteer capacity (Slots needed/ filled).

    (Wont)
    1. System will not process payments natively (Tithing remains through embedded third-party source).
    2. System will not control or initiate the live broadcast (only detect and notify when it begins).
    3. System will not store or display prayer requests inside the application (delivery is email-only).

  Guest requirements:
    1. Guest must be able to view live services.
    2. Guest must be able to tithe.
    3. Guest must be able to browse and watch the video library using filters.
    4. Guest must be able to submit a prayer request (including anonymously).

  Members requirements:
    1. Members must be able to view the event calander.
    2. Members must be able to volunteer for an event.
    3. Member must be able to withdraw/ cancel their volunteer signup.

  Moderator requirements:
    1. Moderator must be able to add events.
    2. Moderator must be able to cancel events.
    3. Moderator must be able to post announcements to the announcement board.

  Admin requirements:
    1. Admin must be able to update video library (add, edit, remove entries and filter metadata).
    2. Admin must be able to ban/unban user accounts.
    3. Admin must be able to edit/remove any events, announcements, and video library entries.

Non-Functional Requirements:

  Availability Requirements:
    1. The system must be accessible at all times, with uninterrupted access during live services and Bible studies.
    2. In the event of unexpected downtime, the application must display a user-friendly error message.
    3. Planned downtime must be scheduled and communicated to users via an in-app banner at least 24 hours in advance.
    4. Live streaming and tithing features are considered mission-critical and must have the highest availability guarentees.

  Performance Requirements:

  (These performance goals apply across both peak usage periods (e.g., live services) and off-peak study use.
   The system should degrade gracefully in poor network conditions without showing blank states or incomplete screens.)

    1. The app must load within 3 seconds on average mobile networks(3G-5G). 
    2. Screen transitions and UI interactions should respond in under 1 second.
    3. Prayer request and volunteer submissions should be processed and confirmed with 2 seconds.
    4. The video library should load its initial content in under 2 seconds, even on 3G.
    5. Embedded videos (YouTube, Facebook Live) should begin buffering and play within 4 seconds on mobile networks.
    6. Push notifications for live streams must be delivered within 30 seconds of detection.

  Security Requirements:
    1. All API access must be authenticated using JWTs(managed by Supabase).
    2. Role-based access must be strictly enforced on both the frontend and backend.
    3. Prayer requests will not be stored in the system to protect user privacy. Instead, they are delivered directly to the church email.
    4. Form submissions accessible to guests must be protected from spam through rate limiting and CAPTCHA mechanisms.
    5. All data must be transmitted over HTTPS.
    6. Admin and Moderator actions must be logged for audit purposes.
    7. Inputs from al user-facing forms must be sanitized to prevent common injection attacks.
    8. The system must avoid exposing internal error messages or stack traces to end users.

  Scalabilty Requirements:
    1. The system should comfortably support up to 200 active users and occasional usage spikes without degradation.
    2. The data model must support long-term accumulation of content, such as:
      - An expanding video library with search/filtering.
      - A growing event history.
      - Admin logs for accountability.
    3. The system architecture should allow for future feature expansion, including:
      - Study tools and bookmarks.
      - Enhanced notification preferences.
      - Calander integration with native mobile apps.
    4. Backend services (Node.js + Supabase) must remain stateless and modular so that specific components (notification handler, prayer form, video sync) cane be scaled independently as needed.le

  Maintainability Requirements:
    1. The application must follow a modular structure, where components are separated and loosely coupled.
    2. The system should remain stable over long periods, with the expectation that after the first 12-24 months of active updates, future changes will focus primarily on bug fixes and minor improvements.
    3. The codebase should be organized with:
      - Clear folder structures and naming conventions.
      - Logical separation between between frontend, backend, and infrastructure concerns.
      - Role-based components access control.
    4. Clean code practices must be followed:
      - Linting and formatting tools in place.
      - Comments and documentation for complex logic and workflows.
      - Well-named, self-explanatory variables and functions.
    5. A basic onboarding guide or README should exist to help future maintainers understand how to:
      - Run the app locally.
      - Deploy backend updates.
      - Connect to Supabase.
      - Understand the role-based system.
    6. Updates should follow a non-breaking change philosophy, especially for shared data models and public facing features.
