<template>
  <article class="relative">
    <div
      class="flex border-b border-charcoal items-center jusitfy-between py-8"
    >
      <NuxtLink
        :to="`/%E2%98%95/${post.id}`"
        class="flex-grow snippet-title font-underground"
        :style="{ margin: '0' }"
      >
        {{ post.metadata.name }}
      </NuxtLink>
      <time class="text-ash" :datetime="_timestamp.toISOString()">
        {{ _clock }}
      </time>
    </div>

    <img :src="post.metadata.image" alt="" class="cover" />
    <section class="content">
      {{ post.metadata.description }}
    </section>
  </article>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'Snippet',
  props: {
    post: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {}
  },
  computed: {
    _timestamp: function () {
      return new Date(this.post.createdAt)
    },
    _clock: function () {
      const timestamp = new Date(this.post.createdAt)
      return `
      ${(timestamp.getMonth() + 1).toLocaleString(undefined, {
        minimumIntegerDigits: 2,
      })}.${timestamp
        .getDate()
        .toLocaleString(undefined, { minimumIntegerDigits: 2 })}.${(
        timestamp.getFullYear() % 100
      ).toLocaleString(undefined, {
        minimumIntegerDigits: 2,
      })}
      `
    },
  },
})
</script>

<style lang="css" scoped></style>
