<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Ressources naturelles du Canada</title>


  <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
  <script src="https://d3js.org/d3.v7.min.js"></script>
  <link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css" />
  <script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>
 


  <style> 
    body {
      font-family: 'Nunito', sans-serif;
      margin: 0;
      background-color: #e3e2dbc7;
      color: #070707;
    }

    header {
      background-color: #056873;
      color: #f9f9f9;
      padding: 30px 20px;
      text-align: center;
    }

    
    .key-numbers {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-around;
      gap: 20px;
      margin-bottom: 30px;
    }

    .key-number {
      background: #66a37c;
      padding: 20px;
      border-radius: 10px;
      flex: 1 1 200px;
      text-align: center;
    }

    
    section {
      max-width: 1200px;
      margin: 0 auto;
      padding: 40px 20px;
    }

    h2 {
      color: #062123;
      margin-bottom: 20px;
    }

    p.description {
      font-size: 1.1em;
      margin-bottom: 30px;
      color: #555;
    }
    


    #filters {
      display: flex;
      flex-wrap: wrap;
      gap: 20px;
      justify-content: center;
      margin-bottom: 30px;
    }

    .legend {
      display: flex;
      align-items: center;
      gap: 10px;
      border-radius: 5px;
      padding: 5px 10px;
      font-size: 14px;
    }

    .color-box {
      width: 18px;
      height: 18px;
      border-radius: 3px;
      border: 1px solid #000000;
    }

    #chart-container {
      width: 100%;
      height: 500px;
      position: relative;
    }

    .tooltip {
      position: absolute;
      background: #fcf5f5;
      border: 1px solid #ccc;
      padding: 6px;
      border-radius: 4px;
      display: none;
      pointer-events: none;
      font-size: 13px;
    }

    #map {
      width: 100%;
      height: 600px;
      border-radius: 10px;
      border: 1px solid #ccc;
    }

    #legend-map {
      margin-top: 20px;
      text-align: left;
    }

    #legend-map ul {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
      list-style: none;
      padding: 0;
      gap: 8px;
    }

    #legend-map li {
      display: flex;
      align-items: center;
      font-size: 14px;
    }

    #legend-map span {
      display: inline-block;
      width: 16px;
      height: 16px;
      margin-right: 8px;
      border-radius: 3px;
    }
   .color-box {
      width: 15px;
      height: 15px;
      display: inline-block;
    }
    
    footer {
      background-color: #056873;
      color: #f9f2f2;
      padding: 20px;
      text-align: center;
      font-size: 14px;
    }
    
     #text-image-container {
      text-align: center;
      margin-top: 40px;
    }

    #text-image-container img {
      max-width: 100%;
      height: auto;
      border-radius: 8px;
      margin-top: 20px;
    }

    #text-image-container p {
      font-size: 1.2em;
      color: #444;
      margin-top: 20px;
      font-weight: bold;
    }
  </style>
</head>
<body>

<header>
  <h1>Les Ressources Naturelles du Canada</h1>
  <p>Analyse économique et géographique des richesses du sol  
</header>

