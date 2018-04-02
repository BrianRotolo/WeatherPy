

```python
import random
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import openweathermapy as owm
from datetime import datetime
from config import wkey
from config import gkey
from citipy import citipy
import csv
```


```python
#city section
cities = []
while len(cities)<700:
    from random import uniform
    x, y = uniform(-180,180), uniform(-90, 90)
    city = citipy.nearest_city(x,y).city_name
    if city not in cities:
        cities.append(city)
len(cities)
```




    700




```python
#settings
settings = {"units": "imperial", "appid": wkey}

#create df
weather_df =pd.DataFrame(columns = ["City","Country", "Max Temp", "Humidity",
                                    "Cloudiness", "Wind Speed", "Lat","Lng"])
weather_df.head()
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
      <th>City</th>
      <th>Country</th>
      <th>Max Temp</th>
      <th>Humidity</th>
      <th>Cloudiness</th>
      <th>Wind Speed</th>
      <th>Lat</th>
      <th>Lng</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
count = 0
index = 0
errors = 0
for city in cities:
    count = count + 1
    print(f'City Number {count}: {city}' )
    try:
        citynospace = city.replace(" ", "%20")
        print(f'{owm.BASE_URL}weather?q={citynospace}&units=imperial&APPID={0}')
        city_stats = owm.get_current(city, **settings)
        weather_df.set_value(index, "City", city_stats["name"])
        weather_df.set_value(index, "Country", city_stats("sys.country"))
        weather_df.set_value(index, "Max Temp", city_stats("main.temp_max"))
        weather_df.set_value(index, "Humidity", city_stats("main.humidity"))
        weather_df.set_value(index, "Cloudiness", city_stats("clouds.all"))
        weather_df.set_value(index, "Wind Speed", city_stats("wind.speed"))
        weather_df.set_value(index, "Lat", city_stats("coord.lat"))
        weather_df.set_value(index, "Lng", city_stats("coord.lon"))
        index = index + 1
    except Exception as e:
        errors = errors + 1
```

    City Number 1: cape town
    http://api.openweathermap.org/data/2.5/weather?q=cape%20town&units=imperial&APPID=0
    City Number 2: pitangui
    http://api.openweathermap.org/data/2.5/weather?q=pitangui&units=imperial&APPID=0
    City Number 3: saint-francois
    http://api.openweathermap.org/data/2.5/weather?q=saint-francois&units=imperial&APPID=0
    City Number 4: longyearbyen
    http://api.openweathermap.org/data/2.5/weather?q=longyearbyen&units=imperial&APPID=0
    City Number 5: ushuaia
    http://api.openweathermap.org/data/2.5/weather?q=ushuaia&units=imperial&APPID=0
    City Number 6: abnub
    http://api.openweathermap.org/data/2.5/weather?q=abnub&units=imperial&APPID=0
    City Number 7: dikson
    http://api.openweathermap.org/data/2.5/weather?q=dikson&units=imperial&APPID=0
    City Number 8: taolanaro
    http://api.openweathermap.org/data/2.5/weather?q=taolanaro&units=imperial&APPID=0
    City Number 9: mocambique
    http://api.openweathermap.org/data/2.5/weather?q=mocambique&units=imperial&APPID=0
    City Number 10: niquero
    http://api.openweathermap.org/data/2.5/weather?q=niquero&units=imperial&APPID=0
    City Number 11: quatre cocos
    http://api.openweathermap.org/data/2.5/weather?q=quatre%20cocos&units=imperial&APPID=0
    City Number 12: bambous virieux
    http://api.openweathermap.org/data/2.5/weather?q=bambous%20virieux&units=imperial&APPID=0
    City Number 13: barentsburg
    http://api.openweathermap.org/data/2.5/weather?q=barentsburg&units=imperial&APPID=0
    City Number 14: manicore
    http://api.openweathermap.org/data/2.5/weather?q=manicore&units=imperial&APPID=0
    City Number 15: castro
    http://api.openweathermap.org/data/2.5/weather?q=castro&units=imperial&APPID=0
    City Number 16: narsaq
    http://api.openweathermap.org/data/2.5/weather?q=narsaq&units=imperial&APPID=0
    City Number 17: qaanaaq
    http://api.openweathermap.org/data/2.5/weather?q=qaanaaq&units=imperial&APPID=0
    City Number 18: berlevag
    http://api.openweathermap.org/data/2.5/weather?q=berlevag&units=imperial&APPID=0
    City Number 19: hermanus
    http://api.openweathermap.org/data/2.5/weather?q=hermanus&units=imperial&APPID=0
    City Number 20: kutum
    http://api.openweathermap.org/data/2.5/weather?q=kutum&units=imperial&APPID=0
    City Number 21: safwah
    http://api.openweathermap.org/data/2.5/weather?q=safwah&units=imperial&APPID=0
    City Number 22: victoria
    http://api.openweathermap.org/data/2.5/weather?q=victoria&units=imperial&APPID=0
    City Number 23: arraial do cabo
    http://api.openweathermap.org/data/2.5/weather?q=arraial%20do%20cabo&units=imperial&APPID=0
    City Number 24: bay roberts
    http://api.openweathermap.org/data/2.5/weather?q=bay%20roberts&units=imperial&APPID=0
    City Number 25: west bay
    http://api.openweathermap.org/data/2.5/weather?q=west%20bay&units=imperial&APPID=0
    City Number 26: talah
    http://api.openweathermap.org/data/2.5/weather?q=talah&units=imperial&APPID=0
    City Number 27: mezen
    http://api.openweathermap.org/data/2.5/weather?q=mezen&units=imperial&APPID=0
    City Number 28: bathsheba
    http://api.openweathermap.org/data/2.5/weather?q=bathsheba&units=imperial&APPID=0
    City Number 29: port elizabeth
    http://api.openweathermap.org/data/2.5/weather?q=port%20elizabeth&units=imperial&APPID=0
    City Number 30: bredasdorp
    http://api.openweathermap.org/data/2.5/weather?q=bredasdorp&units=imperial&APPID=0
    City Number 31: malartic
    http://api.openweathermap.org/data/2.5/weather?q=malartic&units=imperial&APPID=0
    City Number 32: jaypur
    http://api.openweathermap.org/data/2.5/weather?q=jaypur&units=imperial&APPID=0
    City Number 33: mar del plata
    http://api.openweathermap.org/data/2.5/weather?q=mar%20del%20plata&units=imperial&APPID=0
    City Number 34: jamestown
    http://api.openweathermap.org/data/2.5/weather?q=jamestown&units=imperial&APPID=0
    City Number 35: belushya guba
    http://api.openweathermap.org/data/2.5/weather?q=belushya%20guba&units=imperial&APPID=0
    City Number 36: valparaiso
    http://api.openweathermap.org/data/2.5/weather?q=valparaiso&units=imperial&APPID=0
    City Number 37: albany
    http://api.openweathermap.org/data/2.5/weather?q=albany&units=imperial&APPID=0
    City Number 38: hofn
    http://api.openweathermap.org/data/2.5/weather?q=hofn&units=imperial&APPID=0
    City Number 39: caravelas
    http://api.openweathermap.org/data/2.5/weather?q=caravelas&units=imperial&APPID=0
    City Number 40: mafra
    http://api.openweathermap.org/data/2.5/weather?q=mafra&units=imperial&APPID=0
    City Number 41: ponta do sol
    http://api.openweathermap.org/data/2.5/weather?q=ponta%20do%20sol&units=imperial&APPID=0
    City Number 42: wahran
    http://api.openweathermap.org/data/2.5/weather?q=wahran&units=imperial&APPID=0
    City Number 43: port alfred
    http://api.openweathermap.org/data/2.5/weather?q=port%20alfred&units=imperial&APPID=0
    City Number 44: saint-pierre
    http://api.openweathermap.org/data/2.5/weather?q=saint-pierre&units=imperial&APPID=0
    City Number 45: sisimiut
    http://api.openweathermap.org/data/2.5/weather?q=sisimiut&units=imperial&APPID=0
    City Number 46: maragogi
    http://api.openweathermap.org/data/2.5/weather?q=maragogi&units=imperial&APPID=0
    City Number 47: georgetown
    http://api.openweathermap.org/data/2.5/weather?q=georgetown&units=imperial&APPID=0
    City Number 48: belyy yar
    http://api.openweathermap.org/data/2.5/weather?q=belyy%20yar&units=imperial&APPID=0
    City Number 49: mangan
    http://api.openweathermap.org/data/2.5/weather?q=mangan&units=imperial&APPID=0
    City Number 50: aleksandrov gay
    http://api.openweathermap.org/data/2.5/weather?q=aleksandrov%20gay&units=imperial&APPID=0
    City Number 51: illoqqortoormiut
    http://api.openweathermap.org/data/2.5/weather?q=illoqqortoormiut&units=imperial&APPID=0
    City Number 52: mahajanga
    http://api.openweathermap.org/data/2.5/weather?q=mahajanga&units=imperial&APPID=0
    City Number 53: pimentel
    http://api.openweathermap.org/data/2.5/weather?q=pimentel&units=imperial&APPID=0
    City Number 54: kruisfontein
    http://api.openweathermap.org/data/2.5/weather?q=kruisfontein&units=imperial&APPID=0
    City Number 55: bonavista
    http://api.openweathermap.org/data/2.5/weather?q=bonavista&units=imperial&APPID=0
    City Number 56: grand gaube
    http://api.openweathermap.org/data/2.5/weather?q=grand%20gaube&units=imperial&APPID=0
    City Number 57: sao filipe
    http://api.openweathermap.org/data/2.5/weather?q=sao%20filipe&units=imperial&APPID=0
    City Number 58: vilhena
    http://api.openweathermap.org/data/2.5/weather?q=vilhena&units=imperial&APPID=0
    City Number 59: puerto berrio
    http://api.openweathermap.org/data/2.5/weather?q=puerto%20berrio&units=imperial&APPID=0
    City Number 60: weston
    http://api.openweathermap.org/data/2.5/weather?q=weston&units=imperial&APPID=0
    City Number 61: hithadhoo
    http://api.openweathermap.org/data/2.5/weather?q=hithadhoo&units=imperial&APPID=0
    City Number 62: imbituba
    http://api.openweathermap.org/data/2.5/weather?q=imbituba&units=imperial&APPID=0
    City Number 63: ribeira grande
    http://api.openweathermap.org/data/2.5/weather?q=ribeira%20grande&units=imperial&APPID=0
    City Number 64: carnarvon
    http://api.openweathermap.org/data/2.5/weather?q=carnarvon&units=imperial&APPID=0
    City Number 65: carutapera
    http://api.openweathermap.org/data/2.5/weather?q=carutapera&units=imperial&APPID=0
    City Number 66: olafsvik
    http://api.openweathermap.org/data/2.5/weather?q=olafsvik&units=imperial&APPID=0
    City Number 67: upernavik
    http://api.openweathermap.org/data/2.5/weather?q=upernavik&units=imperial&APPID=0
    City Number 68: touros
    http://api.openweathermap.org/data/2.5/weather?q=touros&units=imperial&APPID=0
    City Number 69: vagur
    http://api.openweathermap.org/data/2.5/weather?q=vagur&units=imperial&APPID=0
    City Number 70: kanata
    http://api.openweathermap.org/data/2.5/weather?q=kanata&units=imperial&APPID=0
    City Number 71: monte alegre
    http://api.openweathermap.org/data/2.5/weather?q=monte%20alegre&units=imperial&APPID=0
    City Number 72: watsa
    http://api.openweathermap.org/data/2.5/weather?q=watsa&units=imperial&APPID=0
    City Number 73: bargal
    http://api.openweathermap.org/data/2.5/weather?q=bargal&units=imperial&APPID=0
    City Number 74: saint anthony
    http://api.openweathermap.org/data/2.5/weather?q=saint%20anthony&units=imperial&APPID=0
    City Number 75: yar-sale
    http://api.openweathermap.org/data/2.5/weather?q=yar-sale&units=imperial&APPID=0
    City Number 76: cap malheureux
    http://api.openweathermap.org/data/2.5/weather?q=cap%20malheureux&units=imperial&APPID=0
    City Number 77: cidreira
    http://api.openweathermap.org/data/2.5/weather?q=cidreira&units=imperial&APPID=0
    City Number 78: nguruka
    http://api.openweathermap.org/data/2.5/weather?q=nguruka&units=imperial&APPID=0
    City Number 79: souillac
    http://api.openweathermap.org/data/2.5/weather?q=souillac&units=imperial&APPID=0
    City Number 80: kozluk
    http://api.openweathermap.org/data/2.5/weather?q=kozluk&units=imperial&APPID=0
    City Number 81: muros
    http://api.openweathermap.org/data/2.5/weather?q=muros&units=imperial&APPID=0
    City Number 82: zyryanskoye
    http://api.openweathermap.org/data/2.5/weather?q=zyryanskoye&units=imperial&APPID=0
    City Number 83: bilma
    http://api.openweathermap.org/data/2.5/weather?q=bilma&units=imperial&APPID=0
    City Number 84: kapoeta
    http://api.openweathermap.org/data/2.5/weather?q=kapoeta&units=imperial&APPID=0
    City Number 85: dawlatabad
    http://api.openweathermap.org/data/2.5/weather?q=dawlatabad&units=imperial&APPID=0
    City Number 86: torbay
    http://api.openweathermap.org/data/2.5/weather?q=torbay&units=imperial&APPID=0
    City Number 87: xuddur
    http://api.openweathermap.org/data/2.5/weather?q=xuddur&units=imperial&APPID=0
    City Number 88: ondo
    http://api.openweathermap.org/data/2.5/weather?q=ondo&units=imperial&APPID=0
    City Number 89: vardo
    http://api.openweathermap.org/data/2.5/weather?q=vardo&units=imperial&APPID=0
    City Number 90: scarborough
    http://api.openweathermap.org/data/2.5/weather?q=scarborough&units=imperial&APPID=0
    City Number 91: hun
    http://api.openweathermap.org/data/2.5/weather?q=hun&units=imperial&APPID=0
    City Number 92: amderma
    http://api.openweathermap.org/data/2.5/weather?q=amderma&units=imperial&APPID=0
    City Number 93: acarau
    http://api.openweathermap.org/data/2.5/weather?q=acarau&units=imperial&APPID=0
    City Number 94: las tablas
    http://api.openweathermap.org/data/2.5/weather?q=las%20tablas&units=imperial&APPID=0
    City Number 95: annau
    http://api.openweathermap.org/data/2.5/weather?q=annau&units=imperial&APPID=0
    City Number 96: grand river south east
    http://api.openweathermap.org/data/2.5/weather?q=grand%20river%20south%20east&units=imperial&APPID=0
    City Number 97: vestmannaeyjar
    http://api.openweathermap.org/data/2.5/weather?q=vestmannaeyjar&units=imperial&APPID=0
    City Number 98: tumannyy
    http://api.openweathermap.org/data/2.5/weather?q=tumannyy&units=imperial&APPID=0
    City Number 99: pozo colorado
    http://api.openweathermap.org/data/2.5/weather?q=pozo%20colorado&units=imperial&APPID=0
    City Number 100: coihaique
    http://api.openweathermap.org/data/2.5/weather?q=coihaique&units=imperial&APPID=0
    City Number 101: nizwa
    http://api.openweathermap.org/data/2.5/weather?q=nizwa&units=imperial&APPID=0
    City Number 102: qax
    http://api.openweathermap.org/data/2.5/weather?q=qax&units=imperial&APPID=0
    City Number 103: saint-philippe
    http://api.openweathermap.org/data/2.5/weather?q=saint-philippe&units=imperial&APPID=0
    City Number 104: sinnamary
    http://api.openweathermap.org/data/2.5/weather?q=sinnamary&units=imperial&APPID=0
    City Number 105: comodoro rivadavia
    http://api.openweathermap.org/data/2.5/weather?q=comodoro%20rivadavia&units=imperial&APPID=0
    City Number 106: chuy
    http://api.openweathermap.org/data/2.5/weather?q=chuy&units=imperial&APPID=0
    City Number 107: vila do maio
    http://api.openweathermap.org/data/2.5/weather?q=vila%20do%20maio&units=imperial&APPID=0
    City Number 108: paris
    http://api.openweathermap.org/data/2.5/weather?q=paris&units=imperial&APPID=0
    City Number 109: andenes
    http://api.openweathermap.org/data/2.5/weather?q=andenes&units=imperial&APPID=0
    City Number 110: moose factory
    http://api.openweathermap.org/data/2.5/weather?q=moose%20factory&units=imperial&APPID=0
    City Number 111: kambove
    http://api.openweathermap.org/data/2.5/weather?q=kambove&units=imperial&APPID=0
    City Number 112: hammerfest
    http://api.openweathermap.org/data/2.5/weather?q=hammerfest&units=imperial&APPID=0
    City Number 113: rocha
    http://api.openweathermap.org/data/2.5/weather?q=rocha&units=imperial&APPID=0
    City Number 114: harper
    http://api.openweathermap.org/data/2.5/weather?q=harper&units=imperial&APPID=0
    City Number 115: paita
    http://api.openweathermap.org/data/2.5/weather?q=paita&units=imperial&APPID=0
    City Number 116: marcona
    http://api.openweathermap.org/data/2.5/weather?q=marcona&units=imperial&APPID=0
    City Number 117: ovalle
    http://api.openweathermap.org/data/2.5/weather?q=ovalle&units=imperial&APPID=0
    City Number 118: mitsamiouli
    http://api.openweathermap.org/data/2.5/weather?q=mitsamiouli&units=imperial&APPID=0
    City Number 119: sioux lookout
    http://api.openweathermap.org/data/2.5/weather?q=sioux%20lookout&units=imperial&APPID=0
    City Number 120: luau
    http://api.openweathermap.org/data/2.5/weather?q=luau&units=imperial&APPID=0
    City Number 121: mitu
    http://api.openweathermap.org/data/2.5/weather?q=mitu&units=imperial&APPID=0
    City Number 122: salalah
    http://api.openweathermap.org/data/2.5/weather?q=salalah&units=imperial&APPID=0
    City Number 123: belmonte
    http://api.openweathermap.org/data/2.5/weather?q=belmonte&units=imperial&APPID=0
    City Number 124: soyo
    http://api.openweathermap.org/data/2.5/weather?q=soyo&units=imperial&APPID=0
    City Number 125: senneterre
    http://api.openweathermap.org/data/2.5/weather?q=senneterre&units=imperial&APPID=0
    City Number 126: lekoni
    http://api.openweathermap.org/data/2.5/weather?q=lekoni&units=imperial&APPID=0
    City Number 127: east london
    http://api.openweathermap.org/data/2.5/weather?q=east%20london&units=imperial&APPID=0
    City Number 128: mahibadhoo
    http://api.openweathermap.org/data/2.5/weather?q=mahibadhoo&units=imperial&APPID=0
    City Number 129: praia da vitoria
    http://api.openweathermap.org/data/2.5/weather?q=praia%20da%20vitoria&units=imperial&APPID=0
    City Number 130: chaman
    http://api.openweathermap.org/data/2.5/weather?q=chaman&units=imperial&APPID=0
    City Number 131: surab
    http://api.openweathermap.org/data/2.5/weather?q=surab&units=imperial&APPID=0
    City Number 132: porto novo
    http://api.openweathermap.org/data/2.5/weather?q=porto%20novo&units=imperial&APPID=0
    City Number 133: malanje
    http://api.openweathermap.org/data/2.5/weather?q=malanje&units=imperial&APPID=0
    City Number 134: consett
    http://api.openweathermap.org/data/2.5/weather?q=consett&units=imperial&APPID=0
    City Number 135: saint-augustin
    http://api.openweathermap.org/data/2.5/weather?q=saint-augustin&units=imperial&APPID=0
    City Number 136: mahebourg
    http://api.openweathermap.org/data/2.5/weather?q=mahebourg&units=imperial&APPID=0
    City Number 137: maceio
    http://api.openweathermap.org/data/2.5/weather?q=maceio&units=imperial&APPID=0
    City Number 138: saint-georges
    http://api.openweathermap.org/data/2.5/weather?q=saint-georges&units=imperial&APPID=0
    City Number 139: almeirim
    http://api.openweathermap.org/data/2.5/weather?q=almeirim&units=imperial&APPID=0
    City Number 140: maarianhamina
    http://api.openweathermap.org/data/2.5/weather?q=maarianhamina&units=imperial&APPID=0
    City Number 141: khandbari
    http://api.openweathermap.org/data/2.5/weather?q=khandbari&units=imperial&APPID=0
    City Number 142: henties bay
    http://api.openweathermap.org/data/2.5/weather?q=henties%20bay&units=imperial&APPID=0
    City Number 143: ndele
    http://api.openweathermap.org/data/2.5/weather?q=ndele&units=imperial&APPID=0
    City Number 144: hualmay
    http://api.openweathermap.org/data/2.5/weather?q=hualmay&units=imperial&APPID=0
    City Number 145: tabou
    http://api.openweathermap.org/data/2.5/weather?q=tabou&units=imperial&APPID=0
    City Number 146: adrar
    http://api.openweathermap.org/data/2.5/weather?q=adrar&units=imperial&APPID=0
    City Number 147: porto belo
    http://api.openweathermap.org/data/2.5/weather?q=porto%20belo&units=imperial&APPID=0
    City Number 148: ilulissat
    http://api.openweathermap.org/data/2.5/weather?q=ilulissat&units=imperial&APPID=0
    City Number 149: kurtalan
    http://api.openweathermap.org/data/2.5/weather?q=kurtalan&units=imperial&APPID=0
    City Number 150: taylorville
    http://api.openweathermap.org/data/2.5/weather?q=taylorville&units=imperial&APPID=0
    City Number 151: grindavik
    http://api.openweathermap.org/data/2.5/weather?q=grindavik&units=imperial&APPID=0
    City Number 152: kovylkino
    http://api.openweathermap.org/data/2.5/weather?q=kovylkino&units=imperial&APPID=0
    City Number 153: punta arenas
    http://api.openweathermap.org/data/2.5/weather?q=punta%20arenas&units=imperial&APPID=0
    City Number 154: tasiilaq
    http://api.openweathermap.org/data/2.5/weather?q=tasiilaq&units=imperial&APPID=0
    City Number 155: ouadda
    http://api.openweathermap.org/data/2.5/weather?q=ouadda&units=imperial&APPID=0
    City Number 156: mount pleasant
    http://api.openweathermap.org/data/2.5/weather?q=mount%20pleasant&units=imperial&APPID=0
    City Number 157: busselton
    http://api.openweathermap.org/data/2.5/weather?q=busselton&units=imperial&APPID=0
    City Number 158: ancud
    http://api.openweathermap.org/data/2.5/weather?q=ancud&units=imperial&APPID=0
    City Number 159: korla
    http://api.openweathermap.org/data/2.5/weather?q=korla&units=imperial&APPID=0
    City Number 160: gorakhpur
    http://api.openweathermap.org/data/2.5/weather?q=gorakhpur&units=imperial&APPID=0
    City Number 161: codrington
    http://api.openweathermap.org/data/2.5/weather?q=codrington&units=imperial&APPID=0
    City Number 162: karasburg
    http://api.openweathermap.org/data/2.5/weather?q=karasburg&units=imperial&APPID=0
    City Number 163: khirkiya
    http://api.openweathermap.org/data/2.5/weather?q=khirkiya&units=imperial&APPID=0
    City Number 164: sawakin
    http://api.openweathermap.org/data/2.5/weather?q=sawakin&units=imperial&APPID=0
    City Number 165: luderitz
    http://api.openweathermap.org/data/2.5/weather?q=luderitz&units=imperial&APPID=0
    City Number 166: bahraich
    http://api.openweathermap.org/data/2.5/weather?q=bahraich&units=imperial&APPID=0
    City Number 167: kyzyl-suu
    http://api.openweathermap.org/data/2.5/weather?q=kyzyl-suu&units=imperial&APPID=0
    City Number 168: cayenne
    http://api.openweathermap.org/data/2.5/weather?q=cayenne&units=imperial&APPID=0
    City Number 169: robertsport
    http://api.openweathermap.org/data/2.5/weather?q=robertsport&units=imperial&APPID=0
    City Number 170: jalu
    http://api.openweathermap.org/data/2.5/weather?q=jalu&units=imperial&APPID=0
    City Number 171: toliary
    http://api.openweathermap.org/data/2.5/weather?q=toliary&units=imperial&APPID=0
    City Number 172: sovetskiy
    http://api.openweathermap.org/data/2.5/weather?q=sovetskiy&units=imperial&APPID=0
    City Number 173: sohag
    http://api.openweathermap.org/data/2.5/weather?q=sohag&units=imperial&APPID=0
    City Number 174: hambantota
    http://api.openweathermap.org/data/2.5/weather?q=hambantota&units=imperial&APPID=0
    City Number 175: badou
    http://api.openweathermap.org/data/2.5/weather?q=badou&units=imperial&APPID=0
    City Number 176: chicama
    http://api.openweathermap.org/data/2.5/weather?q=chicama&units=imperial&APPID=0
    City Number 177: alta floresta
    http://api.openweathermap.org/data/2.5/weather?q=alta%20floresta&units=imperial&APPID=0
    City Number 178: benguela
    http://api.openweathermap.org/data/2.5/weather?q=benguela&units=imperial&APPID=0
    City Number 179: thinadhoo
    http://api.openweathermap.org/data/2.5/weather?q=thinadhoo&units=imperial&APPID=0
    City Number 180: grand-lahou
    http://api.openweathermap.org/data/2.5/weather?q=grand-lahou&units=imperial&APPID=0
    City Number 181: bengkulu
    http://api.openweathermap.org/data/2.5/weather?q=bengkulu&units=imperial&APPID=0
    City Number 182: teguldet
    http://api.openweathermap.org/data/2.5/weather?q=teguldet&units=imperial&APPID=0
    City Number 183: nandrin
    http://api.openweathermap.org/data/2.5/weather?q=nandrin&units=imperial&APPID=0
    City Number 184: bereda
    http://api.openweathermap.org/data/2.5/weather?q=bereda&units=imperial&APPID=0
    City Number 185: pergamino
    http://api.openweathermap.org/data/2.5/weather?q=pergamino&units=imperial&APPID=0
    City Number 186: west mifflin
    http://api.openweathermap.org/data/2.5/weather?q=west%20mifflin&units=imperial&APPID=0
    City Number 187: artvin
    http://api.openweathermap.org/data/2.5/weather?q=artvin&units=imperial&APPID=0
    City Number 188: kouroussa
    http://api.openweathermap.org/data/2.5/weather?q=kouroussa&units=imperial&APPID=0
    City Number 189: araouane
    http://api.openweathermap.org/data/2.5/weather?q=araouane&units=imperial&APPID=0
    City Number 190: salinopolis
    http://api.openweathermap.org/data/2.5/weather?q=salinopolis&units=imperial&APPID=0
    City Number 191: alappuzha
    http://api.openweathermap.org/data/2.5/weather?q=alappuzha&units=imperial&APPID=0
    City Number 192: ayagoz
    http://api.openweathermap.org/data/2.5/weather?q=ayagoz&units=imperial&APPID=0
    City Number 193: richards bay
    http://api.openweathermap.org/data/2.5/weather?q=richards%20bay&units=imperial&APPID=0
    City Number 194: kuminskiy
    http://api.openweathermap.org/data/2.5/weather?q=kuminskiy&units=imperial&APPID=0
    City Number 195: carbonia
    http://api.openweathermap.org/data/2.5/weather?q=carbonia&units=imperial&APPID=0
    City Number 196: saldanha
    http://api.openweathermap.org/data/2.5/weather?q=saldanha&units=imperial&APPID=0
    City Number 197: ambilobe
    http://api.openweathermap.org/data/2.5/weather?q=ambilobe&units=imperial&APPID=0
    City Number 198: mahadday weyne
    http://api.openweathermap.org/data/2.5/weather?q=mahadday%20weyne&units=imperial&APPID=0
    City Number 199: clyde river
    http://api.openweathermap.org/data/2.5/weather?q=clyde%20river&units=imperial&APPID=0
    City Number 200: sao joao da barra
    http://api.openweathermap.org/data/2.5/weather?q=sao%20joao%20da%20barra&units=imperial&APPID=0
    City Number 201: roanoke
    http://api.openweathermap.org/data/2.5/weather?q=roanoke&units=imperial&APPID=0
    City Number 202: georgiyevskoye
    http://api.openweathermap.org/data/2.5/weather?q=georgiyevskoye&units=imperial&APPID=0
    City Number 203: lemesos
    http://api.openweathermap.org/data/2.5/weather?q=lemesos&units=imperial&APPID=0
    City Number 204: mizan teferi
    http://api.openweathermap.org/data/2.5/weather?q=mizan%20teferi&units=imperial&APPID=0
    City Number 205: kemijarvi
    http://api.openweathermap.org/data/2.5/weather?q=kemijarvi&units=imperial&APPID=0
    City Number 206: tefe
    http://api.openweathermap.org/data/2.5/weather?q=tefe&units=imperial&APPID=0
    City Number 207: mullaitivu
    http://api.openweathermap.org/data/2.5/weather?q=mullaitivu&units=imperial&APPID=0
    City Number 208: shache
    http://api.openweathermap.org/data/2.5/weather?q=shache&units=imperial&APPID=0
    City Number 209: margate
    http://api.openweathermap.org/data/2.5/weather?q=margate&units=imperial&APPID=0
    City Number 210: namibe
    http://api.openweathermap.org/data/2.5/weather?q=namibe&units=imperial&APPID=0
    City Number 211: inderborskiy
    http://api.openweathermap.org/data/2.5/weather?q=inderborskiy&units=imperial&APPID=0
    City Number 212: mrirt
    http://api.openweathermap.org/data/2.5/weather?q=mrirt&units=imperial&APPID=0
    City Number 213: roscommon
    http://api.openweathermap.org/data/2.5/weather?q=roscommon&units=imperial&APPID=0
    City Number 214: aquiraz
    http://api.openweathermap.org/data/2.5/weather?q=aquiraz&units=imperial&APPID=0
    City Number 215: talnakh
    http://api.openweathermap.org/data/2.5/weather?q=talnakh&units=imperial&APPID=0
    City Number 216: algiers
    http://api.openweathermap.org/data/2.5/weather?q=algiers&units=imperial&APPID=0
    City Number 217: touba
    http://api.openweathermap.org/data/2.5/weather?q=touba&units=imperial&APPID=0
    City Number 218: tsihombe
    http://api.openweathermap.org/data/2.5/weather?q=tsihombe&units=imperial&APPID=0
    City Number 219: cockburn town
    http://api.openweathermap.org/data/2.5/weather?q=cockburn%20town&units=imperial&APPID=0
    City Number 220: san cosme y damian
    http://api.openweathermap.org/data/2.5/weather?q=san%20cosme%20y%20damian&units=imperial&APPID=0
    City Number 221: la rioja
    http://api.openweathermap.org/data/2.5/weather?q=la%20rioja&units=imperial&APPID=0
    City Number 222: kanadey
    http://api.openweathermap.org/data/2.5/weather?q=kanadey&units=imperial&APPID=0
    City Number 223: takoradi
    http://api.openweathermap.org/data/2.5/weather?q=takoradi&units=imperial&APPID=0
    City Number 224: antofagasta
    http://api.openweathermap.org/data/2.5/weather?q=antofagasta&units=imperial&APPID=0
    City Number 225: susangerd
    http://api.openweathermap.org/data/2.5/weather?q=susangerd&units=imperial&APPID=0
    City Number 226: nantucket
    http://api.openweathermap.org/data/2.5/weather?q=nantucket&units=imperial&APPID=0
    City Number 227: labytnangi
    http://api.openweathermap.org/data/2.5/weather?q=labytnangi&units=imperial&APPID=0
    City Number 228: kisanga
    http://api.openweathermap.org/data/2.5/weather?q=kisanga&units=imperial&APPID=0
    City Number 229: manacor
    http://api.openweathermap.org/data/2.5/weather?q=manacor&units=imperial&APPID=0
    City Number 230: kajaani
    http://api.openweathermap.org/data/2.5/weather?q=kajaani&units=imperial&APPID=0
    City Number 231: maltahohe
    http://api.openweathermap.org/data/2.5/weather?q=maltahohe&units=imperial&APPID=0
    City Number 232: irbit
    http://api.openweathermap.org/data/2.5/weather?q=irbit&units=imperial&APPID=0
    City Number 233: attawapiskat
    http://api.openweathermap.org/data/2.5/weather?q=attawapiskat&units=imperial&APPID=0
    City Number 234: abalak
    http://api.openweathermap.org/data/2.5/weather?q=abalak&units=imperial&APPID=0
    City Number 235: kulhudhuffushi
    http://api.openweathermap.org/data/2.5/weather?q=kulhudhuffushi&units=imperial&APPID=0
    City Number 236: ekibastuz
    http://api.openweathermap.org/data/2.5/weather?q=ekibastuz&units=imperial&APPID=0
    City Number 237: santa marta
    http://api.openweathermap.org/data/2.5/weather?q=santa%20marta&units=imperial&APPID=0
    City Number 238: puerto leguizamo
    http://api.openweathermap.org/data/2.5/weather?q=puerto%20leguizamo&units=imperial&APPID=0
    City Number 239: kindu
    http://api.openweathermap.org/data/2.5/weather?q=kindu&units=imperial&APPID=0
    City Number 240: bulaevo
    http://api.openweathermap.org/data/2.5/weather?q=bulaevo&units=imperial&APPID=0
    City Number 241: waterloo
    http://api.openweathermap.org/data/2.5/weather?q=waterloo&units=imperial&APPID=0
    City Number 242: weymouth
    http://api.openweathermap.org/data/2.5/weather?q=weymouth&units=imperial&APPID=0
    City Number 243: chapais
    http://api.openweathermap.org/data/2.5/weather?q=chapais&units=imperial&APPID=0
    City Number 244: ciudad bolivar
    http://api.openweathermap.org/data/2.5/weather?q=ciudad%20bolivar&units=imperial&APPID=0
    City Number 245: santiago del estero
    http://api.openweathermap.org/data/2.5/weather?q=santiago%20del%20estero&units=imperial&APPID=0
    City Number 246: ferme-neuve
    http://api.openweathermap.org/data/2.5/weather?q=ferme-neuve&units=imperial&APPID=0
    City Number 247: oranjemund
    http://api.openweathermap.org/data/2.5/weather?q=oranjemund&units=imperial&APPID=0
    City Number 248: husavik
    http://api.openweathermap.org/data/2.5/weather?q=husavik&units=imperial&APPID=0
    City Number 249: nanortalik
    http://api.openweathermap.org/data/2.5/weather?q=nanortalik&units=imperial&APPID=0
    City Number 250: rio gallegos
    http://api.openweathermap.org/data/2.5/weather?q=rio%20gallegos&units=imperial&APPID=0
    City Number 251: itarema
    http://api.openweathermap.org/data/2.5/weather?q=itarema&units=imperial&APPID=0
    City Number 252: capitan bado
    http://api.openweathermap.org/data/2.5/weather?q=capitan%20bado&units=imperial&APPID=0
    City Number 253: lakota
    http://api.openweathermap.org/data/2.5/weather?q=lakota&units=imperial&APPID=0
    City Number 254: richard toll
    http://api.openweathermap.org/data/2.5/weather?q=richard%20toll&units=imperial&APPID=0
    City Number 255: hobyo
    http://api.openweathermap.org/data/2.5/weather?q=hobyo&units=imperial&APPID=0
    City Number 256: shelburne
    http://api.openweathermap.org/data/2.5/weather?q=shelburne&units=imperial&APPID=0
    City Number 257: gasa
    http://api.openweathermap.org/data/2.5/weather?q=gasa&units=imperial&APPID=0
    City Number 258: raichur
    http://api.openweathermap.org/data/2.5/weather?q=raichur&units=imperial&APPID=0
    City Number 259: saint george
    http://api.openweathermap.org/data/2.5/weather?q=saint%20george&units=imperial&APPID=0
    City Number 260: vila franca do campo
    http://api.openweathermap.org/data/2.5/weather?q=vila%20franca%20do%20campo&units=imperial&APPID=0
    City Number 261: maniitsoq
    http://api.openweathermap.org/data/2.5/weather?q=maniitsoq&units=imperial&APPID=0
    City Number 262: nuuk
    http://api.openweathermap.org/data/2.5/weather?q=nuuk&units=imperial&APPID=0
    City Number 263: santana do livramento
    http://api.openweathermap.org/data/2.5/weather?q=santana%20do%20livramento&units=imperial&APPID=0
    City Number 264: ambodifototra
    http://api.openweathermap.org/data/2.5/weather?q=ambodifototra&units=imperial&APPID=0
    City Number 265: blonie
    http://api.openweathermap.org/data/2.5/weather?q=blonie&units=imperial&APPID=0
    City Number 266: bialystok
    http://api.openweathermap.org/data/2.5/weather?q=bialystok&units=imperial&APPID=0
    City Number 267: olinda
    http://api.openweathermap.org/data/2.5/weather?q=olinda&units=imperial&APPID=0
    City Number 268: tawkar
    http://api.openweathermap.org/data/2.5/weather?q=tawkar&units=imperial&APPID=0
    City Number 269: pangnirtung
    http://api.openweathermap.org/data/2.5/weather?q=pangnirtung&units=imperial&APPID=0
    City Number 270: porto santo
    http://api.openweathermap.org/data/2.5/weather?q=porto%20santo&units=imperial&APPID=0
    City Number 271: sucha beskidzka
    http://api.openweathermap.org/data/2.5/weather?q=sucha%20beskidzka&units=imperial&APPID=0
    City Number 272: felipe carrillo puerto
    http://api.openweathermap.org/data/2.5/weather?q=felipe%20carrillo%20puerto&units=imperial&APPID=0
    City Number 273: birao
    http://api.openweathermap.org/data/2.5/weather?q=birao&units=imperial&APPID=0
    City Number 274: elat
    http://api.openweathermap.org/data/2.5/weather?q=elat&units=imperial&APPID=0
    City Number 275: brigantine
    http://api.openweathermap.org/data/2.5/weather?q=brigantine&units=imperial&APPID=0
    City Number 276: marawi
    http://api.openweathermap.org/data/2.5/weather?q=marawi&units=imperial&APPID=0
    City Number 277: karasjok
    http://api.openweathermap.org/data/2.5/weather?q=karasjok&units=imperial&APPID=0
    City Number 278: raudeberg
    http://api.openweathermap.org/data/2.5/weather?q=raudeberg&units=imperial&APPID=0
    City Number 279: lillehammer
    http://api.openweathermap.org/data/2.5/weather?q=lillehammer&units=imperial&APPID=0
    City Number 280: damara
    http://api.openweathermap.org/data/2.5/weather?q=damara&units=imperial&APPID=0
    City Number 281: bolobo
    http://api.openweathermap.org/data/2.5/weather?q=bolobo&units=imperial&APPID=0
    City Number 282: aswan
    http://api.openweathermap.org/data/2.5/weather?q=aswan&units=imperial&APPID=0
    City Number 283: shetpe
    http://api.openweathermap.org/data/2.5/weather?q=shetpe&units=imperial&APPID=0
    City Number 284: kasama
    http://api.openweathermap.org/data/2.5/weather?q=kasama&units=imperial&APPID=0
    City Number 285: biu
    http://api.openweathermap.org/data/2.5/weather?q=biu&units=imperial&APPID=0
    City Number 286: tome-acu
    http://api.openweathermap.org/data/2.5/weather?q=tome-acu&units=imperial&APPID=0
    City Number 287: lebu
    http://api.openweathermap.org/data/2.5/weather?q=lebu&units=imperial&APPID=0
    City Number 288: conde
    http://api.openweathermap.org/data/2.5/weather?q=conde&units=imperial&APPID=0
    City Number 289: maralal
    http://api.openweathermap.org/data/2.5/weather?q=maralal&units=imperial&APPID=0
    City Number 290: uwayl
    http://api.openweathermap.org/data/2.5/weather?q=uwayl&units=imperial&APPID=0
    City Number 291: havre-saint-pierre
    http://api.openweathermap.org/data/2.5/weather?q=havre-saint-pierre&units=imperial&APPID=0
    City Number 292: malwan
    http://api.openweathermap.org/data/2.5/weather?q=malwan&units=imperial&APPID=0
    City Number 293: ostrovnoy
    http://api.openweathermap.org/data/2.5/weather?q=ostrovnoy&units=imperial&APPID=0
    City Number 294: yirol
    http://api.openweathermap.org/data/2.5/weather?q=yirol&units=imperial&APPID=0
    City Number 295: plettenberg bay
    http://api.openweathermap.org/data/2.5/weather?q=plettenberg%20bay&units=imperial&APPID=0
    City Number 296: shieli
    http://api.openweathermap.org/data/2.5/weather?q=shieli&units=imperial&APPID=0
    City Number 297: awbari
    http://api.openweathermap.org/data/2.5/weather?q=awbari&units=imperial&APPID=0
    City Number 298: turbat
    http://api.openweathermap.org/data/2.5/weather?q=turbat&units=imperial&APPID=0
    City Number 299: umzimvubu
    http://api.openweathermap.org/data/2.5/weather?q=umzimvubu&units=imperial&APPID=0
    City Number 300: mansa
    http://api.openweathermap.org/data/2.5/weather?q=mansa&units=imperial&APPID=0
    City Number 301: amapa
    http://api.openweathermap.org/data/2.5/weather?q=amapa&units=imperial&APPID=0
    City Number 302: kolyvan
    http://api.openweathermap.org/data/2.5/weather?q=kolyvan&units=imperial&APPID=0
    City Number 303: oswego
    http://api.openweathermap.org/data/2.5/weather?q=oswego&units=imperial&APPID=0
    City Number 304: emba
    http://api.openweathermap.org/data/2.5/weather?q=emba&units=imperial&APPID=0
    City Number 305: hvammstangi
    http://api.openweathermap.org/data/2.5/weather?q=hvammstangi&units=imperial&APPID=0
    City Number 306: port-gentil
    http://api.openweathermap.org/data/2.5/weather?q=port-gentil&units=imperial&APPID=0
    City Number 307: necochea
    http://api.openweathermap.org/data/2.5/weather?q=necochea&units=imperial&APPID=0
    City Number 308: dzhusaly
    http://api.openweathermap.org/data/2.5/weather?q=dzhusaly&units=imperial&APPID=0
    City Number 309: borama
    http://api.openweathermap.org/data/2.5/weather?q=borama&units=imperial&APPID=0
    City Number 310: maykor
    http://api.openweathermap.org/data/2.5/weather?q=maykor&units=imperial&APPID=0
    City Number 311: matagami
    http://api.openweathermap.org/data/2.5/weather?q=matagami&units=imperial&APPID=0
    City Number 312: cururupu
    http://api.openweathermap.org/data/2.5/weather?q=cururupu&units=imperial&APPID=0
    City Number 313: iqaluit
    http://api.openweathermap.org/data/2.5/weather?q=iqaluit&units=imperial&APPID=0
    City Number 314: simoes
    http://api.openweathermap.org/data/2.5/weather?q=simoes&units=imperial&APPID=0
    City Number 315: el alto
    http://api.openweathermap.org/data/2.5/weather?q=el%20alto&units=imperial&APPID=0
    City Number 316: taltal
    http://api.openweathermap.org/data/2.5/weather?q=taltal&units=imperial&APPID=0
    City Number 317: westport
    http://api.openweathermap.org/data/2.5/weather?q=westport&units=imperial&APPID=0
    City Number 318: tullow
    http://api.openweathermap.org/data/2.5/weather?q=tullow&units=imperial&APPID=0
    City Number 319: esil
    http://api.openweathermap.org/data/2.5/weather?q=esil&units=imperial&APPID=0
    City Number 320: kristiinankaupunki
    http://api.openweathermap.org/data/2.5/weather?q=kristiinankaupunki&units=imperial&APPID=0
    City Number 321: chililabombwe
    http://api.openweathermap.org/data/2.5/weather?q=chililabombwe&units=imperial&APPID=0
    City Number 322: kangaatsiaq
    http://api.openweathermap.org/data/2.5/weather?q=kangaatsiaq&units=imperial&APPID=0
    City Number 323: anzio
    http://api.openweathermap.org/data/2.5/weather?q=anzio&units=imperial&APPID=0
    City Number 324: chanasma
    http://api.openweathermap.org/data/2.5/weather?q=chanasma&units=imperial&APPID=0
    City Number 325: vila velha
    http://api.openweathermap.org/data/2.5/weather?q=vila%20velha&units=imperial&APPID=0
    City Number 326: kavaratti
    http://api.openweathermap.org/data/2.5/weather?q=kavaratti&units=imperial&APPID=0
    City Number 327: porbandar
    http://api.openweathermap.org/data/2.5/weather?q=porbandar&units=imperial&APPID=0
    City Number 328: remanso
    http://api.openweathermap.org/data/2.5/weather?q=remanso&units=imperial&APPID=0
    City Number 329: yenotayevka
    http://api.openweathermap.org/data/2.5/weather?q=yenotayevka&units=imperial&APPID=0
    City Number 330: vorukh
    http://api.openweathermap.org/data/2.5/weather?q=vorukh&units=imperial&APPID=0
    City Number 331: walvis bay
    http://api.openweathermap.org/data/2.5/weather?q=walvis%20bay&units=imperial&APPID=0
    City Number 332: zonguldak
    http://api.openweathermap.org/data/2.5/weather?q=zonguldak&units=imperial&APPID=0
    City Number 333: monte azul
    http://api.openweathermap.org/data/2.5/weather?q=monte%20azul&units=imperial&APPID=0
    City Number 334: quelimane
    http://api.openweathermap.org/data/2.5/weather?q=quelimane&units=imperial&APPID=0
    City Number 335: gat
    http://api.openweathermap.org/data/2.5/weather?q=gat&units=imperial&APPID=0
    City Number 336: hamilton
    http://api.openweathermap.org/data/2.5/weather?q=hamilton&units=imperial&APPID=0
    City Number 337: conakry
    http://api.openweathermap.org/data/2.5/weather?q=conakry&units=imperial&APPID=0
    City Number 338: morant bay
    http://api.openweathermap.org/data/2.5/weather?q=morant%20bay&units=imperial&APPID=0
    City Number 339: loanda
    http://api.openweathermap.org/data/2.5/weather?q=loanda&units=imperial&APPID=0
    City Number 340: abu samrah
    http://api.openweathermap.org/data/2.5/weather?q=abu%20samrah&units=imperial&APPID=0
    City Number 341: pedra azul
    http://api.openweathermap.org/data/2.5/weather?q=pedra%20azul&units=imperial&APPID=0
    City Number 342: tahoua
    http://api.openweathermap.org/data/2.5/weather?q=tahoua&units=imperial&APPID=0
    City Number 343: umba
    http://api.openweathermap.org/data/2.5/weather?q=umba&units=imperial&APPID=0
    City Number 344: jumla
    http://api.openweathermap.org/data/2.5/weather?q=jumla&units=imperial&APPID=0
    City Number 345: barao de melgaco
    http://api.openweathermap.org/data/2.5/weather?q=barao%20de%20melgaco&units=imperial&APPID=0
    City Number 346: kyshtovka
    http://api.openweathermap.org/data/2.5/weather?q=kyshtovka&units=imperial&APPID=0
    City Number 347: derzhavinsk
    http://api.openweathermap.org/data/2.5/weather?q=derzhavinsk&units=imperial&APPID=0
    City Number 348: blyth
    http://api.openweathermap.org/data/2.5/weather?q=blyth&units=imperial&APPID=0
    City Number 349: aripuana
    http://api.openweathermap.org/data/2.5/weather?q=aripuana&units=imperial&APPID=0
    City Number 350: rosetta
    http://api.openweathermap.org/data/2.5/weather?q=rosetta&units=imperial&APPID=0
    City Number 351: bandarbeyla
    http://api.openweathermap.org/data/2.5/weather?q=bandarbeyla&units=imperial&APPID=0
    City Number 352: handia
    http://api.openweathermap.org/data/2.5/weather?q=handia&units=imperial&APPID=0
    City Number 353: camopi
    http://api.openweathermap.org/data/2.5/weather?q=camopi&units=imperial&APPID=0
    City Number 354: sept-iles
    http://api.openweathermap.org/data/2.5/weather?q=sept-iles&units=imperial&APPID=0
    City Number 355: valdivia
    http://api.openweathermap.org/data/2.5/weather?q=valdivia&units=imperial&APPID=0
    City Number 356: atasu
    http://api.openweathermap.org/data/2.5/weather?q=atasu&units=imperial&APPID=0
    City Number 357: mehamn
    http://api.openweathermap.org/data/2.5/weather?q=mehamn&units=imperial&APPID=0
    City Number 358: mandera
    http://api.openweathermap.org/data/2.5/weather?q=mandera&units=imperial&APPID=0
    City Number 359: isla mujeres
    http://api.openweathermap.org/data/2.5/weather?q=isla%20mujeres&units=imperial&APPID=0
    City Number 360: lupiro
    http://api.openweathermap.org/data/2.5/weather?q=lupiro&units=imperial&APPID=0
    City Number 361: porangatu
    http://api.openweathermap.org/data/2.5/weather?q=porangatu&units=imperial&APPID=0
    City Number 362: moen
    http://api.openweathermap.org/data/2.5/weather?q=moen&units=imperial&APPID=0
    City Number 363: gaoua
    http://api.openweathermap.org/data/2.5/weather?q=gaoua&units=imperial&APPID=0
    City Number 364: yurga
    http://api.openweathermap.org/data/2.5/weather?q=yurga&units=imperial&APPID=0
    City Number 365: baghdad
    http://api.openweathermap.org/data/2.5/weather?q=baghdad&units=imperial&APPID=0
    City Number 366: coquimbo
    http://api.openweathermap.org/data/2.5/weather?q=coquimbo&units=imperial&APPID=0
    City Number 367: farafangana
    http://api.openweathermap.org/data/2.5/weather?q=farafangana&units=imperial&APPID=0
    City Number 368: dingle
    http://api.openweathermap.org/data/2.5/weather?q=dingle&units=imperial&APPID=0
    City Number 369: krasnoselkup
    http://api.openweathermap.org/data/2.5/weather?q=krasnoselkup&units=imperial&APPID=0
    City Number 370: mukhtolovo
    http://api.openweathermap.org/data/2.5/weather?q=mukhtolovo&units=imperial&APPID=0
    City Number 371: chambas
    http://api.openweathermap.org/data/2.5/weather?q=chambas&units=imperial&APPID=0
    City Number 372: havelock
    http://api.openweathermap.org/data/2.5/weather?q=havelock&units=imperial&APPID=0
    City Number 373: detmold
    http://api.openweathermap.org/data/2.5/weather?q=detmold&units=imperial&APPID=0
    City Number 374: kudahuvadhoo
    http://api.openweathermap.org/data/2.5/weather?q=kudahuvadhoo&units=imperial&APPID=0
    City Number 375: chilca
    http://api.openweathermap.org/data/2.5/weather?q=chilca&units=imperial&APPID=0
    City Number 376: upington
    http://api.openweathermap.org/data/2.5/weather?q=upington&units=imperial&APPID=0
    City Number 377: kilindoni
    http://api.openweathermap.org/data/2.5/weather?q=kilindoni&units=imperial&APPID=0
    City Number 378: lasa
    http://api.openweathermap.org/data/2.5/weather?q=lasa&units=imperial&APPID=0
    City Number 379: paamiut
    http://api.openweathermap.org/data/2.5/weather?q=paamiut&units=imperial&APPID=0
    City Number 380: skerries
    http://api.openweathermap.org/data/2.5/weather?q=skerries&units=imperial&APPID=0
    City Number 381: ardino
    http://api.openweathermap.org/data/2.5/weather?q=ardino&units=imperial&APPID=0
    City Number 382: ribas do rio pardo
    http://api.openweathermap.org/data/2.5/weather?q=ribas%20do%20rio%20pardo&units=imperial&APPID=0
    City Number 383: clarence town
    http://api.openweathermap.org/data/2.5/weather?q=clarence%20town&units=imperial&APPID=0
    City Number 384: kiruna
    http://api.openweathermap.org/data/2.5/weather?q=kiruna&units=imperial&APPID=0
    City Number 385: hurghada
    http://api.openweathermap.org/data/2.5/weather?q=hurghada&units=imperial&APPID=0
    City Number 386: marsa matruh
    http://api.openweathermap.org/data/2.5/weather?q=marsa%20matruh&units=imperial&APPID=0
    City Number 387: guajara-mirim
    http://api.openweathermap.org/data/2.5/weather?q=guajara-mirim&units=imperial&APPID=0
    City Number 388: bahia honda
    http://api.openweathermap.org/data/2.5/weather?q=bahia%20honda&units=imperial&APPID=0
    City Number 389: general roca
    http://api.openweathermap.org/data/2.5/weather?q=general%20roca&units=imperial&APPID=0
    City Number 390: goderich
    http://api.openweathermap.org/data/2.5/weather?q=goderich&units=imperial&APPID=0
    City Number 391: mattru
    http://api.openweathermap.org/data/2.5/weather?q=mattru&units=imperial&APPID=0
    City Number 392: morondava
    http://api.openweathermap.org/data/2.5/weather?q=morondava&units=imperial&APPID=0
    City Number 393: dabra
    http://api.openweathermap.org/data/2.5/weather?q=dabra&units=imperial&APPID=0
    City Number 394: boende
    http://api.openweathermap.org/data/2.5/weather?q=boende&units=imperial&APPID=0
    City Number 395: mayumba
    http://api.openweathermap.org/data/2.5/weather?q=mayumba&units=imperial&APPID=0
    City Number 396: gorey
    http://api.openweathermap.org/data/2.5/weather?q=gorey&units=imperial&APPID=0
    City Number 397: geraldton
    http://api.openweathermap.org/data/2.5/weather?q=geraldton&units=imperial&APPID=0
    City Number 398: americus
    http://api.openweathermap.org/data/2.5/weather?q=americus&units=imperial&APPID=0
    City Number 399: nokha
    http://api.openweathermap.org/data/2.5/weather?q=nokha&units=imperial&APPID=0
    City Number 400: nouadhibou
    http://api.openweathermap.org/data/2.5/weather?q=nouadhibou&units=imperial&APPID=0
    City Number 401: kaka
    http://api.openweathermap.org/data/2.5/weather?q=kaka&units=imperial&APPID=0
    City Number 402: qeshm
    http://api.openweathermap.org/data/2.5/weather?q=qeshm&units=imperial&APPID=0
    City Number 403: sur
    http://api.openweathermap.org/data/2.5/weather?q=sur&units=imperial&APPID=0
    City Number 404: callaway
    http://api.openweathermap.org/data/2.5/weather?q=callaway&units=imperial&APPID=0
    City Number 405: ravar
    http://api.openweathermap.org/data/2.5/weather?q=ravar&units=imperial&APPID=0
    City Number 406: buraydah
    http://api.openweathermap.org/data/2.5/weather?q=buraydah&units=imperial&APPID=0
    City Number 407: sao sebastiao
    http://api.openweathermap.org/data/2.5/weather?q=sao%20sebastiao&units=imperial&APPID=0
    City Number 408: groningen
    http://api.openweathermap.org/data/2.5/weather?q=groningen&units=imperial&APPID=0
    City Number 409: thompson
    http://api.openweathermap.org/data/2.5/weather?q=thompson&units=imperial&APPID=0
    City Number 410: qaqortoq
    http://api.openweathermap.org/data/2.5/weather?q=qaqortoq&units=imperial&APPID=0
    City Number 411: laukaa
    http://api.openweathermap.org/data/2.5/weather?q=laukaa&units=imperial&APPID=0
    City Number 412: beloha
    http://api.openweathermap.org/data/2.5/weather?q=beloha&units=imperial&APPID=0
    City Number 413: canavieiras
    http://api.openweathermap.org/data/2.5/weather?q=canavieiras&units=imperial&APPID=0
    City Number 414: brae
    http://api.openweathermap.org/data/2.5/weather?q=brae&units=imperial&APPID=0
    City Number 415: mitzic
    http://api.openweathermap.org/data/2.5/weather?q=mitzic&units=imperial&APPID=0
    City Number 416: oktyabrskoye
    http://api.openweathermap.org/data/2.5/weather?q=oktyabrskoye&units=imperial&APPID=0
    City Number 417: bousse
    http://api.openweathermap.org/data/2.5/weather?q=bousse&units=imperial&APPID=0
    City Number 418: disna
    http://api.openweathermap.org/data/2.5/weather?q=disna&units=imperial&APPID=0
    City Number 419: sultanpur
    http://api.openweathermap.org/data/2.5/weather?q=sultanpur&units=imperial&APPID=0
    City Number 420: faya
    http://api.openweathermap.org/data/2.5/weather?q=faya&units=imperial&APPID=0
    City Number 421: ginebra
    http://api.openweathermap.org/data/2.5/weather?q=ginebra&units=imperial&APPID=0
    City Number 422: acari
    http://api.openweathermap.org/data/2.5/weather?q=acari&units=imperial&APPID=0
    City Number 423: kilifi
    http://api.openweathermap.org/data/2.5/weather?q=kilifi&units=imperial&APPID=0
    City Number 424: doha
    http://api.openweathermap.org/data/2.5/weather?q=doha&units=imperial&APPID=0
    City Number 425: sindor
    http://api.openweathermap.org/data/2.5/weather?q=sindor&units=imperial&APPID=0
    City Number 426: malindi
    http://api.openweathermap.org/data/2.5/weather?q=malindi&units=imperial&APPID=0
    City Number 427: vangaindrano
    http://api.openweathermap.org/data/2.5/weather?q=vangaindrano&units=imperial&APPID=0
    City Number 428: leon
    http://api.openweathermap.org/data/2.5/weather?q=leon&units=imperial&APPID=0
    City Number 429: rudnichnyy
    http://api.openweathermap.org/data/2.5/weather?q=rudnichnyy&units=imperial&APPID=0
    City Number 430: yamunanagar
    http://api.openweathermap.org/data/2.5/weather?q=yamunanagar&units=imperial&APPID=0
    City Number 431: ustye
    http://api.openweathermap.org/data/2.5/weather?q=ustye&units=imperial&APPID=0
    City Number 432: iquique
    http://api.openweathermap.org/data/2.5/weather?q=iquique&units=imperial&APPID=0
    City Number 433: bad munstereifel
    http://api.openweathermap.org/data/2.5/weather?q=bad%20munstereifel&units=imperial&APPID=0
    City Number 434: lagoa
    http://api.openweathermap.org/data/2.5/weather?q=lagoa&units=imperial&APPID=0
    City Number 435: nusaybin
    http://api.openweathermap.org/data/2.5/weather?q=nusaybin&units=imperial&APPID=0
    City Number 436: nandikotkur
    http://api.openweathermap.org/data/2.5/weather?q=nandikotkur&units=imperial&APPID=0
    City Number 437: koslan
    http://api.openweathermap.org/data/2.5/weather?q=koslan&units=imperial&APPID=0
    City Number 438: klaksvik
    http://api.openweathermap.org/data/2.5/weather?q=klaksvik&units=imperial&APPID=0
    City Number 439: stephenville
    http://api.openweathermap.org/data/2.5/weather?q=stephenville&units=imperial&APPID=0
    City Number 440: dapaong
    http://api.openweathermap.org/data/2.5/weather?q=dapaong&units=imperial&APPID=0
    City Number 441: george town
    http://api.openweathermap.org/data/2.5/weather?q=george%20town&units=imperial&APPID=0
    City Number 442: keflavik
    http://api.openweathermap.org/data/2.5/weather?q=keflavik&units=imperial&APPID=0
    City Number 443: rafraf
    http://api.openweathermap.org/data/2.5/weather?q=rafraf&units=imperial&APPID=0
    City Number 444: bardiyah
    http://api.openweathermap.org/data/2.5/weather?q=bardiyah&units=imperial&APPID=0
    City Number 445: ordu
    http://api.openweathermap.org/data/2.5/weather?q=ordu&units=imperial&APPID=0
    City Number 446: mangulile
    http://api.openweathermap.org/data/2.5/weather?q=mangulile&units=imperial&APPID=0
    City Number 447: hirtshals
    http://api.openweathermap.org/data/2.5/weather?q=hirtshals&units=imperial&APPID=0
    City Number 448: inirida
    http://api.openweathermap.org/data/2.5/weather?q=inirida&units=imperial&APPID=0
    City Number 449: san cristobal
    http://api.openweathermap.org/data/2.5/weather?q=san%20cristobal&units=imperial&APPID=0
    City Number 450: viedma
    http://api.openweathermap.org/data/2.5/weather?q=viedma&units=imperial&APPID=0
    City Number 451: sivakasi
    http://api.openweathermap.org/data/2.5/weather?q=sivakasi&units=imperial&APPID=0
    City Number 452: general pico
    http://api.openweathermap.org/data/2.5/weather?q=general%20pico&units=imperial&APPID=0
    City Number 453: talawdi
    http://api.openweathermap.org/data/2.5/weather?q=talawdi&units=imperial&APPID=0
    City Number 454: larsnes
    http://api.openweathermap.org/data/2.5/weather?q=larsnes&units=imperial&APPID=0
    City Number 455: salcininkai
    http://api.openweathermap.org/data/2.5/weather?q=salcininkai&units=imperial&APPID=0
    City Number 456: decatur
    http://api.openweathermap.org/data/2.5/weather?q=decatur&units=imperial&APPID=0
    City Number 457: kamenka
    http://api.openweathermap.org/data/2.5/weather?q=kamenka&units=imperial&APPID=0
    City Number 458: bagotville
    http://api.openweathermap.org/data/2.5/weather?q=bagotville&units=imperial&APPID=0
    City Number 459: angelholm
    http://api.openweathermap.org/data/2.5/weather?q=angelholm&units=imperial&APPID=0
    City Number 460: zhanaozen
    http://api.openweathermap.org/data/2.5/weather?q=zhanaozen&units=imperial&APPID=0
    City Number 461: ajdabiya
    http://api.openweathermap.org/data/2.5/weather?q=ajdabiya&units=imperial&APPID=0
    City Number 462: riyadh
    http://api.openweathermap.org/data/2.5/weather?q=riyadh&units=imperial&APPID=0
    City Number 463: gravdal
    http://api.openweathermap.org/data/2.5/weather?q=gravdal&units=imperial&APPID=0
    City Number 464: kautokeino
    http://api.openweathermap.org/data/2.5/weather?q=kautokeino&units=imperial&APPID=0
    City Number 465: sambava
    http://api.openweathermap.org/data/2.5/weather?q=sambava&units=imperial&APPID=0
    City Number 466: ponta delgada
    http://api.openweathermap.org/data/2.5/weather?q=ponta%20delgada&units=imperial&APPID=0
    City Number 467: cabinda
    http://api.openweathermap.org/data/2.5/weather?q=cabinda&units=imperial&APPID=0
    City Number 468: fecamp
    http://api.openweathermap.org/data/2.5/weather?q=fecamp&units=imperial&APPID=0
    City Number 469: hvide sande
    http://api.openweathermap.org/data/2.5/weather?q=hvide%20sande&units=imperial&APPID=0
    City Number 470: altay
    http://api.openweathermap.org/data/2.5/weather?q=altay&units=imperial&APPID=0
    City Number 471: zinder
    http://api.openweathermap.org/data/2.5/weather?q=zinder&units=imperial&APPID=0
    City Number 472: laguna
    http://api.openweathermap.org/data/2.5/weather?q=laguna&units=imperial&APPID=0
    City Number 473: fernan-nunez
    http://api.openweathermap.org/data/2.5/weather?q=fernan-nunez&units=imperial&APPID=0
    City Number 474: kalabo
    http://api.openweathermap.org/data/2.5/weather?q=kalabo&units=imperial&APPID=0
    City Number 475: nassau
    http://api.openweathermap.org/data/2.5/weather?q=nassau&units=imperial&APPID=0
    City Number 476: sibiti
    http://api.openweathermap.org/data/2.5/weather?q=sibiti&units=imperial&APPID=0
    City Number 477: dalvik
    http://api.openweathermap.org/data/2.5/weather?q=dalvik&units=imperial&APPID=0
    City Number 478: colquechaca
    http://api.openweathermap.org/data/2.5/weather?q=colquechaca&units=imperial&APPID=0
    City Number 479: susehri
    http://api.openweathermap.org/data/2.5/weather?q=susehri&units=imperial&APPID=0
    City Number 480: pauini
    http://api.openweathermap.org/data/2.5/weather?q=pauini&units=imperial&APPID=0
    City Number 481: ballina
    http://api.openweathermap.org/data/2.5/weather?q=ballina&units=imperial&APPID=0
    City Number 482: kem
    http://api.openweathermap.org/data/2.5/weather?q=kem&units=imperial&APPID=0
    City Number 483: atar
    http://api.openweathermap.org/data/2.5/weather?q=atar&units=imperial&APPID=0
    City Number 484: stokmarknes
    http://api.openweathermap.org/data/2.5/weather?q=stokmarknes&units=imperial&APPID=0
    City Number 485: ust-ishim
    http://api.openweathermap.org/data/2.5/weather?q=ust-ishim&units=imperial&APPID=0
    City Number 486: tromso
    http://api.openweathermap.org/data/2.5/weather?q=tromso&units=imperial&APPID=0
    City Number 487: yarada
    http://api.openweathermap.org/data/2.5/weather?q=yarada&units=imperial&APPID=0
    City Number 488: skowhegan
    http://api.openweathermap.org/data/2.5/weather?q=skowhegan&units=imperial&APPID=0
    City Number 489: bannu
    http://api.openweathermap.org/data/2.5/weather?q=bannu&units=imperial&APPID=0
    City Number 490: santiago de las vegas
    http://api.openweathermap.org/data/2.5/weather?q=santiago%20de%20las%20vegas&units=imperial&APPID=0
    City Number 491: tostedt
    http://api.openweathermap.org/data/2.5/weather?q=tostedt&units=imperial&APPID=0
    City Number 492: carrollton
    http://api.openweathermap.org/data/2.5/weather?q=carrollton&units=imperial&APPID=0
    City Number 493: san ramon de la nueva oran
    http://api.openweathermap.org/data/2.5/weather?q=san%20ramon%20de%20la%20nueva%20oran&units=imperial&APPID=0
    City Number 494: issia
    http://api.openweathermap.org/data/2.5/weather?q=issia&units=imperial&APPID=0
    City Number 495: sorvag
    http://api.openweathermap.org/data/2.5/weather?q=sorvag&units=imperial&APPID=0
    City Number 496: rolim de moura
    http://api.openweathermap.org/data/2.5/weather?q=rolim%20de%20moura&units=imperial&APPID=0
    City Number 497: matara
    http://api.openweathermap.org/data/2.5/weather?q=matara&units=imperial&APPID=0
    City Number 498: duz
    http://api.openweathermap.org/data/2.5/weather?q=duz&units=imperial&APPID=0
    City Number 499: aflu
    http://api.openweathermap.org/data/2.5/weather?q=aflu&units=imperial&APPID=0
    City Number 500: natal
    http://api.openweathermap.org/data/2.5/weather?q=natal&units=imperial&APPID=0
    City Number 501: luba
    http://api.openweathermap.org/data/2.5/weather?q=luba&units=imperial&APPID=0
    City Number 502: port said
    http://api.openweathermap.org/data/2.5/weather?q=port%20said&units=imperial&APPID=0
    City Number 503: analipsis
    http://api.openweathermap.org/data/2.5/weather?q=analipsis&units=imperial&APPID=0
    City Number 504: nador
    http://api.openweathermap.org/data/2.5/weather?q=nador&units=imperial&APPID=0
    City Number 505: mahaicony
    http://api.openweathermap.org/data/2.5/weather?q=mahaicony&units=imperial&APPID=0
    City Number 506: sakakah
    http://api.openweathermap.org/data/2.5/weather?q=sakakah&units=imperial&APPID=0
    City Number 507: taoudenni
    http://api.openweathermap.org/data/2.5/weather?q=taoudenni&units=imperial&APPID=0
    City Number 508: altonia
    http://api.openweathermap.org/data/2.5/weather?q=altonia&units=imperial&APPID=0
    City Number 509: bhagalpur
    http://api.openweathermap.org/data/2.5/weather?q=bhagalpur&units=imperial&APPID=0
    City Number 510: abha
    http://api.openweathermap.org/data/2.5/weather?q=abha&units=imperial&APPID=0
    City Number 511: wawa
    http://api.openweathermap.org/data/2.5/weather?q=wawa&units=imperial&APPID=0
    City Number 512: ratnagiri
    http://api.openweathermap.org/data/2.5/weather?q=ratnagiri&units=imperial&APPID=0
    City Number 513: pisco
    http://api.openweathermap.org/data/2.5/weather?q=pisco&units=imperial&APPID=0
    City Number 514: bani walid
    http://api.openweathermap.org/data/2.5/weather?q=bani%20walid&units=imperial&APPID=0
    City Number 515: bhikhi
    http://api.openweathermap.org/data/2.5/weather?q=bhikhi&units=imperial&APPID=0
    City Number 516: barreirinhas
    http://api.openweathermap.org/data/2.5/weather?q=barreirinhas&units=imperial&APPID=0
    City Number 517: santa cruz del norte
    http://api.openweathermap.org/data/2.5/weather?q=santa%20cruz%20del%20norte&units=imperial&APPID=0
    City Number 518: barawe
    http://api.openweathermap.org/data/2.5/weather?q=barawe&units=imperial&APPID=0
    City Number 519: agnibilekrou
    http://api.openweathermap.org/data/2.5/weather?q=agnibilekrou&units=imperial&APPID=0
    City Number 520: solovetskiy
    http://api.openweathermap.org/data/2.5/weather?q=solovetskiy&units=imperial&APPID=0
    City Number 521: benghazi
    http://api.openweathermap.org/data/2.5/weather?q=benghazi&units=imperial&APPID=0
    City Number 522: ayna
    http://api.openweathermap.org/data/2.5/weather?q=ayna&units=imperial&APPID=0
    City Number 523: birjand
    http://api.openweathermap.org/data/2.5/weather?q=birjand&units=imperial&APPID=0
    City Number 524: iralaya
    http://api.openweathermap.org/data/2.5/weather?q=iralaya&units=imperial&APPID=0
    City Number 525: mzimba
    http://api.openweathermap.org/data/2.5/weather?q=mzimba&units=imperial&APPID=0
    City Number 526: beyneu
    http://api.openweathermap.org/data/2.5/weather?q=beyneu&units=imperial&APPID=0
    City Number 527: senador guiomard
    http://api.openweathermap.org/data/2.5/weather?q=senador%20guiomard&units=imperial&APPID=0
    City Number 528: miranorte
    http://api.openweathermap.org/data/2.5/weather?q=miranorte&units=imperial&APPID=0
    City Number 529: mosquera
    http://api.openweathermap.org/data/2.5/weather?q=mosquera&units=imperial&APPID=0
    City Number 530: gobabis
    http://api.openweathermap.org/data/2.5/weather?q=gobabis&units=imperial&APPID=0
    City Number 531: pemba
    http://api.openweathermap.org/data/2.5/weather?q=pemba&units=imperial&APPID=0
    City Number 532: savalou
    http://api.openweathermap.org/data/2.5/weather?q=savalou&units=imperial&APPID=0
    City Number 533: talavera
    http://api.openweathermap.org/data/2.5/weather?q=talavera&units=imperial&APPID=0
    City Number 534: palmares
    http://api.openweathermap.org/data/2.5/weather?q=palmares&units=imperial&APPID=0
    City Number 535: ugoofaaru
    http://api.openweathermap.org/data/2.5/weather?q=ugoofaaru&units=imperial&APPID=0
    City Number 536: boali
    http://api.openweathermap.org/data/2.5/weather?q=boali&units=imperial&APPID=0
    City Number 537: gamba
    http://api.openweathermap.org/data/2.5/weather?q=gamba&units=imperial&APPID=0
    City Number 538: eenhana
    http://api.openweathermap.org/data/2.5/weather?q=eenhana&units=imperial&APPID=0
    City Number 539: villa rica
    http://api.openweathermap.org/data/2.5/weather?q=villa%20rica&units=imperial&APPID=0
    City Number 540: urengoy
    http://api.openweathermap.org/data/2.5/weather?q=urengoy&units=imperial&APPID=0
    City Number 541: agadir
    http://api.openweathermap.org/data/2.5/weather?q=agadir&units=imperial&APPID=0
    City Number 542: bafoulabe
    http://api.openweathermap.org/data/2.5/weather?q=bafoulabe&units=imperial&APPID=0
    City Number 543: rosoman
    http://api.openweathermap.org/data/2.5/weather?q=rosoman&units=imperial&APPID=0
    City Number 544: guisa
    http://api.openweathermap.org/data/2.5/weather?q=guisa&units=imperial&APPID=0
    City Number 545: karaidel
    http://api.openweathermap.org/data/2.5/weather?q=karaidel&units=imperial&APPID=0
    City Number 546: nyrob
    http://api.openweathermap.org/data/2.5/weather?q=nyrob&units=imperial&APPID=0
    City Number 547: presidencia roque saenz pena
    http://api.openweathermap.org/data/2.5/weather?q=presidencia%20roque%20saenz%20pena&units=imperial&APPID=0
    City Number 548: caicedo
    http://api.openweathermap.org/data/2.5/weather?q=caicedo&units=imperial&APPID=0
    City Number 549: obo
    http://api.openweathermap.org/data/2.5/weather?q=obo&units=imperial&APPID=0
    City Number 550: neustadt
    http://api.openweathermap.org/data/2.5/weather?q=neustadt&units=imperial&APPID=0
    City Number 551: blagoyevo
    http://api.openweathermap.org/data/2.5/weather?q=blagoyevo&units=imperial&APPID=0
    City Number 552: samaipata
    http://api.openweathermap.org/data/2.5/weather?q=samaipata&units=imperial&APPID=0
    City Number 553: the valley
    http://api.openweathermap.org/data/2.5/weather?q=the%20valley&units=imperial&APPID=0
    City Number 554: los llanos de aridane
    http://api.openweathermap.org/data/2.5/weather?q=los%20llanos%20de%20aridane&units=imperial&APPID=0
    City Number 555: soltsy
    http://api.openweathermap.org/data/2.5/weather?q=soltsy&units=imperial&APPID=0
    City Number 556: aguimes
    http://api.openweathermap.org/data/2.5/weather?q=aguimes&units=imperial&APPID=0
    City Number 557: los andes
    http://api.openweathermap.org/data/2.5/weather?q=los%20andes&units=imperial&APPID=0
    City Number 558: guelengdeng
    http://api.openweathermap.org/data/2.5/weather?q=guelengdeng&units=imperial&APPID=0
    City Number 559: sorland
    http://api.openweathermap.org/data/2.5/weather?q=sorland&units=imperial&APPID=0
    City Number 560: parana
    http://api.openweathermap.org/data/2.5/weather?q=parana&units=imperial&APPID=0
    City Number 561: camocim
    http://api.openweathermap.org/data/2.5/weather?q=camocim&units=imperial&APPID=0
    City Number 562: luanda
    http://api.openweathermap.org/data/2.5/weather?q=luanda&units=imperial&APPID=0
    City Number 563: semey
    http://api.openweathermap.org/data/2.5/weather?q=semey&units=imperial&APPID=0
    City Number 564: sosva
    http://api.openweathermap.org/data/2.5/weather?q=sosva&units=imperial&APPID=0
    City Number 565: zlobin
    http://api.openweathermap.org/data/2.5/weather?q=zlobin&units=imperial&APPID=0
    City Number 566: tanout
    http://api.openweathermap.org/data/2.5/weather?q=tanout&units=imperial&APPID=0
    City Number 567: listowel
    http://api.openweathermap.org/data/2.5/weather?q=listowel&units=imperial&APPID=0
    City Number 568: whittlesea
    http://api.openweathermap.org/data/2.5/weather?q=whittlesea&units=imperial&APPID=0
    City Number 569: jibuti
    http://api.openweathermap.org/data/2.5/weather?q=jibuti&units=imperial&APPID=0
    City Number 570: turayf
    http://api.openweathermap.org/data/2.5/weather?q=turayf&units=imperial&APPID=0
    City Number 571: gazni
    http://api.openweathermap.org/data/2.5/weather?q=gazni&units=imperial&APPID=0
    City Number 572: kalmunai
    http://api.openweathermap.org/data/2.5/weather?q=kalmunai&units=imperial&APPID=0
    City Number 573: paucartambo
    http://api.openweathermap.org/data/2.5/weather?q=paucartambo&units=imperial&APPID=0
    City Number 574: espinal
    http://api.openweathermap.org/data/2.5/weather?q=espinal&units=imperial&APPID=0
    City Number 575: beira
    http://api.openweathermap.org/data/2.5/weather?q=beira&units=imperial&APPID=0
    City Number 576: tigzirt
    http://api.openweathermap.org/data/2.5/weather?q=tigzirt&units=imperial&APPID=0
    City Number 577: skalistyy
    http://api.openweathermap.org/data/2.5/weather?q=skalistyy&units=imperial&APPID=0
    City Number 578: anuradhapura
    http://api.openweathermap.org/data/2.5/weather?q=anuradhapura&units=imperial&APPID=0
    City Number 579: le port
    http://api.openweathermap.org/data/2.5/weather?q=le%20port&units=imperial&APPID=0
    City Number 580: gondar
    http://api.openweathermap.org/data/2.5/weather?q=gondar&units=imperial&APPID=0
    City Number 581: bereznik
    http://api.openweathermap.org/data/2.5/weather?q=bereznik&units=imperial&APPID=0
    City Number 582: bubaque
    http://api.openweathermap.org/data/2.5/weather?q=bubaque&units=imperial&APPID=0
    City Number 583: gunjur
    http://api.openweathermap.org/data/2.5/weather?q=gunjur&units=imperial&APPID=0
    City Number 584: tibati
    http://api.openweathermap.org/data/2.5/weather?q=tibati&units=imperial&APPID=0
    City Number 585: khomeyn
    http://api.openweathermap.org/data/2.5/weather?q=khomeyn&units=imperial&APPID=0
    City Number 586: lyuban
    http://api.openweathermap.org/data/2.5/weather?q=lyuban&units=imperial&APPID=0
    City Number 587: artyom
    http://api.openweathermap.org/data/2.5/weather?q=artyom&units=imperial&APPID=0
    City Number 588: panjakent
    http://api.openweathermap.org/data/2.5/weather?q=panjakent&units=imperial&APPID=0
    City Number 589: chapeltique
    http://api.openweathermap.org/data/2.5/weather?q=chapeltique&units=imperial&APPID=0
    City Number 590: fruitville
    http://api.openweathermap.org/data/2.5/weather?q=fruitville&units=imperial&APPID=0
    City Number 591: sao felix do xingu
    http://api.openweathermap.org/data/2.5/weather?q=sao%20felix%20do%20xingu&units=imperial&APPID=0
    City Number 592: magadi
    http://api.openweathermap.org/data/2.5/weather?q=magadi&units=imperial&APPID=0
    City Number 593: lokosovo
    http://api.openweathermap.org/data/2.5/weather?q=lokosovo&units=imperial&APPID=0
    City Number 594: kissimmee
    http://api.openweathermap.org/data/2.5/weather?q=kissimmee&units=imperial&APPID=0
    City Number 595: mokrousovo
    http://api.openweathermap.org/data/2.5/weather?q=mokrousovo&units=imperial&APPID=0
    City Number 596: boundiali
    http://api.openweathermap.org/data/2.5/weather?q=boundiali&units=imperial&APPID=0
    City Number 597: umm lajj
    http://api.openweathermap.org/data/2.5/weather?q=umm%20lajj&units=imperial&APPID=0
    City Number 598: quilmana
    http://api.openweathermap.org/data/2.5/weather?q=quilmana&units=imperial&APPID=0
    City Number 599: uray
    http://api.openweathermap.org/data/2.5/weather?q=uray&units=imperial&APPID=0
    City Number 600: manaure
    http://api.openweathermap.org/data/2.5/weather?q=manaure&units=imperial&APPID=0
    City Number 601: loviisa
    http://api.openweathermap.org/data/2.5/weather?q=loviisa&units=imperial&APPID=0
    City Number 602: karauzyak
    http://api.openweathermap.org/data/2.5/weather?q=karauzyak&units=imperial&APPID=0
    City Number 603: karaul
    http://api.openweathermap.org/data/2.5/weather?q=karaul&units=imperial&APPID=0
    City Number 604: bodden town
    http://api.openweathermap.org/data/2.5/weather?q=bodden%20town&units=imperial&APPID=0
    City Number 605: boden
    http://api.openweathermap.org/data/2.5/weather?q=boden&units=imperial&APPID=0
    City Number 606: kollumerland
    http://api.openweathermap.org/data/2.5/weather?q=kollumerland&units=imperial&APPID=0
    City Number 607: nanga eboko
    http://api.openweathermap.org/data/2.5/weather?q=nanga%20eboko&units=imperial&APPID=0
    City Number 608: jiroft
    http://api.openweathermap.org/data/2.5/weather?q=jiroft&units=imperial&APPID=0
    City Number 609: guantanamo
    http://api.openweathermap.org/data/2.5/weather?q=guantanamo&units=imperial&APPID=0
    City Number 610: chernogolovka
    http://api.openweathermap.org/data/2.5/weather?q=chernogolovka&units=imperial&APPID=0
    City Number 611: fasa
    http://api.openweathermap.org/data/2.5/weather?q=fasa&units=imperial&APPID=0
    City Number 612: inongo
    http://api.openweathermap.org/data/2.5/weather?q=inongo&units=imperial&APPID=0
    City Number 613: boiro
    http://api.openweathermap.org/data/2.5/weather?q=boiro&units=imperial&APPID=0
    City Number 614: kumi
    http://api.openweathermap.org/data/2.5/weather?q=kumi&units=imperial&APPID=0
    City Number 615: igrim
    http://api.openweathermap.org/data/2.5/weather?q=igrim&units=imperial&APPID=0
    City Number 616: denizli
    http://api.openweathermap.org/data/2.5/weather?q=denizli&units=imperial&APPID=0
    City Number 617: padang
    http://api.openweathermap.org/data/2.5/weather?q=padang&units=imperial&APPID=0
    City Number 618: ust-kan
    http://api.openweathermap.org/data/2.5/weather?q=ust-kan&units=imperial&APPID=0
    City Number 619: tasbuget
    http://api.openweathermap.org/data/2.5/weather?q=tasbuget&units=imperial&APPID=0
    City Number 620: verkhnyaya balkariya
    http://api.openweathermap.org/data/2.5/weather?q=verkhnyaya%20balkariya&units=imperial&APPID=0
    City Number 621: abonnema
    http://api.openweathermap.org/data/2.5/weather?q=abonnema&units=imperial&APPID=0
    City Number 622: fagernes
    http://api.openweathermap.org/data/2.5/weather?q=fagernes&units=imperial&APPID=0
    City Number 623: caluquembe
    http://api.openweathermap.org/data/2.5/weather?q=caluquembe&units=imperial&APPID=0
    City Number 624: koungou
    http://api.openweathermap.org/data/2.5/weather?q=koungou&units=imperial&APPID=0
    City Number 625: puerto narino
    http://api.openweathermap.org/data/2.5/weather?q=puerto%20narino&units=imperial&APPID=0
    City Number 626: zanjan
    http://api.openweathermap.org/data/2.5/weather?q=zanjan&units=imperial&APPID=0
    City Number 627: nioro
    http://api.openweathermap.org/data/2.5/weather?q=nioro&units=imperial&APPID=0
    City Number 628: rivadavia
    http://api.openweathermap.org/data/2.5/weather?q=rivadavia&units=imperial&APPID=0
    City Number 629: rzhev
    http://api.openweathermap.org/data/2.5/weather?q=rzhev&units=imperial&APPID=0
    City Number 630: durban
    http://api.openweathermap.org/data/2.5/weather?q=durban&units=imperial&APPID=0
    City Number 631: shar
    http://api.openweathermap.org/data/2.5/weather?q=shar&units=imperial&APPID=0
    City Number 632: talcahuano
    http://api.openweathermap.org/data/2.5/weather?q=talcahuano&units=imperial&APPID=0
    City Number 633: esmeralda
    http://api.openweathermap.org/data/2.5/weather?q=esmeralda&units=imperial&APPID=0
    City Number 634: kegayli
    http://api.openweathermap.org/data/2.5/weather?q=kegayli&units=imperial&APPID=0
    City Number 635: pankovka
    http://api.openweathermap.org/data/2.5/weather?q=pankovka&units=imperial&APPID=0
    City Number 636: misratah
    http://api.openweathermap.org/data/2.5/weather?q=misratah&units=imperial&APPID=0
    City Number 637: porosozero
    http://api.openweathermap.org/data/2.5/weather?q=porosozero&units=imperial&APPID=0
    City Number 638: san juan
    http://api.openweathermap.org/data/2.5/weather?q=san%20juan&units=imperial&APPID=0
    City Number 639: ibra
    http://api.openweathermap.org/data/2.5/weather?q=ibra&units=imperial&APPID=0
    City Number 640: kamina
    http://api.openweathermap.org/data/2.5/weather?q=kamina&units=imperial&APPID=0
    City Number 641: turinsk
    http://api.openweathermap.org/data/2.5/weather?q=turinsk&units=imperial&APPID=0
    City Number 642: calvinia
    http://api.openweathermap.org/data/2.5/weather?q=calvinia&units=imperial&APPID=0
    City Number 643: san pedro
    http://api.openweathermap.org/data/2.5/weather?q=san%20pedro&units=imperial&APPID=0
    City Number 644: wajir
    http://api.openweathermap.org/data/2.5/weather?q=wajir&units=imperial&APPID=0
    City Number 645: peterborough
    http://api.openweathermap.org/data/2.5/weather?q=peterborough&units=imperial&APPID=0
    City Number 646: urdzhar
    http://api.openweathermap.org/data/2.5/weather?q=urdzhar&units=imperial&APPID=0
    City Number 647: paradwip
    http://api.openweathermap.org/data/2.5/weather?q=paradwip&units=imperial&APPID=0
    City Number 648: tazovskiy
    http://api.openweathermap.org/data/2.5/weather?q=tazovskiy&units=imperial&APPID=0
    City Number 649: tucuman
    http://api.openweathermap.org/data/2.5/weather?q=tucuman&units=imperial&APPID=0
    City Number 650: ibresi
    http://api.openweathermap.org/data/2.5/weather?q=ibresi&units=imperial&APPID=0
    City Number 651: tambovka
    http://api.openweathermap.org/data/2.5/weather?q=tambovka&units=imperial&APPID=0
    City Number 652: kataysk
    http://api.openweathermap.org/data/2.5/weather?q=kataysk&units=imperial&APPID=0
    City Number 653: murgab
    http://api.openweathermap.org/data/2.5/weather?q=murgab&units=imperial&APPID=0
    City Number 654: maloye kozino
    http://api.openweathermap.org/data/2.5/weather?q=maloye%20kozino&units=imperial&APPID=0
    City Number 655: paragominas
    http://api.openweathermap.org/data/2.5/weather?q=paragominas&units=imperial&APPID=0
    City Number 656: rundu
    http://api.openweathermap.org/data/2.5/weather?q=rundu&units=imperial&APPID=0
    City Number 657: kamakhyanagar
    http://api.openweathermap.org/data/2.5/weather?q=kamakhyanagar&units=imperial&APPID=0
    City Number 658: nizhniy chir
    http://api.openweathermap.org/data/2.5/weather?q=nizhniy%20chir&units=imperial&APPID=0
    City Number 659: geresk
    http://api.openweathermap.org/data/2.5/weather?q=geresk&units=imperial&APPID=0
    City Number 660: mogadishu
    http://api.openweathermap.org/data/2.5/weather?q=mogadishu&units=imperial&APPID=0
    City Number 661: koson
    http://api.openweathermap.org/data/2.5/weather?q=koson&units=imperial&APPID=0
    City Number 662: hunza
    http://api.openweathermap.org/data/2.5/weather?q=hunza&units=imperial&APPID=0
    City Number 663: marktredwitz
    http://api.openweathermap.org/data/2.5/weather?q=marktredwitz&units=imperial&APPID=0
    City Number 664: bethlehem
    http://api.openweathermap.org/data/2.5/weather?q=bethlehem&units=imperial&APPID=0
    City Number 665: cheuskiny
    http://api.openweathermap.org/data/2.5/weather?q=cheuskiny&units=imperial&APPID=0
    City Number 666: urumita
    http://api.openweathermap.org/data/2.5/weather?q=urumita&units=imperial&APPID=0
    City Number 667: skibotn
    http://api.openweathermap.org/data/2.5/weather?q=skibotn&units=imperial&APPID=0
    City Number 668: san carlos de bariloche
    http://api.openweathermap.org/data/2.5/weather?q=san%20carlos%20de%20bariloche&units=imperial&APPID=0
    City Number 669: sabzevar
    http://api.openweathermap.org/data/2.5/weather?q=sabzevar&units=imperial&APPID=0
    City Number 670: najran
    http://api.openweathermap.org/data/2.5/weather?q=najran&units=imperial&APPID=0
    City Number 671: oranjestad
    http://api.openweathermap.org/data/2.5/weather?q=oranjestad&units=imperial&APPID=0
    City Number 672: sikeston
    http://api.openweathermap.org/data/2.5/weather?q=sikeston&units=imperial&APPID=0
    City Number 673: parabel
    http://api.openweathermap.org/data/2.5/weather?q=parabel&units=imperial&APPID=0
    City Number 674: rorvik
    http://api.openweathermap.org/data/2.5/weather?q=rorvik&units=imperial&APPID=0
    City Number 675: mushie
    http://api.openweathermap.org/data/2.5/weather?q=mushie&units=imperial&APPID=0
    City Number 676: novobelokatay
    http://api.openweathermap.org/data/2.5/weather?q=novobelokatay&units=imperial&APPID=0
    City Number 677: usogorsk
    http://api.openweathermap.org/data/2.5/weather?q=usogorsk&units=imperial&APPID=0
    City Number 678: camacha
    http://api.openweathermap.org/data/2.5/weather?q=camacha&units=imperial&APPID=0
    City Number 679: pelaya
    http://api.openweathermap.org/data/2.5/weather?q=pelaya&units=imperial&APPID=0
    City Number 680: shibarghan
    http://api.openweathermap.org/data/2.5/weather?q=shibarghan&units=imperial&APPID=0
    City Number 681: orda
    http://api.openweathermap.org/data/2.5/weather?q=orda&units=imperial&APPID=0
    City Number 682: buchanan
    http://api.openweathermap.org/data/2.5/weather?q=buchanan&units=imperial&APPID=0
    City Number 683: shubarshi
    http://api.openweathermap.org/data/2.5/weather?q=shubarshi&units=imperial&APPID=0
    City Number 684: capaci
    http://api.openweathermap.org/data/2.5/weather?q=capaci&units=imperial&APPID=0
    City Number 685: ulagan
    http://api.openweathermap.org/data/2.5/weather?q=ulagan&units=imperial&APPID=0
    City Number 686: rudsar
    http://api.openweathermap.org/data/2.5/weather?q=rudsar&units=imperial&APPID=0
    City Number 687: uige
    http://api.openweathermap.org/data/2.5/weather?q=uige&units=imperial&APPID=0
    City Number 688: chake chake
    http://api.openweathermap.org/data/2.5/weather?q=chake%20chake&units=imperial&APPID=0
    City Number 689: akureyri
    http://api.openweathermap.org/data/2.5/weather?q=akureyri&units=imperial&APPID=0
    City Number 690: ciras
    http://api.openweathermap.org/data/2.5/weather?q=ciras&units=imperial&APPID=0
    City Number 691: ciurila
    http://api.openweathermap.org/data/2.5/weather?q=ciurila&units=imperial&APPID=0
    City Number 692: aksarka
    http://api.openweathermap.org/data/2.5/weather?q=aksarka&units=imperial&APPID=0
    City Number 693: idanre
    http://api.openweathermap.org/data/2.5/weather?q=idanre&units=imperial&APPID=0
    City Number 694: jacareacanga
    http://api.openweathermap.org/data/2.5/weather?q=jacareacanga&units=imperial&APPID=0
    City Number 695: halifax
    http://api.openweathermap.org/data/2.5/weather?q=halifax&units=imperial&APPID=0
    City Number 696: antsohihy
    http://api.openweathermap.org/data/2.5/weather?q=antsohihy&units=imperial&APPID=0
    City Number 697: corner brook
    http://api.openweathermap.org/data/2.5/weather?q=corner%20brook&units=imperial&APPID=0
    City Number 698: ihosy
    http://api.openweathermap.org/data/2.5/weather?q=ihosy&units=imperial&APPID=0
    City Number 699: doka
    http://api.openweathermap.org/data/2.5/weather?q=doka&units=imperial&APPID=0
    City Number 700: corbelia
    http://api.openweathermap.org/data/2.5/weather?q=corbelia&units=imperial&APPID=0



