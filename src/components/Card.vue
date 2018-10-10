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
            details: Object
        },
        data () {
          return {
              cardDetails: {},
              linkroot: "../images/"
          }
        },
        methods: {
            putPropsInData () {
                this.cardDetails = this.details;
            }
        },
        computed: {
              fullImageSource: function () {
                  return require(`@/images/${this.details.image}`);
              }
        },
        created() {
            this.putPropsInData();
        }
    }
</script>

<style scoped>

    .card-img {
        height: 12rem;
        width: 18rem;
    }

</style>