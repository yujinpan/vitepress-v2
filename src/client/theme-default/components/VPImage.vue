<script lang="ts">
import type { DefaultTheme } from 'vitepress/theme'
import { withBase } from 'vitepress'
import { defineComponent, type PropType } from 'vue';

export default defineComponent({
  inheritAttrs: false,
  props: {
    image: {} as PropType<DefaultTheme.ThemeableImage>,
    alt: String as PropType<string>
  },
  setup() {
    return {
      withBase
    }
  }
})
</script>

<template>
  <span v-if="image">
    <img
      v-if="typeof image === 'string' || 'src' in image"
      class="VPImage"
      v-bind="typeof image === 'string' ? $attrs : { ...image, ...$attrs }"
      :src="withBase(typeof image === 'string' ? image : image.src)"
      :alt="alt ?? (typeof image === 'string' ? '' : image.alt || '')"
    />
    <template v-else>
      <VPImage
        class="dark"
        :image="image.dark"
        :alt="image.alt"
        v-bind="$attrs"
      />
      <VPImage
        class="light"
        :image="image.light"
        :alt="image.alt"
        v-bind="$attrs"
      />
    </template>
  </span>
</template>

<style scoped>
html:not(.dark) .VPImage.dark {
  display: none;
}
.dark .VPImage.light {
  display: none;
}
</style>
