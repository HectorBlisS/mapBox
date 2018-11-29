![](https://i.imgur.com/1QgrNNw.png)

# [](http://materials.ironhack.com/s/rJCE0nGTNN7#google-maps--geolocation "google-maps--geolocation")Google Maps | Geolocation

## [](http://materials.ironhack.com/s/rJCE0nGTNN7#learning-goals "learning-goals")Learning Goals

In this lesson you will learn:

- How to set up an API key
- How to embed a map in HTML
- How to show markers in our map
- How to create a route between two markers

## [](http://materials.ironhack.com/s/rJCE0nGTNN7#introduction "introduction")Introduction

![](https://s3-eu-west-1.amazonaws.com/ih-materials/uploads/upload_30a0611f30853bf6c769b4bbd24bd2a6.png)

Mapbox is a service of location data with features like maps, search and navigation. What does it do? Well... it seems obvious when is called Mapbox

Inside Google Maps API we can find different services like Directions, Geocoding, ReverseGeocoding, Elevation and StreetView.

Mapbox provides the same API for different platforms and technologies like iOS, Android, Web and Web Services.

Mapbox is free to use with certain cuota and they have [different plans](https://www.mapbox.com/pricing/) based on the number of requests your app is getting (how many users visits your app in average).

## Get a Mapbox API key?

The steps might change in the future and sometimes this process can be different, so don't hesitate to try again the same steps if something bad happens in one of the steps. In your career, you will see this kind of situations fairly often since these are all part of the development process of any product.

### Steps to get an API key for the first time

1.  Go to <https://www.mapbox.com/>

2.  Click on the button "Start building" on the cover's call to action button of the page.

[Imgur](https://i.imgur.com/EjjI08a.jpg)

1.  You must create an account completing the form.

[](https://i.imgur.com/uLmgJdb.png)

1.  Once in your dashboard, you already have a token in the Access tokens section, copy it.

[Imgur](https://i.imgur.com/kVwWXj4.png)

1.  You will need to Enable billing for this project.

![](https://i.imgur.com/RPCBY0O.png)

1.  If it's the first time you come here, you will probably need to give your credit card information. Don't worry, Google will not charge you anything and you will have to explicitly tell Google to charge you when you reach your quota.

![](https://i.imgur.com/UJzdDOD.png)

1.  After this, you are all set and you should have access to your API key.

![](https://i.imgur.com/bBcXMjO.png)

### [](http://materials.ironhack.com/s/rJCE0nGTNN7#retrieve-a-former-api-key "retrieve-a-former-api-key")Retrieve a former API key

To retrieve a former API key, the fastest way is to go to <https://console.cloud.google.com/apis/credentials> and potentially change your project name.

## [](http://materials.ironhack.com/s/rJCE0nGTNN7#create-a-map "create-a-map")Create a map

To create our first map we need two files, the `HTML` and the `JavaScript`.

In the `HTML` we will render our map and for that we need a container `div` to embed it.

```
<!-- index.html -->

<!DOCTYPE html>
<html>
  <head>
    <title>My First Map</title>
    <style>
       #map {
        height: 500px;
        width: 100%;
       }
    </style>
  </head>
  <body>
    <h3>My First Map</h3>
    <div id="map"></div>

    <script src="https://maps.googleapis.com/maps/api/js?key=YOUR-API-KEY"></script>
    <script type="text/javascript" src="main.js"></script>
  </body>
</html>

```

Notice that we need to replace `YOUR-API-KEY` from `<script async defer src="https://maps.googleapis.com/maps/api/js?key=YOUR-API-KEY"></script>` with the key you got in the section above.

```
// main.js

function startMap() {
  const ironhackBCN = {
  	lat: 41.3977381,
  	lng: 2.190471916};
  const map = new google.maps.Map(
    document.getElementById('map'),
    {
      zoom: 5,
      center: ironhackBCN
    }
  );
}

startMap();

```

![:bulb:](http://materials.ironhack.com/build/emojify.js/dist/images/basic/bulb.png ":bulb:") If instead of a map you see a grey block, it probably means that you have a problem with your API key. Make sure you enabled "Maps JavaScript API" from your [Dashboard](https://console.cloud.google.com/apis/dashboard). If you see nothing, it's probably because you didn't give a `height` property for your `#map`. Take a look at the HTML part of the code and you will notice that we have some embedded CSS in the <head> part.

Basically, we are on top of two things here:

1.  Create an object with [latitude](https://en.wikipedia.org/wiki/Latitude) and [longitude](https://en.wikipedia.org/wiki/Longitude) to point the map to a specific place (in our case IronhackBCN);

2.  Create an instance of a `Map` which receives two parameters: the first one is the container (`document.getElementById('map')`), and the second is an object of options, we can call it like that. In this case we have two options - the zoom level and the position to center the map.

![:bulb:](http://materials.ironhack.com/build/emojify.js/dist/images/basic/bulb.png ":bulb:") Check other parameters that you can pass. [(https://developers.google.com/maps/documentation/javascript/reference#MapOptions)](https://developers.google.com/maps/documentation/javascript/reference#MapOptions)

Cool 😎 Isn't it? But this is too simple. Let's add some functionality!

## [](http://materials.ironhack.com/s/rJCE0nGTNN7#adding-markers "adding-markers")Adding Markers

Showing only a map is boring. Google Maps API has a built in functionality to add markers in your map.

![](https://s3-eu-west-1.amazonaws.com/ih-materials/uploads/upload_b4bacbf8c4a457bb4459e70599eb6738.png)

To place a marker we need to create an instance of `google.maps.Marker`

```
const myMarker = new google.maps.Marker({
  position: {
  	lat: 41.3977381,
  	lng: 2.190471916
  },
  map: map,
  title: "I'm here"
});

```

The basic options that you can pass:

- position is an object with latitude and longitude;
- map is the variable that references the instance of our map;
- title is a string that will be displayed when we roll over the marker with the mouse.

Take a look [MarkerOptions object specification](https://developers.google.com/maps/documentation/javascript/3.exp/reference#Marker) for more options.

## [](http://materials.ironhack.com/s/rJCE0nGTNN7#using-browser-location "using-browser-location")Using Browser location

How about we take the position from the browser? Since HTML5, we have a set of Web APIs we can use in modern browsers.

Normally all browser have an object [navigator](https://developer.mozilla.org/en-US/docs/Web/API/Navigator) where we can find the property [geolocation](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/geolocation).

`geolocation` allows accessing to the latitude and longitude coordinates of the browser - *if the user gives us permissions*.

```
...
// Try to get a geolocation object from the web browser
if (navigator.geolocation) {

  // Get current position
  // The permissions dialog will pop up
  navigator.geolocation.getCurrentPosition(function (position) {
    // Create an object to match Google's Lat-Lng object format
    const center = {
      lat: position.coords.latitude,
      lng: position.coords.longitude
    };
    console.log('center: ', center)
    // User granted permission
    // Center the map in the position we got
  }, function () {
    // If something goes wrong
    console.log('Error in the geolocation service.');
  });
} else {
  // Browser says: Nah! I do not support this.
  console.log('Browser does not support geolocation.');
}
...

```

```
// the result of the console.log()
center:
  {
    lat: 41.39780037511012,
    lng: 2.1905911449111493
  }

```

Now let's add a marker with our current position and center the map in the marker. Also, we are going to put a marker in Ironhack Barcelona Campus!

```
function startMap() {

  // Store Ironhack's coordinates
  const ironhackBCN = { lat: 41.3977381,  lng: 2.190471916 };

  // Initialize the map
  const map = new google.maps.Map(document.getElementById('map'),
    {
      zoom: 5,
      center: ironhackBCN
    }
  );

  // Add a marker for Ironhack Barcelona
  const IronhackBCNMarker = new google.maps.Marker({
    position: {
      lat: ironhackBCN.lat,
      lng: ironhackBCN.lng
    },
    map: map,
    title: "Barcelona Campus"
  });

  if (navigator.geolocation) {
    navigator.geolocation.getCurrentPosition(function (position) {
      const user_location = {
        lat: position.coords.latitude,
        lng: position.coords.longitude
      };

      // Center map with user location
      map.setCenter(user_location);

      // Add a marker for your user location
      const ironhackBCNMarker = new google.maps.Marker({
        position: {
          lat: user_location.lat,
          lng: user_location.lng
        },
        map: map,
        title: "You are here."
      });

    }, function () {
      console.log('Error in the geolocation service.');
    });
  } else {
    console.log('Browser does not support geolocation.');
  }
}

startMap();

```

## [](http://materials.ironhack.com/s/rJCE0nGTNN7#drawing-a-route-between-two-pins "drawing-a-route-between-two-pins")Drawing a route between two pins

![](https://s3-eu-west-1.amazonaws.com/ih-materials/uploads/upload_3c015b6b5f72af723673b90693f04280.png)

If we want to draw routes between two pins we have to instantiate [DirectionService](https://developers.google.com/maps/documentation/javascript/directions) and `DirectionRenderer` objects.

```
const directionsService = new google.maps.DirectionsService;
const directionsDisplay = new google.maps.DirectionsRenderer;

```

To specify the route that we want to do, we will make a request using the method `route()`.

```
const directionRequest = {
  origin: { lat: 41.3977381, lng: 2.190471916},
  destination: 'Madrid, ES',
  travelMode: 'DRIVING'
};

directionsService.route(
  directionRequest,
  function(response, status) {
    if (status === 'OK') {
      // everything is ok
      directionsDisplay.setDirections(response);

    } else {
      // something went wrong
      window.alert('Directions request failed due to ' + status);
    }
  }
);

directionsDisplay.setMap(map);

```

`directionsService.route(<optionsObject>, <callback>)` has two parameters: an object with options and callback.

The options can be:

| Field         | Description                                              |
| ------------- | -------------------------------------------------------- |
| `origin`      | `string`, `google.maps.Place`, `LatLng`                  |
| `destination` | `string`, `google.maps.Place`, `LatLng`                  |
| `travelMode`  | `string` as `DRIVING`, `BICYCLING`, `TRANSIT`, `WALKING` |

You can check [directionRequest documentation](https://developers.google.com/maps/documentation/javascript/directions#DirectionsRequests)

## [](http://materials.ironhack.com/s/rJCE0nGTNN7#summary "summary")Summary

In this lesson you learned how to use the basic things with Google Maps API. You successfully created a map, learned how to create a pin and how to draw a route between two pins.

## [](http://materials.ironhack.com/s/rJCE0nGTNN7#extra-resources "extra-resources")Extra Resources

[Google Maps JavaScript Documentation](https://developers.google.com/maps/documentation/javascript/tutorial)

[Google Maps Examples](https://developers.google.com/maps/documentation/javascript/examples/)

[Place Autocomplete and Directions](https://developers.google.com/maps/documentation/javascript/examples/places-autocomplete-directions)
