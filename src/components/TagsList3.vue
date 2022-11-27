<template>
  <div ref="block" class="block" :style="{ justifyContent: justify }">
    <template v-for="(tag, index) in tags">
      <span :key="index" class="block__item-dot" :class="{ hidden: !index || index >= tagsVisible }">
        <v-icon color="black" v-text="'mdi-circle-small'" />
      </span>

      <div ref="tag" :key="'tag_' + index" class="block__item-tag" :class="{ hidden: index >= tagsVisible }">
        <v-icon v-text="tag.icon" />
        {{ tag.text }}
      </div>
    </template>
  </div>
</template>

<script>
export default {
  props: {
    justify: {
      type: String,
      default: ''
    },

    width: {
      type: String
    },

    tags: {
      type: Array
    }
  },

  data () {
    return {
      tagsVisible: 0
    }
  },

  mounted () {
    window.addEventListener('resize', this.resizeHandler)
    this.resizeHandler()
  },

  beforeDestroy () {
    window.removeEventListener('resize', this.resizeHandler)
  },

  methods: {
    resizeHandler () {
      const tags = this.$refs.tag
      const dots = document.getElementsByTagName('span')

      this.tagsVisible = 0
      let tagsWidth = 0

      for (let i = 0; i < tags.length; i++) {
        tagsWidth += tags[i].scrollWidth + dots[0].scrollWidth

        if (tagsWidth < this.$refs.block.clientWidth) {
          this.tagsVisible += 1
        } else {
          return
        }
      }
    }
  }
}
</script>
