#code inspirations:
#https://stackoverflow.com/questions/62228489/python-folium-how-to-create-a-folium-map-marker-with-multiple-popup-text-line
#https://www.python-graph-gallery.com/312-add-markers-on-folium-map

import folium
import requests

locat = input ("What station info do you need: ")
input = requests.get('https://subway-map.herokuapp.com/').json()

flag=0
count=0

m = folium.Map(location= [40.6958, -73.9171], zoom_start=11)  #nyc location
stationlist=[]

for data in input: 
  if locat.lower() in data['stationname'].lower():   #going through each station's name
    html = f"""
          Station Name: {data['stationname']}<br>
          Subway Line: {data['subwayline']}<br>
          Routes: {data['route1']}, {data['route2']}, {data['route3']}, {data['route4']}, {data['route5']}, {data['route6']}, {data['route7']}, {data['route8']}, {data['route9']}, {data['route10']}, {data['route11']} <br>
          Entrance Type: {data['entrancetype']}<br>
          Entry: {data['entry']}<br>
          ADA: {data['ada']}<br>
          Freecrossover: {data['freecrossover']}<br>
          """

    count = count + 1

    iframe = folium.IFrame(html, width=230, height=180)
    pop=folium.Popup(iframe, max_width=230)

    
    folium.Marker([data['entrancelat'], data['entrancelong']], pop).add_to(m) #adds map markers for each station

print('Total amount of related stations: ', count)

if count==0:
  print('The following train station <' + locat + '> does not exist. Please enter the name of another train station.')

m.save(outfile='subwayprojectmap.html')
