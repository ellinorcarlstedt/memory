<template>
    <transition-group name="flip">
        <div class="card card-backside"
             key="noImage"
             v-show="!flipped"
             v-on:click="flipCard">
        </div>
        <div class="card"
             key="image"
             v-show="flipped">
            <img :src="fullImageSource"
                 class="card-img">
        </div>
    </transition-group>
</template>

<script>
    export default {
        name: "Card",
        props: {
            img: String,
            twoCardsFlipped: Boolean
        },
        data () {
          return {
              flipped: false,
          }
        },

        methods: {
            flipCard() {
                if (!this.twoCardsFlipped) {
                    this.flipped = !this.flipped;
                    this.$emit('cardShown');
                }
            },
            reFlipCard() {
                if (!this.flipped) {
                    this.flipped = !this.flipped;
                } else {
                    this.flipped = !this.flipped;
                }
            }
        },

        computed: {
              fullImageSource: function () {
                  return require(`@/images/${this.img}`);
              }
        }
    }
</script>

<style>
    * {
        box-sizing: border-box;
    }

    .card-img {
        height: 100%;
        width: 100%;
    }

    .card {
        height: 12rem;
        width: 18rem;
        margin-right: 1rem;
        margin-bottom: 1rem;
        border-radius: 1rem;
        box-shadow: 0.3rem 0.3rem 0.3rem lightgrey;
        overflow: hidden;
    }

    .card-backside {
        background-color: lightblue;
    }

    .flip-enter-active {
        transition: all 0.4s ease;
    }

    .flip-leave-active {
        display: none;
    }

    .flip-enter, .flip-leave {
        transform: rotateY(180deg);
        opacity: 0;

    }



</style>