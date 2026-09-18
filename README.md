# Smart India Hackathon Workshop

## Date: 18/09/2026

## Register Number: 212225040156

## Name: Jijo H Jebas

## Problem Title

**SIH 1710: Enhancing Navigation for Railway Station Facilities and Locations**

## Problem Description

Railway stations contain many important facilities such as platforms, ticket counters, waiting halls, restrooms, food courts, lifts, foot-over bridges and exits. In large and crowded stations, passengers may have difficulty finding these locations within a limited amount of time.

The problem becomes more challenging for elderly passengers, wheelchair users, visually impaired passengers and people visiting an unfamiliar railway station.

The proposed solution provides a simple indoor navigation system that allows passengers to identify their current location, select a destination and receive an appropriate route. Instead of depending completely on GPS, the system uses QR-based location identification at important points inside the station.

The system also provides accessibility-aware routes, allowing passengers to avoid stairs or blocked paths and use facilities such as lifts and ramps.

## Idea

### **RailWayFind – Scan, Select and Navigate**

RailWayFind is a lightweight web-based indoor navigation system designed specifically for railway stations.

The passenger does not need to install a large application. QR codes placed at station entrances, platforms, corridors and important facilities act as location anchors.

When a passenger scans a QR code, the system identifies the approximate station location associated with that QR code. The passenger then selects a destination such as a platform, restroom, ticket counter, food court or exit.

The routing engine calculates a suitable path using a station graph containing locations and connecting paths.

The system also provides different navigation modes:

* **Normal Route** – suitable for general passengers.
* **Accessible Route** – avoids stairs and uses lifts or ramps.
* **Elderly Route** – prioritizes simpler paths and fewer difficult transitions.
* **Voice Route** – provides spoken navigation instructions.

The system can also mark temporary obstacles such as closed corridors, lifts or staircases so that future routes avoid them.

## Key Features

### 1. QR-Based Indoor Positioning

QR codes are placed at important locations inside the railway station.

Example:

```text
Passenger
    |
    v
Scan QR Code
    |
    v
Current Location Identified
    |
    v
Select Destination
```

This avoids depending entirely on GPS, which may not provide accurate indoor positioning.

### 2. Facility Search

Passengers can search for:

* Railway Platforms
* Ticket Counters
* Restrooms
* Waiting Halls
* Food Courts
* Drinking Water
* Lifts
* Ramps
* Foot-Over Bridges
* Station Exits

### 3. Accessibility-Aware Navigation

The passenger can select an accessibility requirement before starting navigation.

```text
             Destination
                  |
        +---------+---------+
        |                   |
     Normal              Accessible
        |                   |
      Stairs                Lift
        |                   |
        +---------+---------+
                  |
             Destination
```

For an accessibility route, the system avoids nodes marked as stairs and prioritizes accessible paths.

### 4. Route Status

Administrators can temporarily change the status of station paths.

Example:

```text
Corridor A
Status: CLOSED

        ↓

Routing Engine

        ↓

Alternative Route
```

This allows the navigation system to avoid known temporary obstacles.

### 5. Step-by-Step Directions

Instead of showing only a destination marker, the system provides simple instructions.

Example:

```text
📍 Starting Point

        ↓

Walk straight for 40 metres

        ↓

Turn right at the waiting hall

        ↓

Take Lift A

        ↓

Walk towards Platform 4

        ↓

🎯 Platform 4
```

### 6. Voice Navigation

The application can provide spoken instructions using the browser's built-in text-to-speech capability.

Example:

> "Walk straight for 30 metres and turn left."

This can assist passengers who have difficulty continuously reading the screen.

### 7. Kiosk Mode

The same web application can be displayed on touchscreen tablets installed at important station locations.

Passengers can select their destination without requiring their own phone.

---

# Proposed Solution / Architecture Diagram

