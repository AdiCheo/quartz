---
publishDate: 2023-01-02T00:00:00Z
title: Multi-Step Summer Camp Signup Flow Plan
# excerpt: Something
tags:
  - markdown
  - blog
  - Astro
draft: true
---

 * **Client:** Magnitude Taekwondo
 * **Program:** Summer Camp (Ages 5-12)
 * **Locations:** Ridgeway & Royal Windsor, Mississauga, ON, Canada
 * **Date of Plan:** May 15, 2025

---

## Overall UI/UX Considerations for the Flow:

* **Progress Indicator:** Display a clear progress bar (e.g., "Step X of 8: [Step Name]") so users know where they are in the process and what's coming next.
* **Clear Navigation:** Consistent "Next" and "Previous" buttons. The "Next" button should ideally only become active when all required fields in the current step are valid.
* **Save Progress (Post-Account Creation):** Once an account is created (Step 3), consider implementing functionality to auto-save progress in subsequent steps. This allows users to return later if interrupted.
* **Mobile-First Design:** Ensure the entire flow is responsive, intuitive, and easy to use on all devices (smartphones, tablets, desktops).
* **Accessibility (A11Y):** Design for all users, including those with disabilities. This includes:
    * Proper HTML semantics.
    * Clear labels for all form fields (`<label for="inputId">`).
    * Keyboard navigability.
    * Sufficient color contrast.
    * ARIA attributes where appropriate.
* **Clear Error Handling:**
    * Inline validation for form fields (e.g., "Please enter a valid email address") appearing as the user types or on blur.
    * A summary of errors at the top of the step if "Next" is clicked with invalid fields.
    * User-friendly error messages that explain what's wrong and how to fix it.
* **Concise Language & Visuals:** Keep instructions clear, simple, and to the point. Use Magnitude's branding consistently. Avoid clutter.
* **Performance:** Optimize for fast loading times between steps. Minimize data reloads.
* **Session Timeout:** Inform users if their session is about to expire and provide an option to extend it.

---

## The Multi-Step Signup Flow:

### Step 1: Select Location

* **Purpose:** User selects which camp location they are interested in.
* **UI Elements & Functionality:**
    * **Heading:** "Step 1: Choose Your Camp Location"
    * **Location Selection:**
        * Visually distinct clickable cards or styled radio buttons for:
            * "Magnitude Taekwondo - Ridgeway" (with full address)
            * "Magnitude Taekwondo - Royal Windsor" (with full address)
        * Optional: A small, non-interactive map image or icon for each.
    * **Information:** Briefly mention that week availability might differ per location (this will be shown in the next step).
    * **Navigation:** "Next: Select Weeks" button.
* **Data Collected:**
    * `selected_location` (e.g., "Ridgeway" or "RoyalWindsor")
* **Considerations:**
    * This step is crucial as all subsequent availability and information might be location-specific.
    * If only one location is active for a period, this step could be skipped or pre-selected.

---

### Step 2: Select Weeks

* **Purpose:** User selects the specific weeks they want to register for at the chosen location.
* **UI Elements & Functionality:**
    * **Heading:** "Step 2: Select Camp Weeks for [Selected Location Name]"
    * **Week Display:**
        * A list, grid, or calendar-style view of all 9 camp weeks.
            * Example: "Week 1: June 30 - July 4, 2025"
            * Example: "Week 2: July 7 - July 11, 2025"
            * ...and so on for all 9 weeks.
        * For each week:
            * Checkbox or toggle for selection.
            * Display price: "$335 CAD per week".
            * **Real-time availability (Crucial):** Show "Spots Available: X", "Limited Spots Remaining!", or "Full" (if full, disable selection and visually indicate it). This requires backend integration to check current enrollment against the capacity of 80 per location per week.
    * **Summary (Dynamic & Visible):**
        * Display number of weeks selected.
        * Running subtotal (e.g., "3 weeks x $335 = $1005 CAD").
    * **Navigation:** "Previous: Location", "Next: Create Account" button.
* **Data Collected:**
    * `selected_weeks`: An array of objects, each containing week identifier and potentially dates (e.g., `[{ week_id: 1, dates: "June 30 - July 4"}, { week_id: 3, dates: "July 14 - July 18" }]`)
* **Considerations:**
    * The selected weeks will apply to all children added in Step 4 for this initial registration session. If a parent wants to register different children for different sets of weeks, they might need to complete the flow multiple times, or the UI in Step 4 would need to allow week selection per child (adds complexity). For now, assume common weeks for all children in one go.
    * Clearly indicate if there are any multi-week discounts; these would be calculated and shown in the Payment step.

