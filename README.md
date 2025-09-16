# Data-Structure-Assignment-
Weather Record ADT
```python
class WeatherRecord:
    def _init_(self, date, city, temperature):
        self.date = date
        self.city = city
        self.temperature = temperature


class WeatherDataStorage:
    def __init__(self, year_count, city_names, start_year): 
        self.year_count = year_count
        self.cities = city_names
        self.start_year = start_year
        self.SENTINEL = -999

        # 2D array [years x cities]
        self.temperature_data = [[self.SENTINEL for _ in range(len(city_names))]
                                 for _ in range(year_count)]

        # list of years
        self.years = [start_year + i for i in range(year_count)]

    # Insert a record
    def insert(self, year, city, temp):
        row = self.get_year_index(year)
        col = self.get_city_index(city)
        if row != -1 and col != -1:
            self.temperature_data[row][col] = temp
            print(f"Inserted: {city} {year} = {temp}")
        else:
            print("Invalid year or city")

    # Delete a record
    def delete(self, year, city):
        row = self.get_year_index(year)
        col = self.get_city_index(city)
        if row != -1 and col != -1:
            self.temperature_data[row][col] = self.SENTINEL
            print(f"Deleted record for {city} in {year}")
        else:
            print("Invalid year or city")

    # Retrieve a record
    def retrieve(self, year, city):
        row = self.get_year_index(year)
        col = self.get_city_index(city)
        if row != -1 and col != -1:
            temp = self.temperature_data[row][col]
            if temp != self.SENTINEL:
                print(f"Temperature of {city} in {year} = {temp}")
            else:
                print(f"No data available for {city} in {year}")
        else:
            print("Invalid year or city")

    # Row-major access
    def row_major_access(self):
        print("\nRow-Major Access:")
        for row in self.temperature_data:
            print(row)

    # Column-major access
    def column_major_access(self):
        print("\nColumn-Major Access:")
        for col in range(len(self.cities)):
            column_values = [self.temperature_data[row][col] for row in range(self.year_count)]
            print(column_values)

    # Helper functions
    def get_year_index(self, year):
        return self.years.index(year) if year in self.years else -1

    def get_city_index(self, city):
        return self.cities.index(city) if city in self.cities else -1


if __name__ == "__main__":
    cities = ["Delhi", "Mumbai", "Chennai"]
    storage = WeatherDataStorage(5, cities, 2020) 

    storage.insert(2020, "Delhi", 32.5)
    storage.insert(2021, "Mumbai", 29.7)
    storage.insert(2022, "Chennai", 35.2)

    storage.retrieve(2020, "Delhi")
    storage.retrieve(2021, "Mumbai")
    
    storage.delete(2020, "Delhi")
    storage.retrieve(2020, "Delhi")
    
    storage.row_major_access()
    storage.column_major_access()
```
