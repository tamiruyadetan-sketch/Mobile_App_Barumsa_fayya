# Mobile_App_Barumsa_fayya
# 🏥 Fayyaa Keenya (HealthGuide)

An Android health-education app written in **Kotlin** with **Jetpack Compose**. It presents common diseases in **Afaan Oromoo**: what they are, their symptoms, causes, prevention and advice. The content comes from the Word document *DHUKKUBA GARAACHAA*.

> **Disclaimer:** This app is for health education only. It does not diagnose or treat any condition. Anyone with symptoms should see a health professional.

---

## ✨ Features

- **19 health topics** from the source document, such as gastritis, hepatitis B, heart disease, sinusitis, kidney disease, kidney stones, cervical, esophageal and breast cancer, malaria, pneumonia, anemia, high blood pressure, TB and skin care
- **Full-text search**: matches titles and the whole article text
- **Category filters**: Digestive, Heart & Blood, Kidney & Urinary, Cancer, Infectious, Other
- **Readable articles**: headings, bullet lists, numbered items and highlighted messages
- **Text size control**: A- / A+ buttons on every article
- **Favorites**: save articles on the device; they are still there after restarting the app
- **Share**: send an article as plain text through any installed app
- **Language button (EN/OM)**: switches the interface labels between Afaan Oromoo and English (article text stays in Afaan Oromoo)
- **Dark mode**: follows the phone setting
- **Offline**: all content is bundled inside the app, so no internet is needed

---

## 🧱 Tech stack

| Area | Choice |
|---|---|
| Language | Kotlin 2.0.21 |
| UI | Jetpack Compose (BOM 2024.10.01), Material 3 |
| Navigation | Navigation Compose 2.8.3 |
| State | `AndroidViewModel` with Compose state |
| Storage | `SharedPreferences` (favorites, language) |
| Content | `assets/diseases.json`, read with the built-in `org.json` |
| Build | Android Gradle Plugin 8.7.3, Gradle 8.9, JDK 17 |
| SDK | minSdk 24 (Android 7.0), compileSdk / targetSdk 35 |

---

## 🚀 Getting started

### Requirements
- Android Studio (a recent version)
- JDK 17 (the JDK bundled with Android Studio works)
- Internet access for the first Gradle sync

### Run
1. Open Android Studio and choose **File > Open**, then select the `HealthGuide` folder.
2. Wait for **Gradle Sync** to finish. If Android Studio offers to update Gradle or plugin versions, accepting is fine.
3. Pick an emulator or connect a phone with USB debugging on.
4. Press **Run ▶**.

### Build an APK
- **Debug APK:** *Build > Build Bundle(s) / APK(s) > Build APK(s)*. The file appears in `app/build/outputs/apk/debug/`.
- **Release APK / AAB:** *Build > Generate Signed Bundle / APK*, then follow the signing wizard.

---

## 📁 Project structure

```
HealthGuide/
├── app/
│   ├── build.gradle.kts
│   └── src/main/
│       ├── AndroidManifest.xml
│       ├── assets/
│       │   └── diseases.json              ← ALL article content
│       ├── res/                           ← app name, theme, launcher icon
│       └── java/com/example/healthguide/
│           ├── MainActivity.kt
│           ├── data/
│           │   ├── Models.kt              ← Disease, Block, Category
│           │   ├── DiseaseRepository.kt   ← loads diseases.json
│           │   └── Prefs.kt               ← favorites + language
│           └── ui/
│               ├── HealthGuideApp.kt      ← navigation + bottom bar
│               ├── AppViewModel.kt        ← search, filter, favorites
│               ├── Strings.kt             ← interface labels (OM / EN)
│               ├── theme/Theme.kt         ← colors
│               └── screens/
│                   ├── HomeScreen.kt
│                   ├── DetailScreen.kt
│                   ├── FavoritesScreen.kt
│                   ├── AboutScreen.kt
│                   └── Components.kt      ← shared disease card
├── build.gradle.kts
├── settings.gradle.kts
└── gradle/wrapper/gradle-wrapper.properties
```

---

## ✏️ Editing the content

All articles live in `app/src/main/assets/diseases.json`. You can fix typos or add new diseases without changing any Kotlin code.

### Structure of one disease

```json
{
  "id": "malaria",
  "title": "Dhukkuba Busaa fi Maloota Ittisaa",
  "titleEn": "Malaria",
  "category": "infectious",
  "emoji": "🦟",
  "summary": "One or two lines shown on the card.",
  "blocks": [
    { "t": "h", "x": "Mallattoolee" },
    { "t": "p", "x": "A normal paragraph." },
    { "t": "b", "x": "A bullet point" },
    { "t": "n", "x": "1. A numbered item" },
    { "t": "callout", "x": "An important highlighted message" }
  ]
}
```

### Block types

| `t` | Shown as |
|---|---|
| `h` | Heading with a colored bar |
| `p` | Paragraph |
| `b` | Bullet point |
| `n` | Numbered item in a tinted box (keep the number in the text) |
| `callout` | Highlighted message card |

### Categories

Use one of these values for `category`: `digestive`, `heart`, `kidney`, `cancer`, `infectious`, `other`. Unknown values fall back to `other`.

### Add a new disease
1. Copy an existing entry inside `"diseases": [ ... ]` in `diseases.json`.
2. Give it a **unique** `id` and fill in the other fields.
3. Run the app. It appears on Home automatically and is included in search.

Keep the file saved as **UTF-8** so Afaan Oromoo characters such as `'` display correctly.

---

## 🎨 Customizing

| What to change | File |
|---|---|
| Colors (teal theme, accent color) | `ui/theme/Theme.kt` |
| Button and label text (OM / EN) | `ui/Strings.kt` |
| Category names and icons | `data/Models.kt` (`Category` enum) |
| App name on the phone | `res/values/strings.xml` |
| Launcher icon | `res/drawable/ic_launcher.xml` |
| Package name / application ID | `app/build.gradle.kts` (and rename the Kotlin package) |

---

## 🧭 How it works

1. `DiseaseRepository` reads `diseases.json` from assets when the app starts.
2. `AppViewModel` holds the list, the search text, the selected category and the favorites. The Home screen reads the filtered list, so it updates as the user types.
3. `HealthGuideApp` handles navigation between Home, Favorites, About and the article screen.
4. `DetailScreen` turns each block into the matching Compose element.

---

## ⚠️ Known limitations

- The interface labels in Afaan Oromoo were written for this project and should be reviewed by a native speaker.
- Article text exists only in Afaan Oromoo; the EN/OM button translates the interface, not the articles.
- No images or diagrams are included yet.
- There are no automated tests yet.

## 🗺️ Ideas for next steps

- Add English translations of the articles
- Add images and diagrams per disease
- Add a "nearest health facility" screen
- Add reminders and daily health tips
- Add unit tests for search and filtering

---

## 📄 License and credits

- Content: based on the document *DHUKKUBA GARAACHAA*.
- Code: add your own license here (for example MIT) before publishing.
