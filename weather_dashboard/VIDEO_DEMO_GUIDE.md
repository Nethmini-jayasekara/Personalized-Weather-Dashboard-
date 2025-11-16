# Video Demo Guide (≤60 seconds)

## Equipment Needed
- Android device or emulator with the app installed
- Screen recording software (e.g., ADB screenrecord, Android's built-in recorder, or OBS)
- Clear voice or background music (optional)

## Video Script & Timeline

### Segment 1: Introduction (5 seconds)
- **Show:** App home screen with title "Personalized Weather Dashboard"
- **Action:** None, just display the initial screen
- **Narration/Text:** "Weather Dashboard - Student Index: [YOUR_INDEX]"

### Segment 2: Input & Calculate (10 seconds)
- **Show:** Student index input field
- **Action:** 
  - Tap on the index field (should show pre-filled value like "194174B")
  - Or type your actual index
- **Show:** Computed coordinates appear automatically
- **Highlight:** Latitude and Longitude values (e.g., 6.90°, 83.10°)

### Segment 3: Fetch Weather - Online (20 seconds)
- **Action:** Tap "Fetch Weather" button
- **Show:** 
  - Loading indicator briefly
  - Weather data appears:
    - Temperature (e.g., 28.5°C)
    - Wind speed (e.g., 12.3 km/h)
    - Weather code (e.g., 3)
    - Last updated timestamp
- **Important:** Scroll down to show the **Request URL** at the bottom
- **Highlight:** The URL should be clearly visible
- **Narration:** "Fetching live weather data..."

### Segment 4: Enable Airplane Mode (10 seconds)
- **Action:** 
  - Swipe down to show notification panel
  - Enable Airplane Mode (show the icon turning on)
  - Close notification panel
- **Narration:** "Testing offline mode..."

### Segment 5: Fetch Weather - Offline (15 seconds)
- **Action:** Tap "Fetch Weather" button again
- **Show:**
  - Error message appears (e.g., "Error: ... Showing cached data if available")
  - Weather data still visible with **(cached)** tag in orange
  - Previous data remains on screen
- **Highlight:** The orange "(cached)" tag
- **Narration:** "Cached data displayed successfully!"

### Total: ~60 seconds

---

## Video Recording Tips

### Option 1: Android Built-in Screen Recorder
1. Go to Settings → Developer Options → Enable USB Debugging
2. Use built-in screen recorder (swipe down, look for screen record)
3. Start recording before opening the app

### Option 2: ADB Screen Record
```bash
# Connect device via USB
adb devices

# Start recording (max 180 seconds)
adb shell screenrecord /sdcard/weather_demo.mp4

# Stop recording: Press Ctrl+C

# Pull video to computer
adb pull /sdcard/weather_demo.mp4
```

### Option 3: Emulator + Screen Capture
1. Run app in Android Emulator
2. Use OBS Studio or similar to record screen
3. Crop to just the phone screen area

---

## Checklist Before Recording

- [ ] App is installed and working
- [ ] Pre-fill with your actual student index
- [ ] Device has internet connection
- [ ] Airplane mode is currently OFF
- [ ] Clear any notifications for clean recording
- [ ] Close all other apps
- [ ] Full battery or plugged in
- [ ] Screen brightness at 100%
- [ ] Practice the flow 2-3 times before final recording

---

## Checklist During Recording

- [ ] Show app title clearly
- [ ] Display student index in input field
- [ ] Show computed latitude/longitude
- [ ] Tap "Fetch Weather" button
- [ ] Wait for loading and weather data
- [ ] **SCROLL DOWN to show Request URL** (VERY IMPORTANT!)
- [ ] Enable Airplane Mode (show icon)
- [ ] Tap "Fetch Weather" again
- [ ] Show error message
- [ ] Show "(cached)" tag on weather data

---

## Video Editing (Optional)

If your raw recording is > 60 seconds:
1. Use a free video editor (e.g., DaVinci Resolve, Shotcut, OpenShot)
2. Speed up slow parts (1.2x-1.5x speed)
3. Trim any dead time at start/end
4. Add text overlays if helpful:
   - "Online Mode"
   - "Offline Mode - Airplane Mode ON"
   - "Cached Data Displayed"

---

## Export Settings

- **Resolution:** 720p or 1080p
- **Format:** MP4 (H.264)
- **Frame Rate:** 30fps
- **Duration:** ≤60 seconds
- **File Size:** Try to keep under 50MB

---

## File Naming

Save as: `video_[YOUR_INDEX].mp4`

Example: `video_194174B.mp4`

---

## Final Check

Watch your video before submitting and verify:
- [ ] Duration is ≤60 seconds
- [ ] Student index is visible
- [ ] Coordinates are shown
- [ ] **Request URL is clearly visible** (critical!)
- [ ] Temperature, wind speed, weather code are shown
- [ ] Timestamp is visible
- [ ] Airplane mode activation is shown
- [ ] Error message appears
- [ ] "(cached)" tag is visible
- [ ] Video quality is clear and readable
- [ ] No sensitive information visible

---

Good luck with your recording! 🎬
