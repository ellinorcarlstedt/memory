<template>
  <div>
    <h1>Memory</h1>
    <Card></Card>
  </div>
</template>

<script>
import Card from './Card.vue';

export default {
    name: 'Memory',
    components: {
      Card
    },
    data () {
        return {
            cards: [
                {
                    image: 'badger.jpg',
                    flipped: false
                },
                {
                    image: 'cat.jpg',
                    flipped: false
                },
                {
                    image: 'cow.jpg',
                    flipped: false
                },
                {
                    image: 'dog.jpg',
                    flipped: false
                },
                {
                    image: 'frog.jpg',
                    flipped: false
                },
                {
                    image: 'meerkat.jpg',
                    flipped: false
                },
                {
                    image: 'monkey.jpg',
                    flipped: false
                },
                {
                    image: 'turtle.jpg',
                    flipped: false
                },
            ]
        }
    }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
