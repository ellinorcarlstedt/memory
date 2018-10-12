<template>
    <div>
        <h1 class="main-heading">Memory</h1>
        <div class="card-wrapper">
            <Card v-for="(item, index) in cards"
                  :key="index"
                  ref="card"
                  :img="item"
                  :twoCardsFlipped="twoCardsFlipped"
                  @cardShown="handleFlippedCards(item, index)">
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

        data() {
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
                cards: [],
                flippedCard: {
                    cardImg: '',
                    index: ''
                },
                cardsMatched: [],
                twoCardsFlipped: false
            }
        },

        methods: {
            handleFlippedCards(cardImg, index) {
                if (!this.flippedCard.cardImg) {
                    this.flippedCard.cardImg = cardImg;
                    this.flippedCard.index = index;
                } else if (this.flippedCard.cardImg === cardImg) {
                    this.cardsMatched.push(cardImg);
                    this.twoCardsFlipped = true;
                    this.flippedCard.cardImg = '';
                    this.flippedCard.index = '';
                    setTimeout(() => {
                        this.twoCardsFlipped = false;
                    }, 1500);
                } else {
                    this.twoCardsFlipped = true;
                    this.$refs.card[index].toggleShakeAnimation();
                    this.$refs.card[this.flippedCard.index].toggleShakeAnimation();
                    setTimeout(() => {
                        this.$refs.card[index].reFlipCard();
                        this.$refs.card[this.flippedCard.index].reFlipCard();
                        this.flippedCard.cardImg = '';
                        this.flippedCard.index = '';
                        this.twoCardsFlipped = false;
                    }, 1500);
                }
            }
        },
        created() {
            const doubleImages = [...this.cardImages, ...this.cardImages];
            this.cards = doubleImages.sort(() => Math.random() - 0.5);
        }
    }

</script>

<style scoped>
    .main-heading {
        font-family: "Nanum Myeongjo", "Helvetica";
    }

    .card-wrapper {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        justify-content: center;
    }
</style>
