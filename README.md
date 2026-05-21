# 🐾 Déserts de Protection Animale — Finistère (29)

Carte interactive et rapport d'analyse territoriale de l'accessibilité aux refuges animaliers en Finistère.  
Réalisé par **Geomark Solutions SIG** pour la **SPA Finistère** — 2026.

🔗 **[Accéder à la carte interactive](https://geomarksig.github.io/SPA/)**

---

## 📌 Contexte

Le Finistère compte 8 établissements de protection animale recensés. Si certains secteurs bénéficient d'une couverture satisfaisante, d'autres zones restent à plus de 45 minutes de tout refuge — notamment le **Finistère intérieur** (Carhaix-Plouguer, Châteauneuf-du-Faou) et la **presqu'île de Crozon**.

Cette étude spatiale multicritères identifie les déserts de protection animale et propose des zones d'implantation prioritaires basées sur des données ouvertes.

---

## 🗺 Carte interactive

La carte propose deux onglets :

- **🗺 Carte interactive** — couches activables/désactivables, popups, 4 fonds de carte
- **📄 Rapport d'analyse** — rapport complet avec méthodologie, statistiques et recommandations

### Fonds de carte disponibles
| Fond | Usage |
|---|---|
| OSM Standard | Vue générale avec labels |
| Fond vierge | Idéal pour visualiser les données sans bruit |
| Fond minimal | Labels seuls, données en avant-plan |
| Satellite | Vérification terrain |

### Groupes de couches
| Groupe | Couches |
|---|---|
| Temps de trajet | Isochrones < 15 / 15–30 / 30–45 / 45–60 min |
| Densité × Accessibilité | Classification 10 classes vert→rouge (FILOSOFI 2021) |
| Zones d'implantation | Zone XXL, finale, large + bâtiments BD TOPO |
| Focus Crozon | Isochrones + population presqu'île |
| Zones candidates | Corridor 1km RN, exclusions |
| Cadastre | Communes Finistère |

---

## 📊 Données

### Sources
| Source | Description |
|---|---|
| **FILOSOFI 2021** — INSEE | Carroyage population 200m × 200m — 55 552 carreaux, 934 560 individus |
| **BD TOPO** — IGN | Bâtiments avec champ NATURE et USAGE |
| **OpenStreetMap** | Réseau routier, fond de carte |
| **ORS Tools** | Calcul des isochrones (OpenRouteService) |
| **Géoportail Urbanisme** | PLU en cours d'intégration |

### Population desservie par refuge (FILOSOFI 2021)

| Refuge | < 15 min | < 30 min | < 45 min | < 60 min |
|---|---|---|---|---|
| L'Arche de Noé — Brest | 156 846 | 335 548 | 477 299 | 638 832 |
| Les Coussinets — Brest | 32 436 | 157 090 | 411 304 | 509 698 |
| Pays de Landerneau | 37 036 | 254 205 | 459 434 | 677 165 |
| Les Mistoufles | 50 335 | 153 342 | 440 530 | 707 989 |
| **Crozon** | **9 010** | **21 035** | **55 322** | **294 691** |
| Plouhinec | 12 154 | 38 392 | 108 598 | 220 752 |
| Quimper | 64 873 | 181 005 | 320 537 | 569 088 |
| Concarneau | 28 941 | 198 662 | 454 946 | 709 411 |

**Totaux :** < 15 min = 391 071 · 15–30 min = 409 995 · 30–45 min = 107 708 · > 45 min = 25 786

---

## 🔬 Méthodologie

### Couche densité × accessibilité

Croise deux variables pour chaque carreau FILOSOFI 2021 :

- **`ind_inc`** — indice normalisé (0.05 → 0.90). Seuils : Q3 = 0.15 · P90 = 0.30
- **`AA_MINS`** — temps ORS vers le refuge le plus proche (15 / 30 / 45 / 60 min / NULL)

10 classes visuelles du vert foncé (bien desservi) au rouge (désert urgent).

### Clusters DBSCAN

- **ε = 600 m**, **minPts = 3**, filtre **CLUSTER_SIZE ≥ 10**
- 171 clusters valides · 303 isolés exclus

### Zone candidate accessible

1. Buffer 5 km clusters prioritaires
2. Intersection corridor 1 km routes nationales
3. Exclusions : buffer 100 m bâti · végétation · PNR · réseau routier · forêts publiques

---

## 📁 Structure du dépôt

```
index.html                    ← Carte + rapport (page principale)
densite_access.geojson        ← 55 552 carreaux FILOSOFI 2021
pop_cible.geojson             ← 1 158 bâtiments BD TOPO candidats
pop_crozon.geojson            ← 13 936 carreaux presqu'île Crozon
zone_implant.geojson          ← Zone candidate finale
zone_implant_large.geojson    ← Zone candidate large
zone_implant_xxl.geojson      ← Zone XXL (buffer 5km clusters)
zone_candid_access.geojson    ← Corridor 1km RN
zone_candid_exclu.geojson     ← Zone avec exclusions
zone_influence_5km.geojson    ← Zone influence 5km carreaux
bati_rehabilit.geojson        ← 1 211 bâtiments en ruine (Finistère entier)
bati_agri_200.geojson         ← Bâtiments agricoles > 200m²
carreau_pop.geojson           ← Carreaux FILOSOFI bruts
communes.geojson              ← Communes Finistère (WGS84)
zone10km.geojson              ← Influence 10km
zone20km.geojson              ← Influence 20km
zone40km.geojson              ← Influence 40km
zones_moins_15min.geojson     ← Isochrones < 15 min
zones_15_30min.geojson        ← Isochrones 15–30 min
zones_30_45min.geojson        ← Isochrones 30–45 min
zones_45_60min.geojson        ← Isochrones 45–60 min
```

---

## 💡 Recommandations

1. **Refuge-relais Châteaulin–Pleyben** — désenclave Crozon ET comble le désert intérieur
2. Exclure la SPA de Lorient (Morbihan) du calcul finistérien
3. Croiser avec les PLU (zones A et AU)
4. Enquête capacité auprès des 8 refuges
5. Visite terrain des 1 158 bâtiments candidats
6. **Objectif** : couverture < 45 min au-dessus de **95%**

---

## 🛠 Technologies

![QGIS](https://img.shields.io/badge/QGIS-3.44_Solothurn-green)
![Leaflet](https://img.shields.io/badge/Leaflet-1.9.4-blue)
![GitHub Pages](https://img.shields.io/badge/GitHub_Pages-deployed-brightgreen)

**QGIS 3.44** · **Leaflet 1.9.4** · **ORS Tools** · **GitHub Pages**

---

**Geomark Solutions SIG** × **SPA Finistère** — 2026  
Lambert-93 (EPSG:2154) → WGS84 (EPSG:4326)
