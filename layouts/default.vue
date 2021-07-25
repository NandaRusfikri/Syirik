<template>
  <v-app app>
    <v-app-bar app color="white" flat>
      <v-toolbar-title style="font-family: Comfortaa;font-weight: 800">
        <b>Syirik</b>
      </v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn class="text-capitalize" @click="dialog = true" outlined>
        Apaini?
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
    <v-main>
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
    <v-dialog max-width="400px" v-model="dialog">
      <v-card class="rounded-lg">
        <v-toolbar flat dense>
          <v-toolbar-title dark><b>Apa Ini ? </b></v-toolbar-title>
          <v-spacer></v-spacer>
          <v-btn icon @click="dialog = false">
            <v-icon>mdi-close</v-icon>
          </v-btn>
        </v-toolbar>

        <v-card-text>
          <p>
            Syirik adalah apps yang mencoba membantu menyelesaikan masalah Kamu
            dalam mengerjakan persoalan Matematika.
          </p>
          <p>
            Saat ini Kita bisa membantu kamu mencari kelipatan persekutuan ter<b
              >kecil (KPK)</b
            >
            & faktor persekutuan ter<b>besar (FPB)</b> atau Menyederhanakan
            bilangan kamu.
          </p>
          <p>
            Kita akan terus menambah materi lain agar dapat membantu kamu.
          </p>

          <p>
            Kamu ada saran atau pertanyaan ? kirim saran atau pertanyaan kamu
            <a href="https://forms.gle/M4JjCK3JjvCDMKeBA" target="_blank"
              >kesini.</a
            >
          </p>
          <p>
            Jika kamu suka, kamu bisa mensupport dengan berdonasi di
            <b>
              <a href="https://saweria.co/nandarusfikri" target="_blank"
                >Saweria.</a
              ></b
            >
          </p>
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn dense small outlined @click="saran()" color="primary">
            Kirim Saran
          </v-btn>
          <v-btn dense small outlined @click="saweria()" color="#faae2b">
            atau Donasi
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-app>
</template>
<script>
import { mapGetters } from "vuex";
export default {
  data() {
    return {
      dialog: false
    };
  },
  methods: {
    saweria() {
      window.open("https://saweria.co/nandarusfikri", "_blank");
    },
    saran() {
      window.open("https://forms.gle/M4JjCK3JjvCDMKeBA", "_blank");
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

    console.log("wasu ", 1 % 3);
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
