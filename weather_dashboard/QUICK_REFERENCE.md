# Quick Reference Guide

## Flutter Commands

### Check Flutter Installation
```bash
flutter doctor
```

### Get Dependencies
```bash
cd weather_dashboard
flutter pub get
```

### Run App
```bash
# List available devices
flutter devices

# Run on connected device
flutter run

# Run on specific device
flutter run -d <device-id>

# Run in release mode (faster)
flutter run --release
```

### Build APK (for Android)
```bash
# Debug APK
flutter build apk --debug

# Release APK
flutter build apk --release

# APK location: build/app/outputs/flutter-apk/app-release.apk
```

### Clean Build
```bash
flutter clean
flutter pub get
flutter run
```

---

## Testing Scenarios

### Test 1: Normal Operation (Online)
1. Ensure device has internet connection
2. Open app
3. Verify index is displayed (e.g., 194174B)
4. Check coordinates appear (e.g., Lat: 6.90°, Lon: 83.10°)
5. Tap "Fetch Weather"
6. Verify loading indicator shows
7. Verify weather data appears:
   - Temperature (e.g., 28.5°C)
   - Wind speed (e.g., 12.3 km/h)
   - Weather code (e.g., 3)
   - Timestamp (e.g., 2025-11-06 14:32:45)
8. Scroll down to verify Request URL is visible

### Test 2: Offline Mode
1. First perform Test 1 to cache data
2. Enable Airplane Mode on device
3. Tap "Fetch Weather"
4. Verify error message appears
5. Verify weather data still visible
6. Verify "(cached)" tag is displayed in orange

### Test 3: Invalid Index
1. Enter invalid index (e.g., "12" - only 2 digits)
2. Tap "Fetch Weather"
3. Verify error message about invalid format

### Test 4: Cache Persistence
1. Fetch weather data
2. Close app completely
3. Reopen app
4. Verify cached data is displayed
5. Verify "(cached)" tag is shown

---

## Project Structure

```
weather_dashboard/
├── lib/
│   └── main.dart                 # Main application code
├── android/                      # Android-specific files
├── ios/                          # iOS-specific files
├── pubspec.yaml                  # Dependencies
├── PROJECT_README.md             # Project documentation
├── REPORT_TEMPLATE.md            # Report template
├── VIDEO_DEMO_GUIDE.md           # Video recording guide
├── SUBMISSION_CHECKLIST.md       # Submission checklist
├── VIVA_PREPARATION.md           # Viva Q&A
└── QUICK_REFERENCE.md            # This file
```

---

## Key Files to Modify

### For Your Index
Edit `lib/main.dart` line ~35:
```dart
final TextEditingController _indexController = TextEditingController(text: '194174B');
```
Change `'194174B'` to your actual index.

---

## Dependencies Used

```yaml
dependencies:
  flutter:
    sdk: flutter
  http: ^1.2.0              # For API calls
  shared_preferences: ^2.2.0 # For caching
  intl: ^0.19.0             # For date formatting
  cupertino_icons: ^1.0.8   # For iOS icons
```

---

## Common Issues & Solutions

### Issue: "Pub get failed"
**Solution:**
```bash
flutter clean
flutter pub get
```

### Issue: "No devices found"
**Solution:**
1. Enable USB Debugging on Android device
2. Connect device via USB
3. Run `flutter devices` to verify
4. Or run Android Emulator from Android Studio

### Issue: App crashes on startup
**Solution:**
1. Check console for error messages
2. Run `flutter clean`
3. Rebuild: `flutter run`

### Issue: API call times out
**Solution:**
1. Check internet connection
2. Verify coordinates are valid
3. Try different network (WiFi vs mobile data)
4. Check if Open-Meteo is accessible in your region

### Issue: Cached data not showing
**Solution:**
1. Fetch weather successfully first (to populate cache)
2. Check SharedPreferences is properly saved
3. Restart app to test persistence

---

## Coordinate Calculation Reference

### Formula
```
firstTwo  = int(index[0..1])
nextTwo   = int(index[2..3])
lat = 5  + (firstTwo / 10.0)
lon = 79 + (nextTwo  / 10.0)
```

