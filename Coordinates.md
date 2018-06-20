var ourCoords = {
 latitude: 47.624851,
 longitude: -122.52099
};

function displayLocation(position) {
 var latitude = position.coords.latitude;
 var longitude = position.coords.longitude;
 console.log("You are at Latitude: " + latitude + ", Longitude: " + longitude);
 var km = computeDistance(position.coords, ourCoords);
 console.log("You are " + km + " km from the WickedlySmart HQ");
}

getCurrentPosition(successHandler, errorHandler, options)

function getMyLocation() { 
  if (navigator.geolocation) { 
  navigator.geolocation.getCurrentPosition(displayLocation, displayError); 
  } else { 
  alert("Oops, no geolocation support"); 
  }
}

function displayError(error) {
 var errorTypes = {
 0: "Unknown error",
 1: "Permission denied by user",
 2: "Position is not available",
 3: "Request timed out"
 };
 var errorMessage = errorTypes[error.code];
 if (error.code == 0 || error.code == 2) {
 errorMessage = errorMessage + " " + error.message;
 }
 console.log(errorMessage);
}

getMyLocation()


//To calculate distance between two points on a sphere

function computeDistance(startCoords, destCoords) {
 var startLatRads = degreesToRadians(startCoords.latitude);
 var startLongRads = degreesToRadians(startCoords.longitude);
 var destLatRads = degreesToRadians(destCoords.latitude);
 var destLongRads = degreesToRadians(destCoords.longitude);
 var Radius = 6371; // radius of the Earth in km
 var distance = Math.acos(Math.sin(startLatRads) * Math.sin(destLatRads) +
 Math.cos(startLatRads) * Math.cos(destLatRads) *
 Math.cos(startLongRads - destLongRads)) * Radius;
 return distance;
}

function degreesToRadians(degrees) {
 var radians = (degrees * Math.PI)/180;
 return radians;
}
