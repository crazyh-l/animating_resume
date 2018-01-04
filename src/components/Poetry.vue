<template>
          <div class="cd-scrolling-bg cd-color-2">
            <div class="cd-container">
              <p>
                {{msg}}
              </p>
            </div> <!-- cd-container -->
          </div> <!-- cd-scrolling-bg -->
</template>

<script>
export default {
  name: 'poetry',
  data () {
    return {
      msg: `   我愿意深深地扎入生活，吮尽生活的骨髓，过得扎实，简单，
           把一切不属于生活的内容剔除得干净利落，把生活逼到绝处，用最基本的形式，简单，简单，再简单。`
    }
  }
}
</script>


