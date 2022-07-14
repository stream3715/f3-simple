<template>
  <v-row></v-row>
</template>

<script>
export default {
  name: 'ClientPage',
  props: {
    userName: {
      type: String,
      default: '',
    },
    roomId: {
      type: String,
      default: '',
    },
  },
  head: {
    title: '部屋' + this.props.roomId,
  },
}
</script>
