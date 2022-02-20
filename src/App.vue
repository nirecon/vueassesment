<template>
  <HeaderComponent title="Opportunity Name" />
  <OpporTunityComponent title="Forcast Name" />
</template>

<script>
import HeaderComponent from "./components/HeaderComponent.vue";
import OpporTunityComponent from "./components/OpportunityComponent.vue";

export default {
  name: "App",
  components: {
    HeaderComponent,
    OpporTunityComponent,
  },
};
</script>

<style>
#app {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
.navbar {
  position: absolute !important;
  width: 100%;
  top: 0;
  padding: 1rem !important;
  justify-content: start !important;
}
.h1,
.h2,
.h3,
.h4,
.h5,
.h6,
h1,
h2,
h3,
h4,
h5,
h6 {
  margin-bottom: 0px !important;
}
</style>
