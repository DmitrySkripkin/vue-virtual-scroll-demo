<template>
  <div class="item" :id="'item-' + index">
    <h2>{{ item.title }}</h2>
    <img :src="item.image">
    <div class="text-wrapper">
      <p>{{ item.text }}</p>
    </div>
    <div class="meta">
      <span class="heart"></span>
      <span>{{ item.likes }}</span>
      <span> | </span>
      <span>Posted by {{ item.author }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'list-item',
  props: ['item', 'index']
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h2 {
  padding: 15px;
}
h2, p {
  margin: 0;
  max-width: 100%;
  display: block;
}

.item {
  overflow: hidden;
  padding: 30px 0 5px 0;
  border-bottom: 1px solid #ddd;
  position: relative;
}

.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  z-index: 1000;
  background-color: #ddd;
  opacity: 1;
}

img, p, video {
  display: block;
  width: 100%;
}

.text-wrapper {
  padding: 15px;
}

.meta {
  padding: 0 15px 15px 15px;
  font-size: 0.8em;
  color: #ccc;
  text-align: right;
}

p {
  word-wrap: break-word;
}

.heart {
  background-color: #aaa;
  display: inline-block;
  height: 10px;
  margin: 0 5px;
  position: relative;
  top: 0;
  transform: rotate(-45deg);
  width: 10px;
}

.heart:before,
.heart:after {
  content: "";
  background-color: #aaa;
  border-radius: 50%;
  height: 10px;
  position: absolute;
  width: 10px;
}

.heart:before {
  top: -5px;
  left: 0;
}

.heart:after {
  left: 5px;
  top: 0;
}
</style>

