---
marp: true
class: invert
---

<style>
  @import url('https://fonts.googleapis.com/css2?family=Fira+Code&display=swap');

  section {
    font-family: 'Fira Code', monospace;
    font-size: 1.5em;
  }

  h1,
  h2,
  h3,
  h4,
  h5,
  h6 {
    text-shadow: rgba(9,75,113,0.5) 0px 0px 18px;
  }
</style>


![Mercury logo](./imgs/mercury-logo-white.png)
Coming real soon now

---

# |- Why ?

  ⚙️ Mercury has not been created with customisation in mind

  🙃 With each new features the soft is harder to maintain

  👓 Responsabilities between front and back are uncleared

  👶 The front stack (Twig/jQuery) is a bit weak for complex UI

  ⚠️ API endpoints does not respect any REST conventions 

  ⏳ Mercury does not bring great UX with long loading times, infinite tab opening, no direct links, etc...

---

# |- How ?

  🚀 API REST 
    ✅ PHP 8 
    ✅ Symfony 5.4
  ⚡ React
  🐋 Docker
  🔥 Google Cloud Platform

---

# |- New

Alias des noms de gènes ![TP53 alias](./imgs/genes-alias-TP53.png)
  - La recherche peut se faire sur les alias des noms de gènes
  - Les alias sont affichés dans les résultats de recherche
  - Les alias sont affichés dans les détails d'un gène

Un back-office pour les bioinfs et les commerciaux qui permet de :
  - Créer des utilisateurs
  - Créer des licences
  - Ajouter des crédits aux licences
  - Gérer les analyses dans les licences
  - Gérer les utilisateurs dans les licences
  - Gérer les rôles des utilisateurs pour chaque licence

Caching

---

# |- Update

Les comptages vont être relancés sur chaque analyse
  - Les comptages seront plus précis
  - Une seule source de vérité (au lieu de 3 actuellement)

Les filtres sont maintenant personnelles
  - Ils peuvent aussi être partagés avec d'autres utilisateurs de ses licences
  - Nouvelle page de gestion des filtres

Nouveau système de cloud-function pour gérer les demandes d'analyses en ligne
  - Plus de problème de token qui expire pendant l'upload : 
    -- Les analyses auront le bon statut
    -- Les emails pour prévenir les bioinfs d'une nouvelle analyse seront envoyés
  - Les analyses ne se crées pas à l'avance mais uniquement quand l'upload aboutit
  - Les crédits se débitent quand l'upload aboutit

---

# ConfigManager 🔧

---

## What is configurable ?

📊 Filters
  - CNA, exons, fusions, germline, somatic, RNA only, QC genes, QC hotspots

🧮 Counting filters
  - CNA, germline, somatic, QC Genes, QC Hotspots

🖥️ Overview

📋Report blocks

---
## How is it better ?

One place instead of being spread in the code

App code is now designed to be more flexible and is not anymore an accumulation of special cases

New config as easy as a copy/paste thanks to overriding/inheritance

Powerfull JSON syntax accessible for everyone (bioinf, dev) _(yet to be documented)_

Versionning of the configuration thanks to git

No more need to deploy the app to change the config

New config slice can be considered more easily

---

# Some User stories

---

## From connection to PDF

- Login to Overview
- Overview to results
- Click variant to modal
- Id card button to page  
- Go back to somatic page
- Change filters to result
- Clicinal report link to page

Legacy : https://www.loom.com/share/5b45b11d702349c899d5c78cf475bf0a
Rework : https://www.loom.com/share/cdd431d776a941f3bcf76e513898b208

---
## Results

| Step                         | Legacy | Rework | Absolute gain (s) | Relatif gain (%) |
|------------------------------|-------:|-------:|------------------:|-----------------:|
| Login to Overview            |     28 |     19 |                 -9 |               -32 |
| Overview to results          |     20 |      5 |                -15 |               -75 |
| _Click variant to modal_     |   _23_ |    _0_ |              _-23_ |            _-100_ |
| Id card button to page       |      6 |      4 |                 -2 |               -33 |
| Go back to somatic page      |     19 |      0 |                -19 |              -100 |
| _Change filters to result_   |   _32_ |    _7_ |              _-25_ |             _-78_ |
| Clicinal report link to page |     29 |      9 |                -20 |               -69 |

---

## Somatic table navigation


| Step                           | Legacy | Rework | Absolute gain (s) | Relatif gain (%) |
|--------------------------------|-------:|-------:|------------------:|-----------------:|
| Default filters to new filters |      9 |      6 |                 -3 |               -33 |
| to page 2                      |      5 |      5 |                 0 |                0 |
| to page 1                      |      9 |      0 |                 -9 |              -100 |
| to default filters             |      6 |      0 |                 -6 |              -100 |

---

## Page navigation

| Step                        | Legacy | Rework | Absolute gain (s) | Relatif gain (%) |
|-----------------------------|-------:|-------:|------------------:|-----------------:|
| Dashboard to overview       |      6 |      3 |                -3 |              -50 |
| overview to somatic results |     18 |      3 |               -15 |              -83 |
| to dashboard                |     13 |      0 |               -13 |             -100 |
| dashboard to overview       |      6 |      0 |                -6 |             -100 |
| overview to somatic results |     20 |      0 |               -20 |             -100 |