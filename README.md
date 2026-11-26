# 🌹 ROSE AI

A Bengali/English AI companion for Android. Built with Kotlin and Jetpack Compose.

- **Package:** `com.roseai.app`
- **Providers:** Groq, OpenRouter, Mistral, Google Gemini
- **Owner answer:** তোমার মালিক কে? → আমার মালিক হচ্ছে রিফাত।

## Project structure

```
ROSE-AI/
├── .github/workflows/android.yml   CI: verify layout, build assembleDebug, upload APK
├── app/
│   ├── build.gradle
│   ├── proguard-rules.pro
│   └── src/main/
│       ├── AndroidManifest.xml
│       ├── java/com/roseai/app/
│       │   ├── MainActivity.kt
│       │   ├── RoseApplication.kt
│       │   ├── ui/theme/       Color, Theme, Type
│       │   ├── ui/screens/     Splash, Home, Chat (+history), Settings (+API), Voice
│       │   ├── ui/components/  AnimatedButton, AICharacter, ChatBubble, LoadingAnimation, GlassCard
│       │   ├── data/           ApiConfig, ChatRepository, ChatMessage
│       │   ├── network/        ApiService (requests/parsing), ApiClient (HTTP + test)
│       │   ├── voice/          SpeechManager, TTSManager
│       │   ├── security/       SecureStorage (Keystore-backed encrypted prefs)
│       │   ├── viewmodel/      RoseViewModel
│       │   └── util/           OwnerRule
│       └── res/                values, drawables, mipmap-* launcher icons
├── gradle/wrapper/             wrapper properties (see note below)
├── backend/                    reserved for a future server (not used by the app)
├── build.gradle
├── settings.gradle             includes ":app"
├── gradle.properties
└── README.md
```

## Build

### On GitHub (no PC needed)

1. Push this repository to GitHub.
2. Open **Actions → Android Debug Build**. It runs on each push, or press **Run workflow**.
3. The workflow checks the project layout, builds `assembleDebug`, and uploads the APK as
   the `rose-ai-debug-apk` artifact. If the build fails, the log shows the Gradle error.

### In Android Studio

1. Open the `ROSE-AI` folder. Let Gradle sync (JDK 17).
2. Run the `app` configuration, or run `gradle :app:assembleDebug`.

## Versions

| Component | Version |
|---|---|
| Android Gradle Plugin | 8.5.2 |
| Kotlin / Compose compiler plugin | 2.0.21 |
| Gradle | 8.9 |
| JDK | 17 |
| compileSdk / targetSdk / minSdk | 34 / 34 / 26 |

## Using the app

1. Open **🔑 API** on the home screen.
2. Choose a provider, paste your key, and check the Model ID.
3. Press **⚡ TEST API CONNECTION**. Success appears only after a real AI reply.
4. Press **CONNECT & SAVE API**. The home screen then shows the active provider.

Keys are stored in Android Keystore-backed encrypted preferences. They are never
hardcoded, logged, or shown in error messages.

## Logo

`app/src/main/res/drawable/ic_launcher_foreground.xml` and the `mipmap-*` launcher icons are
**placeholders**. Replace them with your real ROSE AI logo using Android Studio:
right-click `res` → **New → Image Asset**.

## Known limitations

- The character in `AICharacter.kt` is a stylized animated placeholder. Replace it with your
  anime character artwork when ready.
- `gradlew` and `gradle-wrapper.jar` are not included in this archive. The CI workflow
  installs Gradle 8.9 directly. To add the wrapper locally, run `gradle wrapper --gradle-version 8.9`.
- Replies arrive when complete (no streaming).
- Theme and language settings are not implemented.
