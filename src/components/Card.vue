<template>
    <transition-group name="flip">
        <div class="card card-backside"
             key="noImage"
             v-show="!flipped"
             @click="flipCard">
        </div>
        <div class="card"
             :class="{ shake: shakeAnimation }"
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
              shakeAnimation: false
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
                    this.flipped = false;
            },
            toggleShakeAnimation () {
                this.shakeAnimation = !this.shakeAnimation;
                setTimeout(() =>{
                    this.shakeAnimation = !this.shakeAnimation;
                }, 1500)
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

    .shake {
        animation: shake 0.5s cubic-bezier(.36,.07,.19,.97) both;
        transform: translate3d(0, 0, 0);
        backface-visibility: hidden;
        perspective: 1000px;
    }

/*    .enlarge {
        animation-name: enlarge;
        animation-duration: 0.5s;
        animation-iteration-count: 1;
    }

    @keyframes enlarge {
        from {height: 12rem; width: 18rem}
        to {height: 15rem; width: 22.5rem}
    }*/

    @keyframes shake {
        10%, 90% {
            transform: translate3d(-1px, 0, 0);
        }

        20%, 80% {
            transform: translate3d(2px, 0, 0);
        }

        30%, 50%, 70% {
            transform: translate3d(-4px, 0, 0);
        }

        40%, 60% {
            transform: translate3d(4px, 0, 0);
        }
    }

</style>