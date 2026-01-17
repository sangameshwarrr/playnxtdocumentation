## 1. Actor: The Player (End User)

**Goal:** To find a venue, check real-time availability, and book a slot seamlessly.

### A. Onboarding & Authentication

- **Splash Screen:** Display the PlayNxt logo and branding.
- **Sign Up:**
    - Primary Method: **Phone Number + OTP** (Mandatory).
    - Secondary Method: Email (Optional field).
    - *Requirement:* Simple validation to ensure the phone number is active.
- **Login:**
    - Enter registered Phone/Email -> OTP Verification.
    - "Remember Me" functionality to keep the user logged in.

### B. Discovery & Home Screen

- **Category Tabs:** Sticky tabs at the top for **Turf** and **Badminton** (scalable for future sports).
- **Venue Listing:**
    - List view of venues based on the selected category.
    - **Card Details:** Venue Name, Location/Distance, Rating, and Starting Price.
- **Filters:** Filter by Location, Price Range, and Amenities (e.g., Parking, Showers).

### C. Booking Journey

- **Venue Detail Screen:**
    - Images gallery.
    - Address with a "Get Directions" map link.
    - Amenities list.
- **Slot Selection:**
    - **Date Picker:** Select upcoming dates.
    - **Slot Grid:** Visual representation of time slots.
        - *Green:* Available.
        - *Grey/Red:* Booked.
        - *Yellow:* Selected.
- **Checkout:**
    - Review booking details (Date, Time, Venue, Price).
    - **Payment Gateway Integration:** Support for UPI, Credit/Debit Cards, and Net Banking via 3rd party provider (e.g., Razorpay, Stripe).

### D. Post-Booking & Engagement

- **My Bookings:**
    - **Upcoming:** Show QR code or Booking ID for entry.
    - **Past:** History of games played.
- **Notifications:**
    - **Transactional:** Booking confirmation, Payment success, Reminder 1 hour before the game.
    - **Promotional:** Push notifications for "Price Drops" or "Weekend Deals."

---

## 2. Actor: The Venue Owner

**Goal:** To manage their facility's inventory, pricing, and view business health.

### A. Dashboard & Access

- **Role-Based Login:** Secure login specifically for owners.
- **Owner Dashboard:** A high-level view showing:
    - Today’s Total Bookings.
    - Today’s Revenue.
    - Quick toggles for venue status (Open/Closed).

### B. Inventory Management

- **Slot Management:**
    - View the daily calendar grid.
    - **Manual Block:** Ability to manually mark a slot as "Booked" (e.g., for maintenance or offline walk-in bookings).
- **Pricing Control:**
    - Ability to set/update **Price Per Slot**.
    - *Advanced:* Ability to set "Peak Hour" vs. "Non-Peak Hour" pricing.

### C. Reporting & Analytics

The owner needs a dedicated "Reports" tab with the following capabilities:

| Report Type | Details | Filters Available |
| --- | --- | --- |
| **Booking Volume** | Total number of slots booked vs. empty. | Daily, Weekly, Monthly |
| **Revenue** | Total earnings calculated from completed bookings. | Date Range Picker |
| **Utilization** | Heatmap showing which time slots are most popular. | Weekdays vs. Weekends |

Export to Sheets

---

## 3. Actor: The Super Admin (You)

**Goal:** To maintain the platform health, manage users, and orchestrate marketing.

### A. User & Content Management

- **User Management:** View list of Players and Owners; ability to ban/suspend users.
- **Venue Onboarding:**
    - Admin approves new venues before they go live.
    - Upload venue images and set initial location coordinates.

### B. Marketing & Notifications

- **Notification Engine:**
    - Console to send bulk push notifications (e.g., "50% off on all Turfs this Sunday").
    - Trigger "Price Drop" alerts to users who have previously booked specific venues.

### C. Financial Reconciliation

- **Commission View:** Track total revenue flowing through the app to calculate the platform commission (if applicable) before settling with Venue Owners.

## 5. Actor: The Group Creator (Host)

**Goal:** To organize a game, gather players, and secure a venue without paying upfront immediately.

### A. Group Creation (The "Lobby")

- **Creation Limit Check:**
    - System checks: *Has this user created 2 groups today?*
    - If Yes -> Show Error: "Daily limit reached."
    - If No -> Proceed to creation.
- **Setup Screen:**
    - **Select Venue & Slot:** Choose the desired Turf/Court and Time (e.g., "Smash Arena, 5:00 PM").
    - **Set Capacity:** Define "Max Members" (e.g., Looking for 6 players).
    - **Price Transparency:** Display Total Slot Price and Calculated "Price Per Person" (Total / Max Members).
- **Group Status - "Tentative":**
    - Upon creation, the group is live, but the **Slot is NOT reserved** at the venue yet. It remains open on the public marketplace.

### B. Management & Conflict Resolution

- **The "Slot Lost" Scenario:**
    - Since the slot is still public, a random user might book it while the group is forming.
    - **System Action:** If the slot becomes unavailable, the Group Status changes to **"Slot Unavailable."**
    - **Owner Action:** The Creator receives a push notification. They must click "Edit Game" to select a new Venue or Time Slot without disbanding the group.
- **Finalizing:**
    - Once the group is ready (or Max Members reached), the Creator triggers the **"Book Now"** flow to lock the slot.

---

## 6. Actor: The Group Joiner (Participant)

**Goal:** To find a game to play and coordinate with others.

### A. Discovery & Joining

- **Game Feed:** A section showing "Open Games" filtered by sport and location.
- **Join Logic:**
    - User views details (Venue, Time, Price/Head, Current Member Count).
    - Clicks **"Join Group."**
    - **Constraint:** If `Current Members == Max Members`, the button becomes disabled ("Full").

### B. Payment & Confirmation

- **Payment Window:**
    - Once the group is full (or the Creator initiates), the system triggers a "Payment Required" state.
    - *Requirement:* Payment must be made within 24 hours (or immediately if the game time is close).
- **Fallback:** If the group fails to pay within the time limit, the group is dissolved or the slot is released.

---

## 7. Feature: Group Collaboration (Chat & Coordination)

This feature connects the Creator and Joiners.

### A. The Group Chat

- **Access:** Only available to users who have joined the specific Group.
- **Interface:** Whatsapp-style chat interface.
- **Identity:** Messages show the User's **Name** (from profile) to ensure users know who is talking.
- **System Messages:** The chat window should display auto-alerts:
    - *"User X has joined the group."*
    - *"Alert: The selected slot has been taken. Host is updating details..."*
    - *"Payment is pending. Please complete to confirm."*