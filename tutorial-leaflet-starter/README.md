*English version below* 

# leaflet tutorial
## mijn eigen webmap

### leaflet 
Maak interactieve webmaps voor al je devices. Vladimir Agafonkin maakte het en is een opensource javascript library. Dus gratis en vrij te gebruiken. Weet je al wat van HTML, CSS en JavaScript dan kun je snel aan de slag. Als dit niet gesneden koek voor je is dan kun je met deze tutorial ook al heel goed een start maken.

### wat heb je nodig
* beetje kennis van van HTML, CSS, en JavaScript
* teksteditor voor je HTML code, bijv. brackets, sublime text
* internettoegang
* browser, chrome heeft een fijne debugger

### de eerste kaart
1. open je teksteditor 
2. start met een basis HTML pagina
3. sla deze op in een nieuwe folder en noem deze index.html

	~~~~
	<!doctype html>
	<html lang="nl">
	<html>
 		<head>
			<meta charset="utf-8">
    		<title>basis HTML</title>  
    	</head>
 		<body>
     		<H1>voorbeeld</H1>
 		</body>
		</html>
	~~~~		
	

4. Open http://leafletjs.com/download.html
5. scroll naar beneden en knip de meeste recente leaflet bibliotheek

	
	~~~~
	<link rel="stylesheet" href="https://unpkg.com/leaflet@1.0.0-rc.3/dist/leaflet.css" />
	
	<script src="https://unpkg.com/leaflet@1.0.0-rc.3/dist/leaflet.js"></script>
	~~~~
	
		
6. plak de leaflet.css in de head
7. plak de leafletjs bibliotheek in de body. 
	* Vaak zie je dit ook in de head staan. Het is sneller als je het juist zo ver mogelijk onderaan doet. 

8. Open een nieuw bestand. Noem bestand bijvoorbeeld ‘main.css’  en plaats het in een nieuwe map: ‘style’ in dezelfde folder als je index.html. 
9. Je kunt evt. ook gelijk mappen aanmaken voor:  ‘images’  en ‘ js’. 
10. Open je ‘index.html’ bestand en zet de link naar je css bestand in je head

	~~~~
	<link rel="stylesheet" href=“style/main.css"/>
	~~~~

11. verander de titel in bijv. “mijn eerste kaart met leaflet”
12. Zet een ‘div’ in de body 

	~~~~
	<div id="map"></div>
	~~~~

13. de basis is klaar! Geef je “map” altijd een hoogte (en evt breedte). Dit doe je in de main.css

	~~~~
	#map { height: 300px; width:100%;} 
	~~~~
 
14. speel met de aantal px en/of % tot je een mapformaat hebt wat je goed vindt.

	~~~~
	<!doctype html>
	<html lang="nl">
	<html>
	 	<head>
			<meta charset="utf-8">
	    	<title>Mijn eerste kaart met Leaflet</title>  
			<link rel="stylesheet" href="https://unpkg.com/leaflet@1.0.0-rc.3/dist/leaflet.css" />
			<link rel="stylesheet" href="style/main.css"/>
		</head>   
	 	<body>
	     		<H1>voorbeeld</H1>
				<div id="map"></div>
				<script src="https://unpkg.com/leaflet@1.0.0-rc.3/dist/leaflet.js"></script>
	 	</body>
	</html>
	~~~~

### Baselayer	

Voor de echte kaart heb je een baselayer nodig. Dit is je ondergrond kaart. Deze is opgebouwd uit tegels, dat laadt lekker snel. 

1. Neem het script over en plaats in de body

	~~~~
		<script>
			//initialize the map         
			var map = L.map('map').setView([52.18, 5.5308], 11);
	        
			//maak een baselayer - tegels         
			var achtergrondkaart = L.tileLayer('http://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}.png',
			 	{
	    		attribution: '<a href="http://openstreetmap.org">OpenStreetMap</a>contributors, <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>',
	    		maxZoom: 19
				}
			);
	          
			achtergrondkaart.addTo(map);
		</script>       
	~~~~

