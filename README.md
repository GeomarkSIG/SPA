# Déserts de Protection Animale — Finistère

Carte interactive Leaflet de l'analyse spatiale des refuges animaliers en Finistère (29).

## Déploiement GitHub Pages

1. Fork ou push ce dépôt
2. Settings → Pages → Source : `main` / `root`
3. La carte est accessible à `https://[user].github.io/[repo]/`

## Structure du dépôt

```
index.html                  ← Carte Leaflet principale
refuges.geojson             ← 8 établissements de protection animale
zones_moins_15min.geojson   ← Isochrones < 15 min
zones_15_30min.geojson      ← Isochrones 15–30 min
zones_30_45min.geojson      ← Isochrones 30–45 min
zones_45_60min.geojson      ← Isochrones 45–60 min
zone10km.geojson            ← Zones d'influence 10 km
zone20km.geojson            ← Zones d'influence 20 km
zone40km.geojson            ← Zones d'influence 40 km
zone_influence_5km.geojson  ← Zone d'influence 5 km (carreaux)
zone_candid_access.geojson  ← Zones candidates accessibles (1km RN)
zone_candid_exclu.geojson   ← Zones candidates avec exclusions
bati_rehabilit.geojson      ← Bâtiments à réhabiliter (BD TOPO IGN)
bati_agri_200.geojson       ← Bâtiments agricoles >200m² (BD TOPO IGN)
carreau_pop.geojson         ← Carreaux FILOSOFI 200m (chargement lent)
densite_access.geojson      ← Score densité × accessibilité (chargement lent)
```

## Sources

- Population : FILOSOFI 2015 — INSEE
- Bâtiments : BD TOPO — IGN
- Réseau routier : OpenStreetMap
- Isochrones : OpenRouteService (ORS Tools / QGIS)
- Analyse : QGIS 3.x · Lambert-93 (EPSG:2154)

## Réalisé par

SPA Finistère × Geomark Solutions SIG — 2026
