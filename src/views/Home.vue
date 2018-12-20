<template lang="pug">
  section.bg-white.min-h-screen.px-4
    article.sticky.pin-t.overflow-hidden(v-for="(list, i) in channels", :key="i", :class="cardClasses(i)")
      .min-h-75vh.border.rounded-lg.bg-white.shadow(:class="listClasses(list)")
        header.p-6.cursor-pointer(@click="active = active === i ? null : i")
          h1 {{list.title}}
        ul
          li.p-6.border-t.border-dotted.overflow-hidden(v-for="(item, ii) in list.items", :key="ii", :class="{'border-b': ii === list.items.length - 1, 'opacity-25': active === null }")
            article.max-h-1em
              template(v-if="item.type === 'link'")
                h4.text-sm.truncate {{item.title}}
              template(v-if="item.type === 'text'")
                h4.text-sm.truncate {{item.title}}
              template(v-else-if="item.type === 'image'")
                figure.max-h-1em.px-6.pt-2
                  img.block.m-auto(:src="item.url")
</template>

<script>
import { items as dummyItems } from '@/demo/dummy'
export default {
  name: 'Home',
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
        'pt-4': true
      }
      if (this.active !== i) return {
        'max-h-0': true
      }
    },
    listClasses (list) {
      const type = list.type
      return {
        'border-red text-red': type === 'private',
        'border-green text-green': type === 'public',
        'border-grey text-grey': type === 'closed'
      }
    }
  }
}
</script>