```text
                    +-------------------------+
                    |     STATION ADMIN       |
                    |       PORTAL            |
                    +------------+------------+
                                 |
                    Update facilities,
                    routes & obstacles
                                 |
                                 v
                    +-------------------------+
                    |    CENTRAL DATABASE     |
                    |                         |
                    | • Station Locations     |
                    | • Facilities            |
                    | • QR Locations          |
                    | • Routes                |
                    | • Accessibility Data    |
                    | • Temporary Closures    |
                    +------------+------------+
                                 |
                                 v
                    +-------------------------+
                    |      BACKEND API         |
                    |                         |
                    | • Location Service       |
                    | • Search Service         |
                    | • Route Service          |
                    | • Accessibility Filter  |
                    +------------+------------+
                                 |
                                 v
                    +-------------------------+
                    |     ROUTING ENGINE       |
                    |                         |
                    | Graph + Shortest Path   |
                    | Accessibility Rules     |
                    +------------+------------+
                                 |
              +------------------+------------------+
              |                                     |
              v                                     v
    +---------------------+              +---------------------+
    |   PASSENGER WEB APP |              |    STATION KIOSK    |
    |                     |              |                     |
    | • QR Scanner        |              | • Touch Interface   |
    | • Search Facility   |              | • Station Map       |
    | • Route Display     |              | • Destination Search|
    | • Voice Guidance   |              | • Route Display     |
    +----------+----------+              +----------+----------+
               |                                    |
               v                                    v
        +--------------+                    +--------------+
        | QR LOCATIONS |                    | TOUCH SCREEN |
        | AT STATION   |                    |   KIOSK      |
        +--------------+                    +--------------+
```

## Navigation Flow

```text
                    START
                      |
                      v
              Scan QR / Select
              Kiosk Location
                      |
                      v
             Current Location
                Identified
                      |
                      v
             Search Destination
                      |
                      v
          Select Navigation Mode
                      |
          +-----------+-----------+
          |           |           |
        Normal     Accessible    Voice
          |           |           |
          +-----------+-----------+
                      |
                      v
               Route Engine
                      |
                      v
              Check Obstacles
                      |
                      v
              Calculate Route
                      |
                      v
             Display Directions
                      |
                      v
              Voice Guidance
                      |
                      v
                     END
```

# Use Cases

## Passenger Use Case

A passenger enters an unfamiliar railway station and needs to reach a particular platform.

Instead of asking multiple people for directions, the passenger scans the nearest RailWayFind QR code.

The system identifies the passenger's starting location and displays a list of nearby destinations.

The passenger selects **Platform 4**.

The application calculates the route and displays step-by-step directions.

If the passenger selects **Accessible Mode**, the routing engine avoids stairs and selects a path containing lifts or ramps.

If a corridor is temporarily closed, the system automatically avoids that route and provides an alternative path.

## Example Use Case

```text
Passenger enters station
          |
          v
     Scan QR Code
          |
          v
   Location detected
          |
          v
   Select "Platform 4"
          |
          v
   Select "Normal Route"
          |
          v
    Calculate Route
          |
          v
   Display Station Map
          |
          v
   Step-by-Step Guide
          |
          v
      Platform 4
```

## Accessibility Use Case

```text
Passenger
    |
    v
Scan QR
    |
    v
Select Destination
    |
    v
Select "Accessible"
    |
    v
Remove stair nodes
    |
    v
Prioritize lift/ramp nodes
    |
    v
Calculate accessible route
    |
    v
Display + Voice Guidance
```

# Use Case Diagram

```text
                         +---------------------------+
                         |      RAILWAY NAVIGATION   |
                         |          SYSTEM           |
                         |                           |
Passenger -------------->| Scan QR Code              |
                         |                           |
Passenger -------------->| Search Facility          |
                         |                           |
Passenger -------------->| Select Destination       |
                         |                           |
Passenger -------------->| Select Navigation Mode   |
                         |                           |
Passenger -------------->| View Route               |
                         |                           |
Passenger -------------->| Receive Voice Guidance   |
                         |                           |
Passenger -------------->| Report Blocked Facility  |
                         |                           |
                         +---------------------------+

Admin ------------------>| Manage Station Locations |
                         |                           |
Admin ------------------>| Update Facilities        |
                         |                           |
Admin ------------------>| Block / Open Routes      |
                         |                           |
Admin ------------------>| Manage QR Locations      |
                         +---------------------------+
```

