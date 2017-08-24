

```python
!pip install citipy
```

    Collecting citipy
      Downloading citipy-0.0.5.tar.gz (557kB)
    [K    100% |████████████████████████████████| 563kB 518kB/s ta 0:00:01
    [?25hCollecting kdtree>=0.12 (from citipy)
      Downloading kdtree-0.15-py2.py3-none-any.whl
    Building wheels for collected packages: citipy
      Running setup.py bdist_wheel for citipy ... [?25l- \ done
    [?25h  Stored in directory: /Users/neilvodoor/Library/Caches/pip/wheels/68/ab/e8/bf9e7c2e7a41fd29026e52d88379ebc770f90eace3b616a420
    Successfully built citipy
    Installing collected packages: kdtree, citipy
    Successfully installed citipy-0.0.5 kdtree-0.15



```python
import matplotlib.pyplot as plt
from citipy import citipy as cp
import pandas as pd
```


```python
#Grab list of cities based on coordinates from citipy
citylist = []
count = 0
dup = 'no'

for x in range(-90,90,1):
    for y in range(-180,180,1):
        city = cp.nearest_city(x, y)
        citdict = {}
        citdict['city'] = city.city_name
        citdict['country'] = city.country_code
        citdict['lat'] = x
        citdict['long'] = y
        if len(citylist) == 0:
            citylist.append(citdict)
            count+=1
            continue
        else:
            #Get rid of duplicates
            for city in citylist:
                if city['city'] == citdict['city']:
                    dup = 'yes'
        if dup == 'no':
            citylist.append(citdict)
            count+=1
        else:
            dup = 'no'

print(len(citylist))
```

    7957



```python
print(citylist[0])
```

    {'city': 'vaini', 'country': 'to', 'lat': -90, 'long': -180}



```python
import requests as req
import json
```


```python
#Create dataframe. Grab 500 random cities
citypd = pd.DataFrame({
    'city': [x['city'] for x in citylist],
    'country': [x['country'] for x in citylist],
})

citypd.head()

samplecity = citypd.sample(500)
```


```python
samplecity
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>741</th>
      <td>bulawayo</td>
      <td>zw</td>
    </tr>
    <tr>
      <th>7718</th>
      <td>keuruu</td>
      <td>fi</td>
    </tr>
    <tr>
      <th>3543</th>
      <td>ahuimanu</td>
      <td>us</td>
    </tr>
    <tr>
      <th>4888</th>
      <td>cefalu</td>
      <td>it</td>
    </tr>
    <tr>
      <th>1380</th>
      <td>tual</td>
      <td>id</td>
    </tr>
    <tr>
      <th>3563</th>
      <td>adrar</td>
      <td>dz</td>
    </tr>
    <tr>
      <th>693</th>
      <td>francistown</td>
      <td>bw</td>
    </tr>
    <tr>
      <th>2009</th>
      <td>sembakung</td>
      <td>id</td>
    </tr>
    <tr>
      <th>7950</th>
      <td>batsfjord</td>
      <td>no</td>
    </tr>
    <tr>
      <th>5135</th>
      <td>kranea elassonos</td>
      <td>gr</td>
    </tr>
    <tr>
      <th>575</th>
      <td>puerto pinasco</td>
      <td>py</td>
    </tr>
    <tr>
      <th>7938</th>
      <td>alta</td>
      <td>no</td>
    </tr>
    <tr>
      <th>1561</th>
      <td>baturaja</td>
      <td>id</td>
    </tr>
    <tr>
      <th>6525</th>
      <td>charyshskoye</td>
      <td>ru</td>
    </tr>
    <tr>
      <th>5294</th>
      <td>paytug</td>
      <td>uz</td>
    </tr>
    <tr>
      <th>5532</th>
      <td>turkistan</td>
      <td>kz</td>
    </tr>
    <tr>
      <th>4829</th>
      <td>mikuni</td>
      <td>jp</td>
    </tr>
    <tr>
      <th>3337</th>
      <td>dolores hidalgo</td>
      <td>mx</td>
    </tr>
    <tr>
      <th>4408</th>
      <td>rabat</td>
      <td>ma</td>
    </tr>
    <tr>
      <th>132</th>
      <td>hamilton</td>
      <td>au</td>
    </tr>
    <tr>
      <th>6942</th>
      <td>novokuznetsk</td>
      <td>ru</td>
    </tr>
    <tr>
      <th>7782</th>
      <td>sosnogorsk</td>
      <td>ru</td>
    </tr>
    <tr>
      <th>1957</th>
      <td>tarakan</td>
      <td>id</td>
    </tr>
    <tr>
      <th>5526</th>
      <td>kegayli</td>
      <td>uz</td>
    </tr>
    <tr>
      <th>1483</th>
      <td>lubao</td>
      <td>cd</td>
    </tr>
    <tr>
      <th>883</th>
      <td>guiratinga</td>
      <td>br</td>
    </tr>
    <tr>
      <th>6390</th>
      <td>novouzensk</td>
      <td>ru</td>
    </tr>
    <tr>
      <th>33</th>
      <td>esperance</td>
      <td>au</td>
    </tr>
    <tr>
      <th>5598</th>
      <td>haverhill</td>
      <td>us</td>
    </tr>
    <tr>
      <th>7116</th>
      <td>subate</td>
      <td>lv</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2386</th>
      <td>meyungs</td>
      <td>pw</td>
    </tr>
    <tr>
      <th>3748</th>
      <td>dalmau</td>
      <td>in</td>
    </tr>
    <tr>
      <th>3888</th>
      <td>bushehr</td>
      <td>ir</td>
    </tr>
    <tr>
      <th>6784</th>
      <td>pleshanovo</td>
      <td>ru</td>
    </tr>
    <tr>
      <th>4788</th>
      <td>yuksekova</td>
      <td>tr</td>
    </tr>
    <tr>
      <th>4781</th>
      <td>ceyhan</td>
      <td>tr</td>
    </tr>
    <tr>
      <th>6822</th>
      <td>barguzin</td>
      <td>ru</td>
    </tr>
    <tr>
      <th>459</th>
      <td>villa oliva</td>
      <td>py</td>
    </tr>
    <tr>
      <th>3959</th>
      <td>tallahassee</td>
      <td>us</td>
    </tr>
    <tr>
      <th>4538</th>
      <td>lefka</td>
      <td>cy</td>
    </tr>
    <tr>
      <th>2201</th>
      <td>sabang</td>
      <td>id</td>
    </tr>
    <tr>
      <th>5510</th>
      <td>sabla</td>
      <td>bg</td>
    </tr>
    <tr>
      <th>7649</th>
      <td>ostersund</td>
      <td>se</td>
    </tr>
    <tr>
      <th>7058</th>
      <td>kargat</td>
      <td>ru</td>
    </tr>
    <tr>
      <th>1771</th>
      <td>sao gabriel da cachoeira</td>
      <td>br</td>
    </tr>
    <tr>
      <th>2094</th>
      <td>lagos</td>
      <td>ng</td>
    </tr>
    <tr>
      <th>6776</th>
      <td>zasechnoye</td>
      <td>ru</td>
    </tr>
    <tr>
      <th>2132</th>
      <td>lahad datu</td>
      <td>my</td>
    </tr>
    <tr>
      <th>3041</th>
      <td>manvi</td>
      <td>in</td>
    </tr>
    <tr>
      <th>2852</th>
      <td>bandiagara</td>
      <td>ml</td>
    </tr>
    <tr>
      <th>423</th>
      <td>pilar</td>
      <td>py</td>
    </tr>
    <tr>
      <th>1098</th>
      <td>paucartambo</td>
      <td>pe</td>
    </tr>
    <tr>
      <th>7527</th>
      <td>kirillov</td>
      <td>ru</td>
    </tr>
    <tr>
      <th>6478</th>
      <td>wroclaw</td>
      <td>pl</td>
    </tr>
    <tr>
      <th>1179</th>
      <td>samfya</td>
      <td>zm</td>
    </tr>
    <tr>
      <th>11</th>
      <td>taolanaro</td>
      <td>mg</td>
    </tr>
    <tr>
      <th>306</th>
      <td>artigas</td>
      <td>uy</td>
    </tr>
    <tr>
      <th>6811</th>
      <td>biskamzha</td>
      <td>ru</td>
    </tr>
    <tr>
      <th>1287</th>
      <td>paita</td>
      <td>pe</td>
    </tr>
    <tr>
      <th>5809</th>
      <td>ucluelet</td>
      <td>ca</td>
    </tr>
  </tbody>
</table>
<p>500 rows × 2 columns</p>
</div>




```python
apikey = 'Enter Your API Key'
url = "http://api.openweathermap.org/data/2.5/weather?"
units = "Imperial"
count = 0
samplecity['latitude'] = ""
samplecity['longitude'] = ""
samplecity['temperature'] = ""
samplecity['humidity'] = ""
samplecity['cloudiness'] = ""
samplecity['wind_speed'] = ""

for index,row in samplecity.iterrows():
    count+= 1
    query_url = url + "appid=" + apikey + "&units=" + units + "&q=" + row['city']
    try:
        weather_response = req.get(query_url)
        cityweather = weather_response.json()
#         print(cityweather)
        samplecity.set_value(index, "latitude", int(cityweather['coord']['lat']))
        samplecity.set_value(index, "longitude", int(cityweather['coord']['lat']))
        samplecity.set_value(index, "temperature", int(cityweather['main']['temp']))
        samplecity.set_value(index, "humidity", int(cityweather['main']['humidity']))
        samplecity.set_value(index, "cloudiness", int(cityweather['clouds']['all']))
        samplecity.set_value(index, "wind_speed", int(cityweather['wind']['speed']))
    except:
        print(f"No data for this city: {row['city']}")
    print(f"This is city#: {count}")
    print(f"This is: {row['city']}" )
    print(f"This is the requested URL: {query_url}")

```

    This is city#: 1
    This is: bulawayo
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=bulawayo
    This is city#: 2
    This is: keuruu
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=keuruu
    This is city#: 3
    This is: ahuimanu
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=ahuimanu
    This is city#: 4
    This is: cefalu
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=cefalu
    This is city#: 5
    This is: tual
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tual
    This is city#: 6
    This is: adrar
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=adrar
    This is city#: 7
    This is: francistown
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=francistown
    This is city#: 8
    This is: sembakung
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=sembakung
    This is city#: 9
    This is: batsfjord
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=batsfjord
    This is city#: 10
    This is: kranea elassonos
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kranea elassonos
    This is city#: 11
    This is: puerto pinasco
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=puerto pinasco
    This is city#: 12
    This is: alta
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=alta
    This is city#: 13
    This is: baturaja
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=baturaja
    This is city#: 14
    This is: charyshskoye
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=charyshskoye
    This is city#: 15
    This is: paytug
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=paytug
    This is city#: 16
    This is: turkistan
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=turkistan
    This is city#: 17
    This is: mikuni
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=mikuni
    This is city#: 18
    This is: dolores hidalgo
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=dolores hidalgo
    This is city#: 19
    This is: rabat
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=rabat
    This is city#: 20
    This is: hamilton
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=hamilton
    This is city#: 21
    This is: novokuznetsk
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=novokuznetsk
    This is city#: 22
    This is: sosnogorsk
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=sosnogorsk
    This is city#: 23
    This is: tarakan
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tarakan
    This is city#: 24
    This is: kegayli
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kegayli
    This is city#: 25
    This is: lubao
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=lubao
    This is city#: 26
    This is: guiratinga
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=guiratinga
    This is city#: 27
    This is: novouzensk
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=novouzensk
    This is city#: 28
    This is: esperance
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=esperance
    This is city#: 29
    This is: haverhill
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=haverhill
    This is city#: 30
    This is: subate
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=subate
    This is city#: 31
    This is: otane
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=otane
    This is city#: 32
    This is: bandarban
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=bandarban
    This is city#: 33
    This is: cuiluan
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=cuiluan
    This is city#: 34
    This is: leh
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=leh
    This is city#: 35
    This is: chau doc
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=chau doc
    This is city#: 36
    This is: amurrio
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=amurrio
    This is city#: 37
    This is: gamboula
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=gamboula
    This is city#: 38
    This is: la rioja
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=la rioja
    This is city#: 39
    This is: dumas
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=dumas
    This is city#: 40
    This is: ajaccio
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=ajaccio
    This is city#: 41
    This is: yuzhno-yeniseyskiy
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=yuzhno-yeniseyskiy
    This is city#: 42
    This is: tairua
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tairua
    This is city#: 43
    This is: culebra
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=culebra
    This is city#: 44
    This is: kropachevo
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kropachevo
    This is city#: 45
    This is: roebourne
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=roebourne
    This is city#: 46
    This is: crab hill
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=crab hill
    This is city#: 47
    This is: pathein
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=pathein
    This is city#: 48
    This is: campbell river
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=campbell river
    This is city#: 49
    This is: north vanlaiphai
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=north vanlaiphai
    This is city#: 50
    This is: vega de alatorre
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=vega de alatorre
    This is city#: 51
    This is: vikyrovice
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=vikyrovice
    This is city#: 52
    This is: aliaga
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=aliaga
    This is city#: 53
    This is: aurillac
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=aurillac
    This is city#: 54
    This is: sharlyk
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=sharlyk
    This is city#: 55
    This is: dubai
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=dubai
    This is city#: 56
    This is: lapy
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=lapy
    This is city#: 57
    This is: itupiranga
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=itupiranga
    This is city#: 58
    This is: kodino
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kodino
    This is city#: 59
    This is: uniontown
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=uniontown
    This is city#: 60
    This is: medak
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=medak
    This is city#: 61
    This is: grand forks
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=grand forks
    This is city#: 62
    This is: bow island
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=bow island
    This is city#: 63
    This is: okhtyrka
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=okhtyrka
    This is city#: 64
    This is: oeiras do para
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=oeiras do para
    This is city#: 65
    This is: ceres
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=ceres
    This is city#: 66
    This is: tambo
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tambo
    This is city#: 67
    This is: radcliff
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=radcliff
    This is city#: 68
    This is: mount barker
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=mount barker
    This is city#: 69
    This is: dudinka
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=dudinka
    This is city#: 70
    This is: komsomolskiy
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=komsomolskiy
    This is city#: 71
    This is: stokmarknes
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=stokmarknes
    This is city#: 72
    This is: zambezi
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=zambezi
    This is city#: 73
    This is: migori
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=migori
    This is city#: 74
    This is: palatka
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=palatka
    This is city#: 75
    This is: wanlaweyn
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=wanlaweyn
    This is city#: 76
    This is: steinbach
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=steinbach
    This is city#: 77
    This is: tenenkou
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tenenkou
    This is city#: 78
    This is: ekhabi
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=ekhabi
    This is city#: 79
    This is: ternate
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=ternate
    This is city#: 80
    This is: calama
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=calama
    This is city#: 81
    This is: kochi
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kochi
    This is city#: 82
    This is: kuantan
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kuantan
    This is city#: 83
    This is: jiroft
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=jiroft
    This is city#: 84
    This is: sijunjung
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=sijunjung
    This is city#: 85
    This is: kabanjahe
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kabanjahe
    This is city#: 86
    This is: porterville
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=porterville
    This is city#: 87
    This is: tumannyy
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tumannyy
    This is city#: 88
    This is: libertad
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=libertad
    This is city#: 89
    This is: nemyriv
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=nemyriv
    This is city#: 90
    This is: mezen
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=mezen
    This is city#: 91
    This is: temple
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=temple
    This is city#: 92
    This is: wenling
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=wenling
    This is city#: 93
    This is: okoneshnikovo
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=okoneshnikovo
    This is city#: 94
    This is: kez
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kez
    This is city#: 95
    This is: carandai
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=carandai
    This is city#: 96
    This is: korla
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=korla
    This is city#: 97
    This is: ngaoundere
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=ngaoundere
    This is city#: 98
    This is: zvishavane
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=zvishavane
    This is city#: 99
    This is: karaton
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=karaton
    This is city#: 100
    This is: gejiu
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=gejiu
    This is city#: 101
    This is: villa sandino
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=villa sandino
    This is city#: 102
    This is: skagen
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=skagen
    This is city#: 103
    This is: zhanaozen
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=zhanaozen
    This is city#: 104
    This is: real
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=real
    This is city#: 105
    This is: chongwe
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=chongwe
    This is city#: 106
    This is: seguela
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=seguela
    This is city#: 107
    This is: kholodnyy
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kholodnyy
    This is city#: 108
    This is: telimele
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=telimele
    This is city#: 109
    This is: haimen
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=haimen
    This is city#: 110
    This is: son la
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=son la
    This is city#: 111
    This is: tukrah
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tukrah
    This is city#: 112
    This is: gwanda
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=gwanda
    This is city#: 113
    This is: vozdvizhenka
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=vozdvizhenka
    This is city#: 114
    This is: angul
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=angul
    This is city#: 115
    This is: bara
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=bara
    This is city#: 116
    This is: wewak
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=wewak
    This is city#: 117
    This is: asimion
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=asimion
    This is city#: 118
    This is: sokolo
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=sokolo
    This is city#: 119
    This is: itapirapua
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=itapirapua
    This is city#: 120
    This is: praxedis guerrero
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=praxedis guerrero
    This is city#: 121
    This is: putina
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=putina
    This is city#: 122
    This is: sassenberg
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=sassenberg
    This is city#: 123
    This is: motygino
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=motygino
    This is city#: 124
    This is: new norfolk
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=new norfolk
    This is city#: 125
    This is: ostashkov
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=ostashkov
    This is city#: 126
    This is: cidreira
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=cidreira
    This is city#: 127
    This is: san pablo
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=san pablo
    This is city#: 128
    This is: caraquet
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=caraquet
    This is city#: 129
    This is: namibe
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=namibe
    This is city#: 130
    This is: puerto escondido
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=puerto escondido
    This is city#: 131
    This is: orangeburg
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=orangeburg
    This is city#: 132
    This is: agogo
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=agogo
    This is city#: 133
    This is: kastamonu
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kastamonu
    This is city#: 134
    This is: limbe
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=limbe
    This is city#: 135
    This is: brokopondo
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=brokopondo
    This is city#: 136
    This is: trairi
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=trairi
    This is city#: 137
    This is: mitchell
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=mitchell
    This is city#: 138
    This is: middelburg
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=middelburg
    This is city#: 139
    This is: betanzos
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=betanzos
    This is city#: 140
    This is: panuco
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=panuco
    This is city#: 141
    This is: cocorit
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=cocorit
    This is city#: 142
    This is: kakonko
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kakonko
    This is city#: 143
    This is: acapulco
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=acapulco
    This is city#: 144
    This is: shahr-e babak
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=shahr-e babak
    This is city#: 145
    This is: corralillo
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=corralillo
    This is city#: 146
    This is: witbank
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=witbank
    This is city#: 147
    This is: bernalillo
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=bernalillo
    This is city#: 148
    This is: tonneins
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tonneins
    This is city#: 149
    This is: yumen
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=yumen
    This is city#: 150
    This is: tornio
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tornio
    This is city#: 151
    This is: townsville
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=townsville
    This is city#: 152
    This is: akropong
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=akropong
    This is city#: 153
    This is: rafina
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=rafina
    This is city#: 154
    This is: ivanteyevka
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=ivanteyevka
    This is city#: 155
    This is: linkuva
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=linkuva
    This is city#: 156
    This is: zhaoyang
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=zhaoyang
    This is city#: 157
    This is: la libertad
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=la libertad
    This is city#: 158
    This is: itanhem
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=itanhem
    This is city#: 159
    This is: amos
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=amos
    This is city#: 160
    This is: kintampo
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kintampo
    This is city#: 161
    This is: alanya
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=alanya
    This is city#: 162
    This is: dubovskoye
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=dubovskoye
    This is city#: 163
    This is: portel
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=portel
    This is city#: 164
    This is: orange cove
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=orange cove
    This is city#: 165
    This is: kuito
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kuito
    This is city#: 166
    This is: sibut
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=sibut
    This is city#: 167
    This is: gandajika
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=gandajika
    This is city#: 168
    This is: bagdarin
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=bagdarin
    This is city#: 169
    This is: mancio lima
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=mancio lima
    This is city#: 170
    This is: villa carlos paz
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=villa carlos paz
    This is city#: 171
    This is: wunsiedel
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=wunsiedel
    This is city#: 172
    This is: bodden town
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=bodden town
    This is city#: 173
    This is: streator
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=streator
    This is city#: 174
    This is: ionia
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=ionia
    This is city#: 175
    This is: sjenica
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=sjenica
    This is city#: 176
    This is: raahe
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=raahe
    This is city#: 177
    This is: indiana
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=indiana
    This is city#: 178
    This is: tagusao
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tagusao
    This is city#: 179
    This is: zadar
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=zadar
    This is city#: 180
    This is: sadon
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=sadon
    This is city#: 181
    This is: miranda
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=miranda
    This is city#: 182
    This is: gboko
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=gboko
    This is city#: 183
    This is: surgut
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=surgut
    This is city#: 184
    This is: shagonar
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=shagonar
    This is city#: 185
    This is: kone
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kone
    This is city#: 186
    This is: arona
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=arona
    This is city#: 187
    This is: siddipet
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=siddipet
    This is city#: 188
    This is: grand-santi
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=grand-santi
    This is city#: 189
    This is: moura
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=moura
    This is city#: 190
    This is: ladario
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=ladario
    This is city#: 191
    This is: tambovka
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tambovka
    This is city#: 192
    This is: tuscaloosa
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tuscaloosa
    This is city#: 193
    This is: maues
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=maues
    This is city#: 194
    This is: bundaberg
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=bundaberg
    This is city#: 195
    This is: kadiri
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kadiri
    This is city#: 196
    This is: nenjiang
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=nenjiang
    This is city#: 197
    This is: lishui
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=lishui
    This is city#: 198
    This is: picton
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=picton
    This is city#: 199
    This is: kargapolye
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kargapolye
    This is city#: 200
    This is: north branch
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=north branch
    This is city#: 201
    This is: patan
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=patan
    This is city#: 202
    This is: temirtau
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=temirtau
    This is city#: 203
    This is: sao paulo de olivenca
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=sao paulo de olivenca
    This is city#: 204
    This is: baoning
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=baoning
    This is city#: 205
    This is: vengerovo
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=vengerovo
    This is city#: 206
    This is: chaman
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=chaman
    This is city#: 207
    This is: xiaoshi
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=xiaoshi
    This is city#: 208
    This is: kualakapuas
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kualakapuas
    This is city#: 209
    This is: denpasar
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=denpasar
    This is city#: 210
    This is: las vegas
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=las vegas
    This is city#: 211
    This is: misasi
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=misasi
    This is city#: 212
    This is: xuchang
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=xuchang
    This is city#: 213
    This is: ulverstone
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=ulverstone
    This is city#: 214
    This is: tha mai
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tha mai
    This is city#: 215
    This is: pucallpa
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=pucallpa
    This is city#: 216
    This is: yorosso
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=yorosso
    This is city#: 217
    This is: vitoria da conquista
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=vitoria da conquista
    This is city#: 218
    This is: akhtanizovskaya
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=akhtanizovskaya
    This is city#: 219
    This is: erdenet
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=erdenet
    This is city#: 220
    This is: kontagora
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kontagora
    This is city#: 221
    This is: hillsboro
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=hillsboro
    This is city#: 222
    This is: kloulklubed
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kloulklubed
    This is city#: 223
    This is: horki
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=horki
    This is city#: 224
    This is: supe
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=supe
    This is city#: 225
    This is: hue
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=hue
    This is city#: 226
    This is: moses lake
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=moses lake
    This is city#: 227
    This is: mpanda
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=mpanda
    This is city#: 228
    This is: lamtah
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=lamtah
    This is city#: 229
    This is: agropoli
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=agropoli
    This is city#: 230
    This is: farsund
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=farsund
    This is city#: 231
    This is: west wendover
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=west wendover
    This is city#: 232
    This is: nouna
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=nouna
    This is city#: 233
    This is: varangaon
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=varangaon
    This is city#: 234
    This is: anisoc
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=anisoc
    This is city#: 235
    This is: gondal
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=gondal
    This is city#: 236
    This is: madarounfa
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=madarounfa
    This is city#: 237
    This is: recodo
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=recodo
    This is city#: 238
    This is: tashtagol
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tashtagol
    This is city#: 239
    This is: zig
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=zig
    This is city#: 240
    This is: burns lake
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=burns lake
    This is city#: 241
    This is: pedernales
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=pedernales
    This is city#: 242
    This is: arua
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=arua
    This is city#: 243
    This is: dovers
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=dovers
    This is city#: 244
    This is: azar shahr
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=azar shahr
    This is city#: 245
    This is: solenzo
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=solenzo
    This is city#: 246
    This is: novobelokatay
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=novobelokatay
    This is city#: 247
    This is: san pedro de ycuamandiyu
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=san pedro de ycuamandiyu
    This is city#: 248
    This is: kodar
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kodar
    This is city#: 249
    This is: banatski karlovac
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=banatski karlovac
    This is city#: 250
    This is: timra
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=timra
    This is city#: 251
    This is: bouloupari
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=bouloupari
    This is city#: 252
    This is: hammerfest
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=hammerfest
    This is city#: 253
    This is: liku
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=liku
    This is city#: 254
    This is: allonnes
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=allonnes
    This is city#: 255
    This is: boljarovo
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=boljarovo
    This is city#: 256
    This is: oneonta
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=oneonta
    This is city#: 257
    This is: barinas
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=barinas
    This is city#: 258
    This is: demmin
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=demmin
    This is city#: 259
    This is: latung
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=latung
    This is city#: 260
    This is: skalistyy
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=skalistyy
    This is city#: 261
    This is: sengiley
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=sengiley
    This is city#: 262
    This is: porangatu
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=porangatu
    This is city#: 263
    This is: borujerd
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=borujerd
    This is city#: 264
    This is: oruro
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=oruro
    This is city#: 265
    This is: biak
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=biak
    This is city#: 266
    This is: coremas
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=coremas
    This is city#: 267
    This is: bang len
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=bang len
    This is city#: 268
    This is: goias
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=goias
    This is city#: 269
    This is: guapore
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=guapore
    This is city#: 270
    This is: maracacume
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=maracacume
    This is city#: 271
    This is: estacion coahuila
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=estacion coahuila
    This is city#: 272
    This is: takab
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=takab
    This is city#: 273
    This is: teluk intan
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=teluk intan
    This is city#: 274
    This is: lewisville
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=lewisville
    This is city#: 275
    This is: yusva
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=yusva
    This is city#: 276
    This is: kulu
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kulu
    This is city#: 277
    This is: doctor arroyo
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=doctor arroyo
    This is city#: 278
    This is: viganello
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=viganello
    This is city#: 279
    This is: lolua
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=lolua
    This is city#: 280
    This is: yabrud
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=yabrud
    This is city#: 281
    This is: vagamo
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=vagamo
    This is city#: 282
    This is: puyang
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=puyang
    This is city#: 283
    This is: tyup
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tyup
    This is city#: 284
    This is: bouafle
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=bouafle
    This is city#: 285
    This is: eyemouth
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=eyemouth
    This is city#: 286
    This is: upata
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=upata
    This is city#: 287
    This is: koulikoro
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=koulikoro
    This is city#: 288
    This is: ojhar
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=ojhar
    This is city#: 289
    This is: puerto madryn
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=puerto madryn
    This is city#: 290
    This is: yekaterinovka
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=yekaterinovka
    This is city#: 291
    This is: coffs harbour
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=coffs harbour
    This is city#: 292
    This is: chisec
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=chisec
    This is city#: 293
    This is: zhob
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=zhob
    This is city#: 294
    This is: bezhanitsy
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=bezhanitsy
    This is city#: 295
    This is: serebryansk
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=serebryansk
    This is city#: 296
    This is: altus
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=altus
    This is city#: 297
    This is: edgewater
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=edgewater
    This is city#: 298
    This is: ushibuka
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=ushibuka
    This is city#: 299
    This is: maykain
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=maykain
    This is city#: 300
    This is: sergiyevsk
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=sergiyevsk
    This is city#: 301
    This is: uribia
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=uribia
    This is city#: 302
    This is: selaphum
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=selaphum
    This is city#: 303
    This is: gonda
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=gonda
    This is city#: 304
    This is: yanam
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=yanam
    This is city#: 305
    This is: shaartuz
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=shaartuz
    This is city#: 306
    This is: sondrio
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=sondrio
    This is city#: 307
    This is: santa rita
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=santa rita
    This is city#: 308
    This is: la union
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=la union
    This is city#: 309
    This is: jishu
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=jishu
    This is city#: 310
    This is: cavalcante
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=cavalcante
    This is city#: 311
    This is: tursunzoda
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tursunzoda
    This is city#: 312
    This is: noshiro
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=noshiro
    This is city#: 313
    This is: pital
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=pital
    This is city#: 314
    This is: taltal
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=taltal
    This is city#: 315
    This is: nederland
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=nederland
    This is city#: 316
    This is: korablino
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=korablino
    This is city#: 317
    This is: galbshtadt
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=galbshtadt
    This is city#: 318
    This is: merritt
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=merritt
    This is city#: 319
    This is: yingcheng
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=yingcheng
    This is city#: 320
    This is: jever
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=jever
    This is city#: 321
    This is: torbay
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=torbay
    This is city#: 322
    This is: sabinov
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=sabinov
    This is city#: 323
    This is: bam
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=bam
    This is city#: 324
    This is: anchorage
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=anchorage
    This is city#: 325
    This is: nador
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=nador
    This is city#: 326
    This is: palimbang
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=palimbang
    This is city#: 327
    This is: athni
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=athni
    This is city#: 328
    This is: louga
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=louga
    This is city#: 329
    This is: luang prabang
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=luang prabang
    This is city#: 330
    This is: chaohu
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=chaohu
    This is city#: 331
    This is: arkansas city
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=arkansas city
    This is city#: 332
    This is: jatiroto
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=jatiroto
    This is city#: 333
    This is: buncrana
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=buncrana
    This is city#: 334
    This is: uarini
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=uarini
    This is city#: 335
    This is: tanhacu
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tanhacu
    This is city#: 336
    This is: purgstall
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=purgstall
    This is city#: 337
    This is: itoigawa
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=itoigawa
    This is city#: 338
    This is: ginda
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=ginda
    This is city#: 339
    This is: faya
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=faya
    This is city#: 340
    This is: sao jose de ribamar
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=sao jose de ribamar
    This is city#: 341
    This is: sao mateus
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=sao mateus
    This is city#: 342
    This is: awallan
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=awallan
    This is city#: 343
    This is: xai-xai
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=xai-xai
    This is city#: 344
    This is: camabatela
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=camabatela
    This is city#: 345
    This is: calabozo
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=calabozo
    This is city#: 346
    This is: port macquarie
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=port macquarie
    This is city#: 347
    This is: blankenberge
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=blankenberge
    This is city#: 348
    This is: uvalde
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=uvalde
    This is city#: 349
    This is: cabanas
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=cabanas
    This is city#: 350
    This is: santa marinella
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=santa marinella
    This is city#: 351
    This is: galesong
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=galesong
    This is city#: 352
    This is: tabou
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tabou
    This is city#: 353
    This is: brownwood
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=brownwood
    This is city#: 354
    This is: colac
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=colac
    This is city#: 355
    This is: shaoyang
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=shaoyang
    This is city#: 356
    This is: saint-raymond
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=saint-raymond
    This is city#: 357
    This is: ilhabela
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=ilhabela
    This is city#: 358
    This is: guaymas
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=guaymas
    This is city#: 359
    This is: escanaba
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=escanaba
    This is city#: 360
    This is: kabinda
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kabinda
    This is city#: 361
    This is: kumeny
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kumeny
    This is city#: 362
    This is: belgrade
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=belgrade
    This is city#: 363
    This is: san javier
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=san javier
    This is city#: 364
    This is: pailon
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=pailon
    This is city#: 365
    This is: mokrousovo
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=mokrousovo
    This is city#: 366
    This is: kremenki
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kremenki
    This is city#: 367
    This is: poim
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=poim
    This is city#: 368
    This is: navoi
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=navoi
    This is city#: 369
    This is: la serena
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=la serena
    This is city#: 370
    This is: valday
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=valday
    This is city#: 371
    This is: tautira
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tautira
    This is city#: 372
    This is: aswan
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=aswan
    This is city#: 373
    This is: taman
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=taman
    This is city#: 374
    This is: uusikaupunki
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=uusikaupunki
    This is city#: 375
    This is: giaveno
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=giaveno
    This is city#: 376
    This is: matto
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=matto
    This is city#: 377
    This is: weiser
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=weiser
    This is city#: 378
    This is: cumaribo
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=cumaribo
    This is city#: 379
    This is: voh
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=voh
    This is city#: 380
    This is: piopio
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=piopio
    This is city#: 381
    This is: kodinsk
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kodinsk
    This is city#: 382
    This is: general roca
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=general roca
    This is city#: 383
    This is: macomer
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=macomer
    This is city#: 384
    This is: baykit
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=baykit
    This is city#: 385
    This is: zarate
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=zarate
    This is city#: 386
    This is: natitingou
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=natitingou
    This is city#: 387
    This is: gotsu
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=gotsu
    This is city#: 388
    This is: romitan
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=romitan
    This is city#: 389
    This is: gaoual
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=gaoual
    This is city#: 390
    This is: wasilla
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=wasilla
    This is city#: 391
    This is: smiths falls
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=smiths falls
    This is city#: 392
    This is: san matias
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=san matias
    This is city#: 393
    This is: koumac
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=koumac
    This is city#: 394
    This is: lahij
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=lahij
    This is city#: 395
    This is: nicoya
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=nicoya
    This is city#: 396
    This is: lamar
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=lamar
    This is city#: 397
    This is: vikersund
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=vikersund
    This is city#: 398
    This is: sao joao da barra
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=sao joao da barra
    This is city#: 399
    This is: mahalapye
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=mahalapye
    This is city#: 400
    This is: wichita falls
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=wichita falls
    This is city#: 401
    This is: manalurpet
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=manalurpet
    This is city#: 402
    This is: owatonna
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=owatonna
    This is city#: 403
    This is: carmo do rio claro
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=carmo do rio claro
    This is city#: 404
    This is: laramie
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=laramie
    This is city#: 405
    This is: antalaha
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=antalaha
    This is city#: 406
    This is: coruripe
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=coruripe
    This is city#: 407
    This is: maragogi
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=maragogi
    This is city#: 408
    This is: tepalcatepec
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tepalcatepec
    This is city#: 409
    This is: la ligua
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=la ligua
    This is city#: 410
    This is: hudson bay
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=hudson bay
    No data for this city: ciras
    This is city#: 411
    This is: ciras
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=ciras
    This is city#: 412
    This is: chanute
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=chanute
    This is city#: 413
    This is: cottonwood
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=cottonwood
    This is city#: 414
    This is: iralaya
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=iralaya
    This is city#: 415
    This is: sriperumbudur
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=sriperumbudur
    This is city#: 416
    This is: maceio
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=maceio
    This is city#: 417
    This is: balotra
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=balotra
    This is city#: 418
    This is: seligenstadt
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=seligenstadt
    This is city#: 419
    This is: nueva helvecia
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=nueva helvecia
    This is city#: 420
    This is: newcastle
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=newcastle
    This is city#: 421
    This is: bochil
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=bochil
    This is city#: 422
    This is: landskrona
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=landskrona
    This is city#: 423
    This is: tieli
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tieli
    This is city#: 424
    This is: kavos
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kavos
    This is city#: 425
    This is: guajara
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=guajara
    This is city#: 426
    This is: roura
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=roura
    This is city#: 427
    This is: millau
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=millau
    This is city#: 428
    This is: puli
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=puli
    This is city#: 429
    This is: gornyy
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=gornyy
    This is city#: 430
    This is: korcula
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=korcula
    This is city#: 431
    This is: saryg-sep
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=saryg-sep
    This is city#: 432
    This is: winchester
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=winchester
    This is city#: 433
    This is: jinzhou
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=jinzhou
    This is city#: 434
    This is: tiruvottiyur
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tiruvottiyur
    This is city#: 435
    This is: ulundi
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=ulundi
    This is city#: 436
    This is: fort pierce
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=fort pierce
    This is city#: 437
    This is: jiamusi
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=jiamusi
    This is city#: 438
    This is: orshanka
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=orshanka
    This is city#: 439
    This is: gao
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=gao
    This is city#: 440
    This is: savonlinna
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=savonlinna
    This is city#: 441
    This is: tamsweg
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tamsweg
    This is city#: 442
    This is: kopavogur
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kopavogur
    This is city#: 443
    This is: waverly
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=waverly
    This is city#: 444
    This is: tangshan
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tangshan
    This is city#: 445
    This is: kampong chhnang
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kampong chhnang
    This is city#: 446
    This is: tikrit
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tikrit
    This is city#: 447
    This is: izamal
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=izamal
    This is city#: 448
    This is: voghera
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=voghera
    This is city#: 449
    This is: kamyaran
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kamyaran
    This is city#: 450
    This is: koflach
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=koflach
    This is city#: 451
    This is: maimon
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=maimon
    This is city#: 452
    This is: champasak
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=champasak
    This is city#: 453
    This is: assela
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=assela
    This is city#: 454
    This is: amnat charoen
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=amnat charoen
    This is city#: 455
    This is: senj
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=senj
    This is city#: 456
    This is: tasbuget
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tasbuget
    This is city#: 457
    This is: aksu
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=aksu
    This is city#: 458
    This is: xudat
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=xudat
    This is city#: 459
    This is: benito juarez
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=benito juarez
    This is city#: 460
    This is: capreol
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=capreol
    This is city#: 461
    This is: lloydminster
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=lloydminster
    This is city#: 462
    This is: ishinomaki
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=ishinomaki
    This is city#: 463
    This is: coxim
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=coxim
    This is city#: 464
    This is: kondinskoye
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kondinskoye
    This is city#: 465
    This is: sakiai
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=sakiai
    This is city#: 466
    This is: linkoping
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=linkoping
    This is city#: 467
    This is: ganganagar
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=ganganagar
    This is city#: 468
    This is: chicla
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=chicla
    This is city#: 469
    This is: chumphon
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=chumphon
    This is city#: 470
    This is: danilov
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=danilov
    This is city#: 471
    This is: meyungs
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=meyungs
    This is city#: 472
    This is: dalmau
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=dalmau
    This is city#: 473
    This is: bushehr
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=bushehr
    This is city#: 474
    This is: pleshanovo
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=pleshanovo
    This is city#: 475
    This is: yuksekova
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=yuksekova
    This is city#: 476
    This is: ceyhan
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=ceyhan
    This is city#: 477
    This is: barguzin
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=barguzin
    This is city#: 478
    This is: villa oliva
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=villa oliva
    This is city#: 479
    This is: tallahassee
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=tallahassee
    This is city#: 480
    This is: lefka
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=lefka
    This is city#: 481
    This is: sabang
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=sabang
    This is city#: 482
    This is: sabla
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=sabla
    This is city#: 483
    This is: ostersund
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=ostersund
    This is city#: 484
    This is: kargat
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kargat
    This is city#: 485
    This is: sao gabriel da cachoeira
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=sao gabriel da cachoeira
    This is city#: 486
    This is: lagos
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=lagos
    This is city#: 487
    This is: zasechnoye
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=zasechnoye
    This is city#: 488
    This is: lahad datu
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=lahad datu
    This is city#: 489
    This is: manvi
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=manvi
    This is city#: 490
    This is: bandiagara
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=bandiagara
    This is city#: 491
    This is: pilar
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=pilar
    This is city#: 492
    This is: paucartambo
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=paucartambo
    This is city#: 493
    This is: kirillov
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=kirillov
    This is city#: 494
    This is: wroclaw
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=wroclaw
    This is city#: 495
    This is: samfya
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=samfya
    This is city#: 496
    This is: taolanaro
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=taolanaro
    This is city#: 497
    This is: artigas
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=artigas
    This is city#: 498
    This is: biskamzha
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=biskamzha
    This is city#: 499
    This is: paita
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=paita
    This is city#: 500
    This is: ucluelet
    This is the requested URL: http://api.openweathermap.org/data/2.5/weather?appid=af674cc1474d64a64479c486b1702f8e&units=Imperial&q=ucluelet



```python
samplecity = samplecity[samplecity.latitude != ""]
samplecity
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>country</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>temperature</th>
      <th>humidity</th>
      <th>cloudiness</th>
      <th>wind_speed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>741</th>
      <td>bulawayo</td>
      <td>zw</td>
      <td>-20</td>
      <td>-20</td>
      <td>47</td>
      <td>33</td>
      <td>0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>7718</th>
      <td>keuruu</td>
      <td>fi</td>
      <td>62</td>
      <td>62</td>
      <td>48</td>
      <td>100</td>
      <td>0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>3543</th>
      <td>ahuimanu</td>
      <td>us</td>
      <td>21</td>
      <td>21</td>
      <td>81</td>
      <td>65</td>
      <td>20</td>
      <td>12</td>
    </tr>
    <tr>
      <th>4888</th>
      <td>cefalu</td>
      <td>it</td>
      <td>38</td>
      <td>38</td>
      <td>64</td>
      <td>100</td>
      <td>0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1380</th>
      <td>tual</td>
      <td>id</td>
      <td>-5</td>
      <td>-5</td>
      <td>78</td>
      <td>100</td>
      <td>8</td>
      <td>15</td>
    </tr>
    <tr>
      <th>3563</th>
      <td>adrar</td>
      <td>dz</td>
      <td>27</td>
      <td>27</td>
      <td>104</td>
      <td>14</td>
      <td>75</td>
      <td>13</td>
    </tr>
    <tr>
      <th>693</th>
      <td>francistown</td>
      <td>bw</td>
      <td>-21</td>
      <td>-21</td>
      <td>66</td>
      <td>12</td>
      <td>0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2009</th>
      <td>sembakung</td>
      <td>id</td>
      <td>3</td>
      <td>3</td>
      <td>74</td>
      <td>100</td>
      <td>88</td>
      <td>2</td>
    </tr>
    <tr>
      <th>7950</th>
      <td>batsfjord</td>
      <td>no</td>
      <td>70</td>
      <td>70</td>
      <td>44</td>
      <td>93</td>
      <td>75</td>
      <td>12</td>
    </tr>
    <tr>
      <th>5135</th>
      <td>kranea elassonos</td>
      <td>gr</td>
      <td>39</td>
      <td>39</td>
      <td>54</td>
      <td>80</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>575</th>
      <td>puerto pinasco</td>
      <td>py</td>
      <td>31</td>
      <td>31</td>
      <td>89</td>
      <td>78</td>
      <td>0</td>
      <td>10</td>
    </tr>
    <tr>
      <th>7938</th>
      <td>alta</td>
      <td>no</td>
      <td>69</td>
      <td>69</td>
      <td>47</td>
      <td>76</td>
      <td>75</td>
      <td>12</td>
    </tr>
    <tr>
      <th>1561</th>
      <td>baturaja</td>
      <td>id</td>
      <td>-4</td>
      <td>-4</td>
      <td>71</td>
      <td>97</td>
      <td>92</td>
      <td>7</td>
    </tr>
    <tr>
      <th>6525</th>
      <td>charyshskoye</td>
      <td>ru</td>
      <td>51</td>
      <td>51</td>
      <td>59</td>
      <td>63</td>
      <td>0</td>
      <td>8</td>
    </tr>
    <tr>
      <th>5294</th>
      <td>paytug</td>
      <td>uz</td>
      <td>25</td>
      <td>25</td>
      <td>77</td>
      <td>95</td>
      <td>8</td>
      <td>2</td>
    </tr>
    <tr>
      <th>5532</th>
      <td>turkistan</td>
      <td>kz</td>
      <td>43</td>
      <td>43</td>
      <td>75</td>
      <td>31</td>
      <td>0</td>
      <td>19</td>
    </tr>
    <tr>
      <th>4829</th>
      <td>mikuni</td>
      <td>jp</td>
      <td>36</td>
      <td>36</td>
      <td>86</td>
      <td>58</td>
      <td>75</td>
      <td>9</td>
    </tr>
    <tr>
      <th>3337</th>
      <td>dolores hidalgo</td>
      <td>mx</td>
      <td>21</td>
      <td>21</td>
      <td>77</td>
      <td>50</td>
      <td>75</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4408</th>
      <td>rabat</td>
      <td>ma</td>
      <td>33</td>
      <td>33</td>
      <td>75</td>
      <td>83</td>
      <td>40</td>
      <td>2</td>
    </tr>
    <tr>
      <th>132</th>
      <td>hamilton</td>
      <td>au</td>
      <td>43</td>
      <td>43</td>
      <td>66</td>
      <td>63</td>
      <td>75</td>
      <td>8</td>
    </tr>
    <tr>
      <th>6942</th>
      <td>novokuznetsk</td>
      <td>ru</td>
      <td>53</td>
      <td>53</td>
      <td>58</td>
      <td>86</td>
      <td>76</td>
      <td>6</td>
    </tr>
    <tr>
      <th>7782</th>
      <td>sosnogorsk</td>
      <td>ru</td>
      <td>63</td>
      <td>63</td>
      <td>66</td>
      <td>61</td>
      <td>0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1957</th>
      <td>tarakan</td>
      <td>id</td>
      <td>3</td>
      <td>3</td>
      <td>78</td>
      <td>100</td>
      <td>88</td>
      <td>2</td>
    </tr>
    <tr>
      <th>5526</th>
      <td>kegayli</td>
      <td>uz</td>
      <td>7</td>
      <td>7</td>
      <td>70</td>
      <td>97</td>
      <td>92</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1483</th>
      <td>lubao</td>
      <td>cd</td>
      <td>14</td>
      <td>14</td>
      <td>76</td>
      <td>94</td>
      <td>90</td>
      <td>2</td>
    </tr>
    <tr>
      <th>883</th>
      <td>guiratinga</td>
      <td>br</td>
      <td>-16</td>
      <td>-16</td>
      <td>90</td>
      <td>26</td>
      <td>0</td>
      <td>9</td>
    </tr>
    <tr>
      <th>6390</th>
      <td>novouzensk</td>
      <td>ru</td>
      <td>50</td>
      <td>50</td>
      <td>76</td>
      <td>45</td>
      <td>48</td>
      <td>6</td>
    </tr>
    <tr>
      <th>33</th>
      <td>esperance</td>
      <td>au</td>
      <td>-33</td>
      <td>-33</td>
      <td>42</td>
      <td>86</td>
      <td>0</td>
      <td>7</td>
    </tr>
    <tr>
      <th>5598</th>
      <td>haverhill</td>
      <td>us</td>
      <td>42</td>
      <td>42</td>
      <td>78</td>
      <td>39</td>
      <td>20</td>
      <td>11</td>
    </tr>
    <tr>
      <th>7116</th>
      <td>subate</td>
      <td>lv</td>
      <td>56</td>
      <td>56</td>
      <td>52</td>
      <td>85</td>
      <td>0</td>
      <td>13</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2386</th>
      <td>meyungs</td>
      <td>pw</td>
      <td>7</td>
      <td>7</td>
      <td>79</td>
      <td>83</td>
      <td>40</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3748</th>
      <td>dalmau</td>
      <td>in</td>
      <td>26</td>
      <td>26</td>
      <td>79</td>
      <td>92</td>
      <td>20</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3888</th>
      <td>bushehr</td>
      <td>ir</td>
      <td>28</td>
      <td>28</td>
      <td>91</td>
      <td>59</td>
      <td>20</td>
      <td>4</td>
    </tr>
    <tr>
      <th>6784</th>
      <td>pleshanovo</td>
      <td>ru</td>
      <td>52</td>
      <td>52</td>
      <td>71</td>
      <td>32</td>
      <td>44</td>
      <td>6</td>
    </tr>
    <tr>
      <th>4788</th>
      <td>yuksekova</td>
      <td>tr</td>
      <td>37</td>
      <td>37</td>
      <td>69</td>
      <td>49</td>
      <td>0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>4781</th>
      <td>ceyhan</td>
      <td>tr</td>
      <td>37</td>
      <td>37</td>
      <td>80</td>
      <td>83</td>
      <td>20</td>
      <td>2</td>
    </tr>
    <tr>
      <th>6822</th>
      <td>barguzin</td>
      <td>ru</td>
      <td>53</td>
      <td>53</td>
      <td>38</td>
      <td>83</td>
      <td>32</td>
      <td>3</td>
    </tr>
    <tr>
      <th>459</th>
      <td>villa oliva</td>
      <td>py</td>
      <td>-26</td>
      <td>-26</td>
      <td>95</td>
      <td>34</td>
      <td>0</td>
      <td>25</td>
    </tr>
    <tr>
      <th>3959</th>
      <td>tallahassee</td>
      <td>us</td>
      <td>30</td>
      <td>30</td>
      <td>94</td>
      <td>50</td>
      <td>20</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4538</th>
      <td>lefka</td>
      <td>cy</td>
      <td>35</td>
      <td>35</td>
      <td>80</td>
      <td>74</td>
      <td>20</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2201</th>
      <td>sabang</td>
      <td>id</td>
      <td>5</td>
      <td>5</td>
      <td>84</td>
      <td>100</td>
      <td>24</td>
      <td>7</td>
    </tr>
    <tr>
      <th>5510</th>
      <td>sabla</td>
      <td>bg</td>
      <td>29</td>
      <td>29</td>
      <td>74</td>
      <td>87</td>
      <td>48</td>
      <td>2</td>
    </tr>
    <tr>
      <th>7649</th>
      <td>ostersund</td>
      <td>se</td>
      <td>63</td>
      <td>63</td>
      <td>48</td>
      <td>81</td>
      <td>0</td>
      <td>9</td>
    </tr>
    <tr>
      <th>7058</th>
      <td>kargat</td>
      <td>ru</td>
      <td>55</td>
      <td>55</td>
      <td>62</td>
      <td>74</td>
      <td>0</td>
      <td>8</td>
    </tr>
    <tr>
      <th>1771</th>
      <td>sao gabriel da cachoeira</td>
      <td>br</td>
      <td>0</td>
      <td>0</td>
      <td>80</td>
      <td>99</td>
      <td>20</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2094</th>
      <td>lagos</td>
      <td>ng</td>
      <td>6</td>
      <td>6</td>
      <td>77</td>
      <td>83</td>
      <td>40</td>
      <td>6</td>
    </tr>
    <tr>
      <th>6776</th>
      <td>zasechnoye</td>
      <td>ru</td>
      <td>53</td>
      <td>53</td>
      <td>61</td>
      <td>58</td>
      <td>0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2132</th>
      <td>lahad datu</td>
      <td>my</td>
      <td>5</td>
      <td>5</td>
      <td>76</td>
      <td>100</td>
      <td>56</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3041</th>
      <td>manvi</td>
      <td>in</td>
      <td>15</td>
      <td>15</td>
      <td>72</td>
      <td>91</td>
      <td>64</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2852</th>
      <td>bandiagara</td>
      <td>ml</td>
      <td>14</td>
      <td>14</td>
      <td>72</td>
      <td>96</td>
      <td>88</td>
      <td>1</td>
    </tr>
    <tr>
      <th>423</th>
      <td>pilar</td>
      <td>py</td>
      <td>-9</td>
      <td>-9</td>
      <td>75</td>
      <td>83</td>
      <td>75</td>
      <td>14</td>
    </tr>
    <tr>
      <th>1098</th>
      <td>paucartambo</td>
      <td>pe</td>
      <td>-13</td>
      <td>-13</td>
      <td>66</td>
      <td>24</td>
      <td>40</td>
      <td>3</td>
    </tr>
    <tr>
      <th>7527</th>
      <td>kirillov</td>
      <td>ru</td>
      <td>59</td>
      <td>59</td>
      <td>60</td>
      <td>75</td>
      <td>24</td>
      <td>12</td>
    </tr>
    <tr>
      <th>6478</th>
      <td>wroclaw</td>
      <td>pl</td>
      <td>51</td>
      <td>51</td>
      <td>68</td>
      <td>68</td>
      <td>0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1179</th>
      <td>samfya</td>
      <td>zm</td>
      <td>-11</td>
      <td>-11</td>
      <td>58</td>
      <td>57</td>
      <td>0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>11</th>
      <td>taolanaro</td>
      <td>mg</td>
      <td>-25</td>
      <td>-25</td>
      <td>71</td>
      <td>88</td>
      <td>75</td>
      <td>6</td>
    </tr>
    <tr>
      <th>306</th>
      <td>artigas</td>
      <td>uy</td>
      <td>-30</td>
      <td>-30</td>
      <td>83</td>
      <td>53</td>
      <td>20</td>
      <td>18</td>
    </tr>
    <tr>
      <th>6811</th>
      <td>biskamzha</td>
      <td>ru</td>
      <td>53</td>
      <td>53</td>
      <td>40</td>
      <td>86</td>
      <td>12</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1287</th>
      <td>paita</td>
      <td>pe</td>
      <td>-5</td>
      <td>-5</td>
      <td>73</td>
      <td>64</td>
      <td>0</td>
      <td>13</td>
    </tr>
    <tr>
      <th>5809</th>
      <td>ucluelet</td>
      <td>ca</td>
      <td>48</td>
      <td>48</td>
      <td>59</td>
      <td>82</td>
      <td>75</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
<p>499 rows × 8 columns</p>
</div>




```python
# import datetime
# date = datetime.date.today()
import time
date = time.strftime("%m/%d/%Y")
# print(date)
plt.scatter(samplecity['latitude'],samplecity['temperature'])
plt.title(f"Temperature (F) vs. Latitude {date}")
plt.xlabel("Latitude")
plt.ylabel("Temperature (F)")
plt.style.use('ggplot')
plt.savefig("Temperature.png")
plt.show()
```


![png](output_9_0.png)



```python
# plt.scatter(latitude,humidity)
plt.scatter(samplecity['latitude'], samplecity['humidity'])
plt.title(f"Humidity (%) vs. Latitude {date}")
plt.xlabel("Latitude")
plt.ylabel("Humidity (%)")
plt.style.use('ggplot')
plt.savefig("Humidity.png")
plt.show()
```


![png](output_10_0.png)



```python
# plt.scatter(latitude,cloudy)
plt.scatter(samplecity['latitude'], samplecity['cloudiness'])
plt.title(f"Cloudiness (%) vs. Latitude {date}")
plt.xlabel("Latitude")
plt.ylabel("Cloudiness (%)")
plt.style.use('ggplot')
plt.savefig("Cloudiness.png")
plt.show()
```


![png](output_11_0.png)



```python
# plt.scatter(latitude,windspeed)
plt.scatter(samplecity['latitude'], samplecity['wind_speed'])
plt.title(f"Wind Speed(mph) vs. Latitude {date}")
plt.xlabel("Latitude")
plt.ylabel("Wind Speed(mph)")
plt.style.use('ggplot')
plt.savefig("Wind_Speed.png")
plt.show()
```


![png](output_12_0.png)



```python
# samplecity = samplecity[samplecity.latitude != ""]
#above works to remove blank answers
#Make into CSV
samplecity.to_csv("sampleweather.csv", encoding="utf-8", index=False)
df = pd.read_csv("sampleweather.csv")
df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>country</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>temperature</th>
      <th>humidity</th>
      <th>cloudiness</th>
      <th>wind_speed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>bulawayo</td>
      <td>zw</td>
      <td>-20</td>
      <td>-20</td>
      <td>47</td>
      <td>33</td>
      <td>0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>keuruu</td>
      <td>fi</td>
      <td>62</td>
      <td>62</td>
      <td>48</td>
      <td>100</td>
      <td>0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ahuimanu</td>
      <td>us</td>
      <td>21</td>
      <td>21</td>
      <td>81</td>
      <td>65</td>
      <td>20</td>
      <td>12</td>
    </tr>
    <tr>
      <th>3</th>
      <td>cefalu</td>
      <td>it</td>
      <td>38</td>
      <td>38</td>
      <td>64</td>
      <td>100</td>
      <td>0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>tual</td>
      <td>id</td>
      <td>-5</td>
      <td>-5</td>
      <td>78</td>
      <td>100</td>
      <td>8</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
