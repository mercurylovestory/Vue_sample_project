<template>
  <div
    id="app"
    class="bg-teal-lightest relative p-10">
    
    <div class="md:w-1/2 md:min-h-screen center bg-white overflow-scroll">
      <div>
      <div class="relative mr-6 my-2">
        <svg version="1.1" class="h-4 text-dark" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
	 viewBox="0 0 52.966 52.966" style="enable-background:new 0 0 52.966 52.966;" xml:space="preserve">
        </svg>
        <VueFuse
          :list="books"
          :fuse-opts="options"
          :search="search"
          :map-results="false"
          placeholder="Search anything"
          class="bg-purple-white shadow rounded border-0 p-3 outline-none"
          @fuse-results="handleResults"
        />
    <div class="absolute pin-r pin-t mt-3 mr-4 text-purple-lighter"> </div>
</div>
      </div>
      <div
        v-for="(book, i) in results"
        :key="i"
        class="max-w-md mx-auto bg-white rounded-xl shadow-md overflow-hidden md:max-w-2xl outline-black mb-2 text-left">
        <div class="thumb-img bg-grey">
            <a :href="book.item.email" target="_blank">
                <img :src="book.item.avatar">
            </a>
        </div>
        <div class="p-8">
            <h3 >{{book.item.name}}</h3><br>
            <h6 class="news-title">{{ book.item.title }}</h6><br>
            <div class="news-data"><br>
                <div class="news-source">{{ book.item.address }}{{ book.item.city }}</div>
                
                <div class="news-date">{{ book.item.email}}</div>
            </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import VueFuse from './components/VueFuse.vue'
import UserData from "./users.json"

export default {
  name: 'App',
  components: {
    VueFuse,
  },
  data () {
    return {
      advanced: false,
      search: '',
      includeScore: false,
      results: [],
      books: UserData,
    }
  },
  computed: {
    options () {
      return {
        keys: [
          {
            name: 'name',
            weight: 2,
          },
          'email',
          'address',
          'title',
          
        ],
        includeScore: this.includeScore,
      }
    },
  },
  methods: {
    handleResults (r) {
      this.results = r
    },
  },
}
</script>

<style scoped>
.center {
  margin: auto;
  text-align: center;
}
svg {
  position: sticky;
  top: 15px;
  left: 15px;
}
.fuse {
  position: sticky;
  top: 18px;
  left: 70px;
}
.thumb-img {
  float:left;
  width: 150px;
  margin-right: 10px;
  img {
    width: 150px;
    height: 150px;
    border-radius: 6px;
    display:block;
  }
}
.news-item{
  text-align: left;
  background: #FFF;
  margin: 10px 15px 10px 10px;
  border-radius: 6px;
  border-color: #ececec;
  max-height: 200px;
  overflow: hidden;
  padding: 10px;
  box-shadow: 2px 2px 2px rgba(31,41,56,0.1), -2px -2px 2px rgba(31,41,56,0.1);
  p {
    font-size: 14px;
    line-height: 1.2;
    margin-bottom: .25rem;
  }
}
.news-title{
  font-size: 14px;
  font-weight:bold;
  margin-bottom: .25rem;
}
.news-data{
  display: block;
  font-size: 13px;
  color: #565656;
}
.news-source {
  display:inline-block;
  color: grey;
}
.news-date {
  display: inline-block;
  float:right;
}
</style>
