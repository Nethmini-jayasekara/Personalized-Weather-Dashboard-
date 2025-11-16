# Application Architecture & Flow Diagrams

## System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    User Interface (Flutter)                  │
│  ┌────────────┐  ┌────────────┐  ┌──────────────────────┐  │
│  │   Index    │  │ Coordinates│  │   Weather Display    │  │
│  │   Input    │→ │ Calculation│→ │  (Temp/Wind/Code)   │  │
│  └────────────┘  └────────────┘  └──────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│               State Management (StatefulWidget)              │
│  ┌────────────┐  ┌────────────┐  ┌──────────────────────┐  │
│  │  Loading   │  │   Error    │  │   Weather Data       │  │
│  │   State    │  │  Handling  │  │   State Variables    │  │
│  └────────────┘  └────────────┘  └──────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
                            │
            ┌───────────────┴───────────────┐
            ▼                               ▼
┌──────────────────────┐         ┌──────────────────────┐
│   HTTP Package       │         │  SharedPreferences   │
│  (REST API Calls)    │         │  (Local Caching)     │
└──────────────────────┘         └──────────────────────┘
            │                               │
            ▼                               ▼
┌──────────────────────┐         ┌──────────────────────┐
│  Open-Meteo API      │         │   Device Storage     │
│  (Weather Data)      │         │   (Persistent)       │
└──────────────────────┘         └──────────────────────┘
```

---

## Data Flow Diagram

### Online Mode (Internet Available)

```
   User Action
       │
       ▼
[Tap "Fetch Weather"]
       │
       ▼
[Calculate Coordinates]
   (lat, lon from index)
       │
       ▼
[Build Request URL]
       │
       ▼
[HTTP GET Request]───────┐
       │                 │
       ▼                 │ 10s timeout
[Wait for Response]      │
       │                 │
       ▼                 │
[Parse JSON]◄────────────┘
       │
       ▼
[Extract Weather Data]
   (temp, wind, code)
       │
       ▼
[Update UI State]
       │
       ├──► [Display Temperature]
       ├──► [Display Wind Speed]
       ├──► [Display Weather Code]
       ├──► [Display Timestamp]
       └──► [Display Request URL]
       │
       ▼
[Save to Cache]
   (SharedPreferences)
       │
       ▼
   [Done]
```

### Offline Mode (No Internet)

```
   User Action
       │
       ▼
[Tap "Fetch Weather"]
       │
       ▼
[Calculate Coordinates]
       │
       ▼
[HTTP GET Request]
       │
       ▼
  [Timeout/Error]
       │
       ▼
[Error Caught]
       │
       ├──► [Display Error Message]
       │
       ▼
[Load from Cache]
   (SharedPreferences)
       │
       ▼
[Display Cached Data]
       │
       ├──► [Show "(cached)" Tag]
       ├──► [Show Previous Temp]
       ├──► [Show Previous Wind]
       ├──► [Show Previous Code]
       └──► [Show Previous Time]
       │
       ▼
   [Done]
```

---

## State Diagram

```
                    ┌─────────────┐
                    │   Initial   │
                    │   State     │
                    └──────┬──────┘
                           │
                           ▼
                    ┌─────────────┐
                    │    Idle     │◄────────────┐
                    │  (Waiting)  │             │
                    └──────┬──────┘             │
                           │                    │
              [User taps Fetch Weather]         │
                           │                    │
                           ▼                    │
                    ┌─────────────┐             │
                    │   Loading   │             │
                    │  (API Call) │             │
                    └──────┬──────┘             │
                           │                    │
                ┌──────────┴──────────┐         │
                │                     │         │
         [Success]               [Error]        │
                │                     │         │
                ▼                     ▼         │
         ┌─────────────┐      ┌─────────────┐  │
         │   Online    │      │   Offline   │  │
         │   Success   │      │   /Error    │  │
         │  (Fresh)    │      │  (Cached)   │  │
         └──────┬──────┘      └──────┬──────┘  │
                │                     │         │
                └──────────┬──────────┘         │
                           │                    │
                           └────────────────────┘
```

---

## Component Structure

```
MyApp (MaterialApp)
    │
    └─ WeatherDashboard (StatefulWidget)
           │
           └─ _WeatherDashboardState (State)
                  │
                  ├─ State Variables
                  │    ├─ _indexController (TextEditingController)
                  │    ├─ _latitude, _longitude (double?)
                  │    ├─ _temperature, _windSpeed, _weatherCode (double?/int?)
                  │    ├─ _lastUpdated, _requestUrl (String?)
                  │    ├─ _isLoading (bool)
                  │    ├─ _errorMessage (String?)
                  │    └─ _isCached (bool)
                  │
                  ├─ Methods
                  │    ├─ _loadCachedData()
                  │    ├─ _saveCachedData()
                  │    ├─ _calculateCoordinates()
                  │    └─ _fetchWeather()
                  │
                  └─ UI Build
                       ├─ Scaffold
                       │    ├─ AppBar
                       │    └─ SingleChildScrollView
                       │         └─ Column
                       │              ├─ [Index Input Card]
                       │              ├─ [Coordinates Card]
                       │              ├─ [Fetch Button]
                       │              ├─ [Error Card]
                       │              ├─ [Weather Data Card]
                       │              └─ [Request URL Card]