2. Je hebt nu een kaart gemaakt.
	* var map =  L.map("map"): is het initialiseren van een "map" variabele
	* setView() is een manier voor het centreren van de map (latitude, longitude, zoom level). de projectie is in googlemercator. 
	* Vervolgens voegden we een baselayer van tegels toe. Bijvoorbeeld van OpenStreetMap. 
	* addTo() toevoegen van de laag aan de map
	*

3. Wil je een specifieke plaats in het centrum. Zoek de coordinaten hier: 
http://www.mapcoordinates.net/en		


4. Een andere gratis tegelboer is maps.stamen.com. Deze brengen zelfs drie varianten

	* http://tile.stamen.com/toner/{z}/{x}/{y}.png
	* http://tile.stamen.com/terrain/{z}/{x}/{y}.jpg
	* http://tile.stamen.com/watercolor/{z}/{x}/{y}.jpg


5. Oefen met verschillende tegels, coordinaten en zoomlevels en maak zo je eigen basiskaart.


### markers, cirkels en polygonen
voeg handmatig markers, cirkels en polygonen toe (je eigen woonplaats bijv.). Kies in ieder geval coordinaten die op je kaart liggen.

1. Zet het volgende binnen het script

	~~~~
	var marker = L.marker([51.5, -0.09]).addTo(map);
	~~~~

2. Voeg nog 4 markers toe. (vrienden, of plaatsen waar je ooit gewoond hebt?). Let er wel op dat je steeds de ‘var’ een andere naam geeft. bijv:

	~~~~
	var monique = L.marker([52.070, 4.300]).addTo(map);   
	~~~~

3. Geef elke marker een popup. bij var monique maken we deze popup

	~~~~
	var popup = "schrijf hier je tekst tussen aanhalingstekens.";
	monique.bindPopup(popup); 
	~~~~


4. Zo plaats je een cirkel op de kaart, gebruik je eigen coordinaten

	~~~~
		var circle = L.circle([51.508, -0.11], 500, {
    		color: 'red',
    		fillColor: '#f03',
    		fillOpacity: 0.5
		}).addTo(map);
	~~~~

5. Verbind de markers met een polygoon. Gebruik hiervoor de al eerder gebruikte coordinaten in de juiste volgorde.

	~~~~
	var polygon = L.polygon([
 	   [51.509, -0.08],
	   [51.503, -0.06],
	   [51.51, -0.047]
	]).addTo(map);
	~~~~


6. je script ziet er als volgt uit. Check ook de debugger of alles klopt… 
	
	~~~~
	<script>
	//initialize the map         
	var map = L.map('map').setView([52.18, 5.5308], 11);
	         
	//maak een baselayer - tegels         
	var achtergrondkaart = L.tileLayer('http://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}.png', {
	    attribution: '<a href="http://openstreetmap.org">OpenStreetMap</a>contributors, <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>',
	    maxZoom: 19
	});
	          
	achtergrondkaart.addTo(map);
	       
	//voeg een willekeurige marker toe                       
	var monique = L.marker([52.070, 4.300]);         
	monique.addTo(map);             
	    
	var miranda = L.marker([53.201, 5.799]);         
	miranda.addTo(map);            
	
	var barbel = L.marker([52.351, 4.620]);         
	barbel.addTo(map);  
	         
	var bea = L.marker([51.560, 5.091]);         
	bea.addTo(map);  
	
	//popup toevoegen
	var popup = "Monique woont in Den Haag.";
	monique.bindPopup(popup);   
	         
	var popup1 = "Barbel woon in Heemstede.";
	barbel.bindPopup(popup1)
	
	var popup2 = "Miranda woont in Leeuwarden.";
	miranda.bindPopup(popup2);   
	
	var popup3 = "Bea woont in Tilburg.";
	bea.bindPopup(popup3);   
	
	 //voeg een willekeurig circle toe         
	var circle = L.circle([52.156, 5.387], 4500, {
	    color: 'red',
	    fillColor: '#f03',
	    fillOpacity: 0.5
	}).addTo(map);  
	
	//voeg een willekeurige polygoon toe     
	var polygon = L.polygon([
	    [53.201, 5.799],
	    [52.351, 4.620],
	    [52.070, 4.300], 
	    [51.560, 5.091],
	    
	    ]).addTo(map);              
	</script>
	~~~~

