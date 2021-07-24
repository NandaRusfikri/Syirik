<template>
  <v-app app>
    <v-app-bar app color="white" flat>
      <v-toolbar-title style="font-family: Comfortaa;font-weight: 800">
        <b>Syirik</b>
      </v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn @click="saweria()" outlined>
        About
      </v-btn>
    </v-app-bar>
    <!-- <v-app-bar
      dense
      flat
      :clipped-left="$vuetify.breakpoint.lgAndUp"
      app
      :style="{ background: $vuetify.theme.themes[theme].background }"
    >
      <v-toolbar-title style="font-family: Comfortaa;font-weight: 800" class="ml-0 pl-4">
        <b>Buahati</b>
      </v-toolbar-title>
    </v-app-bar> -->
    <v-main >
      <v-snackbar
        v-model="snackbar.enabled"
        :color="snackbar.color"
        absolute
        top
      >
        <strong>{{ snackbar.message }}</strong>
        <template v-slot:action="{ attrs }">
          <v-btn dark icon v-bind="attrs" @click="snackbar.enabled = false">
            <v-icon dark>mdi-close</v-icon>
          </v-btn>
        </template>
      </v-snackbar>
      <nuxt />
    </v-main>
  </v-app>
</template>
<script>
import { mapGetters } from "vuex";
export default {
  methods: {
    saweria() {
      window.open("https://saweria.co/nandarusfikri", "_blank");
    }
  },
  mounted() {
    // var array = ["(", ")", "(", ")"];

    // var ayam = 0;
    // var bebek = 0;
    // for (let i = 0; i < array.length; i++) {
    //   if (array[i] == "(") {
    //     ayam++;
    //   } else {
    //     bebek++;
    //   }
    // }
    // console.log(Math.max(ayam, bebek) - Math.min(ayam,bebek))


    // for (let i = 1; i <= 100; i++) {
    //  if (i % 3 == 0 && i % 5 == 0 ) {
    //    console.log("Mampu")
    //  }else if (i % 3 == 0) {
    //    console.log("Mam")
    //  }else if (i % 5 == 0) {
    //    console.log("pu")
    //  }else{
    //    console.log(i)
    //  }

    // }

    console.log("wasu ",1%3)
  },
  computed: {
    theme() {
      return this.$vuetify.theme.dark ? "dark" : "light";
    },
    snackbar() {
      return this.$store.getters.Snackbar;
    }
  }
};
</script>
<style scoped></style>
