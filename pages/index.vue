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
          <v-card-title class="text-h5"> Halo Musyrikin!</v-card-title>
          <v-card-subtitle
            >Kita bantu mencari <b> KPK & FPB</b> atau
            <b>Menyekutukan </b>bilangan & Menyederhanakan masalah
            Anda.</v-card-subtitle
          >

          <v-card-actions>
            <v-btn outlined small @click="add()"  :disabled="angka.length >= 4">
              <v-icon small>mdi-plus</v-icon>Angka</v-btn
            >
            <v-spacer />
            <v-btn
              :disabled="angka.length <= 2"
              outlined
              color="error"
              @click="hapus()"
              small
            >
              <v-icon small>mdi-delete</v-icon>Angka</v-btn
            >
          </v-card-actions>

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
          <v-row class="mt-0" align="center" justify="center">
            <v-btn color="primary" @click="hitung()">
              <v-icon small>mdi-run-fast</v-icon>Hitung</v-btn
            >
          </v-row>
        </v-card>

        <v-card-text>
          <v-card
            flat
            v-if="caraFPB.length > 0"
            outlined
            color="primary"
            class="mt-2 rounded-lg"
          >
            <v-card flat>
              <v-toolbar dense flat>
                <v-toolbar-title>Mencari KPK & FPB </v-toolbar-title>
              </v-toolbar>
              <v-card-text class="pt-0">
                Dari bilangan
                <span
                  :style="{ color: $vuetify.theme.themes.light.primary }"
                  v-for="(item, index) in angka.length"
                  :key="index"
                  ><b> {{ angka[index].value }} </b>
                </span>
                menghasilkan
                <b
                  >KPK =
                  <span :style="{ color: $vuetify.theme.themes.light.error }"
                    ><b>{{ KPK }}</b>
                  </span>
                  & FPB =
                  <span :style="{ color: $vuetify.theme.themes.light.error }"
                    ><b>{{ FPB }}</b>
                  </span></b
                >
              </v-card-text>
              <v-row align="center" justify="center">
                <table class="py-2">
                  <tr>
                    <th class="px-1">
                      Pembagi
                    </th>

                    <th v-for="header in angka" :key="header.value">
                      {{ header.value }}
                    </th>
                  </tr>

                  <tr
                    class="text-center"
                    v-for="(item, index) in caraFPB"
                    :key="index"
                  >
                    <td>
                      <v-chip outlined v-if="item.fpb" color="teal" dark>
                        <b>{{ item.pembagi }}</b>
                      </v-chip>

                      <span v-else>{{ item.pembagi }}</span>
                    </td>
                    <td style="min-width:50px" v-for="(j, k) in angka" :key="k">
                      {{ item.angka[k] }}
                    </td>
                  </tr>
                </table>
              </v-row>
              <v-card-text>
                <b>
                  <div>
                    KPK =
                    <span v-for="(item, index) in angkaKPK.length" :key="index">
                      {{ angkaKPK[index] }}
                      <span
                        style="color:black"
                        v-if="angkaKPK.length - 1 != index"
                        >x</span
                      >
                    </span>
                    =
                    <span :style="{ color: $vuetify.theme.themes.light.error }"
                      ><b>{{ KPK }}</b>
                    </span>
                  </div>
                  <div>
                    FPB =
                    <span
                      :style="{ color: $vuetify.theme.themes.light.primary }"
                      v-for="(item, index) in angkaFPB.length"
                      :key="index"
                    >
                      {{ angkaFPB[index] }}
                      <span
                        style="color:black"
                        v-if="angkaFPB.length - 1 != index"
                        >x</span
                      >
                    </span>
                    =
                    <span :style="{ color: $vuetify.theme.themes.light.error }"
                      ><b>{{ FPB }}</b>
                    </span>
                  </div>
                </b>
              </v-card-text>
            </v-card>
          </v-card>

          <v-card
            flat
            v-if="!loading"
            outlined
            color="primary"
            class="rounded-lg mt-2"
          >
            <v-card flat>
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
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-btn text @click="dialog = true">
            Lihat Rumus
          </v-btn>
        </v-card-actions>
      </v-card>
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
      FPB: null,
      KPK: null,
      angkaFPB: [],
      angkaKPK: [],
      caraFPB: []
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
    async hitung() {
      this.loading = true;
      this.$cookies.set("angka", this.angka);
      const prima = await this.Prima(this.angka);

      this.HitungFPB(prima);
      this.penyederhanaan(this.angka);
      this.loading = false;
    },
    async Prima(params) {
      const max = params.reduce(
        (max, p) => (p.value > max ? p.value : max),
        params[0].value
      );
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

      return prima;
    },
    HitungFPB(prima) {
      this.FPB = null;
      this.KPK = null;
      this.angkaKPK = [];
      this.angkaFPB = [];
      var temp = this.$cookies.get("angka");
      var max = temp.reduce(
        (max, p) => (p.value > max ? p.value : max),
        temp[0].value
      );

      this.caraFPB = [];

      for (let index = 0; index < max; index++) {
        for (let ikan = 0; ikan < prima.length; ikan++) {
          let angkasa = temp;
          var babi = null;
          babi = { pembagi: prima[ikan], angka: [] };
          var oke = null;
          for (let burung = 0; burung < angkasa.length; burung++) {
            if (angkasa[burung].value == 0) {
            } else if (angkasa[burung].value % prima[ikan] == 0) {
              angkasa[burung].value = angkasa[burung].value / prima[ikan];
              babi.angka.push(angkasa[burung].value);

              if (babi.fpb != false) {
                babi["fpb"] = true;
              }
              oke = true;
            } else {
              babi.angka.push(angkasa[burung].value);
              babi["fpb"] = false;
            }
          }

          if (oke) {
            this.caraFPB.push(babi);
            break;
          }
        }
      }

      this.FPB = 1;
      this.KPK = 1;
      for (let i = 0; i < this.caraFPB.length; i++) {
        if (this.caraFPB[i].fpb) {
          this.FPB = this.FPB * this.caraFPB[i].pembagi;
          this.angkaFPB.push(this.caraFPB[i].pembagi);
        }
        this.KPK = this.KPK * this.caraFPB[i].pembagi;
        this.angkaKPK.push(this.caraFPB[i].pembagi);
      }
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
