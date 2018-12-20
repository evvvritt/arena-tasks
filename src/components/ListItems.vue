<template lang="pug">
  ul(:class="{'pointer-events-none opacity-25': disabled }")
    li.px-6.border-t.border-dotted.border-grey.overflow-hidden.relative(v-for="(item, i) in items", :key="i", :class="itemClasses(i)", @click="toggleItem(i)")
      article.text-sm(:class="{'max-h-1em': !isActive(i) }")
        template(v-if="item.type === 'link'")
          h4.truncate {{item.title}}
          div.mt-6.text-xs(v-html="item.description")
        template(v-if="item.type === 'text'")
          h4.truncate {{item.title}}
          div.mt-6.text-xs(v-html="item.description")
        template(v-else-if="item.type === 'image'")
          figure.px-12.pt-2(:class="{'grayscale opacity-66': !isActive(i)}")
            img.block.m-auto(:src="item.url")
          h4.mt-8 {{item.title}}
          div.mt-6.text-xs(v-html="item.description")
      //- hghlight
      .absolute.pin-r.pin-t.h-full.border-r-2(v-show="isActive(i)")
</template>

<script>
export default {
  name: 'ListItems',
  props: ['items', 'disabled'],
  data () {
    return {
      active: []
    }
  },
  methods: {
    itemClasses (i) {
      return {
        'py-10': this.isActive(i),
        'overflow-hidden py-6': !this.isActive(i),
        'border-b': i === this.items.length - 1
      }
    },
    isActive (i) {
      return this.active.includes(i)
    },
    toggleItem (i) {
      // console.log(i, this.active)
      if (!this.isActive(i)) return this.active.push(i)
      // deactivate
      let arr = this.active
      const pos = arr.indexOf(i)
      if (pos > -1) this.active = [ ...arr.slice(0, pos), ...arr.slice(pos + 1, arr.length)]
    }
  }
}
</script>

<style>
</style>
