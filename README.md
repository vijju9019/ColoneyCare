# ColoneyCare - Android Native App

A native Android application that wraps the ColoneyCare web app (Community Command Center) in a WebView for seamless mobile experience.

**Web App URL**: https://community-command-center--kakamama88732.replit.app

## Project Structure

```
ColoneyCare/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/colonycare/app/
│   │   │   │   └── MainActivity.java
│   │   │   ├── res/
│   │   │   │   ├── layout/
│   │   │   │   │   └── activity_main.xml
│   │   │   │   ├── values/
│   │   │   │   │   ├── colors.xml
│   │   │   │   │   ├── strings.xml
│   │   │   │   │   └── themes.xml
│   │   │   │   └── xml/
│   │   │   │       ├── backup_rules.xml
│   │   │   │       └── data_extraction_rules.xml
│   │   │   └── AndroidManifest.xml
│   │   └── test/
│   └── build.gradle
├── build.gradle
├── settings.gradle
├── README.md
└── .gitignore
```

## Requirements

- **Android Studio** 2022.1 or later (or Gradle 7.4.2+)
- **Java Development Kit (JDK)** 11 or later
- **Android SDK** API 34 (or download via Android Studio)
- **Minimum Android Version**: Android 6.0 (API 23)
- **Target Android Version**: Android 14 (API 34)

## Build Instructions

### Option 1: Using Android Studio (Recommended)

1. **Open Android Studio**
2. **Clone the repository**:
   - Click "File" → "New" → "Project from Version Control"
   - Paste: `https://github.com/vijju9019/ColoneyCare.git`
   - Click "Clone"

3. **Wait for Gradle sync** to complete automatically

4. **Connect an Android device** or start an emulator:
   - Go to "Tools" → "Device Manager"
   - Create or start a virtual device
   - Or connect a physical Android phone via USB

5. **Build the APK**:
   - Click "Build" → "Build Bundle(s) / APK(s)" → "Build APK(s)"
   - Wait for the build to complete

6. **Run the app**:
   - Click "Run" → "Run 'app'" (or press Shift+F10)
   - Select your device
   - The app will install and launch automatically

### Option 2: Using Command Line (Gradle)

```bash
# Clone the repository
git clone https://github.com/vijju9019/ColoneyCare.git
cd ColoneyCare

# Build the debug APK
./gradlew assembleDebug

# Build the release APK (requires signing key)
./gradlew assembleRelease

# Install on connected device
./gradlew installDebug

# Run on connected device
./gradlew run
```

### Option 3: Using Gradle Wrapper (Windows)

```cmd
REM Clone the repository
git clone https://github.com/vijju9019/ColoneyCare.git
cd ColoneyCare

REM Build the debug APK
gradlew.bat assembleDebug

REM Install on connected device
gradlew.bat installDebug
```

## Where to Find Your APK

After building, the APK will be located at:

```
app/build/outputs/apk/debug/app-debug.apk    (Debug APK)
app/build/outputs/apk/release/app-release.apk (Release APK - requires signing)
```

## Key Features

✅ **WebView Integration**: Loads the ColoneyCare web app
✅ **JavaScript Support**: Full JavaScript execution enabled
✅ **Back Navigation**: Hardware back button navigates through web pages
✅ **Responsive Design**: Fits all screen sizes
✅ **Network Support**: Handles both HTTP and HTTPS
✅ **Zoom Controls**: Built-in zoom functionality
✅ **Cache Management**: Efficient caching for faster loading

## Configuration

To change the loaded web URL, edit `MainActivity.java`:

```java
private static final String WEB_URL = "https://your-url-here.com";
```

## Permissions

The app requires these permissions (defined in AndroidManifest.xml):

- `INTERNET` - To load web content
- `ACCESS_NETWORK_STATE` - To check network connectivity

## Android Version Support

| Component | Version |
|-----------|----------|
| Min SDK   | 23 (Android 6.0) |
| Target SDK| 34 (Android 14) |
| Compile SDK | 34 |

## Signing for Release

To create a release APK for Google Play Store:

1. **Generate a signing key** (one-time):
   ```bash
   keytool -genkey -v -keystore colonycare.keystore -keyalg RSA -keysize 2048 -validity 10000 -alias colonycare
   ```

2. **Add signing configuration** to `app/build.gradle`:
   ```gradle
   signingConfigs {
       release {
           storeFile file('colonycare.keystore')
           storePassword 'your_password'
           keyAlias 'colonycare'
           keyPassword 'your_password'
       }
   }
   
   buildTypes {
       release {
           signingConfig signingConfigs.release
       }
   }
   ```

3. **Build signed release APK**:
   ```bash
   ./gradlew assembleRelease
   ```

## Troubleshooting

### "Failed to sync Gradle"
- Update Android Studio to the latest version
- Delete `.gradle` folder and `build` folder
- Sync again

### "Web content not loading"
- Check internet connection
- Verify the URL is correct in `MainActivity.java`
- Check that the website is accessible from your network

### "APK installation fails on device"
- Ensure minimum Android 6.0 is installed
- Clear app cache: `adb shell pm clear com.colonycare.app`
- Uninstall previous version first

### "Emulator is slow"
- Use AMD Ryzen or Intel processor with virtualization enabled
- Allocate more RAM to the emulator (default is 1.5GB)
- Use a physical device for testing

## Publishing to Google Play Store

1. Create a Google Play Developer account ($25 one-time fee)
2. Sign the APK with your release key (see "Signing for Release" above)
3. Upload APK in Google Play Console
4. Fill in app details, screenshots, and privacy policy
5. Submit for review

## Development Notes

- **WebView Security**: The app uses `setMixedContentMode(WebSettings.MIXED_CONTENT_ALWAYS_ALLOW)` to support both HTTP and HTTPS content
- **User Agent**: Preserves default user agent for compatibility
- **JavaScript**: Enabled for full web functionality
- **DOM Storage**: Enabled for web app local storage
- **Database**: Enabled for SQLite web storage

## License

This project is open source and available under the MIT License.

## Support

For issues or feature requests, please create an issue in the GitHub repository.

---

**Made with ❤️ for ColoneyCare Community**
