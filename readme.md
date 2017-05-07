# how to generate route data

- pipe polyline from google maps api through mapbox decoder:

  - Xàbia to Roma

    ```
    curl -s "https://maps.googleapis.com/maps/api/directions/json?origin=%22Sun+and+Co.+-+Coliving+%7C+Coworking+%7C+Community,+Carrer+Príncep+d'Astúries,+Xàbia,+Alicante,+Spain%22&destination=%22Moll+de+Ponent,+38,+08039+Barcelona,+Spain%22" | jq -r '.routes[0].overview_polyline.points' | /usr/lib/node_modules/@mapbox/polyline/bin/polyline.bin.js --decode
    curl -s "https://maps.googleapis.com/maps/api/directions/json?origin=%22Civitavecchia+Port,+Piazza+Vittorio+Emanuele,+Civitavecchia,+Metropolitan+City+of+Rome,+Italy%22&destination=%2200172+Rome,+Italy%22" | jq -r '.routes[0].overview_polyline.points' | /usr/lib/node_modules/@mapbox/polyline/bin/polyline.bin.js --decode
    ```

  - Roma to Deruta

    ```
    curl -s "https://maps.googleapis.com/maps/api/directions/json?origin=%2200172+Rome,+Italy%22&destination=%22Via+Mancini,+26,+06053+Deruta+PG,+Italy%22" | jq -r '.routes[0].overview_polyline.points' | /usr/lib/node_modules/@mapbox/polyline/bin/polyline.bin.js --decode
    ```

  - Deruta to Kaštel Stari

    ```
    curl -s "https://maps.googleapis.com/maps/api/directions/json?origin=%22Via+Mancini,+26,+06053+Deruta+PG,+Italy%22&destination=%22Avizo+D.o.o,+21216,+Kaštel+Stari,+Croatia%22" | jq -r '.routes[0].overview_polyline.points' | /usr/lib/node_modules/@mapbox/polyline/bin/polyline.bin.js --decode
    ```

  - Kaštel Stari to Dubrovnik

    ```
    curl -s "https://maps.googleapis.com/maps/api/directions/json?origin=%22Avizo+D.o.o,+21216,+Kaštel+Stari,+Croatia%22&destination=%22Hostel+365+For+U,+Vukovarska+ulica,+Dubrovnik,+Croatia%22&waypoints=%22Dugi+Rat,+Croatia|Makarska,+Croatia%22" | jq -r '.routes[0].overview_polyline.points' | /usr/lib/node_modules/@mapbox/polyline/bin/polyline.bin.js --decode
    ```

  - Dubrovnik to Dobrota
  
    ```
    curl -s "https://maps.googleapis.com/maps/api/directions/json?origin=%22Hostel+365+For+U,+Vukovarska+ulica,+Dubrovnik,+Croatia%22&destination=%22Apartment+Angie,+Dobrota,+Montenegro%22" | jq -r '.routes[0].overview_polyline.points' | /usr/lib/node_modules/@mapbox/polyline/bin/polyline.bin.js --decode
    ```

  - Dobrota to Kukës

    ```
    curl -s "https://maps.googleapis.com/maps/api/directions/json?origin=%22Apartment+Angie,+Dobrota,+Montenegro%22&destination=%22Hotel+Gjallica,+Rruga+Dituria,+Kukës,+Albania%22" | jq -r '.routes[0].overview_polyline.points' | /usr/lib/node_modules/@mapbox/polyline/bin/polyline.bin.js --decode
    ```

  - Kukës to Skopje

    ```
    curl -s "https://maps.googleapis.com/maps/api/directions/json?origin=%22Hotel+Gjallica,+Rruga+Dituria,+Kuk%C3%ABs,+Albania%22&destination=%22Vila+Silia,+Vostanichka+30,+Skopje+1000,+Macedonia%22" | jq -r '.routes[0].overview_polyline.points' | /usr/lib/node_modules/@mapbox/polyline/bin/polyline.bin.js --decode
    ```

  - Skopje to Bansko

    ```
    curl -s "https://maps.googleapis.com/maps/api/directions/json?origin=%22Vila+Silia,+Vostanichka+30,+Skopje+1000,+Macedonia%22&destination=%22Cedar+Lodge+3+and+4+Complex,+Stragite+area,+Bansko,+2770,+Bulgaria%22" | jq -r '.routes[0].overview_polyline.points' | /usr/lib/node_modules/@mapbox/polyline/bin/polyline.bin.js --decode
    ```

