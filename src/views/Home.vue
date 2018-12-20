<template lang="pug">
  section.bg-white.min-h-screen.pt-4.px-4
    .sticky.pin-t.pt-4.h-screen(v-for="(list, i) in channels", :key="i", :class="{'-mt-75vh': i > 0}")
      .min-h-75vh.border.rounded-lg.bg-white.shadow(:class="listClasses(list)")
        header.p-4
          h1 {{list.title}}
        ul
          li(v-for="item in list.items")
</template>

<script>
import { items as dummyItems } from '@/demo/dummy'
export default {
  name: 'Home',
  methods: {
    listClasses (list) {
      const type = list.type
      return {
        'border-red text-red': type === 'private',
        'border-green text-green': type === 'public',
        'border-grey text-grey': type === 'closed'
      }
    }
  },
  data () {
    return {
      channels: [
        {
          title: 'watch',
          type: 'public',
          items: dummyItems
        },
        {
          title: 'read',
          type: 'private',
          items: dummyItems
        },
        {
          title: 'listen',
          type: 'closed',
          items: dummyItems
        },
        {
          title: 'news',
          type: 'public',
          items: dummyItems
        },
        {
          title: 'shows',
          type: 'private',
          items: dummyItems
        }
      ]
    }
  }
}
</script>

<style>
</style>
