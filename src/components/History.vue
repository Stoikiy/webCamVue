<template>
    <div class="webcam-captures-container" v-if="captures.length > 0">
        <span class="webcam-captures-text">History</span>
            <div
               class="webcam-image"
               v-for="images in captures"
               :key="images.id"
            >
                <img v-bind:src="images.img" height="240" alt="img" />
            </div>

    </div>
</template>

<script>
    export default {
        name: "History",
        props: {
            captures:{
                type: Array,
                default: () => ([])
            }
        },
    }
</script>

<style scoped>

  .webcam-captures-container {
      display: flex;
      margin-top: 160px;
      justify-content: flex-start;
      width: 100%;
      flex-wrap: wrap;
      position: relative;
  }

  .webcam-captures-text {
      font-size: 40px;
      position: absolute;
      left: 16px;
      bottom: 100%;
  }

  .webcam-image {
      margin: 20px 20px 0 20px;
  }

</style>