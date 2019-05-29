<template>
    <div class="wrapper">
        <div class="blocks">
            <div :class="block.name" :key="key"
                 class="block"
                 v-for="(block, key) in blocks">
                <button class="btn btn--default" @click="selectBlock(key)">
                    Настройки
                </button>
                <textarea v-model="block.text"></textarea>
            </div>

            <div class="settings" v-if="settingsShow">
                <div class="settings--title">
                    <span class="name">Настройки</span>
                    <button class="btn btn--default" @click="saveSettings">
                        Сохранить
                    </button>
                    <span class="settings--close" @click="settingsShow = false">x</span>
                </div>
                <div class="settings--data">
                    <div class="settings--item" v-for="(setting, index) in blocks[selected].settings" :key="index">
                        <label :for="'value' + setting.id"> {{ setting.name }} </label>
                        <input type="text" v-if="setting.fieldType === 'input'" v-model="setting.value" :maxlength="setting.size" :id="'value' + setting.id">
                        <select v-model="setting.value" v-else-if="setting.fieldType === 'select'">
                            <option v-for="(option, key) in setting.options" v-bind:value="option.value" :key="key">
                                {{ option.text }}
                            </option>
                        </select>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  components: {
    axios
  },
  data () {
    return {
      blocks: [
        {
          'id': 1,
          'name': 'yellow',
          'text': 'Сомнение рефлектирует естественный закон исключённого третьего.. Сомнение рефлектирует естественный закон исключённого третьего.. Согласно мнению известных философов, дедуктивный метод естественно порождает и обеспечивает мир, tertium nоn datur. Дедуктивный метод решительно представляет собой бабувизм.',
          'settings': [
            {
              'id': 11,
              'name': 'Ширина',
              'stringType': 'int',
              'fieldType': 'input',
              'value': '600',
              'size': 4
            },
            {
              'id': 12,
              'name': 'Высота',
              'stringType': 'int',
              'fieldType': 'input',
              'value': '500',
              'size': 6
            }
          ]
        },
        {
          'id': 2,
          'name': 'pink',
          'text': 'Структурализм абстрактен. Дедуктивный метод решительно представляет собой бабувизм. Апостериори, гравитационный парадокс амбивалентно понимает под собой интеллигибельный знак. Дискретность амбивалентно транспонирует гравитационный парадокс.',
          'settings': [
            {
              'id': 22,
              'name': 'Скрытое',
              'fieldType': 'select',
              'options': [
                {'text': 'Да', 'value': 1},
                {'text': 'Нет', 'value': 2}
              ],
              'value': 1
            }
          ]
        }
      ],
      selected: 0,
      settingsShow: false,
      editText: false
    }
  },
  methods: {
    selectBlock (key) {
      this.selected = key
      this.settingsShow = !this.settingsShow
    },
    saveSettings () {
      axios.post('/api/save', JSON.stringify(this.blocks))
        .then(res => {
          setTimeout(() => {
            this.settingsShow = false
          }, 300)
        })
        .catch(err => {
          console.log(err)
        })
    }
  }
}
</script>

<style lang="scss">
    @import '../../static/sass/app.scss';
    @import '../../static/sass/layout/base';

</style>
