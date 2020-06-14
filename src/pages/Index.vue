<template>
  <Layout>
    <g-link to="/about">About</g-link>
    <ul>
      <li v-for="item in list" :key="item.id">{{ item.title }}</li>
    </ul>
  </Layout>
</template>

<static-query>
query {
  metadata {
    buildTime
  }
}
</static-query>

<script>
export default {
  computed: {
    listData() {
      return [
        { id: 1, title: 'Item 1', date: new Date('2020-01-01 00:00:00') },
        { id: 2, title: 'Item 2', date: new Date('2020-01-05 00:00:00') },
        // Set it to expire 2 minutes after the build
        // This is to simulate what would happen if an item is added at a later date to the list
        { id: 3, title: 'Item 3', date: new Date(Number(this.$static.metadata.buildTime) + 2 * 60 * 1000) },
      ]
    },

    list() {
      return this.listData.filter(d => d.date < Date.now())
    }
  },

  metaInfo: {
    title: 'Home'
  }
}
</script>

<style scoped>
</style>
