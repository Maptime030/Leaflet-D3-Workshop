*For English see below*

# D3
## grafieken en kaarten maken met d3
is een open javascript bibliotheek. D3 staat voor Data Driven Documents. De data zoek je zelf. De documents zijn web-based (HTML en SVG) en D3 maakt de verbinding tussen de data en de documents(‘drivin’). D3js. is ontwikkeld door Mike Bostock en is volledig open source en vrij beschikbaar op GitHub. Je kunt er prachtige, ook interactieve visualisatie, grafieken van data maken, maar natuurlijk ook een kaart.

* Op de D3 website vind je prachtige voorbeelden, laat je hier vooral inspireren en gebruik de code! https://github.com/mbostock/d3/wiki/Gallery

### wat heb je nodig
* basiskennis van HTML, DOM, CSS en JavaScript is handig. meer uitleg vind je hier: http://alignedleft.com/tutorials/d3/fundamentals
* browser, chrome, heeft een fijne debugger. 

### De eerste kaart
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

4. Ga naar d3js.org. Scroll naar beneden en kopieer de nieuwste release. Aangezien we al utf-8 los in de  head hebben staan, hoeft het niet meer in het script. (utf-8 zorgt ervoor dat alle dakjes en accenten goed komen te staan.)

	~~~~
	<script src="http://d3js.org/d3.v3.min.js"></script>
	~~~~

	* De js bibliotheken, zie je vaak in de head staan. Het is beter om deze zover mogelijk onderaan in de body te plaatsen. Dit scheelt namelijk snelheid bij het laden.


5. Open een nieuw bestand. Noem bestand bijvoorbeeld ‘main.css’ en plaats het in een nieuwe map: ‘style’ in dezelfde folder als je index.html. 
6. Je kunt ook gelijk mappen aanmaken voor: ‘images’ en ‘js’. 
Open je ‘index.html’ bestand en zet de link naar je css bestand in je head

	~~~~
	<link rel="stylesheet" href="style/main.css"/>
	~~~~

7. verander de titel in bijv. “mijn eerste kaart met d3”. je pagina ziet er als volgt uit.

	~~~~
	<!doctype html>
	<html lang="nl">
	<html>
	 	<head>
			<meta charset="utf-8">
	    	<title>Mijn eerste kaart met D3</title> 
			<link rel="stylesheet" href="style/main.css"/>		</head>   
	 	<body>
	     	<H1>voorbeeld</H1>
			<script src="//d3js.org/d3.v3.min.js"></script> 
			<script> hier komt je code </script>
	 	</body>
	</html>
	~~~~


8. Vervang “hier komt je code” met het volgende

	~~~~
		<script> 
			//Width and height
			var w = 500;
			var h = 300;

			//Define map projection
			var projection = d3.geo.mercator()
						.center([ 30, 40 ])
						.translate([ w/2, h/2 ])
						.scale([ w/4 ]);

			//Define path generator
			var path = d3.geo.path()
						.projection(projection);

			//Create SVG
			var svg = d3.select("body")
						.append("svg")
						.attr("width", w)
						.attr("height", h);
			</script>
	~~~~

9. Wat heb je gedaan?
	* // de regel achter de slashes is het commentaar/verduidelijking. Dit geeft de stappen weer wat je aan het doen bent.
	* ; altijd belangrijk geeft het einde van dit stukje code.
	* Als eerste heb je de width en height gedefineerd. 
	* var staat voor variabele. 
	
	~~~~
	//Width and height
		var w = 500;
		var h = 300;
	~~~~
	
 	* vervolgens kiezen we de projectie van de kaart. Mercator is de meest gebruikte
 	* center gaat met longitude en latitude. 
 	* translate zorgt op deze manier ervoor, dat de kaart in het midden komt
	* schaal zegt iets over het zoomniveau.  

	~~~~
	//Define map projection
	 	var projection = d3.geo.mercator()
			 	.center([30, 40])
				.translate([ w/2, h/2 ])
				.scale([ w/7 ]);
	~~~~
				
	* Zodra de variable projection gemaakt is kunnen we de geografische data omzetten naar SVG dmv path 
	
	~~~~
	//Define path generator
		var path = d3.geo.path()
				.projection(projection);
	~~~~			

 	* Vervolgens maken we het ‘canvas’ waarin we de kaart tonen. Je maakt een variabele, die noem je bijv. SVG. 
 	* D3 zorgt ervoor dat we de functies van D3 kunnen aanroepen. 
 	* Select selecteert 1 element van de DOM in dit geval de body. 
 	* vervolgens wordt het SVG toegevoegd met (append) en 
 	* krijgt het nog hoogte en breedte mee (attr. van attribute).
 	
 	~~~~
	//Create SVG
		var svg = d3.select("body")
				.append("svg")
				.attr("width", w)
				.attr("height", h);
	~~~~


