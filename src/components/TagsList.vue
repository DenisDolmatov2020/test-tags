<template functional>
  <div class="block">
    <div
      v-for="(tag, index) in props.tags"
      :key="index"
      class="block__item"
      :class="{ 'block__item-grow': props.spaceBetween }"
    >
      <span class="block__item-dot" >
         <v-icon color="black" v-text="'mdi-circle-small'" />
      </span>

      <span class="block__item-tag">
        <v-icon v-text="tag.icon" />
        {{ tag.text }}
      </span>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.block {
  width: 100%;
  height: 30px;
  overflow: hidden;
  display: flex;
  flex-wrap: wrap;

  &__item {
    display: flex;

    &-grow {
      flex-grow: 1;
    }

    &:first-child {
      flex-grow: 0;

      .block__item-dot {
        display: none;
      }
    }

    &-dot {
      flex-grow: 1;
      text-align: center;
    }

    span {
      color: #333;
      text-wrap: none;
    }
  }
}
</style>
