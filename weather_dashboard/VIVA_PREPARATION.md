# Potential Viva Questions & Answers

*Prepare for a brief explanation session if randomly selected*

---

## 1. Coordinate Derivation

### Q: How did you derive the latitude and longitude from your student index?

**Answer:**
"I extracted the first two digits and the next two digits from my student index. For example, from index 194174B:
- First two digits: 19
- Next two digits: 41
- Latitude = 5 + (19 / 10.0) = 6.90°
- Longitude = 79 + (41 / 10.0) = 83.10°

This formula ensures coordinates fall within Sri Lanka and nearby regions (5°-15.9° N, 79°-89.9° E)."

---

### Q: Why does your formula use division by 10.0 instead of 10?

**Answer:**
"Dividing by 10.0 (a floating-point number) ensures the result is a decimal value rather than an integer. This gives us precise latitude/longitude with decimal places, which is necessary for accurate geographic coordinates."

---

## 2. API Integration

### Q: Which API did you use and why?

**Answer:**
"I used the Open-Meteo API (https://api.open-meteo.com/) because:
1. It doesn't require an API key (easy to use)
2. It's free and open source
3. It provides reliable weather data
4. It returns JSON format which is easy to parse in Flutter
5. It has a simple endpoint structure"

---

### Q: What parameters did you pass to the API?

**Answer:**
"I passed three parameters:
1. `latitude` - Computed from my student index
2. `longitude` - Computed from my student index
3. `current_weather=true` - To get current weather data instead of forecasts

Example URL: `https://api.open-meteo.com/v1/forecast?latitude=6.9&longitude=83.1&current_weather=true`"

---

### Q: How did you parse the JSON response?

**Answer:**
"I used Dart's built-in `json.decode()` function from the `dart:convert` library. The API returns a structure like:
```json
{
  "current_weather": {
    "temperature": 28.5,
    "windspeed": 12.3,
    "weathercode": 3
  }
}
```
I accessed the nested `current_weather` object and extracted the temperature, wind speed, and weather code using keys."

---

## 3. Error Handling & Loading States

### Q: How did you handle network errors?

**Answer:**
"I implemented try-catch blocks around the HTTP request with:
1. A 10-second timeout using `.timeout()` method
2. HTTP status code checking (must be 200)
3. Error messages displayed in a red card on the UI
4. Fallback to cached data when online fetch fails
5. User-friendly error messages instead of technical stack traces"

---

### Q: How did you implement the loading indicator?

**Answer:**
"I used a boolean state variable `_isLoading`. When the user taps 'Fetch Weather':
1. Set `_isLoading = true` and call `setState()`
2. Button shows a CircularProgressIndicator instead of the icon
3. Button is disabled (`onPressed: _isLoading ? null : _fetchWeather`)
4. After API response (success or error), set `_isLoading = false`
This prevents multiple simultaneous requests and gives visual feedback."

---

## 4. Offline Caching

### Q: How did you implement offline caching?

**Answer:**
"I used the `shared_preferences` package, which stores data as key-value pairs on the device. When weather data is successfully fetched:
1. I create a Map with all weather data
2. Convert it to JSON string using `json.encode()`
3. Save it with key 'weather_data'
4. On app start, I load this data using `prefs.getString()`
5. If found, I parse and display it with a '(cached)' tag"

---

### Q: What data do you cache?

**Answer:**
"I cache:
- Temperature
- Wind speed
- Weather code
- Last updated timestamp
- Latitude and longitude
- Request URL

This ensures the user can see meaningful data even when completely offline."

---

### Q: What happens when you fetch weather in offline mode?

**Answer:**
"When offline:
1. The HTTP request fails (times out or throws exception)
2. The error is caught in try-catch block
3. An error message is displayed to the user
4. The `_isCached` flag is set to `true`
5. Previously cached data remains visible with an orange '(cached)' tag
6. User knows they're seeing old data, not live data"

---

## 5. Flutter & Dart Specifics

### Q: What HTTP package did you use?

**Answer:**
"I used the `http` package (version ^1.2.0). It provides simple methods like `http.get()` for making HTTP requests and returns a Response object with status code and body."

---

### Q: What is setState() and why do you use it?

**Answer:**
"`setState()` is a Flutter method that tells the framework to rebuild the widget with updated data. Whenever I change state variables like `_temperature` or `_isLoading`, I wrap the changes in `setState(() {...})` so the UI updates immediately to reflect the new data."

---

### Q: Why did you use StatefulWidget instead of StatelessWidget?

**Answer:**
"I need to manage mutable state (weather data, loading state, error messages) that changes over time based on user actions and API responses. StatefulWidget provides a State object where I can store these variables and update them using `setState()`."

---

## 6. UI/UX Design

### Q: Why did you use Cards in your layout?

**Answer:**
"Cards provide:
1. Visual separation between different sections (index, coordinates, weather data)
2. Material Design elevation/shadow for depth
3. Consistent padding and styling
4. Better readability and organization
5. Professional appearance"

---

### Q: How did you make the Request URL visible and readable?

