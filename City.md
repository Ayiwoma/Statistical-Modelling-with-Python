CityBikes

Send a request to CityBikes for the city of your choice.

```python


import requests
import pandas as pd

url = 'https://api.citybik.es/v2/networks'
response = requests.get(url)
data = response.json()

london_stations = []

# Find the London network
for network in data['networks']:
    if network['location']['city'] == 'London' and network['location']['country'] == 'GB':
        london_network = network
```


Parse through the response to get the details you want for the bike stations in that city (latitude, longitude, number of bikes).

```python
network_id = london_network['id']
network_url = f'https://api.citybik.es/v2/networks/{network_id}'
network_response = requests.get(network_url)
network_data = network_response.json()

bike_stations = network_data['network']['stations']
```

Put your parsed results into a DataFrame.

```python
# Create DataFrame from the parsed results
df = pd.DataFrame(bike_stations)

# Drop unnecessary columns
df1 = df.drop(columns=['extra', 'timestamp'])

# Rename remaining columns
bike_stations = df1.rename(columns={
    'name' : 'bike_station', 
    'id' : 'bike_id'})

bike_stations.head(5)
```




```python

```
