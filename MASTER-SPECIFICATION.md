# Japan Journey - Complete Feature Specification

## Project Overview
**Purpose:** Comprehensive travel companion PWA for Japan trip (Feb 24 - Mar 17, 2025)
**User:** Josh (@gneiss.creative) - Creative professional, photographer, videographer
**Device:** Samsung S24 Ultra (Android)
**Location:** Australia → Japan (Osaka, Kyoto, Tokyo)

---

## Design System

### Visual Aesthetic
- **Style:** Refined, Japan-inspired, intentional (NOT stereotypical)
- **Season:** Late winter/early spring (end of plum blossoms, pre-cherry blossom)
- **Feel:** Joyful but not cluttered, app-like, spacious with depth
- **Reference:** "DVD special features menu" - layered, explorable, not overwhelming

### Color Palette
- Primary background: `#fef6f0` (warm cream)
- Secondary background: `#fae8e0` (soft peach)
- Tertiary background: `#e8d5d0` (dusty rose)
- Accent primary: `#c94b4b` (deep burgundy/red)
- Accent secondary: `#8b3a62` (indigo/purple)
- Text primary: `#2c1810` (dark brown)
- Text secondary: `#8b6f5c` (warm brown)
- Success: `#689f63` (sage green)
- Warning: `#daa520` (goldenrod)

### Typography
- **Body:** Noto Sans JP (300, 400, 500, 600, 700)
- **Headings:** Noto Serif JP (400, 600, 700)
- Avoid: Inter, Roboto, Arial, generic system fonts

### UI Components
- Border radius: 12px (small), 16px (medium), 20px (large), 24px (xl)
- Shadows: Subtle, layered (multiple levels for depth)
- Transitions: 300ms cubic-bezier(0.4, 0, 0.2, 1)
- Backdrop blur: 20px on cards/overlays
- Gradients: Linear gradients for accents, radial for backgrounds

---

## Technical Architecture

### Platform
- **Type:** Progressive Web App (PWA)
- **Hosting:** Netlify, Vercel, or GitHub Pages (user choice)
- **Protocol:** HTTPS required (for PWA features)
- **Offline:** Service worker with cache-first strategy

### Data Storage
- **Primary:** localStorage (5-10MB limit)
- **Photos:** Base64 encoded (inline storage)
- **Backup:** Auto-backup to Google Drive + manual export/import
- **Format:** JSON for all data structures

### Compatibility
- **Primary Device:** Samsung S24 Ultra (Android)
- **Browser:** Samsung Internet, Chrome for Android
- **Network:** Works offline after first load
- **Screen:** Mobile-first, responsive up to tablet
- **Input:** Touch-optimized (44px minimum touch targets)

### APIs & Integrations
- **Currency:** exchangerate-api.io (free tier) or manual entry
- **Weather:** OpenWeatherMap (free tier)
- **Maps:** Google Maps links (no API key needed for links)
- **Google Drive:** Google Drive API v3 (user provides credentials)
- **Translation:** Google Translate app integration (via URL scheme)

---

## Feature 1: Daily Journal

### Core Functionality
- **Date Navigation:**
  - Previous/Next day buttons
  - Date picker (Feb 24 - Mar 17, 2025)
  - Display current day number (Day 1, Day 2, etc.)
  - Trip start: Feb 24, 2025
  - Trip end: Mar 17, 2025

- **Entry Management:**
  - Add new entry
  - Edit existing entry
  - Delete entry (with confirmation)
  - Multiple entries per day
  - Entries display chronologically

### Entry Fields

**Required:**
- Name/Title (text input)

**Optional:**
- Category (dropdown with emoji icons):
  - ⛩️ Shrine
  - 🏯 Temple
  - 🏛️ Museum
  - 🌳 Park
  - 🪴 Garden
  - 🕊️ Memorial
  - 🏪 Store
  - 📍 Landmark
  - 🍜 Restaurant
  - ☕ Café
  - 🏨 Accommodation
  - 🚆 Transport
  - 🎪 Theme Park (triggers nested events UI)
  - ✨ Other

- Time (time picker)
- Location/Maps:
  - Text field for Google Maps URL
  - "Get Directions" button (opens maps with directions from current location)
  - Store address/coordinates

- Photos:
  - Multiple photos per entry
  - Upload from gallery
  - Take photo with camera
  - Grid display (2-3 columns)
  - Click to view full-screen
  - Delete individual photos
  - Base64 storage

### Category-Specific Features

