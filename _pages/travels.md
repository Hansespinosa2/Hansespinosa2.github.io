---
layout: page
title: Travels
permalink: /travels/
description: Places I have been around the world.
nav: true
nav_order: 5
---

<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/leaflet@1.9.4/dist/leaflet.min.css" integrity="sha256-p4NxAoJBhIIN+hmNHrzRCf9tD/miZyoHS5obTRR9BMY=" crossorigin="anonymous" />
<script src="https://cdn.jsdelivr.net/npm/leaflet@1.9.4/dist/leaflet.min.js" integrity="sha256-20nQCchB9co0qIjJZRGuk2/Z9VM+kNiyxNV1lvTlZBo=" crossorigin="anonymous"></script>

<div class="travels-container">

  <!-- Overview Stats -->
  <div class="travels-stats row text-center mb-4 g-2">
    <div class="col-4">
      <div class="stat-card">
        <span class="stat-number">86</span>
        <span class="stat-label">Destinations</span>
      </div>
    </div>
    <div class="col-4">
      <div class="stat-card">
        <span class="stat-number">24</span>
        <span class="stat-label">Countries</span>
      </div>
    </div>
    <div class="col-4">
      <div class="stat-card">
        <span class="stat-number">4</span>
        <span class="stat-label">Continents</span>
      </div>
    </div>
  </div>

  <!-- Interactive Map -->
  <div id="travel-map" class="travel-map mb-4" style="height: 520px; width: 100%; min-height: 520px; position: relative; border-radius: 12px; overflow: hidden;"></div>

  <!-- Continent Directory -->
  <div class="travel-directory mt-4">
    <h3 class="directory-title mb-3">Places by Continent</h3>

    {% assign continents = "Europe,North America,South America,Asia" | split: "," %}

    {% for continent in continents %}
      {% assign continent_places = site.data.places | where: "continent", continent %}
      {% if continent_places.size > 0 %}
        <div class="card region-card mb-3">
          <div class="card-header d-flex justify-content-between align-items-center">
            <h4 class="mb-0 region-heading">
              {{ continent }} <span class="badge region-badge">{{ continent_places.size }}</span>
            </h4>
          </div>
          <div class="card-body">
            <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 g-2">
              {% for place in continent_places %}
                <div class="col">
                  <button class="btn btn-outline-place w-100 text-start d-flex justify-content-between align-items-center" onclick="zoomToPlace({{ place.latitude }}, {{ place.longitude }}, '{{ place.name | escape }}')">
                    <span class="place-name text-truncate">{{ place.name }}</span>
                  </button>
                </div>
              {% endfor %}
            </div>
          </div>
        </div>
      {% endif %}
    {% endfor %}
  </div>

</div>

<script>
(function() {
  const places = {{ site.data.places | jsonify }};
  let mapInstance = null;
  const markers = {};

  function initMap() {
    if (typeof L === "undefined") {
      setTimeout(initMap, 100);
      return;
    }

    const mapElement = document.getElementById("travel-map");
    if (!mapElement || mapInstance) return;

    mapInstance = L.map(mapElement, {
      center: [25, 10],
      zoom: 2,
      minZoom: 2,
      maxZoom: 18,
      scrollWheelZoom: true,
    });

    const isDark = document.documentElement.getAttribute("data-theme") === "dark";
    const lightTiles = "https://{s}.basemaps.cartocdn.com/rastertiles/voyager/{z}/{x}/{y}{r}.png";
    const darkTiles = "https://{s}.basemaps.cartocdn.com/dark_all/{z}/{x}/{y}{r}.png";
    const osmTiles = "https://tile.openstreetmap.org/{z}/{x}/{y}.png";

    // Use OpenStreetMap / CartoDB tiles
    const tileUrl = isDark ? darkTiles : lightTiles;
    const tileLayer = L.tileLayer(tileUrl, {
      attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
      maxZoom: 19,
      subdomains: "abcd",
    }).addTo(mapInstance);

    // Watch dark/light theme toggle
    const observer = new MutationObserver(function() {
      const darkNow = document.documentElement.getAttribute("data-theme") === "dark";
      tileLayer.setUrl(darkNow ? darkTiles : lightTiles);
    });
    observer.observe(document.documentElement, { attributes: true, attributeFilter: ["data-theme"] });

    // Custom Oradia SVG pin icon
    const pinIcon = L.divIcon({
      className: "custom-map-marker",
      html: `<svg width="22" height="28" viewBox="0 0 24 30" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M12 0C5.372 0 0 5.373 0 12C0 19.5 12 30 12 30C12 30 24 19.5 24 12C24 5.373 18.628 0 12 0Z" fill="#4f8064" stroke="#ffffff" stroke-width="1.5"/>
        <circle cx="12" cy="11" r="4.5" fill="#ffffff"/>
      </svg>`,
      iconSize: [22, 28],
      iconAnchor: [11, 28],
      popupAnchor: [0, -26],
    });

    const boundsCoords = [];

    places.forEach(function(place) {
      const lat = place.latitude;
      const lng = place.longitude;
      boundsCoords.push([lat, lng]);

      const marker = L.marker([lat, lng], {
        icon: pinIcon,
        title: place.name,
      }).addTo(mapInstance);

      const popupContent = `
        <div class="map-popup-card">
          <h5 class="map-popup-title" style="margin: 0 0 4px 0; font-family: 'Cormorant Garamond', serif; font-size: 1.15rem;">${place.name}</h5>
          <span class="text-muted" style="font-size: 0.85rem;">${place.country}</span>
        </div>
      `;

      marker.bindPopup(popupContent);
      markers[place.name] = marker;
    });

    if (boundsCoords.length > 0) {
      mapInstance.fitBounds(boundsCoords, { padding: [40, 40], maxZoom: 5 });
    }

    // Invalidate size to ensure full tile rendering
    mapInstance.invalidateSize();
    setTimeout(function() {
      if (mapInstance) mapInstance.invalidateSize();
    }, 250);
    setTimeout(function() {
      if (mapInstance) mapInstance.invalidateSize();
    }, 800);
  }

  window.zoomToPlace = function(lat, lng, name) {
    if (!mapInstance) return;
    mapInstance.flyTo([lat, lng], 11, { duration: 1.2 });
    if (markers[name]) {
      setTimeout(function() {
        markers[name].openPopup();
      }, 700);
    }
    const mapElement = document.getElementById("travel-map");
    if (mapElement) {
      mapElement.scrollIntoView({ behavior: "smooth", block: "center" });
    }
  };

  if (document.readyState === "loading") {
    document.addEventListener("DOMContentLoaded", initMap);
  } else {
    initMap();
  }
  window.addEventListener("load", function() {
    if (mapInstance) mapInstance.invalidateSize();
  });
})();
</script>