**Answer:**
"I displayed it in a Card at the bottom with:
1. Small font size (10pt) to fit the long URL
2. Monospace font family for better readability of URLs
3. SelectableText widget so users can copy it
4. Grey background to distinguish it from other sections
5. Clear label 'Request URL' above it"

---

## 7. Testing & Validation

### Q: How did you test offline functionality?

**Answer:**
"I tested by:
1. First fetching weather data successfully (to populate cache)
2. Enabling Airplane Mode on my device
3. Tapping 'Fetch Weather' again
4. Verifying error message appeared
5. Confirming cached data was still displayed
6. Checking the '(cached)' tag was visible
7. Disabling Airplane Mode and fetching again to verify online mode works"

---

### Q: What edge cases did you consider?

**Answer:**
"I handled:
1. Invalid index format (less than 4 digits)
2. Network timeout (10-second limit)
3. HTTP errors (non-200 status codes)
4. No internet connection
5. App first launch with no cached data
6. API response parsing errors
7. JSON structure changes (though unlikely)"

---

## 8. Code Quality & Best Practices

### Q: Did you follow any design patterns?

**Answer:**
"Yes, I followed:
1. **Separation of concerns** - UI code separate from business logic
2. **Single Responsibility** - Each method has one clear purpose
3. **Async/Await** - For asynchronous operations (API calls, cache)
4. **Error handling** - Try-catch blocks around risky operations
5. **State management** - Using StatefulWidget and setState properly"

---

### Q: What would you improve if you had more time?

**Answer:**
"I would:
1. Decode weather codes to human-readable descriptions (e.g., 3 = 'Overcast')
2. Add icons for different weather conditions
3. Implement a refresh button with pull-to-refresh
4. Show weather history/trends
5. Add unit tests for coordinate calculation
6. Implement better error categorization (network, server, parsing)
7. Add animations for loading and data updates
8. Support multiple indexes for comparison"

---

## 9. Wireless Communication Concepts

### Q: How does this relate to wireless communication?

**Answer:**
"This app demonstrates:
1. **REST API communication** - HTTP requests over mobile networks
2. **Mobile data usage** - Efficient API calls to minimize data
3. **Offline-first architecture** - Works without connectivity
4. **Timeout handling** - Important for unreliable mobile networks
5. **Error recovery** - Graceful degradation when network fails
These are key concepts in mobile wireless communication."

---

### Q: Why is caching important in mobile apps?

**Answer:**
"Caching is crucial because:
1. Mobile networks can be unreliable (tunnels, poor coverage)
2. Users may have limited data plans
3. Reduces API calls and server load
4. Improves app responsiveness (instant data display)
5. Better user experience in offline scenarios
6. Reduces battery consumption (fewer network operations)"

---

## 10. General Implementation

### Q: Walk me through what happens when user taps "Fetch Weather"

**Answer:**
"Step by step:
1. `_fetchWeather()` method is called
2. Coordinates are calculated from the index
3. `_isLoading` is set to `true`, showing loading indicator
4. Request URL is constructed with lat/lon parameters
5. HTTP GET request is made to Open-Meteo API
6. Wait for response (with 10-second timeout)
7. If successful (200 status):
   - Parse JSON response
   - Extract temperature, wind speed, weather code
   - Get current timestamp
   - Update state variables
   - Save to cache
8. If error:
   - Display error message
   - Keep cached data visible
   - Set `_isCached` flag to `true`
9. Set `_isLoading` to `false`
10. UI rebuilds with new data"

---

### Q: Why did you pre-fill the index field?

**Answer:**
"Pre-filling improves user experience:
1. Provides an example format (users understand the expected input)
2. Saves time during testing and demos
3. Users can modify it instead of typing from scratch
4. Reduces input errors
5. Makes the app immediately functional for demo purposes"

---

## 12. Technical Choices

### Q: Why Flutter instead of native Android?

**Answer:**
"Flutter was specified in the assignment, but advantages include:
1. Cross-platform (Android, iOS, Web)
2. Hot reload for faster development
3. Rich widget library (Material Design)
4. Single codebase for all platforms
5. Good performance for UI apps
6. Growing community and package ecosystem"

---

### Q: What is the intl package used for?

**Answer:**
"The `intl` package provides internationalization and localization support. I specifically used `DateFormat` class to format the last updated timestamp in a readable format: 'yyyy-MM-dd HH:mm:ss' (e.g., 2025-11-06 14:32:45)."

---

## Tips for Viva

1. **Be confident but honest** - If you don't know something, say "I'm not sure, but I think..."
2. **Relate to the assignment** - Connect answers back to the requirements
3. **Show your code if needed** - Be ready to point to specific functions
4. **Explain trade-offs** - Mention why you chose one approach over another
5. **Demonstrate** - Have the app running to show features live
6. **Be concise** - Answer directly, then elaborate if asked
7. **Use technical terms correctly** - REST, HTTP, JSON, async, state management
8. **Show problem-solving** - Explain challenges you faced and how you solved them

---

**Remember:** You built this app yourself, so you understand it. Relax and explain what you did! 😊