---

### Step 3: Email + Password Registration (Account Creation/Login)

* **Purpose:** Allow the parent to create a new account or log into an existing one. This is vital for saving progress and future interactions.
* **UI Elements & Functionality:**
    * **Heading:** "Step 3: Your Parent Account"
    * **Options:** Clear tabs or distinct sections for "Create Account" (default) and "Log In".
    * **Create Account Form:**
        * Parent's First Name
        * Parent's Last Name
        * Email Address (with validation for format and uniqueness via backend check).
        * Password (with confirmation field, strength indicator, and clear requirements display e.g., min 8 characters, 1 uppercase, 1 number, 1 symbol).
        * Checkbox: "I agree to the Terms of Service and Privacy Policy" (with links to the documents). *Required.*
    * **Log In Form:**
        * Email Address.
        * Password.
        * "Forgot Password?" link (initiates password reset flow).
    * **Navigation:** "Previous: Select Weeks", "Create Account & Continue" / "Log In & Continue" button.
* **Data Collected (New Account):**
    * `parent_first_name`
    * `parent_last_name`
    * `parent_email`
    * `parent_password` (securely hashed and salted on the backend)
    * `agreed_to_terms_timestamp`
* **Considerations:**
    * Backend validation for email uniqueness. If an email exists, prompt the user to log in or use the "Forgot Password" feature.
    * Secure password handling is paramount.
    * Upon successful account creation/login, the system should associate the selected location and weeks with this user's session/draft registration.
    * Consider sending a "Welcome" email upon new account creation.

---

### Step 4: Add Child Details

