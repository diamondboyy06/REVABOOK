# REVABOOK SYSTEM FEATURE MAP

This document details the system features, partitioned by 4 main Actors: Reader (User), Author/Publisher (Creator), Staff/Moderator, and System Administrator (Admin).

---

## 1. Reader / Listener (User)
*End users using the Mobile App to consume content.*

*   **Account & Profile:**
    *   Register / Login (Email, Google, Apple, Facebook).
    *   Manage personal information, language settings, and preferences.
*   **Discovery / Marketplace:**
    *   Search for books/stories by keyword, author, genre.
    *   Filter by format (Textbook, Comic), dubbing language.
    *   Book recommendations based on reading/listening history (Recommendation Engine).
*   **Store & Wallet:**
    *   Top up Wallet (Coin/Credit) via In-App Purchase (IAP) or Payment Gateway.
    *   Buy or Rent books/stories.
    *   View transaction history.
*   **Smart Player:**
    *   **Textbooks:** Listen to audio, auto-scroll pages, **Highlight text synchronized with voice**. Custom playback speed (0.5x - 2.0x).
    *   **Comics:** Manual Page Turn mode, audio automatically matches the current page/speech bubble.
    *   Download for offline listening/reading (DRM protected).
*   **Interaction:**
    *   Rating, Review books.
    *   **Feedback:** Highlight error text/audio segments (mistranslation, stuttering) and send a Report to the Author.

---

## 2. Author / Publisher (Creator)
*Content creators and copyright owners using Creator Studio (Web/PC App).*

*   **Content Management:**
    *   Create new Book projects, classify (Text/Comic).
    *   Upload manuscripts (Text/Word files) or images (ZIP/PDF).
    *   Manage Chapter lists.
*   **AI Studio & Production Workflow:**
    *   Activate automated analysis processes (OCR/NLP).
    *   Select target languages for translation (Multi-language).
    *   Assign AI voices to each character.
    *   Activate Batch Translation & Dubbing processes.
*   **Interactive AI Correction:**
    *   View Error Reports from Readers.
    *   **AI Chat Agent:** Open a chat box with AI, command local error fixes (e.g., "Re-translate this sentence", "Change voice"). Click "Apply" to save and overwrite the fix.
*   **Sales & Analytics:**
    *   Set selling and renting prices.
    *   View Analytics Dashboard: Views, listens, revenue in real-time.
    *   Request Revenue Withdrawal to bank accounts.

---

## 3. Staff / Moderator
*Platform operations team using Internal Admin Tool.*

*   **Content Moderation:**
    *   Approve or Reject new books/stories before publishing to Marketplace (Check for copyright infringement, sensitive content 18+, violence).
    *   Handle content violation reports from the community.
*   **Customer Support (CS):**
    *   Resolve User complaints (Top-up errors, download issues).
    *   Resolve Creator tickets.
*   **Quality Assurance (QA):**
    *   Randomly listen/read AI translations/dubbing to evaluate system quality.

---

## 4. System Admin
*Highest authority, managing the entire platform.*

*   **Global Dashboard:**
    *   Monitor System Health, online users, total platform revenue.
*   **Financial Management:**
    *   Configure platform Commission Rate (e.g., Platform takes 30%, Author receives 70%).
    *   Approve large withdrawal requests from Creators.
*   **Actor Management:**
    *   Ban/Unban User or Creator accounts.
    *   Create Staff accounts, assign Role-based access control (RBAC).
*   **System Config:**
    *   Manage API Keys for 3rd party services (ElevenLabs, OpenAI, Stripe, etc.).
    *   Adjust AI configurations (e.g., Switch AI Models to optimize cost).
