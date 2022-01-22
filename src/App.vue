<template>
  <div id="app">
    <div class="header">Header</div>
    <div class="flex">
      <div class="sidebar">Sidebar</div>
      <div class="card-grid">
        <Card :car="car" v-for="car in carData" :key="car.card_guid" />
      </div>
    </div>
  </div>
</template>

<script>
import Card from "./components/Card.vue";
import jsonData from "./data.json";

export default {
  name: "App",
  data() {
    return {
      carData: jsonData.data,
    };
  },
  components: {
    Card,
  },
};
</script>

<style lang="scss">
@font-face {
  font-family: "SF Pro";
  font-weight: 300;
  src: local("SF Pro"), url(./fonts/SF-Pro-Text-Light.otf) format("opentype");
}

@font-face {
  font-family: "SF Pro";
  font-weight: 400;
  src: local("SF Pro"), url(./fonts/SF-Pro-Text-Regular.otf) format("opentype");
}

@font-face {
  font-family: "SF Pro";
  font-weight: 700;
  src: local("SF Pro"), url(./fonts/SF-Pro-Text-Bold.otf) format("opentype");
}

#app {
  --brand-primary: #7572ff;
  --dark1: #3f3a50;
  --grey1: #55595d;
  font-family: "SF Pro", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: black;
}

.header {
  background: #ebebeb;
  height: 237px;
  padding: 1rem;
  border-bottom: 1px solid gray;
}

.sidebar {
  background: #ebebeb;
  min-width: 16.6875rem;
  padding: 1rem;

  @media (max-width: 720px) {
    display: none;
  }
}

.flex {
  display: flex;
}

.card-grid {
  width:100%;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 350px));
  grid-gap: 0.9375rem;
  padding: 1rem;

  @media (max-width: 1125px) {
    grid-template-columns: repeat(2, minmax(250px, 1fr));
  }

  @media (max-width: 865px) {
    display: flex;
    flex-direction: column;
  }
}
</style>
