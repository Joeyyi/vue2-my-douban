<template>
  <div>
      <h3>{{ list.title }}</h3>
      <ul>
        <li v-for="movie in list.subjects" @click="showDetail(movie.alt)">
          <img :src="movie.images.small" alt="image">
          <p>{{ movie.title }}  <span>({{ movie.rating.average }}/10)</span></p>
        </li>
      </ul>
  </div>
</template>

<script>
import jsonp from 'jsonp';
export default {
  props: {
    list: {
      type: Object,
      default: {}
    }
  },
  methods: {
    showDetail(alt) {
      console.log(alt);
        var id = alt.match(/[\d]+/);
        var url = 'https://api.douban.com/v2/movie/subject/' + id;
        var param = 'handleResponse';
        var detail = {};
        jsonp(url, param, (err, res) => {
            if(!err) {
                console.log(res);
                detail = res;      
                this.$store.commit('setMovieDetail', detail);
            } else {
                console.log(err);
            }
        });

      this.$store.commit('setVisibility', true);
    }
  }
}
</script>

<style scoped>
  h3 {
    text-align: center;
  }
  ul {
    text-align: center;
    padding: 0;
    margin: 0;
  }
  
  li {
    list-style: none;
    display: inline-block;
    width: 25%;
    vertical-align: top;
  }

  p {
    text-align: center;
  }

  img {
    width: 80%;
    height: 80%;
  }

@media only screen and (max-device-width: 480px) {
    li {
      width: 50%;
    }

    p {
      font-size: 18px;
    }


}

@media only screen and (max-device-width: 640px) {
    li {
      width: 33%;
    }

    p {
      font-size: 22px;
    }


}

</style>

