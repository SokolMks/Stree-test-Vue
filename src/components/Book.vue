<template>
  <div class="flip-card">
    <div class="flip-card-inner">
      <div class="flip-card-front">
        <img :src="book.cover" alt="book cover" />
      </div>
      <div class="flip-card-back">
        <h2 class="title">{{ book.title }}</h2>
        <p class="info">{{ book.description }} {{ book.language }}</p>
        <a v-bind:href="book.detail" data-fancybox="gallery" v-bind:data-caption="book.title">
          <button>More Info</button>
        </a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "book",
  props: {
    book: Object
  }
};
</script>

<style>
/* Books cards flip */
.flip-card-front > img {
  width: 300px;
  height: 420px;
}
.flip-card {
  background-color: transparent;
  width: 300px;
  height: 420px;
  margin: 5px;
  perspective: 1000px;
}
.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.6s;
  transform-style: preserve-3d;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
}
.flip-card:hover .flip-card-inner {
  transform: rotateY(180deg);
}
.flip-card-front,
.flip-card-back {
  display: flex;
  flex-direction: column;
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  justify-content: center;
  align-items: center;
}
.flip-card-front {
  background-color: #c872cfea;
  color: black;
}
.flip-card-back {
  background-color: #c872cfea;
  color: #f2f2f2;
  transform: rotateY(180deg);
}
/* Button */
button {
  background-color: #f2f2f2;
  color: black;
  border-radius: 4px;
  padding: 12px 28px;
  border: 2px solid #555555;
  outline: none;
  transition-duration: 0.4s;
  font-size: 1.08em;
}
button:hover {
  background-color: #555555;
  color: #f2f2f2;
}
.title {
  margin-bottom: 5px;
  font-size: 1.5em;
}
.info {
  margin-top: 5px;
  margin-bottom: 10px;
  width: 80%;
  font-size: 1.08em;
}
</style>