# Raízes

A private family app for keeping the people, stories and curiosities of our family in one place. It is a showcase project and is not published on any app store.

## Privacy

This repository is public, but the family's data is not:

- The Firebase config (`lib/firebase_options.dart`, `android/app/google-services.json`, `firebase.json`) is not committed.
- Access is controlled by [firestore.rules](firestore.rules) and [storage.rules](storage.rules). Only accounts listed in the `members` collection can read or write anything. That list is managed by hand in the Firebase console, and the app cannot change it.
- Personal assets in `assets/family/` are not committed. `assets/demo/` holds sample data instead.

## Running it with your own Firebase project

1. Create a Firebase project and turn on **Authentication**, **Cloud Firestore** and **Storage**.
2. Generate the config files:
   ```sh
   dart pub global activate flutterfire_cli
   flutterfire configure
   ```
   If you'd rather fill it in by hand, copy [lib/firebase_options.example.dart](lib/firebase_options.example.dart) to `lib/firebase_options.dart`.
3. Merge the `firestore` and `storage` entries from [firebase.example.json](firebase.example.json) into the `firebase.json` that `flutterfire` generated, then deploy the rules:
   ```sh
   firebase deploy --only firestore:rules,storage
   ```
4. Sign in once from the app, copy your UID from Authentication → Users, and create a document at `members/<your uid>` in Firestore. Any fields will do, for example `name: "..."`.
5. Run the app:
   ```sh
   flutter run
   ```
