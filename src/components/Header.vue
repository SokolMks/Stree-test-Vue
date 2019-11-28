<template>
  <div>
    <header>
      <div class="logo">
        <img src="../assets/logo.png" alt="Ubiqum bookstore" />
      </div>
      <div id="searchbox">
        <input
          type="text"
          :value="value"
          @input="$emit('input', $event.target.value)"
          name="searchengine"
          id="forsearch"
          placeholder="Search your book"
        />
      </div>
    </header>
  </div>
</template>

<script>
export default {
  props: ["value"]
};
</script>

<style>
header {
  background-color: #673b99;
  display:flex;
  justify-content: space-around;
  margin-bottom: 20px;
  box-shadow: 0px 0px 14px 0px rgba(0, 0, 0, 0.75);
  position: sticky;
  top: 0;
  z-index: 1;
}

#searchbox {
  align-self: center;
}

input {
  background-color: #f2f2f2;
  padding: 10px 22.5px;
  border: 1.5px solid #a0a0a0;
  outline: none;
  font-size: 1.2em;
}
</style>