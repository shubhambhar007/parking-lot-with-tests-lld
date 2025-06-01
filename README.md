# Parking Lot Management System

A simple Python solution to manage a multi-floor parking lot for 2-wheelers and 4-wheelers.  
Supports parking, removal, free-spot queries and vehicle lookup by number or ticket.

## Features

- Configurable layout (floors × rows × columns)  
- Supports two vehicle types: 2-wheeler and 4-wheeler  
- Park vehicles, remove vehicles, query free spots  
- Fast lookup via cache of vehicle number or ticket ID  
- Minimal external dependencies (standard library only)

## Prerequisites

- Python 3.6+

## Installation

Clone or download the repo, then:

```sh
cd c:\Users\shubbhardwaj\Downloads
```

## Usage

Edit your `parking_layout` in `parking.py` to match your lot configuration. Each entry is a string `"T-F"` where:

- `T` = vehicle type (2 or 4)  
- `F` = `1` if the spot is initially free, `0` for occupied/invalid  

Example layout for 2 floors, each 2×4:

```python
parking_layout = [
  [ ["2-1","4-1","2-1","4-1"],
    ["2-1","2-1","4-1","4-1"] ],
  [ ["2-1","2-1","4-1","2-1"],
    ["4-1","4-1","2-1","2-1"] ]
]
```

Run the smoke-test:

```sh
python parking.py
```

You should see output like:

```
Parked BIKE1 at: 0-0-0
Free 2-wheeler spots on floor 0: 3
Removal status (201=success): 201
```

## API Overview

### Solution

- `init(helper, parking_layout)` – initialize floors and cache  
- `park(vehicle_type, vehicle_number, ticket_id) → spot_id or ""`  
- `remove_vehicle(spot_id, vehicle_number, ticket_id) → HTTP-style code`  
- `get_free_spots_count(floor, vehicle_type) → int`  
- `search_vehicle(vehicle_number, ticket_id) → spot_id or ""`

### ParkingFloor

- Manages a single floor’s spots and free-spot counts  
- `park(...)` / `remove_vehicle(...)` / `get_free_spots_count(...)`

### ParkingSpot

- Tracks a single spot’s ID, type and occupancy

### SearchManager

- Caches mapping from vehicle number or ticket ID → spot ID for fast lookup

## License

MIT License. Feel free to use, modify, and extend.  
