<template>
  <div>
    <v-text-field v-model="query" label="Search"></v-text-field>
    <v-btn color="dark" @click="searchMusic">Search</v-btn>
    <v-divider class="mt-5 mb-1"></v-divider>
    <div class="d-flex flex-wrap">
      <v-card
        v-for="(music, index) in results"
        :key="index"
        class="ma-2"
        width="344px"
        height="230px"
        outlined
      >
        <v-list-item three-line>
          <v-list-item-content>
            <div class="overline mb-4">Price: {{ music.collectionPrice }}</div>
            <v-list-item-title class="headline mb-1">
              {{ music.trackName }}
            </v-list-item-title>
            <v-list-item-subtitle>{{ music.artistName }}</v-list-item-subtitle>
          </v-list-item-content>

          <img :src="music.artworkUrl100" alt="" style="width: 50%" />
        </v-list-item>

        <v-card-actions>
          <v-btn outlined rounded text @click="musicUrl(music)">Visit</v-btn>
        </v-card-actions>
      </v-card>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      query: '',
      results: {},
    }
  },
  methods: {
    searchMusic() {
      const url =
        'https://itunes.apple.com/search?term=' + this.query + '&page=1'
      axios.get(url).then((res) => {
        // eslint-disable-next-line no-console
        console.log(res.data.results)
        this.results = res.data.results
      })
    },
    musicUrl(m) {
      window.location = m.trackViewUrl
    },
  },
}
</script>

<style></style>
