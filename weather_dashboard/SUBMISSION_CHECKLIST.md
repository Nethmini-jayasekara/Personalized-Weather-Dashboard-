# Submission Checklist - IN 3510 Final Assignment

**Student Index:** _______________  
**Submission Date:** _______________

---

## 📦 Deliverable 1: Project ZIP File

### File Requirements
- [ ] Filename: `project_[YOUR_INDEX].zip`
  - Example: `project_194174B.zip`
- [ ] Contains complete Flutter project folder
- [ ] Size: Reasonable (exclude build folders if too large)

### What to Include in ZIP
- [ ] `lib/` folder with `main.dart`
- [ ] `pubspec.yaml` with all dependencies
- [ ] `android/` folder
- [ ] `ios/` folder (optional but good to include)
- [ ] `README.md` or `PROJECT_README.md`
- [ ] Any other configuration files

### What to EXCLUDE (to reduce size)
- [ ] `.dart_tool/` folder
- [ ] `build/` folder
- [ ] `.idea/` folder
- [ ] `.gradle/` folder (inside android/)
- [ ] `node_modules/` (if any)
- [ ] Large `.iml` files (optional)

### Create ZIP Command
**Windows PowerShell:**
```powershell
cd "d:\projects\wireless\Personalized-Weather-Dashboard-"
Compress-Archive -Path weather_dashboard -DestinationPath "project_[YOUR_INDEX].zip"
```

**Or manually:**
1. Right-click on `weather_dashboard` folder
2. Send to → Compressed (zipped) folder
3. Rename to `project_[YOUR_INDEX].zip`

---

## 📄 Deliverable 2: Report PDF

### File Requirements
- [ ] Filename: `report_[YOUR_INDEX].pdf`
  - Example: `report_194174B.pdf`
- [ ] Maximum length: 2 pages
- [ ] Format: PDF (convert from Word/Google Docs)

### Content Checklist
- [ ] **Header:** Student index, name, course code
- [ ] **Section 1:** Index, formula explanation, calculated coordinates
- [ ] **Section 2:** Screenshot(s) with weather data
  - [ ] Request URL is **clearly visible** in screenshot
  - [ ] Temperature, wind speed, weather code shown
  - [ ] Timestamp visible
- [ ] **Section 3:** Screenshot of offline/cached mode
  - [ ] Error message visible
  - [ ] "(cached)" tag visible
- [ ] **Section 4:** 3-5 sentence reflection
  - [ ] What you learned
  - [ ] Challenges faced
  - [ ] How you tested offline mode
  - [ ] Future improvements (optional)

### Tips for Screenshots
- Use **Snipping Tool** (Windows) or built-in Android screenshot
- Ensure text is readable (high quality)
- Highlight or circle the Request URL if needed
- Crop unnecessary parts (status bar with personal info)

---

## 🎥 Deliverable 3: Video Demo

### File Requirements
- [ ] Filename: `video_[YOUR_INDEX].mp4`
  - Example: `video_194174B.mp4`
- [ ] Duration: **≤60 seconds** (strictly enforced!)
- [ ] Format: MP4 (H.264 codec recommended)
- [ ] Resolution: 720p or higher

### Content Checklist - Must Show
- [ ] App opening with title visible
- [ ] Student index in input field
- [ ] Computed latitude and longitude displayed
- [ ] Tap "Fetch Weather" button
- [ ] Loading indicator (brief)
- [ ] Weather data appears:
  - [ ] Temperature (°C)
  - [ ] Wind speed (km/h)
  - [ ] Weather code (number)
  - [ ] Last updated timestamp
- [ ] **Request URL scrolled into view** (CRITICAL!)
- [ ] Enable Airplane Mode (show toggle)
- [ ] Tap "Fetch Weather" again
- [ ] Error message displayed
- [ ] Cached data visible with **(cached)** tag

### Video Quality Checklist
- [ ] All text is readable (not blurry)
- [ ] Duration is ≤60 seconds (check actual file!)
- [ ] Audio (if any) is clear or muted
- [ ] No background distractions
- [ ] No personal/sensitive information visible
- [ ] File size is reasonable (<100MB)

---

## 🔍 Pre-Submission Verification

