<template>
    <div class="cd-scrolling-bg cd-color-1">
      <div class="cd-container">
        <p>
          {{msg}}
        </p>
      </div> <!-- cd-container -->
    </div> <!-- cd-scrolling-bg -->
</template>

<script>
export default {
  name: 'chopWood',
  data () {
    return {
      msg: `我步入丛林，因为我希望生活得有意义，我希望活的深刻，并汲取生命中所有的精华。然后从中学习，以免让我在生命终结时，却发现自己从来没有活过。`
    }
  }
}
</script>