- fetch bounds, distance and duration from google maps api:

  - Xàbia to Roma

    ```
    curl -s "https://maps.googleapis.com/maps/api/directions/json?origin=%22Sun+and+Co.+-+Coliving+%7C+Coworking+%7C+Community,+Carrer+Príncep+d'Astúries,+Xàbia,+Alicante,+Spain%22&destination=%2200172+Rome,+Italy%22" | jq '{paths:[.routes[0].legs[].steps[].end_location],bounds:.routes[0].bounds,distance:.routes[0].legs[].distance,duration:.routes[0].legs[].duration}'
    ```

  - Roma to Deruta

    ```
    curl -s "https://maps.googleapis.com/maps/api/directions/json?origin=%2200172+Rome,+Italy%22&destination=%22Via+Mancini,+26,+06053+Deruta+PG,+Italy%22" | jq '{paths:[.routes[0].legs[].steps[].end_location],bounds:.routes[0].bounds,distance:.routes[0].legs[].distance,duration:.routes[0].legs[].duration}'
    ```

  - Deruta to Kaštel Stari

    ```
    curl -s "https://maps.googleapis.com/maps/api/directions/json?origin=%22Via+Mancini,+26,+06053+Deruta+PG,+Italy%22&destination=%22Avizo+D.o.o,+21216,+Kaštel+Stari,+Croatia%22" | jq '{paths:[.routes[0].legs[].steps[].end_location],bounds:.routes[0].bounds,distance:.routes[0].legs[].distance,duration:.routes[0].legs[].duration}'
    ```

  - Kaštel Stari to Dubrovnik

    ```
    curl -s "https://maps.googleapis.com/maps/api/directions/json?origin=%22Avizo+D.o.o,+21216,+Kaštel+Stari,+Croatia%22&destination=%22Hostel+365+For+U,+Vukovarska+ulica,+Dubrovnik,+Croatia%22&waypoints=%22Dugi+Rat,+Croatia|Makarska,+Croatia%22" | jq '{paths:[.routes[0].legs[].steps[].end_location],bounds:.routes[0].bounds,distance:.routes[0].legs[].distance,duration:.routes[0].legs[].duration}'
    ```

  - Dubrovnik to Dobrota
  
    ```
    curl -s "https://maps.googleapis.com/maps/api/directions/json?origin=%22Hostel+365+For+U,+Vukovarska+ulica,+Dubrovnik,+Croatia%22&destination=%22Apartment+Angie,+Dobrota,+Montenegro%22" | jq '{paths:[.routes[0].legs[].steps[].end_location],bounds:.routes[0].bounds,distance:.routes[0].legs[].distance,duration:.routes[0].legs[].duration}'
    ```

  - Dobrota to Kukës

    ```
    curl -s "https://maps.googleapis.com/maps/api/directions/json?origin=%22Apartment+Angie,+Dobrota,+Montenegro%22&destination=%22Hotel+Gjallica,+Rruga+Dituria,+Kukës,+Albania%22" | jq '{paths:[.routes[0].legs[].steps[].end_location],bounds:.routes[0].bounds,distance:.routes[0].legs[].distance,duration:.routes[0].legs[].duration}'
    ```

  - Kukës to Skopje

    ```
    curl -s "https://maps.googleapis.com/maps/api/directions/json?origin=%22Hotel+Gjallica,+Rruga+Dituria,+Kuk%C3%ABs,+Albania%22&destination=%22Vila+Silia,+Vostanichka+30,+Skopje+1000,+Macedonia%22" | jq '{paths:[.routes[0].legs[].steps[].end_location],bounds:.routes[0].bounds,distance:.routes[0].legs[].distance,duration:.routes[0].legs[].duration}'
    ```

  - Skopje to Bansko

    ```
    curl -s "https://maps.googleapis.com/maps/api/directions/json?origin=%22Vila+Silia,+Vostanichka+30,+Skopje+1000,+Macedonia%22&destination=%22Cedar+Lodge+3+and+4+Complex,+Stragite+area,+Bansko,+2770,+Bulgaria%22" | jq '{paths:[.routes[0].legs[].steps[].end_location],bounds:.routes[0].bounds,distance:.routes[0].legs[].distance,duration:.routes[0].legs[].duration}'
    ```

- calculate the centre of the map: http://www.latlong.net/convert-address-to-lat-long.html