### Test Your App One More Time
- [ ] Run `flutter pub get` to ensure all dependencies
- [ ] Test on fresh install (or clean build)
- [ ] Verify coordinates calculation for YOUR index
- [ ] Test online fetch → should work
- [ ] Test offline mode → should show cache
- [ ] Verify Request URL is displayed at bottom

### Code Quality Check
- [ ] No compilation errors
- [ ] No runtime crashes
- [ ] Clean code (remove debug prints if any)
- [ ] Comments in critical sections (optional but good)

### Documentation Check
- [ ] README explains how to run the app
- [ ] Report has all required sections
- [ ] Video shows all required features
- [ ] All files are named correctly

---

## 📊 Marking Rubric Self-Check

| Criteria | Points | Self-Check |
|----------|--------|------------|
| **Correct index→coords & shown in UI** | 15 | ☐ Yes ☐ No |
| - Index input field works | | ☐ |
| - Coordinates calculated correctly | | ☐ |
| - Lat/Lon displayed (2 decimals) | | ☐ |
| | | |
| **Working API call & JSON parsing** | 25 | ☐ Yes ☐ No |
| - API call succeeds | | ☐ |
| - Temperature parsed & shown | | ☐ |
| - Wind speed parsed & shown | | ☐ |
| - Weather code parsed & shown | | ☐ |
| - Request URL displayed | | ☐ |
| | | |
| **Loading, error handling, offline cache** | 25 | ☐ Yes ☐ No |
| - Loading indicator shows | | ☐ |
| - Error message on failure | | ☐ |
| - Cached data persists | | ☐ |
| - "(cached)" tag when offline | | ☐ |
| | | |
| **Clean UI** | 15 | ☐ Yes ☐ No |
| - Labels are clear | | ☐ |
| - Layout is organized | | ☐ |
| - Readable fonts/colors | | ☐ |
| - Professional appearance | | ☐ |
| | | |
| **Report** | 10 | ☐ Yes ☐ No |
| - Clear and well-structured | | ☐ |
| - Screenshots included | | ☐ |
| - Request URL visible | | ☐ |
| - Reflection included (3-5 lines) | | ☐ |
| | | |
| **Video demo** | 10 | ☐ Yes ☐ No |
| - ≤60 seconds | | ☐ |
| - Shows online fetch | | ☐ |
| - Shows offline/cached mode | | ☐ |
| - All features visible | | ☐ |
| | | |
| **TOTAL** | **100** | **_____/100** |

---

## 📤 Submission Method

*[Fill in based on your course requirements]*

- **Platform:** ☐ LMS ☐ Email ☐ Google Drive ☐ Other: _________
- **Deadline:** ___________________
- **Submission Format:** ☐ Separate files ☐ Single ZIP with all three ☐ Other

### Final Upload Checklist
- [ ] `project_[INDEX].zip` uploaded
- [ ] `report_[INDEX].pdf` uploaded
- [ ] `video_[INDEX].mp4` uploaded
- [ ] File names are correct (double-check!)
- [ ] Submission confirmation received

---

## ⚠️ Common Mistakes to Avoid

- [ ] ❌ Forgetting to show Request URL in video
- [ ] ❌ Video longer than 60 seconds
- [ ] ❌ Wrong file naming (typos in index)
- [ ] ❌ Including `build/` folder in ZIP (makes it huge)
- [ ] ❌ Screenshots with personal information visible
- [ ] ❌ Report longer than 2 pages
- [ ] ❌ Not testing offline mode before recording
- [ ] ❌ Blurry screenshots where URL isn't readable
- [ ] ❌ Submitting without testing the ZIP file

---

## 🎯 Final Checklist

- [ ] All three files created and named correctly
- [ ] Tested ZIP extraction and app runs
- [ ] PDF is exactly 2 pages or less
- [ ] Video is exactly 60 seconds or less
- [ ] Request URL visible in BOTH report and video
- [ ] Reflection is 3-5 sentences
- [ ] All features demonstrated
- [ ] Ready for potential viva questions

---

## 📞 Emergency Contacts

*[Add if provided by instructor]*

- **Instructor:** _________________
- **Email:** _________________
- **Office Hours:** _________________

---

**Good luck with your submission! 🚀**

**Signature:** _________________ **Date:** _________________
