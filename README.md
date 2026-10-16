# Wasabi

Wasabi is an open-source messaging app built with Flutter and Firebase. It focuses on fast, simple chat, one-on-one or in groups, with a clean, Signal-inspired design. It runs on Android, iOS and the web (installable as a PWA), and it is built to run on free tiers only.
https://wasabi-texting.web.app
## Features

- **Real-time one-on-one chat** with instant delivery on both devices.
- **Group chats.**
- **Photos, audio notes and camera.** Send images from your gallery, record voice messages, or snap a photo and send it right away.
- **Find people by @username.** Unique usernames are claimed in a single transaction, so no two people can share one.
- **Profiles** with a bio and a profile picture.
- **Message reactions** and **reply to a specific message** with a quoted preview.
- **Seen ticks** (sent and seen), calculated from the unread counter with no extra writes.
- **Chat list** with last message, time and unread count.
- **Push notifications** delivered through Supabase Edge Functions.
- **Media storage** on Supabase.
- **Signal-style interface**: pure black background, floating pill controls, solid blue message bubbles, smooth animations.
- **PWA support**: install the web app to the iPhone Home Screen from Safari.
- **Firestore security rules**: only the members of a chat can read it or send messages in it, and sent messages cannot be edited or deleted by clients.

## Tech stack

| Area | Technology |
| --- | --- |
| App | Flutter and Dart |
| Auth and database | Firebase Authentication, Cloud Firestore |
| Web hosting | Firebase Hosting |
| Media and push logic | Supabase (Storage, Edge Functions: `notify-message`, `grant-media-role`) |
| Packages | provider, google_fonts, flutter_svg, intl, fake_cloud_firestore (tests) |

Everything runs on the Firebase Spark plan and the Supabase free tier.

## Getting started

### Prerequisites

- Flutter SDK (stable channel)
- Firebase CLI and FlutterFire CLI
- A Firebase project (Spark plan is enough)
- A Supabase project (free tier is enough)

### Setup

1. Clone the repository:
   ```bash
   git clone <your-repo-url>
   cd wasabi
   ```
2. Install dependencies:
   ```bash
   flutter pub get
   ```
3. Create your own Firebase project and generate the config. Firebase configuration files are not included in the repository:
   ```bash
   flutterfire configure
   ```
4. Deploy the Firestore rules:
   ```bash
   firebase deploy --only firestore:rules
   ```
5. Set up Supabase: create a project, create a storage bucket for media, and deploy the Edge Functions `notify-message` and `grant-media-role`. Add your Supabase URL and anon key to the app's config.
6. Run the app:
   ```bash
   flutter run              # Android or iOS
   flutter run -d chrome    # Web
   ```

### Deploy the web app

```bash
flutter build web
firebase deploy --only hosting
```

## Testing

```bash
flutter analyze
flutter test
```

The test suite covers services, models, screens, and the reply and username logic.

## Project status

Wasabi is under active development. The latest version is v1.0.2. Release notes: [v1.0.0](RELEASE_NOTES_v1.0.0.md), [v1.0.1](RELEASE_NOTES_v1.0.1.md), [v1.0.2](RELEASE_NOTES_v1.0.2.md).

**Not yet available:** voice and video calls (audio calls are planned but on hold), typing indicator, online/last-seen status.

## Roadmap

- Delete message for me
- In-chat search
- Forward message
- Edit message with an "edited" label
- Dark/light theme toggle
- Audio calls

## Contributing

Issues and pull requests are welcome. Please run `flutter analyze` and `flutter test` before opening a PR.

## License

Add your license here (for example MIT) and include a `LICENSE` file.
