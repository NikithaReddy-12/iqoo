# Document Explainer

Scan or upload a contract, get a calm plain-English summary, and see clauses scored for risk. The app also flags known predatory patterns, answers questions about the document, and includes an offline legal glossary.

## Setup

1. Install the [Flutter SDK](https://docs.flutter.dev/get-started/install).
2. Copy `.env.example` to `.env` and set your Gemini key:

```
GEMINI_API_KEY=your_key_here
```

3. From this folder:

```
flutter pub get
flutter run
```

On web, camera scanning is not available. Use **Upload Document** (PDF with selectable text) or **Paste document text**.

## Web build

```
flutter build web
```

The release files are written to `build/web`. You can preview them locally:

```
python -m http.server 8080 --directory build/web
```

Then open `http://127.0.0.1:8080`.

The Gemini key in `.env` is bundled as a Flutter asset for this demo. Do not treat that as production-grade secret storage.

## Deploy to Firebase Hosting

1. Install the [Firebase CLI](https://firebase.google.com/docs/cli) and sign in:

```
npm install -g firebase-tools
firebase login
```

2. Create a Firebase project in the [Firebase console](https://console.firebase.google.com/), then put its ID in `.firebaserc` (replace `YOUR_FIREBASE_PROJECT_ID`).

3. Build and deploy:

```
flutter build web
firebase deploy --only hosting
```

`firebase.json` serves `build/web` and rewrites unknown paths to `index.html` so Flutter routes work.

## Android APK (Appetize.io backup)

1. Build a release APK:

```
flutter build apk --release
```

The file is:

```
build/app/outputs/flutter-apk/app-release.apk
```

2. Go to [Appetize.io](https://appetize.io/), create an account, and upload that APK.
3. Choose an Android device/version, then use the hosted session URL as a backup demo when Firebase Hosting is unavailable.

Appetize can use the device camera in some plans; for the most reliable demo, use **Upload Document** with a sample PDF.

## Tests

```
flutter analyze
flutter test
```
