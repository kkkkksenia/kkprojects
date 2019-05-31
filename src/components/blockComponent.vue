<template>
    <div :class="blockData.name" class="block">
        <button class="btn btn--default" @click="select">
            Настройки
        </button>
        <textarea v-model="blockData.text"></textarea>
    </div>
</template>

<script>
export default {
  name: 'blockComponent',
  props: {
    blockData: {
      default: []
    },
    executeCallback: {
      type: Function,
      required: true
    }
  },
  data () {
    return {
      settingsShow: true
    }
  },
  methods: {
    select () {
      this.executeCallback(this.blockData.id)
    }
  }
}
</script>
