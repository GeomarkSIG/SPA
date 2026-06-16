🐾 Accessibilité aux refuges animaliers — Finistère (29)

Carte interactive et rapport d'analyse territoriale multicritères de l'accessibilité aux refuges animaliers du Finistère.

Réalisé par Geomark Solutions SIG — 2026.

🔗 → Accéder à la carte interactive et au rapport


📌 Contexte

Le Finistère compte 12 refuges animaliers formels recensés sur son territoire et dans ses départements limitrophes. Si le secteur brestois et l'axe Quimper–Douarnenez bénéficient d'une couverture satisfaisante, d'autres zones restent à plus de 45 minutes de tout refuge — notamment le Finistère intérieur (Carhaix-Plouguer, Châteauneuf-du-Faou, Huelgoat) et la presqu'île de Crozon, dont l'enclavement géographique constitue un cas à part entière.

Cette étude spatiale multicritères analyse l'accessibilité aux refuges formels, identifie les zones sous-dotées, et propose des zones d'implantation prioritaires basées sur des données ouvertes. Elle ne présume pas de l'absence de structures partenaires (associations, familles d'accueil, réseaux bénévoles) non recensées dans les bases officielles.


🗺 La carte interactive

La carte propose deux onglets :


🗺 Carte interactive — couches activables/désactivables avec popups informatifs
📄 Rapport d'analyse — 10 sections : données, isochrones, population, méthodologie, zones candidates, bâtiments, focus Crozon, scénarios, conclusion, limites


Groupes de couches disponibles

GroupeContenuÉtablissementsVision étendue : refuges Finistère + limitrophes (SPA Lorient, APAA, Pontivy)Isochrones — Vision étendue< 15 min · 15–30 · 30–45 · 45–60 min (ORS Tools, voiture)Densité × AccessibilitéClassification FILOSOFI 2021 × temps ORS — 3 catégories (vert/orange/rouge)Zones candidates à l'implantationCorridor 1km RN · Zones d'exclusion · Bâtiments candidats · Bâtiments dégradésFocus CrozonIsochrones depuis Crozon · Population presqu'îleScénario futur — Relais Lothey13 refuges · Isochrones recalculés par palierScénario — Fermeture Crozon12 refuges (sans Crozon + relais Lothey) · Isochrones recalculésFond de carteCommunes Finistère · Limite département


Les couches volumineuses (Densité × Accessibilité ~11 MB, Bâtiments ~1,2 MB) sont chargées à la demande depuis le dépôt GitHub.




📊 Données et résultats clés

Sources de données

SourceDescriptionMillésimeFILOSOFI — INSEECarroyage population 200 × 200 m — 55 552 carreaux, 934 000 hab.2021BD TOPO — IGNBâtiments avec attributs NATURE et USAGE2024ORS ToolsCalcul des isochrones (OpenRouteService, réseau OSM, mode voiture)2025Plan Cadastral InformatiséParcelles (data.gouv.fr)2024OpenStreetMapRéseau routier, fond de carte2025

Couverture de la population finistérienne — Situation actuelle

Calculs basés sur l'union géométrique des isochrones clippée au département (6 755 km²).

PalierPopulation% Finistère< 15 min198 695 hab.21,3 %15–30 min459 280 hab.49,2 %30–45 min212 653 hab.22,8 %45–60 min52 048 hab.5,6 %> 60 min11 324 hab.1,2 %

Comparaison des scénarios futurs

PalierActuelCas 1 — Relais LotheyΔCas 2 — Sans CrozonΔ< 15 min198 695236 528+37 833221 769+23 07415–30 min459 280526 087+66 807515 620+56 34030–45 min212 653158 697−53 956172 052−40 60145–60 min52 0481 485−50 56310 528−41 520> 60 min11 32411 203−12114 031+2 707


Cas 1 : maintien de Crozon + nouveau refuge-relais à Lothey (secteur Châteaulin–Port-Launay)

Cas 2 : fermeture hypothétique de Crozon + nouveau refuge à Lothey




🔬 Méthodologie

1. Calcul des isochrones (ORS Tools)

