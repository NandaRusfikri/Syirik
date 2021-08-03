<template>
  <v-container>
    <v-card
      color="primary "
      outlined
      flat
      class="mx-auto rounded-lg"
      :max-width="$vuetify.breakpoint.mobile ? 400 : 600"
    >
      <v-card flat>
        <v-card flat class="mx-auto rounded-lg">
          <v-card-title class="text-h5"> Logic</v-card-title>
          <v-card-subtitle>Ini Page Untuk Sample Logic</v-card-subtitle>
        </v-card>
      </v-card>
    </v-card>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      dialog: false,
      hasil: null,
      angka: [{ value: 36 }, { value: 54 }],
      time: 0,
      loading: true,
      FPB: null,
      KPK: null,
      angkaFPB: [],
      angkaKPK: [],
      caraFPB: []
    };
  },
  mounted() {
    this.Nawadata();
  },

  methods: {
    Nawadata() {
      const array = [1, 10, 7,13,20];

      var ayam = 0;
      var arraysisa = [];
      array.sort(function(a, b){return a - b});
      console.log("arry sort",array)

      for (let i = 0; i < array.length; i++) {
        for (let y = 0; y < array.length; y++) {
          if (array[y] == 4) {
            ayam = ayam+1;
            array.splice(y, 1);
          } else if (array[y] > 4) {
            if (array[y] % 4 == 0) {
              console.log("asu",array[y] / 4 );
              var c = array[y] / 4
              console.log("ayam sebelum ",ayam)
              ayam = ayam + c;
              array.splice(y, 1);
              // console.log("ayam setelah ditambah ", array[y]);
            } else if (array[y] % 4 > 0) {
              var b = array[y] - (array[y] % 4);
              const sisa = array[y] % 4;
              arraysisa.push(sisa);
              ayam = ayam + b / 4;
              array.splice(y, 1);
            }
          }
        }
      }

      console.log(" arraysisa ", arraysisa);
      console.log("array ", array);
      console.log("ayam ", ayam);

      for (let i = 0; i < arraysisa.length; i++) {
        array.push(arraysisa[i]);
      }
      array.sort(function(a, b){return a - b});
       console.log("selelah ditambah array sisa ", array);


      for (let i = 0; i < array.length; i++) {
        for (let y = 0; y < array.length; y++) {
          if (array[y] + array[array.length - 1] <= 4) {
            ayam++;
            array.splice(y, 1);
            array.splice(array.length - 1, 1);
          }
        }
      }
      if (array.length == 1) {
        ayam++;
      }

      console.log("Minimum bus required is : ", ayam);
      // console.log(array);
    }
  },
  computed: {}
};
</script>
<style scoped>
table,
th,
td {
  border: 1px solid black;
}
#latar {
  background: rgb(0, 199, 166);
  background: radial-gradient(
    circle,
    rgba(0, 199, 166, 0.46589057986475846) 0%,
    rgba(0, 199, 166, 1) 100%
  );
}
</style>
