# Food Bank Locator Map Project

This project aims to extract food bank information from a PDF document, process the data, and visualize the locations on an interactive map.

## Features
- **PDF Text Extraction**: Extracts raw text content from the `Food.pdf` file.
- **Data Parsing**: Uses regular expressions to parse various data points like phone numbers, addresses, city, state, zip, time hours, days of operation, service types, and distance.
- **City-to-County Mapping**: Maps city names to their respective counties for New Jersey locations.
- **Geocoding Addresses**: Converts full addresses into latitude and longitude coordinates using the Nominatim geocoding service, incorporating rate limit handling and retry mechanisms for robustness.
- **Interactive Map Generation**: Creates an interactive HTML map using `folium`, displaying food bank locations as markers.
- **Tooltip Information**: Each marker on the map provides a tooltip showing `time_hours` and `days` of operation when hovered over.

## How It Works
1. **Text Extraction**: The `Food.pdf` document is processed to extract all its textual content.
2. **Data Parsing**: A Python script then takes this raw text and splits it into logical blocks, subsequently parsing each block to extract structured information such as the food bank's name, address, phone number, operating hours, and service type.
3. **County Mapping**: For locations in New Jersey, a predefined dictionary is used to map the extracted city names to their corresponding counties, adding a `County` column to the dataset.
4. **Geocoding**: The `full_address` column is then used to geocode each location, obtaining precise `latitude` and `longitude` coordinates. This step includes error handling for geocoding failures and respects API rate limits to ensure reliable data conversion.
5. **Map Visualization**: Finally, an interactive map is generated using `folium`. The map is centered around the average coordinates of all geocoded locations. Markers are placed at each food bank's coordinates, and hovering over a marker reveals a tooltip with the `time_hours` and `days` of operation.

## Key Files
- `Food.pdf`: The input PDF document containing food bank information.
- `food_bank_parsed.csv`: An intermediate CSV file containing the structured data parsed from the PDF.
- `cities_with_counties.csv`: An intermediate CSV file that includes the parsed data along with the added county information.
- `food_bank_map.html`: The final output, an interactive HTML map visualizing the food bank locations.

## Environment Setup
To run this project, you need to install the following Python libraries. You can do this using pip:
```bash
pip install pandas pdfminer.six requests geopy folium
```

## Usage
This project is designed to be executed as a Jupyter Notebook or Google Colab notebook. Simply run all cells sequentially from top to bottom. The script will handle data extraction, processing, geocoding, and map generation automatically.

## Expected Output
The primary output of this project is an HTML file named `food_bank_map.html`. This file can be opened in any web browser to view the interactive map, which displays markers for each food bank location, complete with useful tooltip information.