**Contextual Prompts** (displayed when category selected):
- **Shrine:** "What was the atmosphere like? Did you feel any particular energy or sense of reverence?"
- **Temple:** "How did the space make you feel? What details drew your eye?"
- **Museum:** "What surprised you? What will you remember?"
- **Park:** "What was the pace like? How did it feel to be there?"
- **Garden:** "What caught your attention? How did the space unfold?"
- **Memorial:** "What emotions came up? What felt important to witness?"
- **Store:** "What drew you in? What did you discover?"
- **Landmark:** "What was it like to be here in person? How did it feel different than expected?"
- **Restaurant:** "Beyond the food — what was the atmosphere? How did you feel?"
- **Café:** "What was the vibe? How did the space invite you to linger or move through?"
- **Accommodation:** "How does this place feel? What's the energy of arriving here?"
- **Transport:** "How did this part of the journey feel? Any interesting observations?"

**AI-Suggested Tags** (per category):
- **Shrine:** sacred, peaceful, ritual, spiritual, quiet, contemplative
- **Temple:** historic, beautiful, peaceful, architecture, spiritual, contemplative
- **Museum:** art, history, culture, learning, discovery, fascinating
- **Park:** nature, peaceful, spacious, relaxing, green, calm
- **Garden:** beautiful, serene, designed, nature, peaceful, contemplative
- **Memorial:** somber, reflective, important, moving, historical, respectful
- **Store:** shopping, discovery, unique, interesting, local, browsing
- **Landmark:** iconic, impressive, crowded, photo-worthy, cultural, tourist
- **Restaurant:** delicious, local-cuisine, memorable, atmosphere, experience
- **Café:** coffee, relaxing, cozy, break, atmosphere, people-watching
- **Accommodation:** comfortable, rest, base, welcoming, sleep
- **Transport:** journey, observation, transit, movement, efficient, scenic

### Nested Events (Theme Parks)
**Triggered when:** Category = "Theme Park"

**UI Changes:**
- Special interface appears
- Can add multiple sub-experiences within the main entry
- Each sub-experience has:
  - Name (text)
  - Time (optional)
  - Photo (optional)
  - Quick note (textarea)
- Add/remove sub-experiences
- All saved under parent entry
- Keeps everything contained in one main entry

**Use Cases:**
- Universal Studios Japan (multiple rides/shows)
- DisneySea (different areas)
- Large shopping districts
- Festival days with multiple events

### Meals & Snacks Section
**Purpose:** Log food without cluttering main entries

**Implementation:**
- Expandable section in every entry (collapsed by default)
- Icon: 🍱 Meals & Snacks
- Multiple meal/snack entries per location
- Each meal entry has:
  - Name (text)
  - Time (optional)
  - Photo (optional)
  - Quick note (textarea)
- Add/remove meal entries
- Useful for theme park days or busy days with multiple food stops

### Expandable Context Sections
All sections start collapsed, expand when clicked:

**📝 Notes & Observations**
- Placeholder: "What did you notice? What caught your attention?"
- Textarea for detailed notes

**💭 Feelings & Energy**
- Placeholder: "How did this place feel? What was the energy like?"
- Textarea for emotional responses

**👥 People & Encounters**
- Placeholder: "Who did you meet? What interactions stood out?"
- Textarea for people/social notes

**🌸 Sensory Details**
- Placeholder: "Sounds, smells, textures, tastes..."
- Textarea for sensory observations

### Tags System
- Manual text input (comma-separated)
- AI-suggested tags based on category
- Click suggested tag to add
- Selected tags highlight
- Display as rounded badges on entry
- Used for filtering/searching later

### Reflections
- Add reflection to any entry after creation
- Separate from main entry
- Fields:
  - Reflection text (textarea)
  - Timestamp (auto-generated when added)
- Display in special box with timestamp
- Visual distinction from main entry
- Can edit/update reflection

### Display & Organization
- Entries grouped by day
- Show all entries for selected date
- Empty state when no entries
- Entry cards show:
  - Title
  - Category icon
  - Time (if set)
  - Photo grid
  - Expandable sections (if content)
  - Tags
  - Reflection (if added)
- Edit/Delete buttons per entry

### Export Options
- Export single day as JSON
- Export all journal data
- Include photos in export

---

## Feature 2: Budget Tracker

### Core Functionality
- Manual expense entry
- Automatic expense import from Purchases & Souvenirs
- Category-based organization
- Currency conversion
- Multiple views (daily, total, category breakdown)
- Export to CSV

### Expense Entry Fields
**Required:**
- Amount (number)
- Currency (AUD or JPY)
- Category (dropdown)

**Optional:**
- Description/Note (text)
- Date (auto-fills to today, can change)
- Time (optional)
- Link to journal entry (if added from journal)
- Link to purchase item (if auto-imported)
- Receipt photo (optional)

### Categories
- 🍜 Food & Dining
- 🚆 Transport
- 🏨 Accommodation
- 🛍️ Shopping
- 🎫 Activities & Attractions
- 🎁 Souvenirs (auto-linked)
- 💊 Health & Wellness
- 📱 Communication (eSIM, etc.)
- ✨ Other

