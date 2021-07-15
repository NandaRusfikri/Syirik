<template>
  <v-container>
    <v-card
      flat
      class="mx-auto rounded-lg"
      :max-width="$vuetify.breakpoint.mobile ? 400 : 600"
    >
      <v-card class="mx-auto rounded-lg">
        <v-list-item two-line>
          <v-list-item-content>
            <v-list-item-title class="text-h5">
              Halo Pemalas!
            </v-list-item-title>
            <v-list-item-subtitle
              >Kita bantu cari <b>Penyekutu</b> angka KPK &
              FPB</v-list-item-subtitle
            >
          </v-list-item-content>
        </v-list-item>

        <v-card-actions>
          <v-btn outlined small @click="add()">
            <v-icon small>mdi-plus</v-icon>Tambah</v-btn
          >
          <v-btn
            :disabled="angka.length <= 2"
            outlined
            color="error"
            @click="hapus()"
            small
          >
            <v-icon small>mdi-delete</v-icon>Hapus</v-btn
          >
          <v-btn color="primary" @click="hitung()" small>
            <v-icon small>mdi-run-fast</v-icon>Hitung</v-btn
          ></v-card-actions
        >

        <br />
        <v-row align="center" justify="center">
          <template v-for="(item, index) in angka.length">
            <v-col cols="3"  md="2" sm="4" class="py-0" :key="index">
              <v-text-field   @keypress="isNumber($event)" v-model="angka[index].value" outlined>
              </v-text-field
            ></v-col>
          </template>
        </v-row>
      </v-card>

      <v-toolbar dense flat>
        <v-toolbar-title>Hasil </v-toolbar-title>
      </v-toolbar>
      <div v-if="!loading">
        <p class="text-h5">{{hasil}}</p>

      </div>

      <v-divider></v-divider>

      <v-card-actions>
        <v-btn text>
          Full Report
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      hasil: null,
      angka: [{ value: 20 }, { value: 40 }],
      time: 0,
      loading: true
    };
  },
  methods: {
      isNumber: function(evt) {
      evt = evt ? evt : window.event;
      var charCode = evt.which ? evt.which : evt.keyCode;
      if (
        charCode > 31 &&
        (charCode < 48 || charCode > 57) &&
        charCode !== 46
      ) {
        evt.preventDefault();
      } else {
        return true;
      }
    },
    add() {
      this.angka.push({ value: 0 });
    },
    hapus() {
      this.angka.splice(this.angka.length - 1, 1);
    },
    hitung() {
      this.loading = true;
      var max = this.angka.reduce(
        (max, p) => (p.value > max ? p.value : max),
        this.angka[0].value
      );

      var hasil = [];

      for (let i = 0; i < max; i++) {
        var ayam = true;
        for (let y = 0; y < this.angka.length; y++) {
          if (this.angka[y].value % i !== 0) {
            ayam = false;
          }
        }
        if (ayam) {
          hasil.push(i);

          // console.log(i);
        }
        ayam = null;
      }
      // console.log("hasil ", hasil);

         hasil.sort(function(a, b){return b - a});
          this.hasil = hasil;
      this.loading = false;

    }
  },
  computed: {

  }
};
</script>
<style scoped>
#latar {
  background: rgb(0, 199, 166);
  background: radial-gradient(
    circle,
    rgba(0, 199, 166, 0.46589057986475846) 0%,
    rgba(0, 199, 166, 1) 100%
  );
}
</style>
