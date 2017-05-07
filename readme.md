# how to generate route data

- get directions from google (polylines were wildly inacurate 2017-05-07):

  '''
  curl "https://maps.googleapis.com/maps/api/directions/json?origin=%22Apartment+Angie,+Dobrota,+Montenegro%22&destination=%22Hotel+Gjallica,+Rruga+Dituria,+Kukës,+Albania%22" | jq '{paths:[.routes[0].legs[].steps[].end_location],bounds:.routes[0].bounds,distance:.routes[0].legs[].distance,duration:.routes[0].legs[].duration}'
  '''

- calculate the centre of the map: http://www.latlong.net/convert-address-to-lat-long.html