### Currency Conversion
**Manual Entry:**
- Input field for exchange rate (AUD to JPY)
- "Last updated" timestamp
- Save rate for reuse

**Auto-Fetch (Optional):**
- "Fetch Current Rate" button
- Uses exchangerate-api.io (free tier)
- Updates rate and timestamp
- Fallback to manual if API fails

**Display Toggle:**
- Switch between AUD and JPY display
- Shows both with one primary
- Example: "¥1,500 (AUD $20.50)"
- Respects user preference

**Default Behavior:**
- Track everything in AUD (home currency)
- Show JPY conversion on toggle
- Save user's preferred display currency

### Views & Visualizations

**Daily Summary:**
- Total spent today
- Breakdown by category
- List of expenses
- Compare to daily budget (if set)

**Trip Total:**
- Total spent so far
- Days remaining
- Average daily spend
- Projected total (if trend continues)

**Category Breakdown:**
- Pie chart or bar chart
- Percentage per category
- Amount per category
- Visual comparison

**Timeline View:**
- Expenses over time (line graph)
- Daily totals
- Identify spending patterns

### Budget Setting (Optional)
- Set total trip budget
- Set daily budget
- Warning when approaching limits
- Progress indicators

### Auto-Integration
- Automatically pull amounts from:
  - Purchases Log entries
  - Souvenirs entries
- Link back to source entry
- Update when source changes
- Can override/adjust if needed

### Export
- CSV format with columns:
  - Date, Time, Category, Description, Amount AUD, Amount JPY, Exchange Rate
- Date range selection
- Include/exclude categories

---

## Feature 3: Language Notes

### Core Functionality
- Pre-loaded essential phrases
- Add custom phrases
- Quick-show full-screen mode
- Search and filtering
- Tag system
- Integration with Google Translate
- Favorites system

### Phrase Structure
Every phrase has 3 components:

**English:**
- Plain English text
- Example: "Excuse me, where is the bathroom?"

**Romaji (Pronunciation):**
- Romanized Japanese for speaking
- Example: "Sumimasen, toire wa doko desu ka?"

**Japanese (To Show):**
- Actual Japanese characters
- Example: "すみません、トイレはどこですか?"

### Pre-loaded Phrase Categories

**Greetings:**
- Hello / Good morning / Good evening
- Thank you / Thank you very much
- Excuse me / Sorry
- Goodbye / See you later
- Please
- Yes / No

**Photo Requests** (Important for photography):
- "May I take your photo?" (polite, encouraging)
- "Would you like me to take a photo of you?"
- "Could we take a photo together?"
- "Thank you for letting me photograph you"

**Food & Dining:**
- "I'd like to order this"
- "What do you recommend?"
- "Delicious!" / "It was very good"
- "The check, please"
- "Do you have vegetarian options?"
- "I have a food allergy to..."
- "This is too spicy"
- "Water, please"

**Directions:**
- "Where is...?"
- "How do I get to...?"
- "Is it far?"
- "I'm lost"
- "Can you show me on a map?"
- "Left / Right / Straight"

**Shopping:**
- "How much is this?"
- "Too expensive"
- "I'll take this"
- "Just looking, thank you"
- "Do you have this in a different size/color?"
- "Can I try this on?"
- "Do you accept credit cards?"

**Emergency:**
- "Help!"
- "I need a doctor"
- "Where is the hospital?"
- "I don't understand"
- "Do you speak English?"
- "Please call the police"

### Quick-Show Mode
**Trigger:** Button on each phrase labeled "Show"

**Behavior:**
- Opens full-screen overlay
- Dark semi-transparent backdrop
- Japanese text ONLY displayed
- Very large, readable font (48-60px)
- Centered on screen
- Easy dismiss:
  - Tap anywhere on screen
  - Or X button in corner
- Returns to phrase list

**Use Case:** When language barrier is too much to speak, show the Japanese text to the person

### Custom Phrases
**Add New Phrase:**
- Input all 3 formats:
  - English
  - Romaji (with helper text: "How to pronounce it")
  - Japanese (with helper text: "Japanese characters")
- Assign tags
- Save to list
- Edit/delete later

### Tag System
**Pre-generated Tags:**
- Greeting
- Food
- Direction
- Shopping
- Emergency
- Transport
- Accommodation
- Photo
- Gratitude
- Question
- Statement

**Tag Behavior:**
- Multiple tags per phrase
- Filter phrases by tag
- Click tag to show only phrases with that tag
- Clear filter to show all

### Search Functionality
- Search across English, Romaji, and Japanese
- Real-time filtering as you type
- Highlights matching text
- Case-insensitive

### Favorites System
- Star icon on each phrase
- Click to favorite/unfavorite
- "Favorites" view shows only starred phrases
- Most recently used auto-appear at top
- Quick access to frequently needed phrases

### Integration Features

