<template>
  <div ref="block" class="block" :style="{ justifyContent: justify }">
    <template v-for="(tag, index) in tags">
      <div ref="tag" :key="'tag_' + index" class="block__item-tag">
        <v-icon v-text="tag.icon" />
        {{ tag.text }}
      </div>
      <span ref="dot" :key="index" class="block__item-dot">
        <v-icon color="black" v-text="'mdi-circle-small'" />
      </span>
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

  mounted () {
    window.addEventListener('resize', this.resizeHandler)
    this.resizeHandler()
  },

  beforeDestroy () {
    window.removeEventListener('resize', this.resizeHandler)
  },

  methods: {
    resizeHandler () {
      const blockWidth = this.$refs.block.clientWidth
      const children = this.$refs.block.children

      let tagsWidth = 0
      let tagsVisible = 0
      let enough = true

      for (let i = 0; i < children.length; i++) {
        children[tagsVisible].classList.remove('hidden')
        if (enough && (tagsWidth + children[i].scrollWidth) < blockWidth) {
          tagsVisible = i % 2 ? i : children.length - 1
          tagsWidth += children[i].scrollWidth
          children[i].classList.remove('hidden')
        } else {
          enough = false
          children[i].classList.add('hidden')
        }
      }

      children[tagsVisible].classList.add('hidden')
    }
  }
}
</script>

<style lang="scss" scoped>
.hidden {
  position: absolute;
  top: -9999px;
}

.block {
  width: 100%;
  height: 100%;
  display: flex;
  flex-wrap: nowrap;

  &__item {

    &-tag {
      white-space: nowrap;
    }
  }
}
</style>