# Technology Stack

## Frontend

* HTML5
* CSS3
* JavaScript
* React.js *(optional for advanced version)*

## Backend

* Python
* Flask

## Database

* SQLite for prototype
* PostgreSQL for large-scale deployment

## Navigation

* Graph-based routing
* Dijkstra / A* algorithm

## Location Identification

* QR Codes

## Accessibility

* Text-to-Speech Web API
* Accessibility-aware route filtering

## Deployment

* GitHub
* Render / similar cloud hosting platform

# System Modules

### 1. Passenger Module

Allows passengers to:

* Scan QR codes
* Search facilities
* Select destinations
* Select accessibility mode
* View routes
* Receive voice instructions

### 2. Navigation Module

Responsible for:

* Creating station paths
* Calculating shortest routes
* Avoiding blocked locations
* Generating step-by-step instructions

### 3. Accessibility Module

Maintains information about:

* Lifts
* Ramps
* Stairs
* Accessible restrooms
* Accessible platforms

It modifies the route according to the selected passenger requirement.

### 4. Admin Module

Administrators can:

* Add facilities
* Update locations
* Add QR codes
* Close routes
* Reopen routes
* Update station information

### 5. Kiosk Module

A touchscreen interface provides the same navigation service for passengers who do not have smartphones or prefer using a station kiosk.

# Database Design

## Locations Table

| Field         | Description                     |
| ------------- | ------------------------------- |
| location_id   | Unique location ID              |
| name          | Location name                   |
| type          | Platform / Lift / Restroom etc. |
| qr_code       | Associated QR identifier        |
| accessibility | Accessibility status            |

## Routes Table

| Field         | Description             |
| ------------- | ----------------------- |
| route_id      | Unique route ID         |
| from_location | Starting node           |
| to_location   | Destination node        |
| distance      | Approximate distance    |
| accessible    | Accessible route status |
| status        | Open / Closed           |

## Example Data

| Location       | Type      | Accessible |
| -------------- | --------- | ---------- |
| Main Entrance  | Entrance  | Yes        |
| Ticket Counter | Facility  | Yes        |
| Platform 1     | Platform  | Yes        |
| Platform 2     | Platform  | Yes        |
| Staircase A    | Staircase | No         |
| Lift A         | Lift      | Yes        |
| Restroom       | Facility  | Yes        |
| Food Court     | Facility  | Yes        |

# Routing Logic

The railway station is represented as a graph.

```text
                 Ticket Counter
                       |
                     30m
                       |
                       v
                    Lift A
                   /     \
                40m       50m
                 /         \
                v           v
          Platform 1     Platform 2
```

Each important station location becomes a **node**.

The path between two locations becomes an **edge**.

The routing algorithm calculates the most suitable path.

For accessible navigation:

```text
IF route contains staircase
        |
        v
    Reject route
        |
        v
Check lift / ramp route
        |
        v
Calculate accessible path
```

# Advantages

* No large application download required
* QR-based indoor positioning
* Simple and low-cost implementation
* Supports accessibility requirements
* Provides alternative routes
* Can work on smartphones and kiosks
* Easy to update station information
* Voice guidance can assist visually impaired passengers
* Same web application can be deployed across multiple devices

# Future Scope

The prototype can later be expanded with:

* Real railway station maps
* Live train information
* Crowd-density information
* BLE-based location assistance
* Computer vision for facility recognition
* Multilingual voice guidance
* Offline navigation
* Emergency evacuation routes
* Integration with railway information systems
* Advanced 3D station visualization

# Expected Outcome

RailWayFind aims to provide passengers with a simple and accessible way to navigate complex railway stations.

By combining QR-based location identification, graph-based routing, accessibility preferences, voice guidance and an administrator-controlled station database, the system can reduce confusion and help passengers reach their destinations more efficiently.

# Project Status

**Prototype / Development Phase**

The initial prototype focuses on:

* QR-based location selection
* Station facility search
* Route calculation
* Accessibility-aware routing
* Interactive station map
* Voice instructions
* Admin route updates
* Kiosk interface
