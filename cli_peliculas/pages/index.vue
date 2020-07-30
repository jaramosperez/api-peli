<template>
 <section class="section">
   <h2 class="title">Películas</h2>
   <div class="columns is-mobile is-multiline">
        <Peli v-for="peli in pelis" :key="peli.id" :peli="peli"/>
     </peli>
   </div>
 </section>
</template>

<script>
import Peli from '~/components/Peli'

export default {
  name: 'HomePage',

  components: {
    Peli
  },
  data: function () {
   return {
     'pelis': [
       {
         'id': 1,
         'titulo': 'El Padrino',
         'favoritos': '3',
         'imagen': 'https://m.media-amazon.com/images/M/MV5BM2MyNjYxNmUtYTAwNi00MTYxLWJmNWYtYzZlODY3ZTk3OTFlXkEyXkFqcGdeQXVyNzkwMjQ5NzM@._V1_UY268_CR3,0,182,268_AL_.jpg',
         'estreno': '1972',
         'resumen': 'The aging patriarch of an organized crime dynasty transfers control of his clandestine empire to his reluctant son.',
       },
       {
         'id': 2,
         'titulo': 'El Padrino: Parte 2',
         'favoritos': '1',
         'imagen': 'https://m.media-amazon.com/images/M/MV5BMWMwMGQzZTItY2JlNC00OWZiLWIyMDctNDk2ZDQ2YjRjMWQ0XkEyXkFqcGdeQXVyNzkwMjQ5NzM@._V1_UY268_CR3,0,182,268_AL_.jpg',
         'estreno': '1974',
         'resumen': 'The early life and career of Vito Corleone in 1920s New York City is portrayed, while his son, Michael, expands and tightens his grip on the family crime syndicate.',
       },
       {
         'id': 3,
         'titulo': 'El Padrino: Parte 3',
         'favoritos': '0',
         'imagen': 'https://m.media-amazon.com/images/M/MV5BNTc1YjhiNzktMjEyNS00YmNhLWExYjItZDhkNWJjZjYxOWZiXkEyXkFqcGdeQXVyNzkwMjQ5NzM@._V1_UX182_CR0,0,182,268_AL_.jpg',
         'estreno': '1990',
         'resumen': 'In the midst of trying to legitimize his business dealings in New York City and Italy in 1979, aging Mafia Don Michael Corleone seeks to avow for his sins, while taking his nephew Vincent Mancini under his wing.',
       }
     ]
   }
 },
}
</script>
