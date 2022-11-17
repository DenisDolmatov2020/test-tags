<template>
  <v-app>
    <v-main>
      <div
        v-for="(event, index) in events"
        :key="index" class="mt-6 pa-3"
        :style="{ width: event.width }"
      >
        <h3 class="mb-2">{{ event.title }}</h3>
        <TagsList :tags="tags" :space-between="event.spaceBetween" />
        <hr class="mx-1" />
      </div>
    </v-main>
  </v-app>
</template>

<script>
import TagsList from '@/components/TagsList'

export default {
  name: 'App',

  components: {
    TagsList
  },

  data: () => ({
    events: [
      { title: 'Город сыра и мира', width: '100%', spaceBetween: true },
      { title: 'Экскурсия в национальный парк "Куршская коса"', width: '100%', spaceBetween: false },
      { title: 'О кирках, рыцарях и замках', width: '50%', spaceBetween: true },
      { title: 'Экскурсия в Янтарный', width: '50%', spaceBetween: false }
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