```python
weather_df.count()
```




    City          619
    Country       619
    Max Temp      619
    Humidity      619
    Cloudiness    619
    Wind Speed    619
    Lat           619
    Lng           619
    dtype: int64




```python
#csv export
weather_df.to_csv("WeatherPy.csv")
```


```python
#plot temp
plt.scatter(weather_df["Lat"], weather_df["Max Temp"])
plt.xlabel('Latitude')
plt.ylabel('Max Temperature (F)')
plt.title(f'City Latitude vs Max Temperature ({datetime.now().date()})')
plt.savefig("lat_temp.png")
plt.show()
```


![png](output_6_0.png)



```python
#plot humidity
plt.scatter(weather_df["Lat"], weather_df["Humidity"])
plt.xlabel('Latitude')
plt.ylabel('Humidity (%)')
plt.title(f'City Latitude vs Humidity ({datetime.now().date()})')
plt.savefig("lat_humidity.png")
plt.show()
```


![png](output_7_0.png)



```python
#plot clouds
plt.scatter(weather_df["Lat"], weather_df["Cloudiness"])
plt.xlabel('Latitude')
plt.ylabel('Cloudiness (%)')
plt.title(f'City Latitude vs Cloudiness ({datetime.now().date()})')
plt.savefig("lat_cloudiness.png")
plt.show()
```


![png](output_8_0.png)



```python
#plot wind
plt.scatter(weather_df["Lat"], weather_df["Wind Speed"])
plt.xlabel('Latitude')
plt.ylabel('Wind Speed (mph)')
plt.title(f'City Latitude vs Wind Speed ({datetime.now().date()})')
plt.savefig("lat_windspeed.png")
plt.show()
```


![png](output_9_0.png)



```python
#Observable Trends
#1. Cities to the west of the Prime Meridian are currently colder than cities to the east.
#2. Cities to the west of the Prime Meridian typically have humidity above 50%, but there is a greater mix to the east.
#3. There are more cities to the east of the Prime Meridian with higher wind speeds.
```
