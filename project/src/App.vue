<template>
  <div id="app">
    <div class="mt-5">
      <pagination-component v-bind:steps="steps">
        <template v-slot:content_0>
          <h2>Première étape</h2>
          <img src="../public/img/1.gif">
        </template>
        <template v-slot:content_1>
          <h2>Deuxième étape</h2>
          <img src="../public/img/2.gif">
        </template>
        <template v-slot:content_2>
          <h2>Troisème étape</h2>
          <img src="../public/img/3.gif">
        </template>
        <template v-slot:content_3>
          <h2>Dernière étape</h2>
          <img src="../public/img/4.gif">
        </template>
      </pagination-component>
    </div>
  </div>
</template>

<script>
import PaginationComponent from './components/PaginationComponent.vue'
import 'bootstrap';

export default {
  name: 'app',
  components: {
    PaginationComponent
  },
  data() {
    return {
      steps: [
        {
          title: 'Introduction',
          allowNext: false
        }, {
          title: 'Deuxième',
          allowNext: false
        }, {
          title: 'Troisième',
          allowNext: false
        }, {
          title: 'Dernière slide',
          allowNext: false
        }
      ]
    }
  }
}
</script>

<style lang="scss">
  @import "~bootstrap/dist/css/bootstrap.min.css";

  h2{
    margin-bottom: 2rem;
  }

  img {
    height: 250px;
  }

</style>