### geoJson-tilelayer
geoJson is de standaard qua data type om webmaps mee te maken. Deze data kun je als kaartlaag toevoegen. 

* Meer weten over geoJson lees je hier https://en.wikipedia.org/wiki/GeoJSON
* ! geoJson werkt vaak alleen op een 'local webserver', meer weten check: https://github.com/mrdoob/three.js/wiki/How-to-run-things-locally

1. plaats het bestand vd.geojson in de js folder
2. plaats vd.png in je imagesfolder
3. neem het script over en check je kaart
    
	~~~~          
	//geojson zonder jQuery met xhr definieer eerst de icon
				
			var vdIcon = L.icon({
	            iconUrl: "images/vd.png",
	            iconSize: [20,20]
	        });
	//maak vervolgens een geojson laag
	        
	       var geojson = L.geoJson(null,{
	            pointToLayer: function(feature,latlng){
	                return L.marker(latlng, {icon: vdIcon});
	            }
	        }).addTo(map);           
	         
	//daarna stop je de daadwerkelijke geojson hierin
	
		var xhr = new XMLHttpRequest();
			xhr.open('GET', encodeURI("js/vd.geojson"));
			xhr.onload = function() {
	    	if (xhr.status === 200) {
	        geojson.addData(JSON.parse(xhr.responseText));
	    } else {
	        alert('Request failed.  Returned status of ' + xhr.status);
	    }
		};
		xhr.send();   
	~~~~
	           
### tips			
* leer de basics van HTML, javascript bij codecademy: https://www.codecademy.com/learn/web
* wil je een speciaal font gebruiken? check ‘google fonts’
* leuke opdracht vind je hier http://maptimeboston.github.io/leaflet-intro/
* lees het online boek 'leaflet tips and tricks, interactive maps made easy' by Malcolm Maclean. https://leanpub.com/leaflet-tips-and-tricks
* bekijk ook de filmpjes over webcartography geoJson and Leaflet van Ian Muehlenhaus. https://www.youtube.com/playlist?list=PLOlUoOtyTOXilBfrGanBziU738fyJdFqn




# English version leaflet tutorial
## My own web-map! 

### Leaflet 
With leaflet you can make interactive web maps for all devices. Leaflet is made by Vladimir Agafonkin and is an open source JAvaScript library. So free to use. If you already know some HTML, CSS and JavaScript, you can start immediately and read through the HTML explanations. If you are not that comfortable with it yet, this tutorial will help you along!

### What do you need?
* A bit of knowledge about HTML, DOM, CSS and JavaScript is useful. A short explanation can be found here: http://alignedleft.com/tutorials/d3/fundamentals
* A text editor for all your code, for example Brackets or Sublime text
* internet
* your browser, for example chrome, which has a nice debugger. 

### Your first map
1. open your text editor 
2. start with a basic HTML page
3. Save the file in a new folder and call the file index.html

	~~~~
	<!doctype html>
	<html lang="nl">
	
	<html>
	 	<head>
			<meta charset="utf-8">
	    		<title>basic HTML</title>  		 
	 	</head>
	       
	 	<body>
	     		<H1>Example</H1>
	 	</body>
	</html>
	~~~~

4. Go to http://leafletjs.com/download.html
5. Scroll down and copy the newest leaflet library release.

	~~~~
	<link rel="stylesheet" href="https://unpkg.com/leaflet@1.0.0-rc.3/dist/leaflet.css" />
	
	<script src="https://unpkg.com/leaflet@1.0.0-rc.3/dist/leaflet.js"></script>
	~~~~
	
		
