<template>
    <div class="list-wrapper">
      <div class="list">
        <div class="chunk" v-for="(chunk, index) in chunks" v-bind:style="{transform: 'translateY(' + chunk.offset + 'px)'}">
          <div class="sentinel-start" v-if="index === 0" v-bind:class="{disabled: lastChunk < 3}"></div>
          <div class="list-item" v-for="(item, index) in chunk.items">
            <list-item class="item-inner" :item="item" :id="'item-' + index"></list-item>
          </div>
          <div class="sentinel" v-if="index === chunks.length - 1" v-bind:class="{disabled: startFlag}"></div>
        </div>
      </div>
    </div>
</template>

<script>
import ListItem from './ListItem'

export default {
  mounted: function () {
    let self = this
    let options = {}
    let endCallback = function (entries, observer) {
      if (entries[0].intersectionRatio > 0) {
        let newChunks = {...self.chunks}
        newChunks = Object.keys(newChunks).map(function (key) { return newChunks[key] })
        newChunks.push({
          items: self.data.slice(self.lastChunk * 15, (self.lastChunk + 1) * 15),
          offset: self.offsets[self.lastChunk] + document.querySelector('.sentinel').offsetTop + 1000
        })
        self.offsets[self.lastChunk + 1] = self.offsets[self.lastChunk] + document.querySelector('.sentinel').offsetTop + 1000
        if (newChunks.length > 2) {
          newChunks.shift()
        }
        self.chunks = newChunks
        self.lastChunk++
        setTimeout(function () {
          startObserver.observe(document.querySelector('.sentinel-start'))
          endObserver.observe(document.querySelector('.sentinel'))
        }, 100)
      }
    }

    let startCallback = function (entries, observer) {
      if (entries[0].intersectionRatio > 0) {
        self.startFlag = true
        let newChunks = {...self.chunks}
        newChunks = Object.keys(newChunks).map(function (key) { return newChunks[key] })
        newChunks.unshift({
          items: self.data.slice((self.lastChunk - 2 - 1) * 15, (self.lastChunk - 2) * 15),
          offset: self.offsets['' + (self.lastChunk - 2)]
        })
        if (newChunks.length >= 2) {
          newChunks.pop()
          self.lastChunk--
        }
        self.chunks = newChunks
        setTimeout(function () {
          self.startFlag = false
          startObserver.observe(document.querySelector('.sentinel-start'))
          endObserver.observe(document.querySelector('.sentinel'))
        }, 100)
      }
    }
    // eslint-disable-next-line
    let endObserver = new IntersectionObserver(endCallback, options) // just two observers
    let endTarget = document.querySelector('.sentinel')
    endObserver.observe(endTarget)

    // eslint-disable-next-line
    let startObserver = new IntersectionObserver(startCallback, options) 
    let startTarget = document.querySelector('.sentinel-start')
    startObserver.observe(startTarget)
  },
  props: ['data'],
  data: function () {
    return {
      chunks: [{
        offset: 0,
        items: this.data.slice(0, 15)
      }],
      offsets: {'1': 0},
      lastChunk: 1,
      startFlag: false
    }
  },
  name: 'list',
  components: {
    ListItem
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.list-wrapper {
  margin: 0 auto;
  max-width: 800px;
  position: relative;
}
.list {
  width: 100%;
}

.chunk {
  width: 100%;
  position: absolute;
  top: 0;
}

.chunk > .sentinel {
  position: absolute;
  pointer-events: none;
  height: 1000px;
  width: 100%;
  visibility: hidden;
  bottom: 0;
  z-index: 9999;
}

.chunk > .sentinel-start {
  position: absolute;
  pointer-events: none;
  height: 1000px;
  width: 100%;
  visibility: hidden;
  top: 0;
  z-index: 9999;
}

.chunk > .sentinel-start.disabled, .chunk > .sentinel.disabled{
  display: none;
}
</style>
