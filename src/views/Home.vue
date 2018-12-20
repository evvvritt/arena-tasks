<template lang="pug">
  section.bg-white.min-h-screen.px-4
    article.sticky.pin-t.overflow-hidden(v-for="(list, i) in channels", :key="i", :class="cardClasses(i)")
      .border.rounded-lg.bg-white.shadow.overflow-hidden(:class="listClasses(list, i)")
        header.cursor-pointer(@click="active = active === i ? null : i")
          h1.p-6.text-2xl.truncate {{list.title}}
        list-items(:items="list.items", :disabled="active !== i")
</template>

<script>
import { items as dummyItems } from '@/demo/dummy'
import ListItems from '@/components/ListItems'
export default {
  name: 'Home',
  components: { ListItems },
  data () {
    return {
      active: null,
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
  },
  methods: {
    cardClasses (i) {
      if (this.active === null) return {
        'h-screen': true,
        '-mt-75vh': i > 0,
        'pt-4': true
      }
      if (this.active === i) return {
        'pt-4 pb-24': true
      }
      if (this.active !== i) return {
        'max-h-0': true
      }
    },
    listClasses (list, i) {
      const type = list.type
      return {
        'h-75vh': this.active === null,
        'min-h-75vh': i === this.active,
        'border-red text-red': type === 'private',
        'border-green text-green': type === 'public',
        'border-grey text-grey': type === 'closed'
      }
    }
  }
}
</script>
