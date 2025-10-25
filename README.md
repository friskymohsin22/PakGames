# PakGames - Ready Frontend (merged)

This repository package was prepared from your uploaded frontend and connector ZIPs and includes:
- Merged frontend + connector source
- GitHub Actions workflow to build a signed release APK automatically
- gradle.properties template (placeholders)
- ProGuard/R8 release config placeholder

## Quick setup after uploading to GitHub

1. Create a GitHub repository (or use your existing one).
2. Upload the extracted project files (this folder) to the repo root.
3. Generate a keystore locally:
   ```bash
   keytool -genkeypair -v -keystore pakgames-release.jks -alias pakgames -keyalg RSA -keysize 2048 -validity 10000
   ```
4. Convert keystore to base64 and add as repository secret `KEYSTORE_BASE64` (see README earlier steps).
   - mac/linux:
     ```bash
     base64 pakgames-release.jks > pakgames-release.txt
     ```
   - windows (powershell):
     ```powershell
     [Convert]::ToBase64String([IO.File]::ReadAllBytes("pakgames-release.jks")) | Out-File pakgames-release.txt
     ```
5. In GitHub repo > Settings > Secrets and variables > Actions add these secrets:
   - KEYSTORE_BASE64 (paste file contents)
   - KEYSTORE_PASSWORD (your keystore password)
   - KEY_ALIAS (pakgames)
   - KEY_PASSWORD (your key password)

6. Commit to `main` branch and trigger the workflow (Actions tab). After run completes, download artifact `pakgames-apk`.

## Notes
- Please DO NOT commit your keystore or passwords to the repo.
- `gradle.properties` contains placeholders for local use only.
- Verify `AndroidManifest.xml` package name is `com.pak.games`. If not, update accordingly.
