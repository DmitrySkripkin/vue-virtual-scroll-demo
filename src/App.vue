<template>
  <div id="app">
    <list :data="data"></list>
  </div>
</template>

<script>
import List from './components/List'

const images = [
  'https://images.unsplash.com/photo-1417577097439-425fb7dec05e?dpr=1&auto=format&crop=entropy&fit=crop&w=767&h=431&q=80&cs=tinysrgb',
  'https://images.unsplash.com/photo-1424460421773-58b49adfc68a?dpr=1&auto=format&crop=entropy&fit=crop&w=767&h=511&q=80&cs=tinysrgb',
  'https://images.unsplash.com/photo-1446776877081-d282a0f896e2?dpr=1&auto=format&crop=entropy&fit=crop&w=767&h=511&q=80&cs=tinysrgb',
  'https://images.unsplash.com/photo-1473813585561-ec87eac91e39?dpr=1&auto=format&crop=entropy&fit=crop&w=767&h=534&q=80&cs=tinysrgb',
  'https://images.unsplash.com/photo-1447433909565-04bfc496fe73?dpr=1&auto=format&crop=entropy&fit=crop&w=767&h=511&q=80&cs=tinysrgb',
  'https://images.unsplash.com/photo-1429305336325-b84ace7eba3b?dpr=1&auto=format&crop=entropy&fit=crop&w=767&h=511&q=80&cs=tinysrgb',
  'https://images.unsplash.com/photo-1442876906995-6761040d1f0b?dpr=1&auto=format&crop=entropy&fit=crop&w=767&h=511&q=80&cs=tinysrgb',
  'https://images.unsplash.com/photo-1473806189829-9641421a59f1?dpr=1&auto=format&crop=entropy&fit=crop&w=767&h=512&q=80&cs=tinysrgb',
  'https://images.unsplash.com/photo-1461143625960-5c2878bd4264?dpr=1&auto=format&crop=entropy&fit=crop&w=767&h=512&q=80&cs=tinysrgb',
  'https://images.unsplash.com/photo-1473813585561-ec87eac91e39?dpr=1&auto=format&crop=entropy&fit=crop&w=767&h=534&q=80&cs=tinysrgb',
  'https://images.unsplash.com/photo-1468186402854-9a641fd7a7c4?dpr=1&auto=format&crop=entropy&fit=crop&w=767&h=512&q=80&cs=tinysrgb',
  'https://images.unsplash.com/photo-1467173572719-f14b9fb86e5f?dpr=1&auto=format&crop=entropy&fit=crop&w=767&h=511&q=80&cs=tinysrgb',
  'https://images.unsplash.com/photo-1443926818681-717d074a57af?dpr=1&auto=format&crop=entropy&fit=crop&w=767&h=767&q=80&cs=tinysrgb',
  'https://images.unsplash.com/photo-1422513391413-ddd4f2ce3340?dpr=1&auto=format&crop=entropy&fit=crop&w=767&h=511&q=80&cs=tinysrgb',
  'https://images.unsplash.com/12/sky.JPG?dpr=1&auto=format&crop=entropy&fit=crop&w=767&h=575&q=80&cs=tinysrgb',
  'https://images.unsplash.com/photo-1428709671697-959dbd39a3ac?dpr=1&auto=format&crop=entropy&fit=crop&w=767&h=431&q=80&cs=tinysrgb',
  'https://images.unsplash.com/photo-1426840963626-ffdf2d7ef80b?dpr=1&auto=format&crop=entropy&fit=crop&w=767&h=511&q=80&cs=tinysrgb',
  'https://images.unsplash.com/photo-1466853817435-05b43fe45b39?dpr=1&auto=format&crop=entropy&fit=crop&w=767&h=557&q=80&cs=tinysrgb',
  'https://images.unsplash.com/reserve/qw4JvEnzT3iyU1HR9Ed5_DSC02436.jpg?dpr=1&auto=format&crop=entropy&fit=crop&w=767&h=430&q=80&cs=tinysrgb',
  'https://images.unsplash.com/photo-1471324652636-ea67fe86bce9?dpr=1&auto=format&crop=entropy&fit=crop&w=767&h=511&q=80&cs=tinysrgb',
  'https://images.unsplash.com/photo-1473683409080-b66239d1e547?dpr=1&auto=format&crop=entropy&fit=crop&w=767&h=511&q=80&cs=tinysrgb'
]

const texts = [
  `In mathematics, "infinity" is often treated as a number (i.e., it counts or measures things: "an infinite number of terms") but it is not the same sort of number as natural or real numbers.
Georg Cantor formalized many ideas related to infinity and infinite sets during the late 19th and early 20th centuries. In the theory he developed, there are infinite sets of different sizes (called cardinalities). For example, the set of integers is countably infinite, while the infinite set of real numbers is uncountable.`,
  `Infinity (symbol: ∞) is an abstract concept describing something without any bound or larger than any number. Philosophers have speculated about the nature of the infinite, such as Zeno of Elea, who proposed many paradoxes involving infinity, and Eudoxus of Cnidus, who used the idea of infinitely small quantities in his method of exhaustion. Modern mathematics uses the concept of infinity in the solution of many practical and theoretical problems, such as in calculus and set theory, and the idea also is used in physics and the other sciences.`,
  `Infinity (symbol: ∞) is an abstract concept describing something without any bound or larger than any number. Philosophers have speculated about the nature of the infinite, such as Zeno of Elea, who proposed many paradoxes involving infinity, and Eudoxus of Cnidus, who used the idea of infinitely small quantities in his method of exhaustion. Modern mathematics uses the concept of infinity in the solution of many practical and theoretical problems, such as in calculus and set theory, and the idea also is used in physics and the other sciences.
  In mathematics, "infinity" is often treated as a number (i.e., it counts or measures things: "an infinite number of terms") but it is not the same sort of number as natural or real numbers.
Georg Cantor formalized many ideas related to infinity and infinite sets during the late 19th and early 20th centuries. In the theory he developed, there are infinite sets of different sizes (called cardinalities). For example, the set of integers is countably infinite, while the infinite set of real numbers is uncountable.
`
]

let hugeList = []
let i = 0

for (i; i < 1000; i++) {
  hugeList.push(
    {
      index: i,
      title: 'Post #' + i,
      text: texts[Math.floor((Math.random() * texts.length - 1) + 1)],
      author: 'Unknown',
      image: images[Math.floor((Math.random() * images.length - 1) + 1)],
      likes: Math.floor((Math.random() * 100) + 1)
    }
  )
}

export default {
  name: 'app',
  components: {
    List
  },
  data () {
    return {
      data: hugeList
    }
  }
}
</script>

<style>
body {
  padding: 0;
  margin: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