* **Purpose:** Collect detailed information for each child attending the camp.
* **UI Elements & Functionality (Form is dynamically repeatable for each child):**
    * **Heading:** "Step 4: Child Information" (e.g., "Child #1", "Child #2")
    * **Input Fields (per child):**
        * Child's Full Legal Name (First, Middle (optional), Last).
        * Preferred Name/Nickname (optional).
        * Date of Birth (use a date picker; validate for age 5-12 as of camp start).
        * Gender (Dropdown: Male, Female, Prefer not to say, Other - specify).
        * Home Address (Street, Apartment/Unit #, City - Mississauga, Province - ON, Postal Code).
            * Option: "Same as Parent's Address" checkbox (if parent address is collected in Step 3 or 5).
        * T-Shirt Size (Dropdown, if camp t-shirts are provided: Youth XS, S, M, L, XL).
        * **Health Information (Crucial - clearly label this section as sensitive):**
            * Known Allergies (Textarea or structured input: e.g., "Peanuts - severe anaphylaxis. EpiPen required." "Pollen - mild hayfever, takes Claritin.").
                * Checkbox: "Child carries an EpiPen?"
                * Checkbox: "Child carries an Inhaler?"
            * Medications (Textarea or structured input: Name, dosage, timing, reason for ALL medications to be administered or potentially needed at camp. e.g., "Ventolin inhaler - as needed for asthma." "Amoxicillin - 5ml twice daily for ear infection, complete by July 5th").
            * Special Needs/Considerations (Textarea: e.g., "Autism Spectrum Disorder - benefits from clear, literal instructions, may need quiet breaks." "ADHD - requires occasional reminders to stay on task. Responds well to positive reinforcement."). This helps staff provide appropriate support.
            * Dietary Restrictions/Preferences (Textarea, if meals/snacks are provided by the camp, or for allergy awareness).
        * **Emergency Information:**
            * Emergency Contact Name #1 (someone other than the registering parent, if possible).
            * Relationship to Child (e.g., Aunt, Grandparent, Family Friend).
            * Emergency Contact Phone Number #1 (Primary).
            * Emergency Contact Phone Number #2 (Alternate, optional).
            * Ontario Health Card Number (OHIP) (clearly state purpose: "For emergency medical services only").
            * Family Doctor's Name & Clinic.
            * Family Doctor's Phone Number.
    * **Multi-Child Management:**
        * "Save This Child & Add Another Child" button (saves current child's data to the session/draft registration, clears form for next child).
        * "Save Child & Continue" button (if this is the last/only child).
        * A summary section/list displaying names of children already added for this registration (e.g., "Children Added: John Doe, Jane Smith"), with "Edit" / "Remove" options per child.
    * **Navigation:** "Previous: Account", "Next: Parent Details" button (active after at least one child is added and all their required fields are saved).
* **Data Collected (per child):** All fields listed. This will be an array of child objects associated with the parent's account/registration.
* **Considerations:**
    * **PIPEDA Compliance:** This is highly sensitive personal and health information. Ensure secure data handling, storage, and clear consent language regarding its use for camp operations and emergencies.
    * The selected weeks from Step 2 apply to each child added here.
    * Age validation based on DOB and camp start date is important.
    * Make it clear which fields are mandatory.

---

### Step 5: Add Parent/Guardian Details

* **Purpose:** Collect/confirm detailed contact information for the parent(s)/guardian(s) responsible.
* **UI Elements & Functionality:**
    * **Heading:** "Step 5: Parent/Guardian Information"
    * **Parent/Guardian 1 (Primary Contact):**
        * Full Name (First, Last) - *May be pre-filled from Step 3, but editable.*
        * Relationship to Child(ren) (e.g., Mother, Father, Guardian).
        * Primary Phone Number (Mobile preferred, with validation).
        * Alternate Phone Number (optional).
        * Email Address - *Pre-filled from Step 3, likely read-only or requires re-verification if changed.*
        * Home Address (Street, Apt/Unit, City - Mississauga, Province - ON, Postal Code).
            * Can have a "Same as Child #1's Address" checkbox to auto-fill if child's address was entered.
    * **Parent/Guardian 2 (Optional but Recommended):**
        * "Add Second Parent/Guardian" button/toggle to reveal fields.
        * Full Name (First, Last).
        * Relationship to Child(ren).
        * Primary Phone Number.
        * Email Address (optional).
    * **Navigation:** "Previous: Child Details", "Next: Waivers & Agreements" button.
* **Data Collected:** All fields for Parent/Guardian 1 (and Parent/Guardian 2 if provided).
* **Considerations:**
    * Ensure the primary contact for communication is clearly designated.
    * If address was collected in Step 3, pre-fill here.

---

### Step 6: Sign Waivers, Releases, Policies

* **Purpose:** Obtain legally binding consents and acknowledgments for various camp policies and releases.
* **UI Elements & Functionality:**
    * **Heading:** "Step 6: Agreements, Waivers & Consents"
    * **Document Display & Agreement (for each required document):**
        * **Liability Waiver & Indemnification Agreement:**
            * Clear title.
            * A scrollable `<iframe>`, text area displaying the full text, or a prominent "View Full Document (PDF)" link that opens in a new tab/modal.
            * Checkbox: "I, [Parent's Full Name - auto-filled from Step 5], have read, understood, and agree to the terms of the Liability Waiver & Indemnification Agreement." *Required.*
        * **Medical Consent Form (Consent for Emergency Treatment):**
            * Similar display and checkbox as above.
        * **Photo & Video Release:**
            * Similar display.
            * Options:
                * Checkbox: "I consent to the use of my child(ren)'s photo/video as per the Photo & Video Release policy." (Opt-in)
                * OR Radio buttons: "Yes, I consent" / "No, I do not consent". *Make this clear and respect the choice.*
        * **Behaviour Policy / Code of Conduct Agreement:**
            * Similar display and checkbox for acknowledgment and agreement.
        * **Pickup Authorization Policy:**
            * Similar display and checkbox for acknowledgment.
            * May include fields to list authorized pickup persons (Name, Relationship, Phone) if not covered elsewhere.
        * **Other specific policies** (e.g., Illness Policy, Late Pickup Policy).
    * **Digital Signature Section:**
        * Statement: "By typing my full name below, I acknowledge that I am electronically signing these agreements."
        * Input field: "Type your full name as a digital signature." (Auto-filled with Parent 1's name, but they must confirm/re-type or it must be actively typed).
        * Date (auto-filled to current date, read-only).
    * **Navigation:** "Previous: Parent Details", "Agree & Continue to Payment" button (active only when all *mandatory* agreements are checked and the digital signature field is validly filled).
* **Data Collected:**
    * Record of agreement (boolean + timestamp) for each waiver/policy.
    * `digital_signature_name`
    * `signature_date`
* **Considerations:**
    * **Legal Review:** All waiver and policy text MUST be drafted or reviewed by a legal professional familiar with Ontario law and child activity regulations.
    * **Storage & Audit Trail:** Securely store a digital copy or an immutable record of the exact versions of waivers agreed to by each parent, along with their signature and timestamp. This is critical.
    * **Accessibility:** Ensure documents are accessible (e.g., screen-reader friendly).
    * Provide an option for parents to download/print copies of all signed documents for their records, either here or in the confirmation step/email.

---

### Step 7: Payment

* **Purpose:** Collect payment for the camp registration.
* **UI Elements & Functionality:**
    * **Heading:** "Step 7: Review & Payment"
    * **Order Summary (Read-only, clearly itemized):**
        * Location: [Selected Location Name]
        * **For each Child:**
            * Child's Name
            * Selected Weeks (e.g., "Week 1, Week 3, Week 5: 3 weeks x $335 = $1005.00")
        * Subtotal for all children.
        * Discounts Applied (if any, e.g., "Multi-Week Discount: -$50.00", "Sibling Discount: -$25.00"). *Clearly explain discount logic if applied.*
        * Subtotal before tax.
        * HST (13% for Ontario): $[Calculated HST Amount].
        * **Grand Total CAD: $[Final Amount]**.
    * **Payment Method Section:**
        * Typically Credit Card. Display accepted card logos (Visa, Mastercard, Amex).
        * Use a secure, embedded payment form from a PCI-compliant payment processor (e.g., Stripe Elements, Square Web Payments SDK, Moneris Hosted Paypage).
            * Cardholder Name.
            * Card Number.
            * Expiry Date (MM/YY).
            * CVV/CVC.
        * Billing Address (auto-fill from Parent 1's address, with an option to edit if different for the card).
    * **Promo Code (Optional):**
        * Input field: "Enter Promo Code".
        * "Apply" button (validates code and updates Order Summary via AJAX if possible).
    * **Refund Policy Link:** A brief, clear statement or prominent link to the full refund policy visible near the payment button.
    * **Navigation:** "Previous: Waivers", "Complete Registration & Pay $[Grand Total CAD]" button (button text should reflect the final amount).
* **Data Collected (via Payment Processor):**
    * Payment transaction ID.
    * Payment status (success/failure).
    * Last 4 digits of card (for display on receipt).
    * **Important: Do NOT store raw credit card details on your server.**
* **Considerations:**
    * **PCI Compliance:** Absolutely essential. Rely on your payment processor for handling sensitive card data.
    * Clear communication of all charges, including taxes.
    * Handle payment errors gracefully (e.g., "Payment failed. Please check your card details or try another card." Provide specific error codes if possible from the processor).
    * Consider alternative payment methods if feasible (e.g., Interac Online, e-transfer instructions for offline payment - though this complicates instant confirmation). The current flow implies online card payment.
    * If offering payment plans or deposits, this step would need significant modification. The current flow assumes full payment.

---

### Step 8: Confirmation

* **Purpose:** Confirm successful registration and payment, provide important next steps and information.
* **UI Elements & Functionality:**
    * **Heading:** "Registration Confirmed! Thank You, [Parent's First Name]!" or "You're All Set, [Parent's First Name]!"
    * **Success Message:** "Your registration for the Magnitude Taekwondo Summer Camp is complete. We're excited to see [Child #1 Name], [Child #2 Name]!"
    * **Key Details Summary (Read-only):**
        * Registration/Order ID.
        * Location(s).
        * Child(ren)'s Name(s).
        * Registered Weeks for each child.
        * Total Amount Paid & Payment Method (e.g., "Paid: $1005.00 CAD via Visa ending in 1234").
    * **Next Steps / Important Information:**
        * "A confirmation email with all these details and your receipt has been sent to [Parent's Email Address]."
        * "What to Bring to Camp" (link to a page/PDF, or a brief list).
        * "Camp Drop-off/Pick-up Procedures" (link or brief info, including location-specific details).
        * Link to "Frequently Asked Questions (FAQ)".
        * Camp contact information (phone, email for camp-specific questions).
    * **Call to Actions (Optional but helpful):**
        * "Print This Confirmation" button.
        * "Download Receipt (PDF)" button.
        * "Download Signed Waivers (PDF)" button.
        * "Add Camp Dates to Calendar" button (generates .ics file for Week 1 start, or for all selected weeks).
        * "Go to My Account Dashboard" (if a parent portal exists where they can view/manage registrations).
        * Social sharing buttons (e.g., "Share that your child is going to Magnitude Camp! #MagnitudeCamp #[LocationName]").
* **Considerations:**
    * **Automated Confirmation Email:** This is critical. Trigger a comprehensive confirmation email immediately upon successful payment. This email should include:
        * All registration details (names, weeks, location).
        * A detailed payment receipt.
        * Copies of (or secure links to download) the signed waivers.
        * All "Next Steps" information.
    * This page should be reassuring and provide all immediate information the parent needs, reducing follow-up inquiries.
    * Track successful completion of this step for conversion analytics.

---