6. Place the leaflet.css in the head
7. Place the leafletjs library in the body. 
	* JavaScript libraries are often placed in the head. Though, it is best to place them as far as possible to the bottom of the body. This is much quicker while loading! 

8. Open a new file and save this as ‘main.css’ in a new folder called: ‘style’. The style folder is placed in the same folder as where your index.html file is saved. 
9. You can also create the following folders here: ‘images’ and ‘js’. 
10. Open your ‘index.html’ file and put the link to your CSS file in the *head*

	~~~~
	<link rel="stylesheet" href=“style/main.css"/>
	~~~~

11. Change the title to “My first Leaflet map".
12. Place a ‘div’ in the body 

	~~~~
	<div id="map"></div>
	~~~~

13. The basics are done! Provide your "map" always with a height(and optional width). This you do in the main.css

	~~~~
	#map { height: 300px; width:100%;} 
	~~~~
 
14. Change the amount of pixels and/or % to the map size you prefer.

	~~~~
	<!doctype html>
	<html lang="nl">
	<html>
	 	<head>
			<meta charset="utf-8">
	    	<title>My first Leaflet map</title>  
			<link rel="stylesheet" href="https://unpkg.com/leaflet@1.0.0-rc.3/dist/leaflet.css" />
			<link rel="stylesheet" href="style/main.css"/>
		</head>   
	 	<body>
	     		<H1>example</H1>
				<div id="map"></div>
				<script src="https://unpkg.com/leaflet@1.0.0-rc.3/dist/leaflet.js"></script>
	 	</body>
	</html>
	~~~~

### Base layer	

For a real map you need a base layer. This is the background of your map, made out of png tiles, which are quick to load!

1. Put the following script in the body

	~~~~
		<script>
			//initialize the map         
			var map = L.map('map').setView([52.18, 5.5308], 11);
	        
			//Create baselayer - tiles         
			var achtergrondkaart = L.tileLayer('http://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}.png',
			 	{
	    		attribution: '<a href="http://openstreetmap.org">OpenStreetMap</a>contributors, <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>',
	    		maxZoom: 19
				}
			);
	          
			achtergrondkaart.addTo(map);
		</script>       
	~~~~

2. Now you have made a map.
	* var map =  L.map("map"): initializes the "map" variable
	* setView() centres the map (latitude, longitude, zoom level). The projection is Google Mercator. 
	* Next we add our base-layer tiles. For example from OpenStreetMap. 
	* addTo() adds the layer to the map
	

3. Looking for a specific place to centre on? Find your coordinates here:  
http://www.mapcoordinates.net/en		


4. Another free tile provider is maps.stamen.com. These even provide 3 varieties:
Or have a look at https://leaflet-extras.github.io/leaflet-providers/preview/ 

	* http://tile.stamen.com/toner/{z}/{x}/{y}.png
	* http://tile.stamen.com/terrain/{z}/{x}/{y}.jpg
	* http://tile.stamen.com/watercolor/{z}/{x}/{y}.jpg


5. Practice with different tiles, coordinates and zoom levels to make your own base map.


### Markers, circles and polygons
Add custom markers, circles and polygons to your map. (for example your home address). At least, choose coordinates which are on your map.

1. Add the following to your map:

	~~~~
	var marker = L.marker([51.5, -0.09]).addTo(map);
	~~~~

2. Add another 4 markers. (friends, places you lived or visited?). Note: do give the ‘var’ another name every time. Example:

	~~~~
	var monique = L.marker([52.070, 4.300]).addTo(map);   
	~~~~

3. Provide the markers with a pop-up. For monique we add the following pop-up:

	~~~~
	var popup = "Write your pop up text here";
	monique.bindPopup(popup); 
	~~~~


4. How to place a circle on the map, use your own coordinates:

	~~~~
		var circle = L.circle([51.508, -0.11], 500, {
    		color: 'red',
    		fillColor: '#f03',
    		fillOpacity: 0.5
		}).addTo(map);
	~~~~