**Google Translate Button:**
- Button labeled "Open in Translate"
- Opens Google Translate app (if installed)
- Pre-fills the phrase
- URL scheme: `googletranslate://translate?sl=en&tl=ja&text=[phrase]`
- Fallback to web version if app not installed

**Copy to Clipboard:**
- Button labeled "Copy"
- Copies Japanese text to clipboard
- Shows brief confirmation
- Can paste into messaging apps

### Display & Organization
- List view by default
- Search bar at top
- Filter by tag
- Sort options:
  - Alphabetical
  - Most used
  - Recently added
  - Favorites first

---

## Feature 4: Purchases Log

### Purpose
Chronological list of all personal purchases with simplified view

### Entry Fields
- **Item name** (text)
- **Store/location** (text)
- **Date** (auto from journal entry or manual)
- **Time** (optional)
- **Price** (AUD or JPY)
- **Photo** (optional)
- **Notes** (textarea)
- **Link to journal entry** (if added from journal)

### Display
- Chronological list (newest first or oldest first toggle)
- Simplified card view:
  - Item name (bold)
  - Store
  - Date + Time
  - Price
- Expand card for full details
- Filter by date range
- Search by item name or store

### Integration
- Can add purchase from journal entry
- Automatically feeds into Budget Tracker
- Photo syncs with journal

### Export
- CSV with all fields
- Include photos as separate files or links

---

## Feature 5: Souvenirs Tracker

### Purpose
Track gifts purchased for others with recipient filtering

### Entry Fields
- **Item name** (text)
- **Recipient** (text or dropdown of common names)
- **Store/location** (text)
- **Date** (auto from journal or manual)
- **Price** (AUD or JPY)
- **Photo** (optional)
- **Notes** (textarea)
- **Exclude "for myself"** (checkbox to exclude self-purchases from this view)

### Filtering
- Filter by recipient
- "All recipients" view
- "Unpurchased" view (if planning ahead)
- Sort by: recipient, date, price

### Gift Planning
- Add planned purchases (mark as "planned" vs "purchased")
- Budget per person (optional)
- Checklist view

### Integration
- Automatically feeds into Budget Tracker
- Can add from journal entry

---

## Feature 6: Stamp Rally

### Purpose
Track event/location stamps collected during trip

### Two Components

**1. Daily Planning:**
- Pre-plan which stamps to hunt each day
- List of stamps by date
- Checkbox to mark as collected
- Notes about where to find
- Can add stamps to multiple days (if unsure)

**2. Collection Log:**
- Photo of stamp (upload)
- Location name (text)
- Date collected (auto or manual)
- Time (optional)
- Notes (textarea)
- Link to journal entry (if applicable)

### Stamp Quest Integration
- Manual field: "Stamp Quest station?" (yes/no)
- Stamp Quest ID (if applicable)
- Notes about quest
- Since no API: manual tracking only

### Display
- Grid view of collected stamps
- List view with details
- Filter by: date, location, Stamp Quest
- "Collected" vs "Planned" tabs

### Stats
- Total stamps collected
- Stamps per day
- Stamp Quest progress (if tracking)

---

## Feature 7: Goshuin Collection

### Purpose
Digital shrine/temple stamp book for sacred seals

### Entry Fields
- **Shrine/Temple name** (text)
- **Photo of goshuin** (required - upload)
- **Location** (text, can link to maps)
- **Date received** (auto or manual)
- **Price paid** (most are ¥300-500)
- **Significance/notes** (textarea - what makes this special)
- **Link to journal entry** (if visited that shrine/temple)

### Display
- Beautiful gallery view (like a stamp book)
- Grid of goshuin images
- Click to see full details
- Chronological or by location
- Special reverent aesthetic (important - these are sacred)

### Integration
- Link to shrine/temple journal entries
- Can add goshuin when logging shrine/temple visit
- Photos stored with high priority

---

## Feature 8: Transport Log

### Purpose
Log interesting train journeys (not every single one)

### Entry Fields
- **Route** (text, e.g. "Kyoto to Tokyo")
- **Train type** (Shinkansen, local, JR, etc.)
- **Train name/number** (optional)
- **Date & time** (auto or manual)
- **Duration** (optional)
- **Observations** (textarea - what was interesting)
- **Photo** (optional - train, view, station)
- **Link to journal entry** (if part of larger day)

### Display
- Simple list view
- Map view showing routes (if possible)
- Filter by: date, train type

### Use Case
- Track special Shinkansen rides
- Scenic routes
- Interesting observations
- Not every single train - only memorable ones

---

## Feature 9: Moments

### Purpose
Quick captures - photo + one sentence, no full entry needed

### Entry Fields
- **Photo** (required - upload or camera)
- **One sentence** (text, max ~100 chars)
- **Date & time** (auto)
- **Location** (optional)

### Display
- Instagram-like grid of photos
- Hover/tap shows sentence
- Click for full view
- Chronological or shuffle

