<template lang="pug">
.notification(:class="c")
  .notification-title {{ value.title }}
  .notification-body {{ value.body }}
</template>

<script>
import {mapMutations} from "vuex";

export default {
  name: "Notification",
  data() {
    return {
      c: {}
    }
  },
  props: {
    value: {
      type: Object,
      required: true
    }
  },
  methods: {
    ...mapMutations({
      delete: "notification/deleteNotification"
    })
  },
  mounted() {
    setTimeout(() => {
      this.delete(this.value)
    }, this.value.time * 1000)
    if (this.value.type) {
      this.c[this.value.type] = true;
    }
  }
}
</script>

<style scoped lang="stylus">
.info
  background-color #9cebff !important
  color #1c1c1c
.danger
  background-color #ff7185 !important
  color #ffffff

.notification
  margin 5px
  min-height 20px
  padding 10px
  border-radius 5px
  background-color #e0e0e0
  .notification-title
    font-weight bold
    font-size 15px
  .notification-body
    font-size 13px

</style>
