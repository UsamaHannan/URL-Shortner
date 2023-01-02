<template>
  <v-app>
    <MainHeader />
    <v-main>
      <MainSection />
    </v-main>
    <MainFooter />
  </v-app>
</template>

<script>
import MainHeader from "./components/MainHeader";
import MainFooter from "./components/MainFooter";
import MainSection from "./components/MainSection";

export default {
  name: "App",

  components: {
    MainSection,
    MainHeader,
    MainFooter,
  },

  data: () => ({
    //
  }),
};
</script>
