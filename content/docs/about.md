# About

I'm a software engineer from Germany, now living in Brooklyn, New York. My passion for coding has lead me to exploring with different technologies throughout the years. While I work at Spotify, the opinions expressed on my blog are solely my own and do not reflect company policy in any way. 

Most of my recent work is only available within Spotify, but see [research]() to see what is available publicly. 

At work I mainly write code in Java, Typescript, Swift, Kotlin and occasionally some C++ and Scala. My side project's backend is written in Typescript and Go as well as Swift and Kotlin for mobile frontend clients.

## Travel
I've decided to visualize my travel history to keep history of countries I've visited while making plans to visit places in the future once we are back to being able to travel around the world (with Japan at the top of my wishlist).

So far I've visited <span id="num-countries">X</span> countries: <span id="country-flags" style="font-family: "></span>
<div id="map" style="height: 400px;"></div>

## Languages

<link rel="stylesheet" type="text/css" href="/css/jquery-jvectormap-2.0.5.css">
<script src="/js/jquery.js"></script>
<script src="/js/jquery-jvectormap-2.0.5.min.js"></script>
<script src="/js/countries.js"></script>
<script src="/js/worldmap.js"></script>
<script type="text/javascript">
document.getElementById("num-countries").innerHTML = countriesVisited.length;
const flagsElem = document.getElementById("country-flags");
var countryColors = {};
countriesVisited.sort();
countriesVisited.forEach(function(countryCode) {
  countryColors[countryCode] = 1; // color the country on the vector map
  var base = 0xDDE6;
  let flagEmoji = countryCode.replace(/./g, function(c) {
    // https://www.fileformat.info/info/unicode/char/1f1e6/index.htm
    return "\uD83C" + String.fromCharCode(0xDDE6 + c.charCodeAt(0) - 'A'.charCodeAt(0));
  });
  const span = document.createElement('span');
  span.innerText = flagEmoji;
  span.style.marginLeft = '0.2em';
  span.style.fontFamily = 'apple color emoji,segoe ui emoji,noto color emoji,android emoji,emojisymbols,emojione mozilla,twemoji mozilla,segoe ui symbol';
  span.title = countryCode;
  flagsElem.appendChild(span);
  flagsElem.appendChild(document.createTextNode(' '));
});
$('#map').vectorMap({
  map: 'world_mill_en',
  backgroundColor: 'white',
  zoomMax: 6,
  regionStyle: {
    initial: {
      fill: '#aaa',
      "fill-opacity": 0.7,
      stroke: 'none',
      "stroke-width": 0,
      "stroke-opacity": 1
    },
    hover: {
      "fill-opacity": 1.0,
    },
  },
  series: {
    regions: [{
      values: countryColors,
      scale: ['#C8EEFF', '#0071A4'],
      normalizeFunction: 'polynomial',
    }],
  },
});
</script>