### Use Case
- Quick beautiful moment
- Don't want full journal entry
- Fast capture in the moment
- Can promote to full journal entry later

---

## Feature 10: EDC (Every Day Carry) Planner

### Purpose
Plan and track daily gear, especially photography equipment

### Structure

**Standard Kit:**
- Base loadout that's always packed
- Checklist format
- Example items:
  - Camera body
  - Lens 1, 2, 3
  - Extra batteries
  - Memory cards
  - Phone
  - Wallet
  - Passport
  - etc.

**Day-Specific Additions:**
- Add extra gear for specific days
- Example: "Universal Studios - add wide lens"
- Save presets for activity types:
  - "Temple day" (specific gear)
  - "City exploring" (different gear)
  - "Night photography" (different gear)

### Features
- **Pre-plan:** Set EDC for upcoming days
- **Daily view:** See today's checklist
- **Check off:** Mark items as packed
- **Reset:** Uncheck all for next day
- **Templates:** Save common loadouts
- **Weight tracking:** Optional total weight

### Display
- Calendar view showing which days have custom EDC
- Daily checklist view
- Edit mode for planning ahead

---

## Feature 11: People Met

### Purpose
Log interesting people encounters, exchange contact info

### Bilingual Form (For Others to Fill)
**Fields visible to person filling form:**
- Name / 名前 (required)
- Contact (optional - Instagram, email, etc.) / 連絡先（任意 - Instagram、メールなど、お好きな方法で）
- Where we met / 出会った場所

**Clarification text:**
"Contact (optional — Instagram, email, or however you'd like to stay connected)"
"連絡先（任意 — Instagram、メールなど、お好きな方法で）"