```

---

## Sequence Diagram: Successful Fetch

```
User          UI          State       HTTP       API      Cache
 │            │            │           │         │         │
 │──[Enter]──►│            │           │         │         │
 │   Index    │            │           │         │         │
 │            │            │           │         │         │
 │──[Tap]────►│            │           │         │         │
 │  Fetch     │            │           │         │         │
 │            │            │           │         │         │
 │            │─[Calc]────►│           │         │         │
 │            │ Coords     │           │         │         │
 │            │            │           │         │         │
 │            │◄──[Lat]────┤           │         │         │
 │            │   [Lon]    │           │         │         │
 │            │            │           │         │         │
 │            │            │──[GET]───►│         │         │
 │            │            │  Request  │         │         │
 │            │            │           │         │         │
 │            │            │           │─[Call]─►│         │
 │            │            │           │   API   │         │
 │            │            │           │         │         │
 │            │            │           │◄[JSON]──┤         │
 │            │            │           │ Response│         │
 │            │            │           │         │         │
 │            │            │◄[Data]────┤         │         │
 │            │            │  Weather  │         │         │
 │            │            │           │         │         │
 │            │            │─[Save]────┼─────────┼────────►│
 │            │            │  Cache    │         │         │
 │            │            │           │         │         │
 │            │◄[Update]───┤           │         │         │
 │◄[Display]──┤   UI       │           │         │         │
 │  Weather   │            │           │         │         │
```

---

## Sequence Diagram: Failed Fetch (Offline)

```
User          UI          State       HTTP       Cache
 │            │            │           │          │
 │──[Enable]──│            │           │          │
 │  Airplane  │            │           │          │
 │            │            │           │          │
 │──[Tap]────►│            │           │          │
 │  Fetch     │            │           │          │
 │            │            │           │          │
 │            │─[Calc]────►│           │          │
 │            │ Coords     │           │          │
 │            │            │           │          │
 │            │            │──[GET]───►│          │
 │            │            │  Request  │          │
 │            │            │           │          │
 │            │            │           │─[Timeout]│
 │            │            │           │  Error   │
 │            │            │           │          │
 │            │            │◄[Error]───┤          │
 │            │            │  Caught   │          │
 │            │            │           │          │
 │            │            │─[Load]────┼─────────►│
 │            │            │  Cache    │          │
 │            │            │           │          │
 │            │            │◄[Cached]──┼──────────┤
 │            │            │  Data     │          │
 │            │            │           │          │
 │            │◄[Update]───┤           │          │
 │◄[Display]──┤   UI       │           │          │
 │  Cached +  │  (cached)  │           │          │
 │  Error     │   tag      │           │          │
```

---

## Cache Management Flow

```
┌─────────────────────────────────────────────┐
│           App Lifecycle                     │
├─────────────────────────────────────────────┤
│                                             │
│  [App Start]                                │
│      │                                      │
│      ▼                                      │
│  [initState()]                              │
│      │                                      │
│      ▼                                      │
│  [_loadCachedData()]                        │
│      │                                      │
│      ▼                                      │
│  [Check SharedPreferences]                  │
│      │                                      │
│      ├─[Data Found]──► [Display Cached]    │
│      │                      with tag        │
│      │                                      │
│      └─[No Data]─────► [Show Empty]        │
│                                             │
│                                             │
│  [User Fetches Weather]                     │
│      │                                      │
│      ▼                                      │
│  [API Call Success?]                        │
│      │                                      │
│      ├─[Yes]─► [_saveCachedData()]         │
│      │              │                       │
│      │              ▼                       │
│      │         [Update Storage]             │
│      │                                      │
│      └─[No]──► [Keep Old Cache]            │
│                                             │
└─────────────────────────────────────────────┘
```

---

## Error Handling Flow

```
                  [Error Occurs]
                        │
            ┌───────────┴───────────┐
            │                       │
      [Network Error]        [HTTP Error]
      (timeout/no net)       (status ≠ 200)
            │                       │
            └───────────┬───────────┘
                        │
                        ▼
                [Try-Catch Block]
                        │
                        ▼
              [Set Error Message]
                        │
                        ▼
              [Set _isCached = true]
                        │
                        ▼
              [Keep Existing Data]
                        │
                        ▼
                [Update UI State]
                        │
            ┌───────────┴───────────┐
            │                       │
     [Show Red Card]         [Show Orange Tag]
     (Error Message)          "(cached)"
            │                       │
            └───────────┬───────────┘
                        │
                        ▼
                   [User Sees]
              "Error: [message]"
        "Showing cached data if available"
