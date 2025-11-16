# Personalized Weather Dashboard - Report Template

**Student Index:** [YOUR_INDEX_HERE]  
**Name:** [YOUR_NAME]  
**Course:** IN 3510 Wireless Communication & Mobile Networks  
**Date:** November 6, 2025

---

## 1. Coordinate Derivation

### Student Index
My student index is: **[YOUR_INDEX]** (e.g., 194174B)

### Formula Used
```
firstTwo  = int(index[0..1])
nextTwo   = int(index[2..3])
lat = 5  + (firstTwo / 10.0)
lon = 79 + (nextTwo  / 10.0)
```

### Calculated Coordinates
- **First two digits:** [XX]
- **Next two digits:** [YY]
- **Latitude:** 5 + ([XX] / 10.0) = **[XX.X]°**
- **Longitude:** 79 + ([YY] / 10.0) = **[YY.Y]°**

---

## 2. Screenshots

### Screenshot 1: Normal Operation (Online)
*[Insert screenshot showing:]*
- Student index input field
- Computed coordinates
- Fetch Weather button
- Weather data (temperature, wind speed, weather code)
- Last updated time
- **Request URL visible at bottom**

**Request URL:**
```
https://api.open-meteo.com/v1/forecast?latitude=[LAT]&longitude=[LON]&current_weather=true
```

### Screenshot 2: Offline/Cached Mode
*[Insert screenshot showing:]*
- Error message displayed
- **(cached)** tag visible on weather data
- Previous weather information still displayed

---

## 3. Technical Implementation

### Dependencies Used
- **http**: REST API communication
- **shared_preferences**: Local data caching
- **intl**: Date/time formatting

### API Endpoint
Open-Meteo API: `https://api.open-meteo.com/v1/forecast`
- No API key required
- Parameters: latitude, longitude, current_weather=true

---

## 4. Reflection (3-5 sentences)

[Write your reflection here. Consider including:]
- What you learned about REST APIs and Flutter development
- Challenges faced during implementation (e.g., coordinate calculation, caching, error handling)
- How you tested the offline functionality
- What you would improve if given more time

**Example:**
*"This project taught me how to effectively integrate REST APIs in Flutter applications and implement offline-first architecture using shared_preferences. The most challenging aspect was handling error states gracefully while maintaining cached data visibility. I learned the importance of timeout handling and user feedback during network operations. Testing the offline functionality by toggling airplane mode helped me understand real-world app behavior. If given more time, I would add a weather code decoder to show human-readable weather conditions and implement location-based automatic index detection."*

---

## 5. Features Checklist

- [x] Text input for student index
- [x] Automatic coordinate calculation from index
- [x] Display computed latitude/longitude (2 decimals)
- [x] "Fetch Weather" button with API call
- [x] Display temperature (°C)
- [x] Display wind speed (km/h)
- [x] Display weather code
- [x] Display last updated time
- [x] Show request URL on screen
- [x] Loading indicator during fetch
- [x] Error handling with friendly messages
- [x] Offline cache using shared_preferences
- [x] "(cached)" tag when showing offline data

---

## 6. Testing Evidence

### Online Test Results
- **Latitude:** [X.XX]°
- **Longitude:** [Y.YY]°
- **Temperature:** [ZZ.Z]°C
- **Wind Speed:** [WW.W] km/h
- **Weather Code:** [CC]
- **Timestamp:** 2025-11-06 [HH:MM:SS]

### Offline Test Results
- Airplane mode activated: ✓
- Error message displayed: ✓
- Cached data visible: ✓
- "(cached)" tag shown: ✓

---

**End of Report**
