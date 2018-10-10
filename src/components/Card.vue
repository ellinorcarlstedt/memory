<template>
    <div>
        <img :src="fullImageSource"
             class="card-img">
    </div>
</template>

<script>
    export default {
        name: "Card",
        props: {
            img: String
        },
        data () {
          return {
              flipped: false,
          }
        },
        computed: {
              fullImageSource: function () {
                  return require(`@/images/${this.img}`);
              }
        }
    }
</script>

<style scoped>

    .card-img {
        height: 12rem;
        width: 18rem;
    }

</style>