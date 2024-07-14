# GPS-TOLL-BASED-SYSTEM-SIMULATIONimport random
import math

# Haversine formula to calculate the distance between two GPS points
def haversine(lon1, lat1, lon2, lat2):
    Radius = 6371  # Earth radius in kilometers
    dlon = math.radians(lon2 - lon1)
    dlat = math.radians(lat2 - lat1)
    b = math.sin(dlat / 2) ** 2 + math.cos(math.radians(lat1)) * math.cos(math.radians(lat2)) * math.sin(dlon / 2) ** 2
    d = 2 * math.atan2(math.sqrt(b), math.sqrt(1 - b))
    return Radius * d

# Define toll points with GPS coordinates and rates
toll_points = [
    {"name": "Toll Point 1", "lat": 12.9716, "lon": 77.5946, "rate": 10.0},
    {"name": "Toll Point 2", "lat": 13.0827, "lon": 80.2707, "rate": 15.0},
    {"name": "Toll Point 3", "lat": 17.3850, "lon": 78.4867, "rate": .0}
]

# Simulate vehicle movement with random GPS coordinates
vehicle_path = [
    {"lat": 12.9718, "lon": 77.5950},
    {"lat": 13.0000, "lon": 77.6000},
    {"lat": 13.0827, "lon": 80.2707},	
    {"lat": 17.3852, "lon": 78.4869}
]

# Calculate total toll charges
total_toll_amount = 0

for point in vehicle_path:
    for toll in toll_points:
        distance = haversine(point["lon"], point["lat"], toll["lon"], toll["lat"])
        if distance < 1:  # Assuming a toll is charged if within 1 km
            total_toll_amount += toll["rate"]
            print(f"Passed {toll['name']} - Toll: {toll['rate']}")

print(f"Total Toll Cost: {total_toll_amount}")





