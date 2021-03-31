# pokedex

[![Netlify Status](https://api.netlify.com/api/v1/badges/23b84609-d319-495a-af65-4eb0d21932c7/deploy-status)](https://app.netlify.com/sites/jmenchero-pokedex/deploys)

You can check the app here: [jmenchero-pokedex.netlify.app](https://jmenchero-pokedex.netlify.app/)

## Description

Proyecto Vue de prueba que utiliza [Pokeapi](https://pokeapi.co/) para mostrar una lista filtrable de Pokemons con sus caracteristicas principales.

La mayor parte de los ficheros han sido autogenerados por Nuxt, por lo que los ficheros interesantes a evaluar con la logica de la aplicacion son:

- [index.vue](pages/index.vue): Layout, logica de peticiones, filtrado y scroll infinito.
- [Card.vue](components/Card.vue): Maquetacion de las tarjetas.
- [FilterBox.vue](components/FilterBox.vue): Maquetacion de la barra de filtrado.
- [Loading.vue](components/Loading.vue): Maquetacion de la animacion de loading.

## To-Do's

- BUG: No image update after empty pokemon (blastoise after looking for "nid" and cleaning search).
- BUG: Loading intro doesn't render properly on mobile
- FEAT: Transitions for loading card
- FEAT: Mark cards as clickable
- FEAT: Close card button
- FEAT: Pokemon detail layout
- FEAT: URL opens detail
- FEAT: Search filters
- FEAT: Improve styles
- REF: Avoid pixel sizing
- REF: Dynamically requesting entire pokemons list (not hardcoded to 15000)
- REF: Avoid requesting data inside Card component (send data from parent)
- REF: Split logic between more components (tag, highlight, ...)
