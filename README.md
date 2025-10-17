# sustainable_city_blueprint.py
ESS HL CITY
# Sustainable City Simulation
# By: [matthew kurnaiawan]
# For: ESS Project

import random

# --- Classes ---
class Building:
    def __init__(self, name, energy_use, solar_panels=False):
        self.name = name
        self.energy_use = energy_use  # kWh per day
        self.solar_panels = solar_panels
    
    def daily_energy_balance(self):
        if self.solar_panels:
            solar_energy = random.randint(30, 70)  # Random solar generation
            balance = self.energy_use - solar_energy
            return max(balance, 0)  # Can't be negative
        else:
            return self.energy_use

class Car:
    def __init__(self, car_type):
        self.car_type = car_type  # 'electric' or 'gas'
    
    def daily_emissions(self):
        if self.car_type == 'electric':
            return random.uniform(0.1, 0.5)  # in kg CO2
        else:
            return random.uniform(2.0, 5.0)

class RecyclingCenter:
    def __init__(self):
        self.collected = 0  # kg recycled per day
    
    def collect(self, amount):
        self.collected += amount
    
    def report(self):
        return f"Total recycled today: {self.collected:.1f} kg"

# --- Simulation ---
class SustainableCity:
    def __init__(self, name):
        self.name = name
        self.buildings = []
        self.cars = []
        self.recycling_center = RecyclingCenter()
    
    def add_building(self, building):
        self.buildings.append(building)
    
    def add_car(self, car):
        self.cars.append(car)
    
    def simulate_day(self):
        print(f"\n🌱 Welcome to {self.name} - Daily Sustainability Report 🌱")
        print("-" * 60)

        total_energy = sum(b.daily_energy_balance() for b in self.buildings)
        total_emissions = sum(c.daily_emissions() for c in self.cars)
        recycled_today = random.randint(100, 300)
        self.recycling_center.collect(recycled_today)

        print(f"🏢 Total buildings: {len(self.buildings)}")
        print(f"🚗 Total cars: {len(self.cars)}")
        print(f"⚡ Total city energy use: {total_energy:.1f} kWh")
        print(f"🌍 Total daily CO2 emissions: {total_emissions:.1f} kg")
        print(f"♻️ {self.recycling_center.report()}")
        
        sustainability_score = 1000 / (total_emissions + total_energy / 10)
        print(f"\n💚 Sustainability Score: {sustainability_score:.2f}/100\n")
        print("-" * 60)

# --- Example Run ---
if __name__ == "__main__":
    city = SustainableCity("GreenVille")

    # Add buildings
    city.add_building(Building("School", 200, solar_panels=True))
    city.add_building(Building("Hospital", 400))
    city.add_building(Building("Apartment", 150, solar_panels=True))

    # Add cars
    for _ in range(5):
        city.add_car(Car("electric"))
    for _ in range(3):
        city.add_car(Car("gas"))

    # Simulate one day
    city.simulate_day()
