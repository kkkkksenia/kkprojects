<template>
    <div class="settings" v-if="settingsShow">
        <div class="settings--title">
            <span class="name">Настройки</span>
            <button @click="save" class="btn btn--default">
                Сохранить
            </button>
            <span @click="close" class="settings--close">x</span>
        </div>

        <div class="settings--data">
            <div :key="index" class="settings--item" v-for="(setting, index) in settingsData">
                <label :for="'value' + setting.id"> {{ setting.name }} </label>
                <input :id="'value' + setting.id" :maxlength="setting.size" type="text"
                       v-if="setting.fieldType === 'input'" v-model="setting.value">
                <select v-else-if="setting.fieldType === 'select'" v-model="setting.value">
                    <option :key="key" v-bind:value="option.text" v-for="(option, key) in setting.options">
                        {{ option.text }}
                    </option>
                </select>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'settingsComponent',
  props: {
    settingsData: {
      default: []
    },
    executeCallback: {
      type: Function,
      required: true
    },
    closeCallback: {
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
    save () {
      this.executeCallback(this.settingsData)
    },
    close () {
      this.closeCallback('closeSettings')
    }
  }
}
</script>
