<template>
  <v-card
    height="100%"
    width="100%"
    class="mx-auto pa-2"
    :elevation="6"
    :shaped="false"
  >
    <v-row v-if="jsonNazioneOggi" class="mx-auto">
      <v-col lg="2" cols="6">
        <v-card height="100%" class="" color="red" :elevation="6" outlined tile>
          <v-card-title class="text-left">
            <span class="headline font-weight-light white--text"
              >Attuali Positivi
            </span></v-card-title
          >
          <v-card-text
            class="headline text-center font-weight-black white--text"
            >{{ jsonNazioneOggi.totale_positivi }}</v-card-text
          >
          <v-divider style="border-color: white"></v-divider>
          <v-card-subtitle
            class="caption text-center font-weight-light white--text"
            >Variazione 24h</v-card-subtitle
          >
          <v-card-text
            class="headline text-center font-weight-light white--text"
            >{{ jsonNazioneOggi.variazione_totale_positivi }}</v-card-text
          >
        </v-card>
      </v-col>
      <v-col lg="2" cols="6">
        <v-card
          height="100%"
          class=""
          color="green"
          :elevation="6"
          outlined
          tile
        >
          <v-card-title class="text-left">
            <span class="headline font-weight-light white--text"
              >Dimessi/Guariti
            </span></v-card-title
          >
          <v-card-text
            class="headline text-center font-weight-black white--text"
            >{{ jsonNazioneOggi.dimessi_guariti }}</v-card-text
          >
          <v-divider style="border-color: white"></v-divider>
          <v-card-subtitle
            class="caption text-center font-weight-light white--text"
            >Variazione 24h</v-card-subtitle
          >
          <v-card-text
            v-if="jsonNazioneOggi.dimessi_guariti"
            class="headline text-center font-weight-light white--text"
            >{{
              jsonNazioneOggi.dimessi_guariti - jsonNazioneIeri.dimessi_guariti
            }}</v-card-text
          >
        </v-card>
      </v-col>
      <v-col lg="2" cols="6">
        <v-card
          height="100%"
          class=""
          color="black"
          :elevation="6"
          outlined
          tile
        >
          <v-card-title class="text-left">
            <span class="headline font-weight-light white--text"
              >Deceduti
            </span></v-card-title
          >
          <v-card-text
            class="headline text-center font-weight-bold white--text"
          >
            {{ jsonNazioneOggi.deceduti }}
          </v-card-text>
          <v-divider style="border-color: white"></v-divider>
          <v-card-subtitle
            class="caption text-center font-weight-light white--text"
            >Variazione 24h</v-card-subtitle
          >
          <v-card-text
            class="headline text-center font-weight-light white--text"
            >{{
              jsonNazioneOggi.deceduti - jsonNazioneIeri.deceduti
            }}</v-card-text
          >
        </v-card>
      </v-col>
      <v-col lg="2" cols="6">
        <v-card
          height="100%"
          class=""
          color="orange"
          :elevation="6"
          outlined
          tile
        >
          <v-card-title class="text-left">
            <span class="headline font-weight-light white--text"
              >Totale Casi
            </span></v-card-title
          >
          <v-card-text
            class="headline text-center font-weight-black white--text"
          >
            {{ jsonNazioneOggi.totale_casi }}</v-card-text
          >
          <v-divider style="border-color: white"></v-divider>
          <v-card-subtitle
            class="caption text-center font-weight-light white--text"
            >Variazione 24h</v-card-subtitle
          >
          <v-card-text
            class="headline text-center font-weight-light white--text"
            >{{ jsonNazioneOggi.nuovi_positivi }}</v-card-text
          >
        </v-card>
      </v-col>
      <v-col lg="4" cols="12">
        <v-card>
          <v-card-subtitle>Notizie</v-card-subtitle>
          <v-list max-height="175px" class="overflow-y-auto">
            <v-list-item-group>
              <v-list-item dense v-for="(item, i) in jsonNoteCron" :key="i">
                <v-list-item-content>
                  <!-- <v-list-item-title v-text="item.note"> </v-list-item-title> -->
                  <v-list-item-title class="text-left">
                    {{ formatData(item.data) }}
                  </v-list-item-title>
                  <span class="body-2 text-justify">{{ item.note }}</span>
                </v-list-item-content>
              </v-list-item>
            </v-list-item-group>
          </v-list>
        </v-card>
      </v-col>
    </v-row>
  </v-card>
</template>

<script>
export default {
  components: {},
  props: {
    jsonTrendNazione: {
      type: Array,
    },
    jsonNote: {
      type: Array,
    },
  },
  data: function () {
    return {};
  },
  methods: {
    formatData: function (data) {
      let d = new Date(data);
      //let datastr = d.getDay() + "/" + d.getMonth() + "/" + d.getFullYear();
      return d.toLocaleString();
    },
  },
  mounted() {},

  computed: {
    jsonNoteCron() {
      let rev = this.jsonNote;
      return rev.reverse();
    },

    jsonNazioneIeri() {
      return this.jsonTrendNazione[this.jsonTrendNazione.length - 2];
    },
    jsonNazioneOggi() {
      return this.jsonTrendNazione[this.jsonTrendNazione.length - 1];
    },
  },
};
</script>