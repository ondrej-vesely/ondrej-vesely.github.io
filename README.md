The **The Why Factory Globe** is a fork of open platform for geographic data visualization created by the Google Data Arts Team aproprieted for The Why Factory studio at TU Delft.

Check out the original project at https://experiments.withgoogle.com/chrome/globe.

----

**The WebGL Globe** supports data in `JSON` format, a sample of which you can find [here](https://github.com/dataarts/webgl-globe/blob/master/globe/population909500.json). `webgl-globe` makes heavy use of the [Three.js library](https://github.com/mrdoob/three.js/).

# Data Format

The following illustrates the `JSON` data format that the globe expects:

```javascript
var data = [
    [
    'seriesA', [ latitude, longitude, magnitude, latitude, longitude, magnitude, ... ]
    ],
    [
    'seriesB', [ latitude, longitude, magnitude, latitude, longitude, magnitude, ... ]
    ]
];
```

# Basic Usage

The following code polls a `JSON` file (formatted like the one above) for geo-data and adds it to an animated, interactive WebGL globe.

```javascript
// Where to put the globe?
var container = document.getElementById( 'container' );

// Make the globe
var globe = new DAT.Globe( container );

// We're going to ask a file for the JSON data.
var xhr = new XMLHttpRequest();

// Where do we get the data?
xhr.open( 'GET', 'myjson.json', true );

// What do we do when we have it?
xhr.onreadystatechange = function() {

    // If we've received the data
    if ( xhr.readyState === 4 && xhr.status === 200 ) {

        // Parse the JSON
        var data = JSON.parse( xhr.responseText );

        // Tell the globe about your JSON data
        for ( var i = 0; i < data.length; i ++ ) {
            globe.addData( data[i][1], {format: 'magnitude', name: data[i][0]} );
        }

        // Create the geometry
        globe.createPoints();

        // Begin animation
        globe.animate();

    }

};

// Begin request
xhr.send( null );
```
