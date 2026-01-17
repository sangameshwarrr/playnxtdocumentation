# PlayNxt – Product Requirements & User Flows

---

## 1. Actor: The Player (End User)

**Goal:** To find a venue, check real-time availability, and book a slot seamlessly.

---

### A. Onboarding & Authentication

#### Splash Screen
- Display the **PlayNxt logo and branding**.

#### Sign Up
- **Primary Method:** Phone Number + OTP (Mandatory).
- **Secondary Method:** Email (Optional field).
- **Requirement:** Simple validation to ensure the phone number is active.
- **Preference Selection:** User selects favorite sports (e.g., Football, Badminton) to personalize the home feed.

#### Login
- Enter registered **Phone/Email → OTP Verification**.
- Error screen for **OTP failure**.
- **"Remember Me"** functionality to keep the user logged in.

---

### B. Discovery & Home Screen

#### Category Tabs
- Sticky tabs at the top for **Turf** and **Badminton** (scalable for future sports).

#### Venue Listing
- List view of venues based on the selected category and **Location**.
- **Card Details:**
  - Venue Name
  - Location / Distance
  - Rating
  - Starting Price

#### Filters
- Location (Radius of **15 km**)
- Price Range
- Amenities (e.g., Parking, Showers)

#### Sorting
- Low to High
- High to Low

#### Search Bar
- Search the venue by typing.
- Should show **auto hints while typing**.

---

### C. Booking Journey

#### Venue Detail Screen
- Images gallery.
- Show the sport availability in that venue.
- Operating hours of the venue.
- Venue rules and guidelines.
- Address with a **"Get Directions"** map link.
- Amenities list.

#### Slot Selection
- **Date Picker:** Select upcoming dates (can be up to **15 days**).
- **Slot Grid:** Visual representation of time slots.
  - Green: Available
  - Grey/Red: Booked
  - Yellow: Selected
- Multiple slots can be selected and should be **calculated based on hours**.

#### Checkout
- Review booking details (Date, Time, Venue, Price).
- **Cancellation Policy Display:**  
  A clear box stating the refund tiers:
  - 100% refund > 24 hrs
  - 50% refund > 12 hrs
  - No refund < 6 hrs
- **Agreement:** Mandatory checkbox to accept terms.
- **Payment Gateway Integration:**  
  Support for UPI, Credit/Debit Cards, and Net Banking via 3rd-party providers (e.g., Razorpay, Stripe).
- Show **Booking Confirmation Page** with details.
- Confirmation screen should show **upcoming matches**.

---

### D. Post-Booking & Engagement

#### My Bookings
- **Upcoming:** Show QR code or Booking ID for entry.
- **Past:** History of games played.

#### Cancellation Flow
- User selects **"Cancel Booking"** on an upcoming slot.
- **System Action:** Calculate refund amount based on current time vs. booking time.
- **Confirmation Message:**  
  `"You will get $[X] back. Proceed?"`
- **Outcome:**
  - Slot released
  - Refund triggered
  - Notification sent to Venue Owner

#### Notifications
- **Transactional:**
  - Booking confirmation
  - Payment success
  - Reminder 1 hour before the game
- **Promotional:**
  - Push notifications for **"Price Drops"**
  - **"Weekend Deals"**

---

## 2. Actor: The Venue Owner

**Goal:** To manage their facility's inventory, pricing, and view business health.

---

### A. Dashboard & Access

- **Role-Based Login:** Secure login specifically for owners.
- **Utilization Heatmap:** Visual guide showing which hours/days are most profitable.
- **Owner Dashboard (High-Level View):**
  - Today’s Total Bookings
  - Today’s Revenue
  - Quick toggles for venue status (Open / Closed)

---

### B. Inventory Management

#### Slot Management
- View the daily calendar grid.
- **Manual Block:** Ability to manually mark a slot as "Booked"  
  (e.g., for maintenance or offline walk-in bookings).
- **Check-in Tool:** Built-in QR scanner to verify Player tickets upon arrival.

#### Pricing Control
- Ability to set/update **Price Per Slot**.
- **Advanced:**
  - Set **Peak Hour** vs. **Non-Peak Hour** pricing.

---

### C. Reporting & Analytics

The owner needs a dedicated **"Reports"** tab with the following capabilities:

| Report Type       | Details                                              | Filters Available        |
|------------------|------------------------------------------------------|--------------------------|
| Booking Volume   | Total number of slots booked vs. empty               | Daily, Weekly, Monthly  |
| Revenue          | Total earnings from completed bookings               | Date Range Picker       |
| Utilization      | Heatmap showing most popular time slots              | Weekdays vs. Weekends   |

