---
layout: page
title: Travels
permalink: /travels/
description: Places I have been around the world.
nav: true
nav_order: 5
---

<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

<div class="travels-container">

  <!-- Interactive Map -->
  <div id="travel-map" class="travel-map mb-4" style="height: 520px; width: 100%; min-height: 520px; position: relative; border-radius: 12px; overflow: hidden; border: 1px solid var(--global-divider-color);"></div>

  <!-- Continent Directory -->
  <div class="travel-directory mt-4">
    <h3 class="directory-title mb-3">Places by Continent</h3>

    {% assign continents = "Europe,North America,South America,Asia" | split: "," %}

    {% for continent in continents %}
      {% assign continent_places = site.data.places | where: "continent", continent %}
      {% if continent_places.size > 0 %}
        <div class="continent-section mb-3">
          <div class="continent-header mb-2">
            <h4 class="continent-name mb-0">
              {{ continent }} <span class="continent-count">({{ continent_places.size }})</span>
            </h4>
          </div>
          <div class="continent-chips d-flex flex-wrap">
            {% for place in continent_places %}
              <button class="btn place-chip" onclick="zoomToPlace({{ place.latitude }}, {{ place.longitude }}, '{{ place.name | escape }}')">
                {{ place.name }}
              </button>
            {% endfor %}
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
      setTimeout(initMap, 50);
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
    const lightBaseUrl = "https://server.arcgisonline.com/ArcGIS/rest/services/Canvas/World_Light_Gray_Base/MapServer/tile/{z}/{y}/{x}";
    const lightRefUrl = "https://server.arcgisonline.com/ArcGIS/rest/services/Canvas/World_Light_Gray_Reference/MapServer/tile/{z}/{y}/{x}";
    const darkBaseUrl = "https://server.arcgisonline.com/ArcGIS/rest/services/Canvas/World_Dark_Gray_Base/MapServer/tile/{z}/{y}/{x}";
    const darkRefUrl = "https://server.arcgisonline.com/ArcGIS/rest/services/Canvas/World_Dark_Gray_Reference/MapServer/tile/{z}/{y}/{x}";

    const baseLayer = L.tileLayer(isDark ? darkBaseUrl : lightBaseUrl, {
      attribution: 'Tiles &copy; Esri &mdash; Esri, DeLorme, NAVTEQ',
      maxZoom: 16,
    }).addTo(mapInstance);

    const refLayer = L.tileLayer(isDark ? darkRefUrl : lightRefUrl, {
      attribution: '',
      maxZoom: 16,
      pane: "shadowPane",
    }).addTo(mapInstance);

    // Watch dark/light theme toggle
    const observer = new MutationObserver(function() {
      const darkNow = document.documentElement.getAttribute("data-theme") === "dark";
      baseLayer.setUrl(darkNow ? darkBaseUrl : lightBaseUrl);
      refLayer.setUrl(darkNow ? darkRefUrl : lightRefUrl);
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

    // Force tile recalculation
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
