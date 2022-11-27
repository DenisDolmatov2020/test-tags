<template>
  <v-app>
    <v-main>
      <div
        v-for="(event, index) in events"
        :key="index" class="mt-6 pa-3"
        :style="{ width: event.width }"
      >
        <h3 class="mb-2">{{ event.title }}</h3>
        <div>#1</div>
        <TagsList :tags="tags" :justify="event.justify" :width="event.width" />
        <hr class="mx-1" />
        <div>#2</div>
        <TagsList2 :tags="tags" :justify="event.justify" :width="event.width" />
        <hr class="mx-1" />
        <div>#3</div>
        <TagsList3 :tags="tags" :justify="event.justify" :width="event.width" />
        <hr class="mx-1" />
      </div>
    </v-main>
  </v-app>
</template>

<script>
import TagsList from '@/components/TagsList'
import TagsList2 from '@/components/TagsList2'
import TagsList3 from '@/components/TagsList3'

export default {
  name: 'App',

  components: {
    TagsList,
    TagsList2,
    TagsList3
  },

  data: () => ({
    events: [
      { title: 'Город сыра и мира', width: '100%', justify: 'space-between' },
      { title: 'Экскурсия в национальный парк "Куршская коса"', width: '100%', justify: 'left' },
      { title: 'О кирках, рыцарях и замках', width: '50%', justify: 'space-between' },
      { title: 'Экскурсия в Янтарный', width: '50%', justify: 'left' }
    ],

    tags: [
      { icon: 'mdi-star-outline', text: '5' },
      { text: 'Обзорная' },
      { icon: 'mdi-bus', text: 'На автобусе' },
      { text: '25 марта' },
      { icon: 'mdi-clock-outline', text: '6 часов' },
      { icon: 'mdi-plus', text: 'Дополнительный' }
    ]
  })
}
</script>
<style lang="scss">
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

  .hidden {
    position: absolute;
    opacity: 0;
  }
}
</style>
