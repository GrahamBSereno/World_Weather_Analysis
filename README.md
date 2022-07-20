# World_Weather_Analysis


<!DOCTYPE html>
<meta charset="utf-8">
<head>
  <title>Geo (spinning))</title>
</head>

<style>
body {
  font-family: "Helvetica Neue", Helvetica, sans-serif;
  font-size: 14px;
  color: #333;
  background-color: #eee;
}
</style>

<body>
  <div id="content">
    <canvas width="1800" height="1600"></canvas>
  </div>

  <script src="https://cdnjs.cloudflare.com/ajax/libs/d3/4.2.2/d3.min.js"></script>

  <script>
var geojson = {}

var context = d3.select('#content canvas')
  .node()
  .getContext('2d');

var projection = d3.geoOrthographic()
  .scale(600)
  .translate([900, 700]);

var geoGenerator = d3.geoPath()
  .projection(projection)
  .pointRadius(4)
  .context(context);

var yaw = 320;

function update() {
  projection.rotate([yaw])

  context.clearRect(0, 0, 1800, 1600);

  context.lineWidth = 0.3;
  context.strokeStyle = '#333';

  context.beginPath();
  geoGenerator({type: 'FeatureCollection', features: geojson.features})
  context.stroke();

  yaw -= 0.2
}



// REQUEST DATA
d3.json('ne_110m_admin_0_countries.json', function(err, json) {
  geojson = json;
  window.setInterval(update, 100);
  update()
})

  </script>
</body>
</html>
