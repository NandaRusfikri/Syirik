<template>
  <v-container>
    <v-card
      color="primary "
      outlined
      flat
      class="mx-auto rounded-lg"
      :max-width="$vuetify.breakpoint.mobile ? 400 : 600"
    >
      <v-card>
        <v-tabs v-model="tab" centered icons-and-text>
          <v-tabs-slider></v-tabs-slider>

          <v-tab href="#tab-1">
            Persegi
            <v-icon>mdi-crop-square</v-icon>
          </v-tab>

          <v-tab href="#tab-2">
            Segitiga
            <v-icon>mdi-triangle-outline</v-icon>
          </v-tab>

          <v-tab href="#tab-3">
            Lingkaran
            <v-icon>mdi-checkbox-blank-circle-outline</v-icon>
          </v-tab>

        </v-tabs>

        <v-tabs-items v-model="tab">
          <v-tab-item value="tab-1">
            <v-card flat>
              <v-card-text>
                persegi adalah bangun datar dua dimensi yang dibentuk oleh empat
                buah rusuk yang sama panjang dengan membentuk 4 titik sudut yang
                mana besar setiap sudutnya siku-siku 90 derajat.
                <v-row align="center" justify="center">
                  <v-col cols="6" class="d-flex justify-end mb-6">
                    <div
                      class="d-flex justify-center "
                      v-bind:style="{
                        width: width + 'px',
                        height: height + 'px',
                        border: border + 'px solid #000'
                      }"
                      style="max-width:200px; max-height:200px; min-width:100px; min-height:100px"
                    ></div
                  ></v-col>
                  <v-col cols="6" class="justify-start mb-6">
                    <v-text-field
                      dense
                      class="text-green"
                      v-model="width"
                      prefix="P : "
                      style="max-width:100px"
                    >
                    </v-text-field>
                    <v-text-field
                      dense
                      v-model="height"
                      prefix="L : "
                      style="max-width:100px"
                    >
                    </v-text-field>
                    </v-col
                  >
                </v-row>

                <v-card flat outlined color="primary" class="rounded-lg mt-4">
                  <v-card flat>
                    <v-toolbar dense flat>
                      <v-toolbar-title>Luas Persegi </v-toolbar-title>
                    </v-toolbar>
                    <v-card-text class="pt-0">
                      <b>P</b>anjang <b>{{ width }}</b> x <b>L</b>ebar
                      <b>{{ height }}</b> =
                      <b>{{ width * height }}</b>
                    </v-card-text>
                  </v-card>
                </v-card>
                <v-card flat outlined color="primary" class="rounded-lg mt-4">
                  <v-card flat>
                    <v-toolbar dense flat>
                      <v-toolbar-title>Keliling Persegi </v-toolbar-title>
                    </v-toolbar>
                    <v-card-text class="pt-0">
                      Rumus Keliling Persegi <b>2x(P+L)</b> atau
                      <b
                        >2x(<span
                          :style="{ color: $vuetify.theme.themes.light.error }"
                          >{{ width }}</span
                        >+<span
                          :style="{ color: $vuetify.theme.themes.light.error }"
                          >{{ height }}</span
                        >) =
                      </b>
                      <b>{{ 2 * (height + width) }}</b>
                    </v-card-text>
                  </v-card>
                </v-card>
              </v-card-text>
            </v-card>
          </v-tab-item>
          <v-tab-item value="tab-2">
               <v-card flat outlined color="primary" class="rounded-lg mt-4">
                  <v-card flat>
                    <v-toolbar dense flat>
                      <v-toolbar-title>Masih Proses Pengerjaan </v-toolbar-title>
                    </v-toolbar>
                    <v-card-text class="pt-0">
                      Trimakasih sudah berkunjung, nantikan update selanjutnya.
                    </v-card-text>
                  </v-card>
                </v-card>
          </v-tab-item>
           <v-tab-item value="tab-3">
               <v-card flat outlined color="primary" class="rounded-lg mt-4">
                  <v-card flat>
                    <v-toolbar dense flat>
                      <v-toolbar-title>Masih Proses Pengerjaan </v-toolbar-title>
                    </v-toolbar>
                    <v-card-text class="pt-0">
                      Trimakasih sudah berkunjung, nantikan update selanjutnya.
                    </v-card-text>
                  </v-card>
                </v-card>
          </v-tab-item>
        </v-tabs-items>
      </v-card>
    </v-card>
  </v-container>
</template>
<script>

export default {

  data() {
    return {
      border: 2,
      width: 150,
      height: 120,
      Lwidth: this.width * 50,
      Lheight: this.height * 50,
      tab: null,
      text:
        "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat."
    };
  }
};
</script>
<style>
.square {
  height: 50px;
  width: 50px;
  border: 2px solid #000;
}
.square2 {
  height: 50px;
  width: 70px;
  border: 2px solid #000;
}
.circle {
  height: 50px;
  width: 50px;
  border: 2px solid #000;
  border-radius: 50%;
}
</style>
