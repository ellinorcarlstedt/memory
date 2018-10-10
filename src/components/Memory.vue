<template>
  <div>
    <h1>Memory</h1>
      <div class="card-wrapper">
        <Card v-for="item in cards" v-bind:img="item.image"></Card>
      </div>
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
            cardImages: [
                'badger.jpg',
                'cat.jpg',
                'cow.jpg',
                'dog.jpeg',
                'frog.jpg',
                'meerkat.jpg',
                'monkey.jpg',
                'turtle.jpg'
            ]
        }
    },
    computed: {
        cards: function () {
            const copiedImages = this.cardImages.slice(0);
            const doubleImages = copiedImages.concat(this.cardImages);
            let cards = [];
            for(let img of doubleImages) {
                cards.push({
                    image: img,
                    order: Math.floor(Math.random() * 100)
                });
            }
            const cardsInRandomOrder = cards.sort(function(a, b){
                return a.order - b.order}
            );
            return cardsInRandomOrder;
        }
    }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
 .card-wrapper {
   display: flex;
   flex-direction: row;
   flex-wrap: wrap;
   justify-content: center;
 }
</style>
