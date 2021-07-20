<template>
  <v-container>
    <v-card
      flat
      class="mx-auto rounded-lg"
      :max-width="$vuetify.breakpoint.mobile ? 400 : 600"
    >
      <v-card flat class="mx-auto rounded-lg">
        <v-list-item three-line>
          <v-list-item-content>
            <v-list-item-title class="text-h5">
              Halo Musyrikin!
            </v-list-item-title>
            <v-list-item-subtitle
              >Kita bantu <b>Menyekutukan</b> bilangan Anda atau mencari
              <b> KPK & FPB</b></v-list-item-subtitle
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
            <v-col cols="3" md="2" sm="4" class="py-0" :key="index">
              <v-text-field
                @keypress="isNumber($event)"
                v-model="angka[index].value"
                outlined
              >
              </v-text-field
            ></v-col>
          </template>
        </v-row>
      </v-card>

      <v-card-text>
        <v-card v-if="!loading" outlined color="primary" class="rounded-lg">
          <v-card>
            <v-toolbar dense flat>
              <v-toolbar-title>Penyederhanaan bilangan </v-toolbar-title>
            </v-toolbar>
            <v-card-text class="pt-0">
              bilangan
              <span
                :style="{ color: $vuetify.theme.themes.light.primary }"
                v-for="(item, index) in angka.length"
                :key="index"
                ><b> {{ angka[index].value }} </b>
              </span>
              bisa di sederhanakan dengan dibagi
              <span :style="{ color: $vuetify.theme.themes.light.error }"
                ><b>{{ hasil[0] }}</b>
              </span>
              <b>Hasilnya :</b>

              <span
                v-for="(item, index) in angka.length"
                :key="angka[index].value"
              >
                <div style="font-weight: bold;">
                  <span
                    :style="{ color: $vuetify.theme.themes.light.primary }"
                    >{{ angka[index].value }}</span
                  >/<span
                    :style="{ color: $vuetify.theme.themes.light.error }"
                    >{{ hasil[0] }}</span
                  >
                  =
                  <span
                    :style="{ color: $vuetify.theme.themes.light.secondary }"
                    >{{ angka[index].value / hasil[0] }}</span
                  >
                </div>
              </span>
            </v-card-text>
          </v-card>
        </v-card>
        <v-card
          v-if="!loading"
          outlined
          color="primary"
          class="mt-2 rounded-lg"
        >
          <v-card>
            <v-toolbar dense flat>
              <v-toolbar-title>Mencari FPB </v-toolbar-title>
            </v-toolbar>
            <v-card-text class="pt-0">
              Faktor Persekutuan Terbesar dari bilangan
              <span
                :style="{ color: $vuetify.theme.themes.light.primary }"
                v-for="(item, index) in angka.length"
                :key="index"
                ><b> {{ angka[index].value }} </b>
              </span>
              <b>adalah </b>
              <span :style="{ color: $vuetify.theme.themes.light.error }"
                ><b>{{ hasil[0] }}</b>
              </span>
            </v-card-text>
            <v-row>
              <v-col v-for="item in FPB" :key="item" cols="12" md="4" sm="6">
                <v-timeline>
                  <v-timeline-item
                    left
                    v-for="n in item"
                    :key="n"
                    fill-dot
                    color="red lighten-2"
                  >
                    <template v-slot:icon>
                      <v-avatar>
                        <span class="white--text text-h5">{{ n.hasil }}</span>
                      </v-avatar>
                    </template>

                    <v-card v-if="n.pembagi" color="primary" max-width="50">
                      <v-avatar color="primary" size="36">
                        <span class="white--text text-h5">{{ n.pembagi }}</span>
                      </v-avatar>
                    </v-card>
                  </v-timeline-item>
                </v-timeline>
              </v-col>
            </v-row>
          </v-card>
        </v-card>

        <v-card
          v-if="!loading"
          outlined
          color="primary"
          class="mt-2 rounded-lg"
        >
          <v-card>
            <v-toolbar dense flat>
              <v-toolbar-title>Mencari KPK </v-toolbar-title>
            </v-toolbar>
            <v-card-text class="pt-0">
              Maaf Saat Ini <b>KPK</b>nya sedang di Nerf. jika sudah normal akan
              di publish
            </v-card-text>
          </v-card>
        </v-card>
      </v-card-text>

      <v-divider></v-divider>

      <v-card-actions>
        <v-btn text @click="dialog = true">
          Lihat Rumus
        </v-btn>
      </v-card-actions>
    </v-card>

    <v-dialog max-width="400px" v-model="dialog">
      <v-card class="rounded-lg">
        <v-toolbar flat dense>
          <v-toolbar-title dark><b>Lihat Rumus </b></v-toolbar-title>
          <v-spacer></v-spacer>
          <v-btn icon @click="dialog = false">
            <v-icon>mdi-close</v-icon>
          </v-btn>
        </v-toolbar>

        <v-card-text>
          <p>
            Beliin Saya <b>Kopi</b> atau <b>sawer</b> di saweria Nanti Saya
            Kasih tau rumus cepetnya.
          </p>
          <a href="https://saweria.co/nandarusfikri" target="_blank"
            ><img
              src="https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png"
              alt="Buy Me A Coffee"
              style="height: 41px !important;width: 174px !important;box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;-webkit-box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;"
          /></a>
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn dense small outlined @click="saweria()" color="primary">
            Beliin
          </v-btn>
          <v-btn dense small @click="saweria()" color="#faae2b">
            Sawer
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

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
      FPB: []
    };
  },

  methods: {
    saweria() {
      window.open("https://saweria.co/nandarusfikri", "_blank");
    },
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
      const angka = this.angka;
      this.penyederhanaan(angka);
      this.loading = false;
    },
    penyederhanaan(params) {
      var temp = params;
      var max = temp.reduce(
        (max, p) => (p.value > max ? p.value : max),
        temp[0].value
      );

      var pembagi = [];

      for (let i = 0; i < max; i++) {
        var ayam = true;
        for (let y = 0; y < temp.length; y++) {
          if (temp[y].value % i !== 0) {
            ayam = false;
          }
        }
        if (ayam) {
          pembagi.push(i);
        }
        ayam = null;
      }

      pembagi.sort(function(a, b) {
        return b - a;
      });
      console.log("pembagi ", pembagi);
      this.hasil = pembagi;

      var prima = [];

      for (let x = 1; x <= max; x++) {
        var pembagi = 0;
        for (let z = 1; z <= x; z++) {
          if (x % z == 0) {
            pembagi++;
          }
        }
        if (pembagi == 2) {
          prima.push(x);
        }
      }

      var result = [];

      for (let s = 0; s < temp.length; s++) {
        var bilangan,
          sapi = [],
          ayam;
        bilangan = temp[s].value;
        ayam = { pembagi: null, hasil: bilangan };
        sapi.push(ayam);
        for (let index = 0; index < max; index++) {
          for (let h = 0; h < prima.length; h++) {
            if (bilangan % prima[h] == 0) {
              bilangan = bilangan / prima[h];

              ayam = { pembagi: prima[h], hasil: bilangan };
              sapi.push(ayam);
              break;
            }
          }
        }

        result.push(sapi);
      }

      this.FPB = result;
    }
  },
  computed: {}
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
