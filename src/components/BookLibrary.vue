<template>
  <div>
    <div v-if="loading===false" class="container">
      <book 
        v-for="(book,i) in getBooks"
        v-bind:key="i"
        :book="book"/>
    <div v-if="getBooks==''" id="noresults">There are no books matching your search.</div>
    </div>

    <div v-if="loading===true" id="load-icon">
      <div class="lds-ellipsis">
        <div></div>
        <div></div>
        <div></div>
        <div></div>
      </div>
    </div>
  </div>
</template>

<script>
import book from "./Book";
export default {
  name: "library",
  data() {
    return {
      books:[],

      loading: true
    };
  },
  components: {
    book
  },
  props: {
    search: String
  },
  methods: {
    getData() {
      fetch("https://api.myjson.com/bins/zyv02", {
        method: "GET",
        headers:{}
      })
      .then(library => {
        console.log(library);
        return library.json();
      })
      .then(library => {
        console.log(library);
        this.books = library.books;
        this.loading = false;
      })
      .catch(function(error) {
        console.log(error);
      });
    }
  },
  computed: {
    getBooks() {
      return this.books.filter(book => {
        let titlefilter = book.title
          .toUpperCase()
          .includes(this.search.toUpperCase());
        let descriptionfilter = book.description
          .toUpperCase()
          .includes(this.search.toUpperCase());

        return titlefilter || descriptionfilter;
      });
    }
  },
  created() {
    this.getData();
  }
};
</script>

<style>
.container {
  display: flex;
  flex-wrap: wrap;
  margin: auto;
  padding: auto;
  justify-content: center;
}

/* Loader */
#load-icon {
  text-align: center;
}

.lds-ellipsis {
  display: inline-block;
  position: relative;
  width: 64px;
  height: 64px;
}
.lds-ellipsis div {
  position: absolute;
  top: 27px;
  width: 11px;
  height: 11px;
  border-radius: 50%;
  background: rgb(3, 5, 109);
  animation-timing-function: cubic bezier(0, 1, 1, 0);
}
.lds-ellipsis div:nth-child(1) {
  left: 6px;
  animation: lds-ellipsis1 0.6s infinite;
}
.lds-ellipsis div:nth-child(2) {
  left: 6px;
  animation: lds-ellipsis2 0.6s infinite;
}
.lds-ellipsis div:nth-child(3) {
  left: 26px;
  animation: lds-ellipsis2 0.6s infinite;
}
.lds-ellipsis div:nth-child(4) {
  left: 45px;
  animation: lds-ellipsis3 0.6s infinite;
}
@keyframes lds-ellipsis1 {
  0% {
    transform: scale(0);
  }
  100% {
    transform: scale(1);
  }
}
@keyframes lds-ellipsis3 {
  0% {
    transform: scale(1);
  }
  100% {
    transform: scale(0);
  }
}
@keyframes lds-ellipsis2 {
  0% {
    transform: translate(0, 0);
  }
  100% {
    transform: translate(19px, 0);
  }
}

/* No result message */
#noresults {
  text-align: center;
  font-size: 1.1em;
  width: 50%;
  margin: 0 auto;
}
</style>