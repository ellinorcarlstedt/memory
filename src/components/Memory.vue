<template>
  <div>
    <h1>Memory</h1>
      <div class="card-wrapper">
        <Card v-for="(item, index) in cards"
              v-bind:key="index"
              v-bind:ref="index"
              v-bind:img="item.image"
              v-bind:twoCardsFlipped="twoCardsFlipped"
              v-on:cardShown="handleFlippedCards(item.image, index)">
        </Card>
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
            ],
            flippedCard: {
                cardImg: '',
                index: ''
            },
            twoCardsFlipped: false
        }
    },

    methods: {
        handleFlippedCards(cardImg, index) {
            if (!this.flippedCard.cardImg) {
                this.flippedCard.cardImg = cardImg;
                this.flippedCard.index = index;
            } else if (this.flippedCard.cardImg === cardImg) {
                this.twoCardsFlipped = true;
                this.flippedCard.cardImg = '';
                this.flippedCard.index = '';
                setTimeout(() => {
                    this.twoCardsFlipped = false;
                }, 1500);
            } else {
                this.twoCardsFlipped = true;
                  setTimeout(() => {
                      this.$refs[index][0].reFlipCard();
                      this.$refs[this.flippedCard.index][0].reFlipCard();
                      this.flippedCard.cardImg = '';
                      this.flippedCard.index = '';
                      this.twoCardsFlipped = false;
                  }, 1500);
            }
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