- **Export to Sheets**

---

## 3. Actor: The Super Admin (You)

**Goal:** To maintain platform health, manage users, and orchestrate marketing.

---

### A. User & Content Management

- **User Management:** View list of Players and Owners; ability to ban/suspend users.
- **Dispute Resolution:** Ability to manually trigger refunds in case of venue closure or player disputes.

#### Venue Onboarding
- Admin approves new venues before they go live.
- Upload venue images.
- Set initial location coordinates.

---

### B. Marketing & Notifications

#### Notification Engine
- Console to send bulk push notifications  
  (e.g., **"50% off on all Turfs this Sunday"**).
- Trigger **"Price Drop"** alerts to users who have previously booked specific venues.

---

### C. Financial Reconciliation

- **Commission View:**  
  Track total revenue flowing through the app to calculate platform commission (if applicable) before settling with Venue Owners.

---

## 5. Actor: The Group Creator (Host)

**Goal:** To organize a game, gather players, and secure a venue without paying upfront immediately.

---

### A. Group Creation (The "Lobby")

#### Creation Limit Check
- System checks: Has this user created **2 groups today**?
  - If **Yes** → Show Error: `"Daily limit reached."`
  - If **No** → Proceed to creation

#### Setup Screen
- **Select Venue & Slot:**  
  Choose Turf/Court and Time (e.g., *"Smash Arena, 5:00 PM"*).
- **Set Capacity:**  
  Define "Max Members" (e.g., Looking for 6 players).
- **Price Transparency:**  
  Display Total Slot Price and calculated **Price Per Person** (Total / Max Members).
- **Share:**  
  Deep-link to WhatsApp / Socials to invite friends.

#### Group Status – "Tentative"
- Upon creation, the group is live.
- The slot is **NOT reserved** at the venue yet.
- It remains open on the public marketplace.

#### Fraud Prevention
- Money is held in **Escrow** by the platform.
- Creator never touches the joiners’ money directly.
- **Problem Statement:**  
  If a random person joins but doesn’t pay, or if the group owner is a fraud and disappears with money.

---

### B. Management & Conflict Resolution

#### The "Slot Lost" Scenario
- Since the slot is public, a random user might book it.
- **System Action:**  
  Group Status changes to **"Slot Unavailable"**.
- **Owner Action:**  
  Creator receives a push notification and must click **"Edit Game"** to select a new venue or time slot without disbanding the group.

#### Finalizing
- Once the group is ready (or Max Members reached), the Creator triggers **"Book Now"** to lock the slot.

---

## 6. Actor: The Group Joiner (Participant)

**Goal:** To find a game to play and coordinate with others.

---

### A. Discovery & Joining

- **Game Feed:**  
  Section showing **"Open Games"** filtered by sport and location.

#### Join Logic
- User views details:
  - Venue
  - Time
  - Price per Head
  - Current Member Count
- Clicks **"Join Group"**.
- **Constraint:**  
  If Current Members == Max Members → Button disabled ("Full").

---

### B. Payment & Confirmation

#### Payment Window
- Once the group is full (or Creator initiates), system triggers **"Payment Required"**.
- **Requirement:**  
  Payment must be made within **24 hours** (or immediately if game time is close).
- **Fallback:**  
  If payment fails within time limit, the group is dissolved or the slot is released.

---

## 7. Feature: Group Collaboration (Chat & Coordination)

This feature connects the Creator and Joiners.

---

### A. The Group Chat

- **Access:** Only available to users who joined the specific Group.
- **Interface:** WhatsApp-style chat interface.
- **Identity:** Messages show the User’s Name (from profile).
- **System Messages:**
  - `"User X has joined the group."`
  - `"Alert: The selected slot has been taken. Host is updating details..."`
  - `"Payment is pending. Please complete to confirm."`

---

## 8. System Logic: Cancellation & Refund Policy

| Time of Cancellation          | Refund Percentage | Slot Status           |
|------------------------------|-------------------|-----------------------|
| > 24 Hours before start      | 100% Refund       | Released to Public    |
| 12 – 24 Hours before start   | 50% Refund        | Released to Public    |
| < 6 Hours before start       | 0% Refund         | Released to Public    |
| Venue Cancels (Rain/Repair)  | 100% Refund       | Blocked               |

---