5. Connect all previous markers with a polygon. Use all previous coordinates and combine them in the right order.
	~~~~
	var polygon = L.polygon([
 	   [51.509, -0.08],
	   [51.503, -0.06],
	   [51.51, -0.047]
	]).addTo(map);
	~~~~


6. Your script should look like the following. Also check the debugger in the browser if everything is correct: F12
	
	~~~~
	<script>
	//initialize the map         
	var map = L.map('map').setView([52.18, 5.5308], 11);
	         
	//Create baselayer - tiles         
	var achtergrondkaart = L.tileLayer('http://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}.png', {
	    attribution: '<a href="http://openstreetmap.org">OpenStreetMap</a>contributors, <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>',
	    maxZoom: 19
	});
	          
	achtergrondkaart.addTo(map);
	       
	//Add markers                      
	var monique = L.marker([52.070, 4.300]);         
	monique.addTo(map);             
	    
	var miranda = L.marker([53.201, 5.799]);         
	miranda.addTo(map);            
	
	var barbel = L.marker([52.351, 4.620]);         
	barbel.addTo(map);  
	         
	var bea = L.marker([51.560, 5.091]);         
	bea.addTo(map);  
	
	//Add pop-ups
	var popup = "Monique lives in Den Haag.";
	monique.bindPopup(popup);   
	         
	var popup1 = "Barbel lives in Heemstede.";
	barbel.bindPopup(popup1)
	
	var popup2 = "Miranda lives in Leeuwarden.";
	miranda.bindPopup(popup2);   
	
	var popup3 = "Bea lives in Tilburg.";
	bea.bindPopup(popup3);   
	
	 //add a circle     
	var circle = L.circle([52.156, 5.387], 4500, {
	    color: 'red',
	    fillColor: '#f03',
	    fillOpacity: 0.5
	}).addTo(map);  
	
	//add a polygon   
	var polygon = L.polygon([
	    [53.201, 5.799],
	    [52.351, 4.620],
	    [52.070, 4.300], 
	    [51.560, 5.091],
	    
	    ]).addTo(map);              
	</script>
	~~~~

### geoJson-tilelayer
geoJson is the standard data type to create web maps with. You can add this data as another map layer. 

* Do you want to know more about geojson have a look at https://en.wikipedia.org/wiki/GeoJSON
* ! geoJson mostly works on a 'local webserver', check: https://github.com/mrdoob/three.js/wiki/How-to-run-things-locally

1. Place the vd.geojson file in your js folder
2. Plave vd.png in your img folder
3. Copy the following script and have a look at your map    
	~~~~          
	//geojson without jQuery with xhr define icon first
				
			var vdIcon = L.icon({
	            iconUrl: "images/vd.png",
	            iconSize: [20,20]
	        });
	//create the geojson layer
	        
	       var geojson = L.geoJson(null,{
	            pointToLayer: function(feature,latlng){
	                return L.marker(latlng, {icon: vdIcon});
	            }
	        }).addTo(map);           
	         
	//add your geojson data to the layer
	
		var xhr = new XMLHttpRequest();
			xhr.open('GET', encodeURI("js/vd.geojson"));
			xhr.onload = function() {
	    	if (xhr.status === 200) {
	        geojson.addData(JSON.parse(xhr.responseText));
	    } else {
	        alert('Request failed.  Returned status of ' + xhr.status);
	    }
		};
		xhr.send();   
	~~~~
	           
### Tips			
* Learn basic HTML, CSS and JavaScript. For example at codecademy: https://www.codecademy.com/learn/web
* Do you want to use a special font? check ‘google fonts’
* Other nice exercise can be found at http://maptimeboston.github.io/leaflet-intro/
* Read the on line book 'leaflet tips and tricks, interactive maps made easy' by Malcolm Maclean. https://leanpub.com/leaflet-tips-and-tricks
* On Youtube watch films about web cartography geoJson and Leaflet of Ian Muehlenhaus. https://www.youtube.com/playlist?list=PLOlUoOtyTOXilBfrGanBziU738fyJdFqn