### Josh's Private Fields (Not shown to person)
- **Photo** (Josh adds later)
- **Notes** (Josh's private notes about the person)
- **Context** (how they met, what they talked about)
- **Link to journal entry** (if applicable)

### QR Code Feature
- Generate QR code that links to contact form
- Person scans QR
- Fills out their info
- Josh receives it
- Josh adds photo/notes later

**Alternative:** Josh logs manually (simpler for Phase 1)

### Display
- List of people
- Search by name
- Filter by: date met, location
- Click to see full details

### Use Case
- Portrait photography - exchange contact to send photos later
- Interesting locals who give recommendations
- Fellow travelers
- Keep track of connections made

---

## Feature 12: Seasonal Observations

### Purpose
Track seasonal items, limited releases, special experiences

### Entry Fields
- **Item/Observation** (text)
- **Category** (dropdown):
  - 🌸 Nature (plum blossoms, early cherry blossoms)
  - 🍱 Food & Drink (seasonal menu items, limited editions)
  - 🎪 Event (festivals, seasonal activities)
  - 🛍️ Product (seasonal merchandise, limited releases)
  - 🏮 Other
- **Photo** (required or optional depending on category)
- **Location** (where observed)
- **Date** (auto or manual)
- **Notes** (textarea)
- **Purchased?** (yes/no checkbox)
- **Price** (if purchased)

### Display
- Grid view with photos
- Filter by category
- Sort by date
- "Purchased" vs "Just observed" filter

### Use Case
- End of plum blossom season
- Pre-cherry blossom seasonal items
- Limited-edition food/drink
- Seasonal merchandise Josh might not buy but wants to remember
- Track what was available during this specific time

---

## Feature 13: Recommendations

### Purpose
Log places/things recommended by locals or others

### Entry Fields
- **Recommendation** (text - place name or activity)
- **Type** (restaurant, shop, sight, activity, etc.)
- **Recommended by** (text - who suggested it)
- **Location/address** (text)
- **Google Maps link** (optional)
- **Why recommended** (textarea - what they said about it)
- **Priority** (high, medium, low)
- **Status** (want to go, visited, skipped)
- **Date recommended** (auto)
- **Date visited** (if visited)
- **Link to journal entry** (if visited)

### Display
- List view
- Filter by: status, priority, type
- Sort by: priority, date, location
- Map view (if possible)

### Integration
- Can mark as "visited" and link to journal entry
- Can add notes after visiting

### Use Case
- Local recommendations
- Fellow traveler suggestions
- Things mentioned in guidebooks
- Reddit/blog suggestions
- Keep track of must-dos vs nice-to-dos

---

## Feature 14: Landing Page / Home Dashboard

### Purpose
Central hub with quick info and navigation

### Components

**Weather Card:**
- Current temperature
- Conditions
- High/low
- Location (auto-detect or manual)
- API: OpenWeatherMap (free tier)

**Trip Stats:**
- Days elapsed / days remaining
- Total journal entries
- Total photos captured
- Total stamps collected
- Total spent (from budget)

**Today's Plan:**
- Manual entry of planned activities
- Or link to Wanderlog for full itinerary
- Quick view of today's schedule
- Fields per plan item:
  - Title
  - Time (optional)
  - Google Maps link
  - Notes
  - "View" and "Get directions" buttons

**Quick Navigation:**
- Yesterday | Today | Tomorrow buttons
- Jump to specific date
- Quick access to today's journal

**Quick Actions:**
- Add journal entry
- Log expense
- Quick moment capture
- View language phrases

### Wanderlog Integration
**Options:**
1. Link to Wanderlog per day (simple)
2. API integration (if Wanderlog has one)
3. Manual entry (works offline)

**Suggested:** Start with manual entry or simple links

---

## Cross-Feature Integration

### Data Relationships

**Journal Entry → Budget:**
- Expense amount can be added when creating journal entry
- Auto-creates budget entry
- Link between them

**Journal Entry → Purchases:**
- Can mark items purchased during entry
- Auto-creates purchase log entry
- Photo syncs

**Journal Entry → Goshuin:**
- Add goshuin when visiting shrine/temple
- Links back to journal entry

**Purchases/Souvenirs → Budget:**
- Auto-import amounts
- Update budget when prices change
- Link to original entry

**Recommendations → Journal:**
- Mark recommendation as "visited"
- Link to journal entry when visited
- Can add notes after visit

**Transport Log → Journal:**
- Can create journal entry from transport log
- Or link transport to existing entry

### Universal Features

**Search:**
- Global search across all features
- Search by: text, date, location, tag, category

**Export:**
- Export all data as JSON
- Export specific feature as CSV
- Include photos in export
- Timestamped backups

**Backup:**
- Auto-backup to Google Drive (daily)
- Manual export anytime
- Import to restore

**Night Mode:**
- Toggle for all features
- Saves preference
- Easy on eyes for evening journaling

---

## Technical Implementation Details

### File Structure
```
/
├── index.html          (main app - all features)
├── manifest.json       (PWA config)
├── sw.js              (service worker)
└── README.md          (setup instructions)
```

### Data Structure (localStorage)

```javascript
{
  version: "1.0.0",
  settings: {
    nightMode: false,
    exchangeRate: 109.36,
    lastRateUpdate: "2025-02-05T10:30:00Z",
    preferredCurrency: "AUD",
    driveConnected: false,
    lastBackup: "2025-02-05T10:30:00Z"
  },
  journal: {
    "2025-02-24": [
      {
        id: "uuid",
        name: "Fushimi Inari Shrine",
        category: "shrine",
        time: "14:30",
        location: {
          address: "68 Fukakusa Yabunouchicho, Fushimi Ward",
          mapsLink: "https://maps.google.com/?q=..."
        },
        photos: ["base64...", "base64..."],
        nestedEvents: [], // if theme park
        meals: [
          {
            name: "Takoyaki",
            time: "12:00",
            photo: "base64...",
            note: "From street vendor"
          }
        ],
        notes: "Incredible atmosphere...",
        feelings: "Peaceful and contemplative...",
        people: "Met a local photographer...",
        sensory: "Smell of incense, sound of bells...",
        tags: ["sacred", "peaceful", "photography"],
        reflection: {
          text: "Looking back...",
          date: "2025-02-25T08:00:00Z"
        },
        createdAt: "2025-02-24T14:30:00Z",
        updatedAt: "2025-02-24T14:30:00Z"
      }
    ]
  },
  budget: [
    {
      id: "uuid",
      amount: 1500,
      currency: "JPY",
      amountAUD: 20.50,
      category: "food",
      description: "Lunch at restaurant",
      date: "2025-02-24",
      time: "12:30",
      linkedEntry: "journal-entry-uuid",
      linkedPurchase: null,
      createdAt: "2025-02-24T12:30:00Z"
    }
  ],
  purchases: [
    {
      id: "uuid",
      item: "Fujifilm film",
      store: "Bic Camera",
      date: "2025-02-24",
      time: "15:00",
      price: 2500,
      currency: "JPY",
      photo: "base64...",
      notes: "Found good deal",
      linkedJournalEntry: "uuid",
      createdAt: "2025-02-24T15:00:00Z"
    }
  ],
  souvenirs: [
    {
      id: "uuid",
      item: "Ceramic bowl",
      recipient: "Mom",
      store: "Pottery shop in Kyoto",
      date: "2025-03-01",
      price: 5000,
      currency: "JPY",
      photo: "base64...",
      notes: "Hand-painted design",
      createdAt: "2025-03-01T14:00:00Z"
    }
  ],
  stamps: [
    {
      id: "uuid",
      location: "Tokyo Station",
      photo: "base64...",
      date: "2025-03-10",
      stampQuest: true,
      notes: "Limited edition",
      linkedJournalEntry: "uuid",
      createdAt: "2025-03-10T10:00:00Z"
    }
  ],
  goshuin: [
    {
      id: "uuid",
      shrineName: "Fushimi Inari Taisha",
      photo: "base64...",
      location: "Kyoto",
      date: "2025-02-24",
      price: 300,
      significance: "First goshuin of trip",
      linkedJournalEntry: "uuid",
      createdAt: "2025-02-24T15:00:00Z"
    }
  ],
  transport: [
    {
      id: "uuid",
      route: "Kyoto to Tokyo",
      trainType: "Shinkansen Nozomi",
      trainNumber: "123",
      date: "2025-03-10",
      time: "09:00",
      duration: "2h 15m",
      observations: "Mount Fuji visible!",
      photo: "base64...",
      linkedJournalEntry: "uuid",
      createdAt: "2025-03-10T09:00:00Z"
    }
  ],
  moments: [
    {
      id: "uuid",
      photo: "base64...",
      caption: "Perfect sunset at Kiyomizu-dera",
      date: "2025-02-26",
      time: "17:45",
      location: "Kyoto",
      createdAt: "2025-02-26T17:45:00Z"
    }
  ],
  edc: {
    standard: [
      { item: "Camera body", checked: false },
      { item: "23mm lens", checked: false }
    ],
    daily: {
      "2025-02-24": [
        { item: "Wide angle lens", checked: true },
        { item: "Extra battery", checked: true }
      ]
    },
    templates: {
      "temple-day": [...],
      "city-exploring": [...]
    }
  },
  people: [
    {
      id: "uuid",
      name: "Takeshi",
      contact: "@takeshi_photo",
      whereMet: "Fushimi Inari",
      photo: "base64...",
      notes: "Local photographer, gave great tips",
      context: "Met while shooting torii gates",
      linkedJournalEntry: "uuid",
      dateMet: "2025-02-24",
      createdAt: "2025-02-24T14:30:00Z"
    }
  ],
  language: [
    {
      id: "uuid",
      english: "May I take your photo?",
      romaji: "Shashin wo totte mo ii desu ka?",
      japanese: "写真を撮ってもいいですか？",
      tags: ["photo", "question"],
      favorite: true,
      custom: false,
      usageCount: 5,
      lastUsed: "2025-02-24T14:00:00Z"
    }
  ],
  seasonal: [
    {
      id: "uuid",
      item: "Plum blossom mochi",
      category: "food",
      photo: "base64...",
      location: "Kyoto station",
      date: "2025-02-25",
      notes: "Limited edition for plum season",
      purchased: true,
      price: 800,
      createdAt: "2025-02-25T10:00:00Z"
    }
  ],
  recommendations: [
    {
      id: "uuid",
      recommendation: "Tsukiji Outer Market",
      type: "food",
      recommendedBy: "Hotel concierge",
      location: "Tokyo",
      mapsLink: "https://maps.google.com/?q=...",
      why: "Best sushi breakfast in Tokyo",
      priority: "high",
      status: "want-to-go",
      dateRecommended: "2025-03-08",
      dateVisited: null,
      linkedJournalEntry: null,
      createdAt: "2025-03-08T10:00:00Z"
    }
  ],
  todaysPlan: {
    "2025-02-24": [
      {
        id: "uuid",
        title: "Fushimi Inari Shrine",
        time: "14:00",
        mapsLink: "https://maps.google.com/?q=...",
        note: "Allow 2-3 hours, wear good shoes",
        completed: false
      }
    ]
  }
}
```

### API Keys Needed (User Provides)
- Google Drive API (client ID + secret)
- OpenWeatherMap API (optional, free tier)
- Exchange rate API (optional, free tier - no key needed)

### PWA Requirements
- HTTPS hosting
- manifest.json
- Service worker
- Icons (can use emoji SVG as placeholder)
- Proper meta tags

### Browser Compatibility
- **Primary:** Chrome for Android, Samsung Internet
- **iOS Safari:** Will work but "Add to Home Screen" slightly different
- **Desktop:** Works but optimized for mobile

### Performance Considerations
- **Photo size:** Recommend max 1MB per photo
- **localStorage limit:** ~5-10MB total
- **Solution:** Export backups frequently, or implement photo compression
- **Lazy loading:** Load photos as needed, not all at once

### Offline Functionality
- **Service worker:** Cache all static assets
- **Strategy:** Cache-first for assets, network-first for data
- **Sync:** When back online, attempt to sync with Google Drive
- **Indicator:** Show online/offline status

---

## Development Phases

### Phase 1: Core Experience ✅ (INCOMPLETE)
**Status:** Delivered but missing features
- Daily Journal (missing: nested events, meals section, maps)
- Basic structure and design
- PWA setup
- Night mode

**What's Missing:**
- Nested events for theme parks
- Meals & snacks section
- Location/Maps integration

### Phase 2: Daily Tools (Next)
- Complete Daily Journal (add missing features)
- Budget Tracker
- Language Notes

### Phase 3: Collections
- Purchases Log
- Souvenirs Tracker
- Stamp Rally
- Goshuin Collection

### Phase 4: Supporting Tools
- Transport Log
- Moments
- EDC Planner
- People Met

### Phase 5: Extras
- Seasonal Observations
- Recommendations
- Landing Page
- Google Drive integration

### Phase 6: Polish & Testing
- Bug fixes
- Performance optimization
- User testing
- Documentation
- Pre-trip preparation

---

## User Context & Constraints

### User Profile
- Creative professional (photography, videography, writing, art)
- Returning to university for Paleontology degree
- Deals with mental paralysis, motivation issues, overwhelm
- Values intentional, meaningful design
- Appreciates depth but needs manageable complexity

### Technical Comfort
- Can set up API keys
- Comfortable with basic technical tasks
- May need clear instructions
- Has used VPN, various apps

### Trip Context
- Feb 24 - Mar 17, 2025 (22 days)
- Osaka → Kyoto → Tokyo
- With wife
- Bringing photography/videography gear
- Pre-booked: Universal Studios Japan, Nintendo Museum lottery (Mar 5 birthday)
- Using data-only eSIM (no calls/SMS)

### Design Preferences
- Refined over flashy
- Intentional over busy
- Joyful but not cluttered
- Depth without overwhelm
- No generic AI aesthetics
- Japan-inspired but respectful

### Key Requirements
- Must work offline
- Must save reliably
- Must be mobile-friendly
- Must handle photos
- Must be testable before trip
- Must have backup options

---

## Success Criteria

### Before Trip
- [ ] All Phase 1-2 features working
- [ ] Installed as PWA on Samsung
- [ ] Tested with sample data
- [ ] Backup/restore tested
- [ ] Works offline
- [ ] Photo upload works
- [ ] Save confirmation works
- [ ] Google Drive backup configured

### During Trip
- [ ] Use daily without friction
- [ ] Captures moments easily
- [ ] Data persists reliably
- [ ] No lost entries/photos
- [ ] Offline mode works
- [ ] Quick captures possible

### After Trip
- [ ] All data safely backed up
- [ ] Can export to other formats
- [ ] Photos preserved
- [ ] Searchable archive
- [ ] Shareable content

---

## Known Issues & Risks

### Technical Risks
1. **Photo storage limits** - localStorage ~5-10MB
   - Solution: Regular backups, photo compression
2. **Browser compatibility** - Some features may not work on all browsers
   - Solution: Test on Samsung Internet specifically
3. **Offline sync** - Might miss saves if unexpected crashes
   - Solution: Auto-backup, save confirmations
4. **API rate limits** - Free tier limits on weather/currency
   - Solution: Fallback to manual entry

### User Experience Risks
1. **Complexity** - Too many features might overwhelm
   - Solution: Phase releases, hide unused features
2. **In-moment friction** - If too slow to capture moments
   - Solution: Quick capture options, simplified flows
3. **Data loss** - Catastrophic if all data lost
   - Solution: Multiple backup strategies

### Mitigation Strategies
- Phase releases (don't build everything at once)
- Extensive testing before trip
- Multiple backup methods
- Clear error messages
- Graceful degradation
- Offline-first architecture

---

## Future Enhancements (Post-Trip)

### Possible Additions
- Multi-trip support
- Sharing/export to blog
- Photo galleries
- Map visualizations
- Statistics & insights
- PDF report generation
- Social sharing
- Collaboration (share with wife)
- Cloud sync between devices
- Native apps (iOS/Android)
- Desktop version
- Analytics dashboard

### Productization
If successful, could be:
- Template for others
- Paid product
- Open source project
- Travel blog integration
- Photography workflow tool

---

## Questions to Resolve

### For User to Decide
1. Which Phase 2-5 features are must-haves vs nice-to-haves?
2. Preferred hosting platform? (Netlify, Vercel, GitHub Pages)
3. Set up Google Drive API now or later?
4. Daily budget target? (for budget tracker)
5. Prioritize which features to build first?

### Technical Decisions
1. Single HTML file or split into modules?
2. Use a JavaScript framework or vanilla JS?
3. Photo compression on upload?
4. Implement full Wanderlog integration or just links?
5. Build native contact form for People Met or manual only?

---

## Summary

This is a comprehensive travel companion PWA with 14 major features designed specifically for a 22-day Japan trip. The system prioritizes offline functionality, reliable data persistence, mobile-first design, and a refined Japan-inspired aesthetic.

**Current Status:** Phase 1 (Daily Journal) partially complete, missing nested events, meals section, and maps integration.

**Next Steps:** Complete Phase 1, then build Phase 2 (Budget + Language Notes).

**Timeline:** 18 days remaining before trip departure.

**Goal:** Functional, tested, reliable system ready by Feb 24, 2025.
