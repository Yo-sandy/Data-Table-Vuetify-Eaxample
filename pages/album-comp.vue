
<template>
  <div class="container">
    <div>
      <Logo />
      <div class="card"></div>
      <template  >
        <v-card >
          <v-card-title>
            Nutrition
            <v-spacer></v-spacer>
            <v-text-field
              v-model="search"
              append-icon="mdi-magnify"
              label="Search"
              single-line
              hide-details
            ></v-text-field>
          </v-card-title>
          <v-data-table
            :headers="headers"
            :items="albums"
            :search="search"
            :items-per-page="5"
          >
            <template v-slot:item.url="{ item }">
              <div class="p-2">
                <v-img :src="item.url" :alt="item.url" height="100"></v-img>
              </div>
            </template>
            <template v-slot:item.thumbnailUrl="{ item }">
              <div class="p-2">
                <v-img :src="item.thumbnailUrl" :alt="item.thumbnailUrl"></v-img>
              </div>
            </template>
          </v-data-table>
        </v-card>
      </template>
    </div>
  </div>
</template>


<script>
export default {
  data () {
    return {
      search: '',
      albums: [],
      album: {
        title: "",
        url: "",
        id: null,
        albumId: null,
      }
    }
  },
  computed:{
    headers() {
      return [
        {text:"Title",value:"title"},
        {text: 'url', value: 'url'},
        {text: 'thumbnailUrl', value: 'thumbnailUrl'},
        {text: 'Id', value: 'id'},
      ]
    }
  },
  mounted() {
    this.getAlbums();
  },
  methods: {
    async getAlbums() {
      const url = "https://jsonplaceholder.typicode.com/albums/1/photos";
      const {data} = await this.$axios.get(url);
      this.albums = data;
    },
  }
}
</script>
<style scoped>
.card{
  padding-top: 54px;
}
</style>
