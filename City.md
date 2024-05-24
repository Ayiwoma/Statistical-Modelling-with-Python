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





      <th></th>
      <th>empty_slots</th>
      <th>free_bikes</th>
      <th>bike_id</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>bike_station</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>17</td>
      <td>7f3020118e56165ed8b2f61899edb971</td>
      <td>51.529163</td>
      <td>-0.109971</td>
      <td>001023 - River Street , Clerkenwell</td>
    </tr>
    <tr>
      <th>1</th>
      <td>19</td>
      <td>17</td>
      <td>67e6c16bce05410ba4b1f0f5000726ea</td>
      <td>51.499607</td>
      <td>-0.197574</td>
      <td>001018 - Phillimore Gardens, Kensington</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5</td>
      <td>12</td>
      <td>26184215d38089fcad213ef222e69780</td>
      <td>51.505974</td>
      <td>-0.092754</td>
      <td>001024 - Park Street, Bankside</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>21</td>
      <td>1eabd7ac8e781befd03f52ef56a18aa7</td>
      <td>51.523951</td>
      <td>-0.122502</td>
      <td>001022 - Brunswick Square, Bloomsbury</td>
    </tr>
    <tr>
      <th>4</th>
      <td>38</td>
      <td>9</td>
      <td>23efb32f80a9dcd0e4f61fb44b353ce1</td>
      <td>51.521681</td>
      <td>-0.130432</td>
      <td>000980 - Malet Street, Bloomsbury</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
