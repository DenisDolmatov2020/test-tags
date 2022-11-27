<template>
  <div id="block" :style="{ justifyContent: justify }">
    <template v-for="(tag, index) in updatedTags">
      <span :key="index" class="block__item-dot" :class="{ hidden: tag.dotHidden }">
        <v-icon color="black" v-text="'mdi-circle-small'" />
      </span>

      <div ref="tag" :key="'tag_' + index" class="block__item-tag" :class="{ hidden: tag.tagHidden }">
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
      updatedTags: this.tags
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
      const blockWidth = document.getElementById('block').offsetWidth
      const tags = this.$refs.tag
      const dots = document.getElementsByTagName('span')
      const dotWidth = dots[0].scrollWidth

      this.updatedTags = []

      for (let i = 0; i < tags.length; i++) {
        this.updatedTags.push({ ...this.tags[i] })
        const tagsWidth = i ? this.updatedTags[i - 1].tagsWidth : 0
        this.updatedTags[i].tagsWidth = tagsWidth + tags[i].scrollWidth + dotWidth
        this.updatedTags[i].tagHidden = this.updatedTags[i].tagsWidth > blockWidth

        if (!i || this.updatedTags[i - 1].tagHidden || this.updatedTags[i].tagHidden) {
          this.updatedTags[i].dotHidden = true
        }
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.hidden {
  display: none;
}

#block {
  width: 100%;
  height: 100%;
  display: flex;
  flex-wrap: nowrap;

  .block__item-tag {
      white-space: nowrap;
  }
}
</style>
