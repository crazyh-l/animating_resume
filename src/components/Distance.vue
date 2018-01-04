<template>
        <div class="cd-scrolling-bg cd-color-3">
          <div class="cd-container">
            <p>
              {{msg}}
            </p>
          </div> <!-- cd-container -->
        </div> <!-- cd-scrolling-bg -->
</template>

<script>
export default {
  name: 'distance',
  data () {
    return {
      msg: `时间决定你会在生命中遇见谁，你的心决定你想要谁出现在你的生命里，而你的行为决定最后谁能留下。`
    }
  }
}
</script>
