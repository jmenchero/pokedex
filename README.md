# pokedex

[![Netlify Status](https://api.netlify.com/api/v1/badges/23b84609-d319-495a-af65-4eb0d21932c7/deploy-status)](https://app.netlify.com/sites/jmenchero-pokedex/deploys)

You can check the app here: [jmenchero-pokedex.netlify.app](https://jmenchero-pokedex.netlify.app/)

## Running

1. Clone the repo
2. Install dependencies with `yarn install`
3. Run in development mode with `yarn dev`

## Description

Proyecto Vue de prueba que utiliza [Pokeapi](https://pokeapi.co/) para mostrar una lista filtrable de Pokemons con sus caracteristicas principales.

La mayor parte de los ficheros han sido autogenerados por Nuxt, por lo que los ficheros interesantes a evaluar con la logica de la aplicacion son:

- [index.vue](frontend/pages/index.vue): Layout, logica de peticiones, filtrado y scroll infinito.
- [Card.vue](frontend/components/Card.vue): Maquetacion de las tarjetas.
- [FilterBox.vue](frontend/components/FilterBox.vue): Maquetacion de la barra de filtrado.
- [Loading.vue](frontend/components/Loading.vue): Maquetacion de la animacion de loading.
- [animations.css](frontend/assets/css/animations.css): Maquetacion de la animacion de loading.
- [nuxt.config.js](frontend/nuxt.config.js): Configuracion del vue-router.

## To-Do's

- BUG: Faking loading with sleep makes background delay with direct url (eg http://localhost:3000/pokemons/charmeleon)
- FEAT: Click on evolution opens pokemon
- FEAT: Close card button
- FEAT: Search filters
- FEAT: Improve styles
- FEAT: Add 404 not found
- DOC: Instructions for running locally
- REF: Move scroll functionality and routing functionality to separate files
- REF: Clean unused Nuxt directories and readmes
- REF: Avoid pixel sizing
- REF: Dynamically requesting entire pokemons list (not hardcoded to 15000)
- REF: Avoid requesting data inside Card component (send data from parent)
- REF: Split logic between more components (tag, highlight, ...)
