<template>
  <section class="container"> 
    <h2>Community</h2>
    <table>
      <thead>
       <tr>
         <th>Streamer</th>
         <th>Average Rating</th>
       </tr>
     </thead>
     <tbody>
        <CommunityRating 
          v-for="stat in stats"
          :stat="stat"
          :key="stat.user_name" 
        />
     </tbody>
    </table>

    <h2>Community Favorites</h2>
    <ul>
      <CommunityFavorite 
        v-for="favorite in favorites"
        :favorite="favorite"
        :key="favorite.user_name" />
    </ul>
  </section>
</template>

<script>
import api from '../../services/api';
import CommunityRating from './CommunityRating'; 
import CommunityFavorite from './CommunityFavorite';

export default {
  data() {
    return {
      stats: null,
      favorites: null
    };
  },

  created() {
    api.getStats()
      .then(stats => this.stats = stats);
    api.getAllFavorites()
      .then(favorites => this.favorites = favorites);
  },

  methods: {
    getRatings() {
      return api.getRatings()
        .then(ratings => {
          this.ratings = ratings;
        });
    }
  }, 
  
  components: {
    CommunityRating,
    CommunityFavorite
  }
};
</script>

<style scoped>
.container {
  display: flex;
  flex-flow: column;
}
h1 {
  text-align: center;
  font-size: 6vh;
  margin: 2vh 35vw 2vh 35vw;
  border: solid gray 2px;
  border-radius: 20vw;
  color: gray;
  width: 25vw;
  justify-content: center;
}
thead {
  background-color: rgb(177, 158, 214);
  color: white;
  font-size: 3.5vh;
}
th {
  border: solid gray 2px;
}
table {
  width: 60vw;
  align-items: center;
  justify-content: center;
  margin: 0 20vw 5vh 20vw;
}
ul {
    list-style-type: none;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-column-gap: 3vw;;
    grid-gap: 20px;
    margin: 4vw;
  }
</style>