Isochrones calculés depuis chaque refuge en mode voiture sur le réseau OSM, aux paliers 15 / 30 / 45 / 60 minutes. Vision étendue intégrant les refuges des départements limitrophes (Morbihan, Côtes-d'Armor).

2. Couche Densité × Accessibilité

Croise deux variables pour chaque carreau FILOSOFI 2021 :


ind_inc — indice de densité normalisé. Seuils : Q3 = 0,15 (75e percentile) · P90 = 0,30 (90e percentile)
AA_MINS — temps de trajet ORS vers le refuge le plus proche


3 catégories (ensemble de règles QGIS) :

WHEN "AA_MINS" <= 30                              → VERT  (bien desservi)
WHEN "AA_MINS" > 30 AND "AA_MINS" <= 45 AND "ind_inc" > 0.30  → ORANGE (à surveiller)
WHEN "AA_MINS" > 45 AND "ind_inc" > 0.30         → ROUGE (prioritaire)

3. Zones candidates à l'implantation

Trois filtres successifs appliqués dans QGIS :


Clusters DBSCAN — ε = 600 m, minPts = 3 → 171 clusters valides de population sous-dotée · buffer 5 km dissous
Corridor routier — intersection avec corridor 1 km autour des routes nationales (N165, N12, N164)
Exclusions — buffer 100 m bâti existant · Parc Naturel Régional d'Armorique · forêts domaniales · végétation dense


4. Identification des parcelles candidates

Pour les zones retenues, la prospection foncière s'appuie sur :


PCI Vecteur (data.gouv.fr) — numéros de parcelles
DGFIP (service ADF) — identité des propriétaires sur demande motivée
Géofoncier (georefip.gouv.fr) — mutations foncières récentes
PLU communaux — compatibilité réglementaire (zones A, AU, Nh)



🗂 Structure du dépôt

index.html                          ← Application principale (carte + rapport, auto-contenu)
index_last.html                     ← Version de sauvegarde précédente

# Données population et accessibilité
carreau_pop.geojson                 ← 55 552 carreaux FILOSOFI 2021 (pop. brute)
densite_access.geojson              ← Carreaux avec classification densité × accessibilité (~11 MB)
communes.geojson                    ← Communes du Finistère (WGS84)
refuges.geojson                     ← 12 refuges finistériens (points)

# Zones candidates
zone_candid_access.geojson          ← Corridor 1 km autour des routes nationales
zone_candid_1km.geojson             ← Zone candidate après intersection corridor 1km
Zone_exclu.geojson                  ← Zones d'exclusion (bâti, PNR, forêts)
zone_implant_large.geojson          ← Zone candidate large (avant exclusions)

# Bâtiments
pop_cible.geojson                   ← Bâtiments > 200 m² en zone candidate (~432 KB)
bati_rehabilit.geojson              ← Bâtiments dégradés — Finistère entier (~1,2 MB)
bati_agri_200.geojson               ← Bâtiments agricoles > 200 m²

# Focus Crozon
pop_crozon.geojson                  ← Carreaux FILOSOFI presqu'île Crozon (~2,6 MB)

# Isochrones — Situation actuelle (vision étendue)
Vison_refuge_globale_moins_15.geojson    ← Isochrones < 15 min
Vison_refuge_globale_15_30.geojson       ← Isochrones 15–30 min
Vison_refuge_globale_30_45.geojson       ← Isochrones 30–45 min
Vison_refuge_globale_45_60.geojson       ← Isochrones 45–60 min

# Isochrones — Scénario futur (relais Lothey, 13 refuges)
Vison_refuge_globale_future_moins_15.geojson
Vison_refuge_globale_future_15_30.geojson
Vison_refuge_globale_future_30_45.geojson
Vison_refuge_globale_future_45_60.geojson

# Isochrones — Scénario fermeture Crozon (12 refuges sans Crozon + relais)
Vision_refuge_sans_Crozon_moins_15.geojson
Vision_refuge_sans_Crozon_15_30.geojson
Vision_refuge_sans_Crozon_30_45.geojson
Vision_refuge_sans_Crozon_45_60.geojson

# Autres scénarios
Future_refuge_Finistere.geojson     ← Points des 13 refuges (scénario relais)
Future_refuge_Finistère_sans_relai.geojson
Vision_finistere_etendue.geojson    ← Refuges Finistère + limitrophes (vision étendue)
Vision_refuge_sans_Crozon.geojson   ← Points des 12 refuges (scénario fermeture)
Departement.geojson                 ← Contour département Finistère (WGS84)


💡 Recommandations principales


Priorité 1 — Refuge-relais à Lothey / Port-Launay : seul point géographique depuis lequel une structure peut simultanément desservir la presqu'île de Crozon (−30 min), le Finistère intérieur et rester accessible depuis Brest et Quimper en < 40 min. Porterait la couverture < 15 min à 25,3 % et réduirait la zone > 45 min à 1,4 % de la population.
Maintien impératif de Crozon : la fermeture laisserait 55 125 habitants sans accès en moins de 45 minutes — un impact irréductible que nul autre refuge ne peut compenser géographiquement.
Prospection foncière ciblée : lancer l'identification parcellaire sur le secteur Châteaulin–Port-Launay–Pleyben via PCI Vecteur + PLU communaux.
Enquête de capacité : contacter les 12 refuges pour obtenir taux d'occupation et listes d'attente — nécessaire pour affiner le diagnostic.
Objectif : couverture < 45 min au-dessus de 95 % de la population finistérienne.



🛠 Stack technique

Afficher l'image
Afficher l'image
Afficher l'image
Afficher l'image

OutilUsageQGIS 3.44 SolothurnTraitement géospatial, calcul isochrones, classification, export GeoJSONORS ToolsCalcul des isochrones sur réseau routier OSMLeaflet.js 1.9.4Cartographie web interactiveFILOSOFI 2021Données de population carroyées 200 m (INSEE)BD TOPO IGNDonnées bâtimentsGitHub PagesHébergement statique (application auto-contenue)

Projection source : Lambert-93 (EPSG:2154) → WGS84 (EPSG:4326) pour le web.


Geomark Solutions SIG — Robin Maume, Géomaticien indépendant · La Réunion

geomarksig.github.io · 2026
