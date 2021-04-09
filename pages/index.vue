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
            :items="posts"
            :search="search"
          >
          </v-data-table>
        </v-card>
      </template>
    </div>
    <nuxt-link to="/album-comp" >album link</nuxt-link>
  </div>
</template>

<script>
export default {
  data () {
    return {
      search: '',
      posts: [],
      post: {
        title: "",
        body: "",
        id: null,
        userId: null,
      }
    }
  },
  computed:{
    headers() {
      return [
        {text:"Title",value:"title"},
        {text:"Body",value:"body"},
        {text: 'User Id', value: 'userId'},
        {text: 'Id', value: 'id'},
      ]
    }
  },
  mounted() {
    this.getPosts();
  },
  methods: {
    async getPosts() {
      const url = "https://jsonplaceholder.typicode.com/posts";
      const {data} = await this.$axios.get(url);
      this.posts = data;
    },
  }
}
</script>
<style scoped>
.card{
  padding-top: 54px;
}
</style>
