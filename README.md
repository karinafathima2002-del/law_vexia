# ⚖️ LexQuest – Constitutional Law 1 App
> Flutter app for iOS & Android. 100% free. No Firebase.

---

## 📁 Project Structure

```
lib/
├── main.dart                        # App entry point + Supabase init
├── constants/
│   └── app_theme.dart               # Colors, fonts, theme
├── models/
│   └── models.dart                  # Unit, Topic, CaseLaw, QuizQuestion, etc.
├── services/
│   ├── supabase_service.dart        # All DB + Auth operations + seed data
│   └── question_generator.dart     # Random question generation logic
└── screens/
    ├── auth/
    │   └── login_screen.dart        # Login / Signup / Skip
    ├── home_screen.dart             # BYJU's-style learning path
    ├── unit_detail_screen.dart      # All games entry point for each unit
    ├── notes_screen.dart            # Notes with PDF open support
    ├── revision_screen.dart         # Mind map / tree diagram revision
    ├── profile_screen.dart          # User stats + admin access
    ├── admin_upload_screen.dart     # Upload PDFs + add questions
    └── games/
        ├── flashcard_screen.dart    # Flip card game (Known / Review)
        ├── quiz_screen.dart         # Kahoot-style solo quiz with timer
        ├── match_screen.dart        # Match the pairs game
        ├── verdict_screen.dart      # Verdict Call (Valid / Invalid)
        └── caselaw_screen.dart      # Case Law browse + quiz
```

---

## 🚀 Setup in 5 Steps

### Step 1 – Flutter Setup
```bash
flutter pub get
```

### Step 2 – Supabase (Free)
1. Go to [supabase.com](https://supabase.com) → New project (free)
2. Go to **SQL Editor** → paste contents of `supabase_schema.sql` → Run
3. Go to **Storage** → New bucket → name it `pdfs` → Public ON
4. Go to **Settings → API** → copy your `URL` and `anon key`

### Step 3 – Add Keys to App
Open `lib/main.dart` and replace:
```dart
url: 'https://YOUR_PROJECT.supabase.co',   // ← your URL here
anonKey: 'YOUR_ANON_KEY',                  // ← your anon key here
```

### Step 4 – Run
```bash
# iOS
flutter run -d ios

# Android
flutter run -d android
```

### Step 5 – Add Content
- **Option A (Easiest):** Supabase Dashboard → Table Editor → insert rows directly
- **Option B (In-app):** Login → Profile → Admin: Upload Content
- **Option C (SQL):** Write INSERT statements and run in SQL Editor

> ⚠️ App has full built-in seed data for all 6 units so it works offline even without Supabase configured.

---

## 🎮 Game Modes

| Screen | Description |
|--------|-------------|
| **Flashcard** | Flip cards – mark Known ✅ or Review ❌ |
| **Quick Quiz** | Kahoot-style 4-option MCQ with 15s timer + streak bonus |
| **Match Pairs** | Connect left column to right column |
| **Verdict Call** | Read a statement → tap VALID ✅ or INVALID ❌ |
| **Case Law Memory** | Browse cases + 10-question quiz on facts/holdings |
| **Mind Map Revision** | Expandable tree: topics + key points + case laws |

---

## 📦 pubspec.yaml Dependencies

```yaml
supabase_flutter: ^2.5.0    # Free backend
google_fonts: ^6.1.0        # Plus Jakarta Sans
flutter_animate: ^4.3.0     # Smooth animations
confetti: ^0.7.0             # Quiz celebration
file_picker: ^8.0.3          # PDF upload
url_launcher: ^6.2.5         # Open PDF in browser
percent_indicator: ^4.2.3
shared_preferences: ^2.2.2
provider: ^6.1.1
```

---

## 🗄️ Supabase Free Tier

| Resource | Free Limit | Usage |
|----------|-----------|-------|
| Database | 500 MB | 500,000+ questions |
| Storage | 1 GB | ~500 PDFs |
| Auth | Unlimited users | ✅ |
| API calls | 50,000/month | ✅ |
| **Cost** | **$0/month** | ✅ |

---

## 📱 iOS Setup

Add to `ios/Runner/Info.plist`:
```xml
<key>NSPhotoLibraryUsageDescription</key>
<string>Select PDF from files</string>
<key>LSSupportsOpeningDocumentsInPlace</key>
<true/>
```

Minimum iOS version: **12.0** (set in Xcode → Runner → Deployment Info)

## 🤖 Android Setup

Add to `android/app/src/main/AndroidManifest.xml` inside `<application>`:
```xml
<provider
    android:name="androidx.core.content.FileProvider"
    android:authorities="${applicationId}.fileprovider"
    android:exported="false"
    android:grantUriPermissions="true">
    <meta-data
        android:name="android.support.FILE_PROVIDER_PATHS"
        android:resource="@xml/file_paths" />
</provider>
```

Minimum SDK: **21** (already default in Flutter)

---

## ✏️ How to Change App Name

1. **Android:** `android/app/src/main/AndroidManifest.xml` → `android:label`
2. **iOS:** `ios/Runner/Info.plist` → `CFBundleName`

---

## 🔄 How to Add New Questions (3 ways)

### Way 1: Supabase Table Editor (Easiest)
1. Open Supabase Dashboard
2. Table Editor → `questions`
3. Insert row → fill columns

### Way 2: In-App Admin
1. Open app → Profile → Admin: Upload Content
2. Select unit → fill question form → Save

### Way 3: SQL
```sql
insert into questions (unit_id, question, options, correct_index, explanation, type)
values (
  'unit1',
  'Who was the first Governor-General of Bengal?',
  array['Lord Cornwallis', 'Warren Hastings', 'Lord Wellesley', 'Lord Dalhousie'],
  1,
  'Warren Hastings was appointed the first Governor-General under the Regulating Act 1773.',
  'mcq'
);
```

---

## 📄 How to Upload PDF Notes

1. Go to Profile → Admin: Upload Content
2. Select Unit → Select Topic → Pick PDF file
3. Tap "Upload to Supabase"
4. PDF is stored in Supabase Storage (free 1GB)
5. Students tap "Open PDF Notes" button in Notes screen

---

## 🎨 Design

- **Palette:** Scholar Gold – cream background, navy, terracotta, sage green
- **Font:** Plus Jakarta Sans (Google Fonts)
- **No dark mode** (as requested)
- Style inspired by BYJU's/Unacademy with warm, academic colors

---

## 📌 Units Covered

1. Historical Background (Regulating Act → Independence Act)
2. Making of Constitution (Drafting, Sources, Preamble, Features)
3. Union & Citizenship (Art 1–11)
4. Fundamental Rights (Art 12–35, Doctrines, Cases)
5. DPSP & Fundamental Duties (Part IV, Art 51A)
6. Amendment & Basic Structure (Art 368, Basic Structure Doctrine)

Each unit includes:
- Study notes with key points
- Case law with facts, held, significance
- 8+ MCQ questions
- All 5 game modes
