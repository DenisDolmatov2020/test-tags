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
  name: 'App',

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
      const tags = this.$refs.tag
      const dots = this.$refs.dot

      let tagsWidth = 0
      let tagsVisible = 0
      let enough = true

      for (let i = 0; i < tags.length; i++) {
        if (enough && (tagsWidth + tags[i].scrollWidth + dots[i].scrollWidth) < blockWidth) {
          tagsVisible = i
          tagsWidth += tags[i].scrollWidth + dots[i].scrollWidth
          tags[i].classList.remove('hidden')
          dots[i].classList.remove('hidden')
        } else {
          enough = false
          tags[i].classList.add('hidden')
          dots[i].classList.add('hidden')
        }
      }

      dots[tagsVisible].classList.add('hidden')
    }
  }
}
</script>

<style lang="scss" scoped>
.hidden {
  visibility: hidden;
}
.block {
  width: 100%;
  height: 100%;
  overflow: hidden;
  display: flex;
  flex-wrap: nowrap;

  &__item {
    // display: flex;

    &-tag {
      white-space: nowrap;
    }

    &:first-child {
      // flex-grow: 0;

      .block__item-dot {
        display: none;
      }
    }

    &-dot {
      text-align: center;
    }

    span {
      color: #333;
      text-wrap: none;
    }
  }
}
</style>