```

---

## UI Layout Hierarchy

```
Scaffold
├── AppBar
│   └── "Personalized Weather Dashboard"
│
└── SingleChildScrollView
    └── Column (padding: 16)
        │
        ├── Card #1: Student Index
        │   └── TextField
        │       ├── Controller: _indexController
        │       ├── Hint: "e.g., 194174B"
        │       └── Icon: person
        │
        ├── Card #2: Coordinates (if calculated)
        │   ├── "Latitude: X.XX°"
        │   └── "Longitude: Y.YY°"
        │
        ├── ElevatedButton: "Fetch Weather"
        │   ├── Icon: cloud_download (or loading)
        │   └── Disabled when _isLoading = true
        │
        ├── Card #3: Error (if _errorMessage exists)
        │   ├── Color: red.shade50
        │   ├── Icon: error_outline
        │   └── Text: _errorMessage
        │
        ├── Card #4: Weather Data (if _temperature exists)
        │   ├── Header: "Current Weather" + "(cached)" tag
        │   ├── Temperature: "XX.X°C"
        │   ├── Wind Speed: "XX.X km/h"
        │   ├── Weather Code: "XX"
        │   └── Last Updated: "YYYY-MM-DD HH:MM:SS"
        │
        └── Card #5: Request URL (if _requestUrl exists)
            ├── Color: grey.shade100
            ├── Label: "Request URL"
            └── SelectableText: full URL
                (font: 10pt, monospace)
```

---

## Coordinate Calculation Algorithm

```
Input: Student Index (String)
Example: "194174B"

Step 1: Extract Digits
│
├─ Remove non-numeric characters
│  "194174B" → "194174"
│
└─ Result: numericPart = "194174"

Step 2: Parse First Two Digits
│
├─ substring(0, 2) = "19"
│  parseInt("19") = 19
│
└─ Result: firstTwo = 19

Step 3: Parse Next Two Digits
│
├─ substring(2, 4) = "41"
│  parseInt("41") = 41
│
└─ Result: nextTwo = 41

Step 4: Calculate Latitude
│
├─ lat = 5 + (firstTwo / 10.0)
│  lat = 5 + (19 / 10.0)
│  lat = 5 + 1.9
│
└─ Result: latitude = 6.90

Step 5: Calculate Longitude
│
├─ lon = 79 + (nextTwo / 10.0)
│  lon = 79 + (41 / 10.0)
│  lon = 79 + 4.1
│
└─ Result: longitude = 83.10

Output:
├─ Latitude: 6.90°
└─ Longitude: 83.10°
```

---

## JSON Parsing Flow

```
HTTP Response (String)
        │
        ▼
  json.decode()
        │
        ▼
   Map<String, dynamic>
        │
   ┌────┴────┐
   │         │
   ▼         ▼
data['current_weather']
   │
   ▼
Map<String, dynamic>
   │
   ├─► currentWeather['temperature'] → double
   ├─► currentWeather['windspeed']   → double
   └─► currentWeather['weathercode'] → int
        │
        ▼
   Store in State Variables
   ├─ _temperature = ...
   ├─ _windSpeed = ...
   └─ _weatherCode = ...
        │
        ▼
   setState(() {...})
        │
        ▼
    UI Rebuilds
```

---

## Key Design Decisions

### 1. Why StatefulWidget?
```
StatelessWidget (❌)          StatefulWidget (✅)
     │                              │
     ├─ Immutable                   ├─ Mutable state
     ├─ No state changes            ├─ setState() available
     ├─ Build once                  ├─ Rebuild on state change
     └─ Can't handle                └─ Handles user input,
        dynamic data                   API calls, loading
```

### 2. Why SharedPreferences?
```
Alternatives Comparison:

SQLite:
└─ ❌ Overkill for simple key-value storage
└─ ❌ Requires schema definition
└─ ❌ More complex API

File I/O:
└─ ❌ Need to manage file paths
└─ ❌ Manual JSON serialization
└─ ❌ More code required

SharedPreferences:
└─ ✅ Simple key-value API
└─ ✅ Automatic persistence
└─ ✅ Cross-platform
└─ ✅ Perfect for cache
```

### 3. Why Cards?
```
Material Design Benefits:
├─ Visual Hierarchy
├─ Content Grouping
├─ Elevation (depth)
├─ Consistent spacing
├─ Professional look
└─ User familiarity
```

---

## Performance Considerations

```
Optimization Strategies Used:

1. Async Operations
   ├─ HTTP calls don't block UI
   ├─ Cache loading doesn't freeze app
   └─ User can interact during loading

2. Minimal Rebuilds
   ├─ setState() only when needed
   ├─ Scoped state updates
   └─ Efficient widget tree

3. Timeout Handling
   ├─ 10-second max wait
   ├─ Prevents infinite hangs
   └─ Better UX

4. Lazy Loading
   ├─ Cache loaded only on init
   ├─ Data fetched on demand
   └─ No unnecessary operations

5. Error Recovery
   ├─ Cached data fallback
   ├─ No crashes on errors
   └─ Graceful degradation
```

---

**End of Architecture Documentation**