<section>

  <div class="content-block">
    <h2>Bienvenue,</h2>
    <p class="description">
      Le Canada est reconnu comme un chef de file mondial dans le secteur de l’exploitation minière. Son secteur des minéraux, qui englobe l’exploration, l’extraction, les activités de soutien, la transformation primaire et la fabrication de produits en aval, constitue un pilier essentiel de l’économie nationale. Présent dans chaque province et territoire, il soutient des milliers d’emplois et stimule l’activité économique à l’échelle du pays, tout en jouant un rôle stratégique dans la transition vers une économie plus verte grâce à l’exploitation responsable de ressources critiques. Ce site met en valeur l’évolution économique des principales ressources naturelles du Canada à travers un graphique interactif et une carte localisant les sites d’exploitation. 
 </p>
     <div class="content-block">
    <h3>Les chiffres clées : </h3>
       
  </div>

  <div class="key-numbers">
      <div class="key-number"><strong>125 milliards de Dollars</strong><br/> au PIB </div>
      <div class="key-number"><strong> 50 millions  </strong> de minerais de Fer produit <br/> </div>
      <div class="key-number"><strong>1e</strong><br/> producteur mondial de potasse </div>
    </div>

  <div class="content-block">
    <h2>Graphique interactif des ressources</h2>
    <p class="description">
      Sélectionnez les types de ressources ci-dessous pour visualiser leur évolution en millions de dollars de 2013 à 2023.
    </p>

    <div id="filters">
      <div class="legend"><input type="checkbox" id="all-filters" checked> <label for="all-filters"><strong>Toutes</strong></label></div>
      <div class="legend"><div class="color-box" style="background:#080100;"></div> <label><input type="checkbox" class="filter" value="Réserves de charbon" checked> Charbon</label></div>
      <div class="legend"><div class="color-box" style="background:#1f1ea0;"></div> <label><input type="checkbox" class="filter" value="Réserves de pétrole" checked> Pétrole</label></div>
      <div class="legend"><div class="color-box" style="background:#3f8747;"></div> <label><input type="checkbox" class="filter" value="Réserves de potasse" checked> Potasse</label></div>
      <div class="legend"><div class="color-box" style="background:#d6dc20;"></div> <label><input type="checkbox" class="filter" value="Réserves des mines d'or" checked> Or</label></div>
      <div class="legend"><div class="color-box" style="background:#9b8e8e;"></div> <label><input type="checkbox" class="filter" value="Réserves de minerai de fer" checked> Fer</label></div>
      <div class="legend"><div class="color-box" style="background:#d08439;"></div> <label><input type="checkbox" class="filter" value="Stocks en bois" checked> Bois</label></div>
      <div class="legend"><div class="color-box" style="background:#3785ac;"></div> <label><input type="checkbox" class="filter" value="Réserves de minéraux divers" checked> Minéraux divers</label></div>
    </div>

    <div id="chart-container">
      <svg id="chart"></svg>
    </div>
  </div>
    
      <h3>Le Charbon  : </h3>
<p class="description">
      En 2021, les mines canadiennes ont produit environ 42 millions de tonnes de charbon, soit une légère hausse de 2 % par rapport à 2020. Toutefois, la valeur de cette production a doublé, atteignant 8,0 milliards de dollars, principalement en raison de la hausse des prix du charbon métallurgique, utilisé dans la fabrication de l’acier. Le Canada extrait à la fois du charbon thermique (utilisé pour la production d’électricité) et du charbon métallurgique, ce dernier représentant plus de 60 % de la production totale. Dans un effort de transition énergétique, le gouvernement canadien a annoncé en 2018 son intention d’éliminer progressivement la production d’électricité à base de charbon traditionnel d’ici 2030.
 </p>
      <h3>Le Pétrole </h3>
    <p class="description">
      Le Canada est le quatrième producteur mondial de pétrole brut et détient la troisième réserve prouvée de pétrole au monde, principalement dans les sables bitumineux de l’Alberta. En 2022, la production canadienne de pétrole s’élevait à environ 4,6 millions de barils par jour. Le secteur énergétique est un moteur économique majeur, représentant plus de 10 % des exportations canadiennes.
      </p> 
    
      <h3>La Potasse </h3>
       <p class="description">
         Le Canada est le premier producteur mondial de potasse, un engrais essentiel à l’agriculture mondiale. La Saskatchewan concentre l’essentiel de cette production, qui a atteint près de 23 millions de tonnes en 2022, alimentant les marchés d’Asie, d’Amérique du Sud et d’Europe.
      </p> 
    
      <h3>L'Or </h3>
       <p class="description">
         L’or est l’un des métaux précieux les plus exploités au Canada, avec une production de près de 223 tonnes en 2022. Le pays se classe 5e producteur mondial, avec des mines actives en Ontario, au Québec, au Nunavut et en Colombie-Britannique.
      </p> 
    
      <h3>Le Fer : </h3>
       <p class="description">
         Le Canada est un important producteur de minerai de fer, principalement concentré au Québec et à Terre-Neuve-et-Labrador. En 2021, la production dépassait 50 millions de tonnes, servant surtout à l’exportation, notamment vers l’Europe et l’Asie.
      </p> 
    
      <h3>Le Bois : </h3>
       <p class="description">
         Les forêts couvrent environ 38 % du territoire canadien, soit près de 347 millions d’hectares. Le Canada est l’un des principaux exportateurs mondiaux de bois d’œuvre, de pâte à papier et de papier journal. L’industrie forestière emploie directement environ 200 000 personnes, particulièrement dans les régions rurales.
      </p> 
      <h3>Les Mineraux divers: </h3>
     <p class="description">
       Le Canada est riche en minéraux essentiels à la transition énergétique, comme le lithium, le cobalt, le nickel, le cuivre, le graphite et les terres rares. Le pays investit massivement dans leur développement pour répondre à la demande croissante liée aux batteries, aux véhicules électriques et aux technologies propres.
      </p> 
    
    
  <div class="content-block">
    <h2>Carte des sites miniers</h2>
    <p class="description">Ci-dessous, la carte interactive affiche les principaux sites d’exploitation au Canada. Cliquez sur un point pour savoir de quels types de minnes il s'agit. </p>
    <div id="map"></div>
    <div id="legend-map">
      <h4>Légende</h4>
      <ul id="legend-list"></ul>
    </div>
  </div>

  <div id="text-image-container">
    <p> Pour aller plus loin : l'infographie  sur les ressources naturelles du Canada </p>
    <img src="Infographie_E_BAUDRILLER.jpg" alt="Infographie des ressources naturelles du Canada" />
  </div>
  
