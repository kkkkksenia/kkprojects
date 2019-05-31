<template>
    <div class="wrapper">
        <div class="blocks">
            <block-component v-for="(block, key) in blocks" :key="key" :blockData="block" :execute-callback="selectBlock"></block-component>
        </div>
        <settings-component :settingsData="selectedBlock.settings" :execute-callback="saveSettings" :close-callback="closeSettings" v-if="settingsShow"></settings-component>
    </div>
</template>

<script>
import axios from 'axios'
import SettingsComponent from './settingsComponent'
import BlockComponent from './blockComponent'
export default {
  name: 'mainComponent',
  props: {
    msg: String
  },
  components: {
    BlockComponent,
    SettingsComponent,
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
              'value': 'Да'
            }
          ]
        }
      ],
      selected: 1,
      settingsShow: false,
      editText: false
    }
  },
  computed: {
    selectedBlock () {
      return this.blocks.find(item => item.id === this.selected)
    }
  },
  methods: {
    selectBlock (id) {
      if (id === this.selected || !this.settingsShow) { this.settingsShow = !this.settingsShow }
      this.selected = id
    },
    saveSettings (settings) {
      this.selectedBlock.settings = settings
      axios.post('/api/save', JSON.stringify(this.blocks))
        .then(res => {
          setTimeout(() => {
            this.settingsShow = false
          }, 300)
        })
        .catch(err => {
          console.log(err)
        })
    },
    closeSettings () {
      this.settingsShow = false
    }
  }
}
</script>

<style lang="scss">
    @import '../../static/sass/app.scss';
    @import '../../static/sass/layout/base';

</style>