### Examples
| Index    | First Two | Next Two | Latitude | Longitude |
|----------|-----------|----------|----------|-----------|
| 194174B  | 19        | 41       | 6.90°    | 83.10°    |
| 205538C  | 20        | 55       | 7.00°    | 84.50°    |
| 180265A  | 18        | 02       | 6.80°    | 79.20°    |
| 219987D  | 21        | 99       | 7.10°    | 88.90°    |

---

## API Reference

### Endpoint
```
https://api.open-meteo.com/v1/forecast
```

### Parameters
- `latitude`: Float (5.0 - 15.9)
- `longitude`: Float (79.0 - 89.9)
- `current_weather`: Boolean (true)

### Example Request
```
https://api.open-meteo.com/v1/forecast?latitude=6.9&longitude=83.1&current_weather=true
```

### Example Response
```json
{
  "latitude": 6.9,
  "longitude": 83.1,
  "current_weather": {
    "temperature": 28.5,
    "windspeed": 12.3,
    "weathercode": 3,
    "time": "2025-11-06T14:30"
  }
}
```

### Weather Codes (WMO)
- 0: Clear sky
- 1, 2, 3: Mainly clear, partly cloudy, overcast
- 45, 48: Fog
- 51, 53, 55: Drizzle
- 61, 63, 65: Rain
- 71, 73, 75: Snow
- 95: Thunderstorm

---

## Useful VS Code Extensions

- **Dart** by Dart Code
- **Flutter** by Dart Code
- **Awesome Flutter Snippets** by Nash
- **Pubspec Assist** by Jeroen Meijer

---

## Git Commands (Optional)

```bash
# Initialize repository
git init

# Add all files
git add .

# Commit
git commit -m "Initial commit - Weather Dashboard"

# Create branch
git branch dev

# Switch to branch
git checkout dev

# View status
git status
```

---

## Screen Recording Commands

### Android ADB
```bash
# Check connected devices
adb devices

# Start recording (max 180 seconds)
adb shell screenrecord /sdcard/weather_demo.mp4

# Stop: Press Ctrl+C

# Pull video
adb pull /sdcard/weather_demo.mp4

# Delete from device
adb shell rm /sdcard/weather_demo.mp4
```

---

## Submission File Naming

✅ **Correct:**
- `project_194174B.zip`
- `report_194174B.pdf`
- `video_194174B.mp4`

❌ **Incorrect:**
- `project.zip`
- `my_report.pdf`
- `weather_video.mp4`
- `project_194174b.zip` (lowercase 'b')

---

## File Size Tips

### Reduce Project ZIP Size
1. Delete `build/` folder before zipping
2. Delete `.dart_tool/` folder
3. Delete `android/.gradle/` folder
4. Use compression (ZIP format)

### Reduce Video Size
1. Export at 720p instead of 1080p
2. Use H.264 codec
3. Reduce bitrate if > 50MB
4. Trim unnecessary parts

---

## Keyboard Shortcuts (VS Code)

- `Ctrl + S` - Save file
- `Ctrl + Shift + P` - Command palette
- `F5` - Start debugging
- `Ctrl + C` - Stop terminal process
- `Shift + F5` - Stop debugging
- `Ctrl + K, Ctrl + S` - Keyboard shortcuts reference

---

## Hot Reload vs Hot Restart

### Hot Reload (r)
- Fast (~1 second)
- Preserves app state
- Use for UI changes

### Hot Restart (R)
- Slower (~3-5 seconds)
- Resets app state
- Use for logic changes

---

## Final Pre-Submission Check

```bash
# 1. Clean and rebuild
flutter clean
flutter pub get
flutter run

# 2. Test all features
# - Enter index
# - Fetch weather (online)
# - Enable airplane mode
# - Fetch weather (offline/cached)

# 3. Take screenshots with URL visible

# 4. Record video (≤60 seconds)

# 5. Create ZIP (exclude build folder)

# 6. Create PDF report (≤2 pages)

# 7. Verify file names:
#    - project_[INDEX].zip
#    - report_[INDEX].pdf
#    - video_[INDEX].mp4
```

---

## Contact for Help

**Official Course Channel:**
- [Add instructor/TA contact if available]

**Flutter Documentation:**
- https://flutter.dev/docs

**Open-Meteo API Docs:**
- https://open-meteo.com/en/docs

---

## Emergency Backup

Before submission, backup your project:
1. Copy project folder to USB drive
2. Upload to cloud storage (Google Drive, OneDrive)
3. Keep original on your computer

---

**Good luck! 🚀**