</body>
  
</section>

<footer>
  <p>&copy; Baudriller Eglantine – Les Ressources naturelles du Canada</p>
</footer>

<script>
  const data = {
    "Réserves de charbon": [40479, 24631, 15611, 31302, 76144, 76805, 53711, 34745, 105021, 198604, 200141],
    "Réserves de pétrole": [357943, 526148, 64534, 51177, 307345, 335090, 400908, 80668, 402895, 855303, 607532],
    "Réserves de potasse": [67370, 47785, 54040, 0, 8632, 43422, 57138, 65973, 98199, 318380, 140345],
    "Réserves des mines d'or": [0, 2468, 6977, 12087, 15666, 19198, 17313, 42326, 34741, 41253, 52188],
    "Réserves de minerai de fer": [68670, 33479, 4228, 14615, 48627, 55171, 75764, 120209, 177801, 125334, 121025],
    "Stocks en bois": [160346, 179062, 175586, 184490, 244019, 307140, 184875, 221297, 449027, 376857, 266570],
    "Réserves de minéraux divers": [48095.5, 47563.1, 54591.0, 45912.0, 58006.8, 57120.4, 59928.2, 48946.3, 71042.2, 81567.5, 92071.8]
  };

  const colors = {
    "Réserves de charbon": "#080100",
    "Réserves de pétrole": "#1f1ea0",
    "Réserves de potasse": "#3f8747",
    "Réserves des mines d'or": "#d6dc20",
    "Réserves de minerai de fer": "#9b8e8e",
    "Stocks en bois": "#d08439",
    "Réserves de minéraux divers": "#3785ac"
  };

  const years = [2013, 2014, 2015, 2016, 2017, 2018, 2019, 2020, 2021, 2022, 2023];

  function updateChart() {
    const selected = $(".filter:checked").map(function () { return this.value; }).get();
    const svg = d3.select("#chart").html("").attr("width", 1000).attr("height", 500);
    const margin = { top: 20, right: 30, bottom: 50, left: 80 },
          width = 1000 - margin.left - margin.right,
          height = 500 - margin.top - margin.bottom;

    const x = d3.scaleBand().domain(years).range([0, width]).padding(0.2);
    const y = d3.scaleLinear().domain([0, d3.max(Object.values(data).flat())]).range([height, 0]);

    const g = svg.append("g").attr("transform", `translate(${margin.left},${margin.top})`);
    g.append("g").attr("transform", `translate(0,${height})`).call(d3.axisBottom(x));
    g.append("g").call(d3.axisLeft(y).tickFormat(d3.format(",")));

    const tooltip = d3.select("body").append("div").attr("class", "tooltip");

    selected.forEach((res, i) => {
      g.selectAll(`.bar-${i}`)
        .data(data[res])
        .enter().append("rect")
        .attr("x", (_, j) => x(years[j]) + (i * (x.bandwidth() / selected.length)))
        .attr("y", height)
        .attr("width", x.bandwidth() / selected.length)
        .attr("height", 0)
        .attr("fill", colors[res])
        .on("mouseover", function (event, d) {
          tooltip.style("display", "block").html(`${res}: ${d.toLocaleString()} M$`)
            .style("left", (event.pageX + 10) + "px")
            .style("top", (event.pageY - 20) + "px");
        })
        .on("mousemove", function (event) {
          tooltip.style("left", (event.pageX + 10) + "px")
            .style("top", (event.pageY - 20) + "px");
        })
        .on("mouseout", function () {
          tooltip.style("display", "none");
        })
        .transition().duration(800)
        .attr("y", d => y(d))
        .attr("height", d => height - y(d));
    });
  }

  $("#all-filters").change(function () {
    $(".filter").prop("checked", this.checked);
    updateChart();
  });

  $(".filter").change(updateChart);
  updateChart();


  const map = L.map('map').setView([48, -72], 6);
  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '© OpenStreetMap contributors'
  }).addTo(map);

  const categories = {
    "Aluminium": "#18e2c9",
    "Calcaire": "#c0b5b5",
    "Charbon": "#080100",
    "Cuivre": "#b15d10",
    "Diamants": "#0c07ee",
    "Fer": "#c08e5d",
    "Gypse": "#d3d4ac",
    "Helium": "#2c3e50",
    "Lithium": "#182047",
    "Magnesium": "#637667",
    "Nickel": "#1d0d0d",
    "Or": "#d6dc20",
    "Petrole": "#321942",
    "Potasse": "#253727",
    "Sel": "#146d85",
    "Resources Rare": "#0e98ce",
    "Uranium": "#8859b4",
    "Zinc": "#2e484e",
    

  };

  const produits = [
    // Aluminium
  { id: 1, product: 'Aluminium', latitude: 48.43, longitude: -71.17565 },
  { id: 2, product: 'Aluminium', latitude: 50.16, longitude: -66.4429 },
  { id: 3, product: 'Aluminium', latitude: 49.00, longitude: -68.1429 },
  { id: 4, product: 'Aluminium', latitude: 48.75, longitude: -69.2501 },
  { id: 5, product: 'Aluminium', latitude: 50.22, longitude: -67.1429 },
  { id: 6, product: 'Aluminium', latitude: 47.89, longitude: -69.8002 },
  { id: 7, product: 'Aluminium', latitude: 45.77, longitude: -75.8703 },

  // Calcaire
  { id: 8, product: 'Calcaire', latitude: 47.88, longitude: -69.1015 },
  { id: 9, product: 'Calcaire', latitude: 46.32, longitude: -70.1924 },
  { id: 10, product: 'Calcaire', latitude: 44.87, longitude: -70.2183 },
  { id: 11, product: 'Calcaire', latitude: 45.23, longitude: -69.3489 },
  { id: 12, product: 'Calcaire', latitude: 45.53, longitude: -72.1342 },
  { id: 13, product: 'Calcaire', latitude: 45.74, longitude: -72.8917 },
  { id: 14, product: 'Calcaire', latitude: 44.99, longitude: -71.2582 },

  // Charbon
  { id: 15, product: 'Charbon', latitude: 49.26, longitude: -68.1491 },
  { id: 16, product: 'Charbon', latitude: 50.31, longitude: -67.3448 },
  { id: 17, product: 'Charbon', latitude: 48.60, longitude: -69.0007 },
  { id: 18, product: 'Charbon', latitude: 47.94, longitude: -69.1250 },
  { id: 19, product: 'Charbon', latitude: 49.05, longitude: -67.2123 },
  { id: 20, product: 'Charbon', latitude: 50.13, longitude: -68.4512 },
  { id: 21, product: 'Charbon', latitude: 48.70, longitude: -68.8479 },

  // Cuivre
  { id: 22, product: 'Cuivre', latitude: 50.34, longitude: -64.1479 },
  { id: 23, product: 'Cuivre', latitude: 51.11, longitude: -63.3301 },
  { id: 24, product: 'Cuivre', latitude: 49.82, longitude: -67.4389 },
  { id: 25, product: 'Cuivre', latitude: 48.56, longitude: -66.7249 },
  { id: 26, product: 'Cuivre', latitude: 50.25, longitude: -67.9373 },
  { id: 27, product: 'Cuivre', latitude: 49.90, longitude: -65.2831 },
  { id: 28, product: 'Cuivre', latitude: 50.12, longitude: -68.0569 },

  // Diamants
  { id: 29, product: 'Diamants', latitude: 45.65, longitude: -75.7803 },
  { id: 30, product: 'Diamants', latitude: 45.76, longitude: -76.1581 },
  { id: 31, product: 'Diamants', latitude: 46.43, longitude: -72.9285 },
  { id: 32, product: 'Diamants', latitude: 45.88, longitude: -74.9356 },
  { id: 33, product: 'Diamants', latitude: 44.76, longitude: -72.7023 },
  { id: 34, product: 'Diamants', latitude: 47.56, longitude: -74.2763 },
  { id: 35, product: 'Diamants', latitude: 45.28, longitude: -73.8515 },

  // Fer
  { id: 36, product: 'Fer', latitude: 46.10, longitude: -74.5521 },
  { id: 37, product: 'Fer', latitude: 45.22, longitude: -73.3135 },
  { id: 38, product: 'Fer', latitude: 44.56, longitude: -71.8242 },
  { id: 39, product: 'Fer', latitude: 45.84, longitude: -70.3420 },
  { id: 40, product: 'Fer', latitude: 46.50, longitude: -69.7842 },
  { id: 41, product: 'Fer', latitude: 47.44, longitude: -72.1407 },
  { id: 42, product: 'Fer', latitude: 44.99, longitude: -70.7024 },

  // Gypse
  { id: 43, product: 'Gypse', latitude: 45.72, longitude: -75.2072 },
  { id: 44, product: 'Gypse', latitude: 45.81, longitude: -74.3928 },
  { id: 45, product: 'Gypse', latitude: 46.00, longitude: -73.6932 },
  { id: 46, product: 'Gypse', latitude: 44.88, longitude: -70.6341 },
  { id: 47, product: 'Gypse', latitude: 45.33, longitude: -72.8320 },
  { id: 48, product: 'Gypse', latitude: 44.51, longitude: -73.8472 },
  { id: 49, product: 'Gypse', latitude: 45.64, longitude: -75.6509 },

  // Helium
  { id: 50, product: 'Helium', latitude: 45.88, longitude: -74.2149 },
  { id: 51, product: 'Helium', latitude: 46.76, longitude: -75.3779 },
  { id: 52, product: 'Helium', latitude: 44.99, longitude: -73.1927 },
  { id: 53, product: 'Helium', latitude: 45.45, longitude: -72.6673 },
  { id: 54, product: 'Helium', latitude: 45.88, longitude: -74.0091 },
  { id: 55, product: 'Helium', latitude: 46.10, longitude: -73.4120 },
  { id: 56, product: 'Helium', latitude: 46.29, longitude: -72.1562 },

  // Lithium
  { id: 57, product: 'Lithium', latitude: 45.29, longitude: -75.2100 },
  { id: 58, product: 'Lithium', latitude: 44.79, longitude: -73.2339 },
  { id: 59, product: 'Lithium', latitude: 45.69, longitude: -72.5489 },
  { id: 60, product: 'Lithium', latitude: 46.54, longitude: -75.0389 },
  { id: 61, product: 'Lithium', latitude: 45.33, longitude: -74.1228 },
  { id: 62, product: 'Lithium', latitude: 46.16, longitude: -73.5401 },
  { id: 63, product: 'Lithium', latitude: 45.71, longitude: -72.7654 },

  // Magnesium
  { id: 64, product: 'Magnesium', latitude: 45.90, longitude: -75.0194 },
  { id: 65, product: 'Magnesium', latitude: 46.34, longitude: -72.3308 },
  { id: 66, product: 'Magnesium', latitude: 46.04, longitude: -70.8715 },
  { id: 67, product: 'Magnesium', latitude: 45.64, longitude: -72.2681 },
  { id: 68, product: 'Magnesium', latitude: 45.98, longitude: -73.1417 },
  { id: 69, product: 'Magnesium', latitude: 45.72, longitude: -73.8926 },
  { id: 70, product: 'Magnesium', latitude: 44.86, longitude: -71.3501 },

  // Nickel
  { id: 71, product: 'Nickel', latitude: 45.95, longitude: -74.1489 },
  { id: 72, product: 'Nickel', latitude: 45.66, longitude: -73.6195 },
  { id: 73, product: 'Nickel', latitude: 46.01, longitude: -74.1493 },
  { id: 74, product: 'Nickel', latitude: 45.33, longitude: -71.9501 },
  { id: 75, product: 'Nickel', latitude: 45.21, longitude: -73.2025 },
  { id: 76, product: 'Nickel', latitude: 46.45, longitude: -72.5281 },
  { id: 77, product: 'Nickel', latitude: 46.76, longitude: -73.0102 },

  // Or
  { id: 78, product: 'Or', latitude: 45.92, longitude: -73.8272 },
  { id: 79, product: 'Or', latitude: 46.05, longitude: -74.1108 },
  { id: 80, product: 'Or', latitude: 45.74, longitude: -75.2887 },
  { id: 81, product: 'Or', latitude: 46.20, longitude: -72.4739 },
  { id: 82, product: 'Or', latitude: 45.81, longitude: -72.1920 },
  { id: 83, product: 'Or', latitude: 45.33, longitude: -70.9480 },
  { id: 84, product: 'Or', latitude: 46.02, longitude: -73.6165 },

  // Pétrole
  { id: 85, product: 'Petrole', latitude: 45.39, longitude: -75.2189 },
  { id: 86, product: 'Petrole', latitude: 46.07, longitude: -74.2129 },
  { id: 87, product: 'Petrole', latitude: 45.81, longitude: -73.5497 },
  { id: 88, product: 'Petrole', latitude: 46.31, longitude: -73.1147 },
  { id: 89, product: 'Petrole', latitude: 45.45, longitude: -74.2541 },
  { id: 90, product: 'Petrole', latitude: 45.12, longitude: -72.9223 },
  { id: 91, product: 'Petrole', latitude: 46.15, longitude: -73.4898 },

  // Potasse
  { id: 92, product: 'Potasse', latitude: 45.25, longitude: -73.8429 },
  { id: 93, product: 'Potasse', latitude: 45.88, longitude: -72.7523 },
  { id: 94, product: 'Potasse', latitude: 46.03, longitude: -74.4602 },
  { id: 95, product: 'Potasse', latitude: 45.65, longitude: -71.9899 },
  { id: 96, product: 'Potasse', latitude: 46.34, longitude: -72.5294 },
  { id: 97, product: 'Potasse', latitude: 45.77, longitude: -73.2287 },
  { id: 98, product: 'Potasse', latitude: 44.92, longitude: -73.5555 },

  // Sel
  { id: 99, product: 'Sel', latitude: 45.51, longitude: -75.8814 },
  { id: 100, product: 'Sel', latitude: 45.22, longitude: -74.1357 },
  { id: 101, product: 'Sel', latitude: 46.12, longitude: -75.3487 },
  { id: 102, product: 'Sel', latitude: 45.42, longitude: -74.7812 },
  { id: 103, product: 'Sel', latitude: 45.76, longitude: -73.6172 },
  { id: 104, product: 'Sel', latitude: 46.31, longitude: -73.2463 },
  { id: 105, product: 'Sel', latitude: 45.65, longitude: -73.5780 },

  // Terres rares
  { id: 106, product: 'Resources Rare', latitude: 46.30, longitude: -73.8525 },
  { id: 107, product: 'Resources Rare', latitude: 45.98, longitude: -74.3840 },
  { id: 108, product: 'Resources Rare', latitude: 45.59, longitude: -73.6504 },
  { id: 109, product: 'Resources Rare', latitude: 45.89, longitude: -72.1159 },
  { id: 110, product: 'Resources Rare', latitude: 45.47, longitude: -74.0546 },
  { id: 111, product: 'Resources Rare', latitude: 45.68, longitude: -72.6519 },
  { id: 112, product: 'Resources Rare', latitude: 45.91, longitude: -73.5560 },

  // Uranium
  { id: 113, product: 'Uranium', latitude: 45.30, longitude: -73.9943 },
  { id: 114, product: 'Uranium', latitude: 45.57, longitude: -72.9857 },
  { id: 115, product: 'Uranium', latitude: 46.28, longitude: -74.1540 },
  { id: 116, product: 'Uranium', latitude: 45.86, longitude: -73.1279 },
  { id: 117, product: 'Uranium', latitude: 45.33, longitude: -73.9871 },
  { id: 118, product: 'Uranium', latitude: 45.76, longitude: -73.4889 },
  { id: 119, product: 'Uranium', latitude: 46.04, longitude: -72.7827 },

  // Zinc
  { id: 120, product: 'Zinc', latitude: 45.19, longitude: -75.9832 },
  { id: 121, product: 'Zinc', latitude: 45.88, longitude: -73.5241 },
  { id: 122, product: 'Zinc', latitude: 46.23, longitude: -74.2873 },
  { id: 123, product: 'Zinc', latitude: 45.43, longitude: -72.9957 },
  { id: 124, product: 'Zinc', latitude: 45.64, longitude: -73.1263 },
  { id: 125, product: 'Zinc', latitude: 46.13, longitude: -73.4729 },
  { id: 126, product: 'Zinc', latitude: 45.51, longitude: -74.2320 }
];

  produits.forEach(p => {
    L.circleMarker([p.latitude, p.longitude], {
      radius: 8,
      fillColor: categories[p.product] || '#555',
      color: '#222',
      weight: 1,
      fillOpacity: 0.9
    }).addTo(map).bindPopup(`<strong>${p.product}</strong>`);
  });

  const legendList = document.getElementById("legend-list");
  for (let key in categories) {
    const li = document.createElement("li");
    li.innerHTML = `<span style="background:${categories[key]}"></span>${key}`;
    legendList.appendChild(li);
  }
</script>
  
</body>
</html>
