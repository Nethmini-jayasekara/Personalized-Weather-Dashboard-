# Personalized Weather Dashboard

## Project Overview
This Flutter application is a personalized weather dashboard that derives geographic coordinates from a student index number and fetches real-time weather data from the Open-Meteo API.

## Features Implemented

### 1. Student Index Input
- Text field for entering student index (pre-filled with example: 194174B)
- Validates and processes the index to extract numeric digits

### 2. Coordinate Derivation
The app automatically calculates latitude and longitude using the formula:
```
firstTwo  = int(index[0..1])     // e.g., 19
nextTwo   = int(index[2..3])     // e.g., 41
lat = 5  + (firstTwo / 10.0)     // Range: 5.0 to 15.9
lon = 79 + (nextTwo  / 10.0)     // Range: 79.0 to 89.9
```

### 3. Weather Data Fetching
- **Fetch Weather** button triggers API call to Open-Meteo
- Displays:
  - Temperature (°C)
  - Wind speed (km/h)
  - Weather code (raw number)
  - Last updated timestamp

### 4. Request URL Display
- Shows the complete API request URL in a readable format
- URL format: `https://api.open-meteo.com/v1/forecast?latitude=LAT&longitude=LON&current_weather=true`

### 5. Loading & Error Handling
- Loading indicator during API fetch
- Friendly error messages when network fails
- Timeout handling (10 seconds)

### 6. Offline Cache
- Uses `shared_preferences` to cache last successful weather data
- Displays **(cached)** tag when showing offline data
- Data persists across app restarts

## Technical Stack

### Dependencies
- **flutter**: UI framework
- **http ^1.2.0**: REST API calls
- **shared_preferences ^2.2.0**: Local data caching
- **intl ^0.19.0**: Date/time formatting

### API Used
- **Open-Meteo API**: https://api.open-meteo.com/v1/forecast
  - No API key required
  - Parameters: `latitude`, `longitude`, `current_weather=true`

## How to Run

### Prerequisites
- Flutter SDK (3.8.1 or higher)
- Android Studio or VS Code with Flutter extension
- Android device/emulator or other platform

### Installation Steps

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd weather_dashboard
   ```

2. **Install dependencies**
   ```bash
   flutter pub get
   ```

3. **Run the app**
   ```bash
   flutter run
   ```

## Testing the App

### Online Mode Test
1. Enter your student index (e.g., 194174B)
2. Observe computed latitude and longitude
3. Tap **Fetch Weather**
4. Verify weather data appears with current timestamp
5. Check request URL is displayed at the bottom

### Offline Mode Test
1. Fetch weather data once (to cache it)
2. Enable Airplane Mode on device
3. Tap **Fetch Weather** again
4. Verify error message appears
5. Verify cached data is still displayed with **(cached)** tag

## Code Structure

```
lib/
└── main.dart
    ├── MyApp (Root widget)
    ├── WeatherDashboard (Main screen)
    └── _WeatherDashboardState
        ├── _calculateCoordinates()
        ├── _fetchWeather()
        ├── _loadCachedData()
        └── _saveCachedData()
```

## Example Calculations

### For Index: 194174B
- First two digits: **19**
- Next two digits: **41**
- Latitude: 5 + (19 / 10.0) = **6.90°**
- Longitude: 79 + (41 / 10.0) = **83.10°**

### For Index: 205538C
- First two digits: **20**
- Next two digits: **55**
- Latitude: 5 + (20 / 10.0) = **7.00°**
- Longitude: 79 + (55 / 10.0) = **84.50°**

## Deliverables Checklist

- [x] **project_<index>.zip** - Full Flutter project
- [ ] **report_<index>.pdf** - 2-page report with:
  - Student index, formula, and coordinates
  - Screenshots showing request URL
  - 3-5 sentence reflection
- [ ] **video_<index>.mp4** - 60-second demo showing:
  - Index input → Fetch → live result
  - Airplane mode → error → cached state

## Marking Criteria Coverage

| Area | Points | Status |
|------|--------|--------|
| Correct index→coords & shown in UI | 15 | ✅ Implemented |
| Working API call & JSON parsing | 25 | ✅ Implemented |
| Loading, error handling, offline cache | 25 | ✅ Implemented |
| Clean UI (labels, layout, readability) | 15 | ✅ Implemented |
| Report (clear + screenshots + URL) | 10 | ⏳ To be created |
| Video demo (≤60s, shows online + cached) | 10 | ⏳ To be created |

**Total: 100 points**

## Known Issues & Limitations

- Weather code is displayed as raw number (0-99 WMO code)
- Network timeout set to 10 seconds
- Requires at least 4 digits in student index

## License
University of Moratuwa - Academic Project

## Author
Student Index: [YOUR_INDEX_HERE]
Date: November 2025
