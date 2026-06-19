# TITAN OMEGA CI/CD Pipeline

Automated CI/CD for building and releasing **TITAN OMEGA** v40+ — an advanced Android-based AGI agent with:

- `DecisionEngine` for autonomous task execution and retry logic
- `GeminiBridge` for zero-cost LLM integration (clipboard prompt injection into Gemini/Bard app)
- `Humanizer` for realistic human-like touch gestures (randomized Bezier paths + timing jitter)
- `SkillRecorder` + playback for **Muscle Memory** / imitation learning
- System-level stealth: `ForegroundService`, `WakeLock`, full `AccessibilityService` with gesture dispatch

## 🚀 How it works

This repository's GitHub Actions workflow **self-generates the entire Android project** from embedded source code on every run. 
No need to push Java source files — the pipeline is fully self-contained.

**Trigger** → Build → Signed APK → GitHub Release (automatic)

## 📋 One-time Setup

### 1. Add Repository Secrets

Go to: **Settings → Secrets and variables → Actions**

Add the following secret:

| Secret Name          | Description                                      | Required |
|----------------------|--------------------------------------------------|----------|
| `KEYSTORE_BASE64`    | Base64 of your signing keystore (`lml-stable.keystore`) | Yes     |

```bash
# Generate the secret value
base64 -w 0 path/to/lml-stable.keystore
```

Optional overrides:
- `KEYSTORE_PASSWORD`
- `KEY_ALIAS`
- `KEY_PASSWORD`

### 2. (Optional) Make repository public
Releases are more useful when the repo is public.

## ▶️ Triggering the Pipeline

- **Automatic**: Push any change to `main` branch
- **Manual**: 
  1. Go to **Actions** tab
  2. Select **TITAN OMEGA CI/CD Pipeline**
  3. Click **Run workflow** → **Run workflow**

## 📦 What you get

Every successful workflow creates:

- A new **GitHub Release** tagged `OMEGA-v40.<run_number>`
- The signed APK: `LML-TITAN-OMEGA-v40.<run_number>.apk`

## ⚙️ Technical Details (auto-generated in CI)

- **Android**: compileSdk 34, minSdk 26, targetSdk 34
- **Java**: 17 (Temurin)
- **Gradle**: 8.7 + Android Gradle Plugin 8.5.2
- **Signing**: Release build with provided keystore
- **Versioning**: Auto-increment via `GITHUB_RUN_NUMBER`

## ⚠️ Important Notes

- The generated app is an **Accessibility Service** + floating overlay agent. It requires:
  - Accessibility permission
  - "Display over other apps" permission
- `GeminiBridge` launches the Gemini app and injects prompts via clipboard (current package may need update: `com.google.android.apps.bard` → current Gemini package)
- This project is for **research and educational purposes** in Android automation / AGI agents.
- Use ethically and respect all terms of service of target applications.

## 🔄 Workflow Improvements Applied

- Fixed Java compilation error (`ScreenNode` class visibility — changed to package-private)
- Added Gradle wrapper generation for reliable `./gradlew` execution
- Added `set -e` and graceful keystore handling
- Clean YAML structure and French step names preserved

---

**Project created and workflow launched on:** 19 June 2026

**Repo URL:** https://github.com/dorianpirus68-ctrl/titan-omega-cicd-pipeline

**Actions:** https://github.com/dorianpirus68-ctrl/titan-omega-cicd-pipeline/actions

Check the first run status in the Actions tab. If it fails on signing, add the `KEYSTORE_BASE64` secret and re-run the workflow.