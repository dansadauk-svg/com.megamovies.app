# Mega Movies Android

Package: `com.megamovies.app`  
Website: `https://megamovies.com.ng/`

Upload the contents of this project directory to the root of a private GitHub repository. Never commit the signing key or passwords. Add the three MEGA_KEYSTORE_BASE64, MEGA_KEYSTORE_PASSWORD and MEGA_KEY_PASSWORD repository secrets from the separate private signing backup. The key alias is mega_movies.

The supplied Firebase configuration for `com.megamovies.app` is included at `app/google-services.json`. Upload it to GitHub with the project. A `MEGA_GOOGLE_SERVICES_JSON_BASE64` GitHub secret may be used as a fallback if the file is absent. Run the GitHub Actions build to generate an APK and AAB. Push notifications require the matching Firebase project and server configuration; the app subscribes to `mega_movies_all`.

For Android App Links, publish `assetlinks.json` at `https://megamovies.com.ng/.well-known/assetlinks.json` with HTTPS and application/json. Its fingerprint is the upload-key certificate, useful for APKs signed with that key. If Play App Signing is enabled, also add the Play app-signing certificate SHA-256 from Play Console; the upload-key fingerprint alone will not verify Play-distributed installs.

The new application ID creates a separate app from GK Movies. If com.megamovies.app is already published, a new key will not update it unless its existing signing identity or an approved upload-key reset is used.

Project uses Android SDK 36 and Java 17. It was not built or tested in this environment.

## Broadcast notifications
All installations that open the app and successfully subscribe join the Firebase topic `mega_movies_all`. Sending to this topic requires Firebase Console or a server configured with credentials for the same Firebase project; the WordPress frontend notification plugin does not send these pushes. The topic is for broadcast, not per-user targeting. On Android 13+ users must permit notifications. Offline devices receive messages only subject to FCM expiry and platform conditions. FCM topic delivery is optimized for throughput; identical delivery times or delivery to every user cannot be guaranteed.