### Data
Data inladen, ‘binden’ is de volgende stap. Je kunt D3 koppelen met data van .csv of in dit geval .json files. 

1. plaats het bestand landen.json in je js folder
2. neem het volende script over

	~~~~
	//Load in GeoJSON data
		d3.json("/js/landen.json", function(json) {

	//Bind data and create one path per GeoJSON feature
			svg.selectAll("path")
				   .data(json.features)
				   .enter()
				   .append("path")
				   .attr("d", path);
			});	
	~~~~			
			
3. check in je browser of je een wereldkaart ziet
4. Kijk op https://github.com/mbostock/d3/wiki/Geo-Projections voor verschillende projecties
5. Je kunt nu met de projection en zoom spelen 
6. probeer bijvoorbeeld in te zoomen op Nederland

	~~~~
	var projection = d3.geo.mercator()
				.center([4, 52])
				.translate([ w/2, h/2 ]                                       	 			.scale(1000);
	~~~~


### extra data
Nu kun je bijvoorbeeld ook de vd data als circle inladen.

1. plaats de vd.geojson in je js folder
2. neem het script over 
	
	~~~~
	d3.json("js/vd.geojson", function(data){
                    
     //Create a circle for each city
		svg.selectAll("circle")
  				.data(data.features)
  				.enter()
 	  			.append("circle")
  				.attr("cx", function(d) {
    		//[0] returns the first coordinate (x) of the projected value
  					return projection(d.geometry.coordinates)[0];
  					})
  					.attr("cy", function(d) {
    		//[1] returns the second coordinate (y) of the projected value
  					return projection(d.geometry.coordinates)[1];
  					})
  				.attr("r", 5)
  				.style("fill", "blue")
  				.style("opacity", 0.75);
		});
	~~~~              
                   
3. verander de kleur speel met de styles 

### meer weten?
* boek: interactive data visualization Scott Murray. of online via http://alignedleft.com/tutorials/d3/about
* volg de starter tutorials op youtube van bijvoorbeeld D3.vienno



# D3 English version
## Making maps and graphs with d3
D3 is a open JavaScript library. D3 stands for Data Driven Documents. The data you provide yourself.  D3 makes the connection between your data and the ('driven')documents, which are web-based(HTML and SVG). D3.js is developed by Mike Bostocke and completely open source and free available at Github. With D3, you can make beautiful interactive visualizations, graphs of your date but also: a map!

* On the website of D3 you can find beautiful examples. Be inspired and have a look at their code! https://github.com/mbostock/d3/wiki/Gallery

### What do you need?
* A basic knowledge of HTML, DOM, CSS and JavaScript is useful. A short explanation can be found here: http://alignedleft.com/tutorials/d3/fundamentals
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

4. Go to d3js.org. Scroll down and copy the newest release. Because we already have utf-8 stated in the *head* we do not have to specify it in the script. (utf-8 makes sure all diacritical marks are placed right)

	~~~~
	<script src="http://d3js.org/d3.v3.min.js"></script>
	~~~~

	* JavaScript libraries are often placed in the head. Though, it is best to place them as far as possible to the bottom of the body. This is much quicker while loading! 
	


5. Open a new file and save this as ‘main.css’ in a new folder called: ‘style’. The style folder is placed in the same folder as where your index.html file is saved. 
6. You can also create the following folders here: ‘images’ and ‘js’. 
Open your ‘index.html’ file and put the link to your CSS file in the *head*

	~~~~
	<link rel="stylesheet" href="style/main.css"/>
	~~~~

7. Change the title to “My first map in D3”. Your file will look the following:

	~~~~
	<!doctype html>
	<html lang="nl">
	<html>
	 	<head>
			<meta charset="utf-8">
	    	<title>My first map in D3</title> 
			<link rel="stylesheet" href="style/main.css"/>		
		</head>   
	 	<body>
	     	<H1>Example</H1>
			<script src="//d3js.org/d3.v3.min.js"></script> 
			<script> your code goes here </script>
	 	</body>
	</html>
	~~~~


8. Replace “your code goes here” with:

	~~~~
		<script> 
			//Width and height
			var w = 500;
			var h = 300;

			//Define map projection
			var projection = d3.geo.mercator()
						.center([ 30, 40 ])
						.translate([ w/2, h/2 ])
						.scale([ w/4 ]);

			//Define path generator
			var path = d3.geo.path()
						.projection(projection);

			//Create SVG
			var svg = d3.select("body")
						.append("svg")
						.attr("width", w)
						.attr("height", h);
			</script>
	~~~~

9. What did you do?
	* // text behind the slashes are comments for clarification describing which steps you are taking. They do not do anything. 
	* ; marks the end of a part of code.
	* var stands for variable. 
	* First you defined the width and height of your map (named w and h) for your browser screen(in pixels)
	
	~~~~
	//Width and height
		var w = 500;
		var h = 300;
	~~~~
	
 	* Next we chose our projection of the map. Mercator is the most common.
 	* The centre we set with longitude and latitude. 
 	* translate, in this way, takes care that our map is in the centre of the area.
	* scale is the zoom-level  

	~~~~
	//Define map projection
	 	var projection = d3.geo.mercator()
			 	.center([30, 40])
				.translate([ w/2, h/2 ])
				.scale([ w/7 ]);
	~~~~
				
	* When the projection is created we can transform our geographic data to SVG with the help of D3.geo.path 
	
	~~~~
	//Define path generator
		var path = d3.geo.path()
				.projection(projection);
	~~~~			

 	* Next, we create our 'canvas' where we will display our map. You create a variable and give it a name, for example *svg*. 
 	* D3 is a call to the functions of D3. 
 	* Select, selects one element of the DOM, in this case the *body*. 
 	* append, appends a SVG to the 'canvas' called *svg* 
 	* next we also provide the attributes, width and height (attr. = attributes).
 	
 	~~~~
	//Create SVG
		var svg = d3.select("body")
				.append("svg")
				.attr("width", w)
				.attr("height", h);
	~~~~


### Data
To 'bind' your data to the DOM is the next step. With D3 you can connect data like .csv or in our case .json files.

1. Place the file landen.json in your js folder
2. Copy the following script, below the previous script (index.html)

	~~~~
	//Load in GeoJSON data
		d3.json("/js/landen.json", function(json) {

	//Bind data and create one path per GeoJSON feature
			svg.selectAll("path")
				   .data(json.features)
				   .enter()
				   .append("path")
				   .attr("d", path);
			});	
	~~~~			
			
3. check in your browser if you see a world map
4. Have a look at https://github.com/mbostock/d3/wiki/Geo-Projections for different projections
5. You can also play around with the projection, centre and zoom level. 
6. For example, try to zoom in on the Netherlands!

	~~~~
	var projection = d3.geo.mercator()
				.center([4, 52])
				.translate([ w/2, h/2 ]                                       	 			.scale(1000);
	~~~~


### Extra data
Now we will load the vd data and visualize it as circles. (from the leaflet starter workshop)

1. Put the vd.geojson file in your js folder
2. Copy the next script
	
	~~~~
	d3.json("js/vd.geojson", function(data){
                    
     //Create a circle for each city
		svg.selectAll("circle")
  				.data(data.features)
  				.enter()
 	  			.append("circle")
  				.attr("cx", function(d) {
    		//[0] returns the first coordinate (x) of the projected value
  					return projection(d.geometry.coordinates)[0];
  					})
  					.attr("cy", function(d) {
    		//[1] returns the second coordinate (y) of the projected value
  					return projection(d.geometry.coordinates)[1];
  					})
  				.attr("r", 5)
  				.style("fill", "blue")
  				.style("opacity", 0.75);
		});
	~~~~              
                   
3. Change the colours and play around with the style attributes! 

### Do you want to learn more?
* Book: interactive data visualization Scott Murray. Or on-line via http://alignedleft.com/tutorials/d3/about
* follow tutorials on YouTube for example of D3.vienno
