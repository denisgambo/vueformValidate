<template>
  <div class="home">
    <div>
      <TechnoList @technos="catchTecho" />
      <p v-for="tech in mytechnos"> {{ tech }}</p>
    </div>
  </div>

  <Registration />
</template>

<script>
// @ is an alias to /src
import TechnoList from '@/components/TechnoList.vue';
import Registration from '@/components/Registration.vue';

export default {
  name: 'HomeView',
  components: {
    TechnoList,
    Registration
  },
  data() {
    return {
      mytechnos: [],
      newTechno: ""
    }
  },

  methods: {
    catchTecho(technologies) {
      this.mytechnos = technologies
    }
  }
}
</script>
