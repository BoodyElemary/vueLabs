<template>
  <div>
    <div class="row">
      <HeaderComponent />
    </div>
    <div class="row">
      <div class="col-4">
        <LinksComponent />
      </div>
      <div class="col-7">
        <BodyComponent />
      </div>
    </div>
    <div class="row">
      <FooterComponent />
    </div>
  </div>
</template>

<script>
import HeaderComponent from "./components/HeaderComponent.vue";
import FooterComponent from "./components/FooterComponent.vue";
import BodyComponent from "./components/BodyComponent.vue";
import LinksComponent from "./components/LinksComponent.vue";

export default {
  components: {
    HeaderComponent,
    FooterComponent,
    LinksComponent,
    BodyComponent,
  },
};
</script>


<style>
</style>