<script>
import { store } from '../../store/index'
import CustomInput from '../CustomInput/CustomInput.vue'
import PlusIcon from '../icons/PlusIcon.vue'
import ChildRow from '../ChildRow/ChildRow.vue'
export default {
  components: {
    CustomInput,
    PlusIcon,
    ChildRow
  },
  data: function () {
    return {
      arr: [],
      person: {
        name: '',
        age: null,
        childs: []
      },
      id: null
    }
  },
  methods: {
    add() {
      let ind = this.arr.length
      this.id = Date.now()
      if (ind < 5) {
        this.arr.push([
          {
            label: 'Имя',
            name: `name`
          },
          {
            label: 'Возраст',
            name: `age`
          }
        ])
        console.log(this.arr)
      }
    },
    onSubmit(e) {
      e.preventDefault()
      console.log('person', this.person)
      console.log('onSubmit')
    },
    onUpdateName(val) {
      console.log('onUpdate', val)
      this.person.name = val.value
    },
    onUpdateAge(val) {
      console.log('onUpdateAge', val)
      this.person.age = val.value
    },
    onUpdateChilds(val) {
      //   console.log('onUpdateChilds', val)
      let res = []
      const ind = this.person.childs.filter((item) => item.id == val.id)
      if (!ind.length) {
        res.push(val)
        this.person.childs = [...res]
        console.log('childs', this.person.childs)
      } else {
        ind[0].push(val)
        console.log('res 2', this.person.childs)
      }
      //   this.person.childs.push(val)
      //   console.log('childs', this.person.childs)
    }
  }
}
</script>

<template>
  <form class="form" @submit="onSubmit">
    <fieldset class="fieldset">
      <legend class="title">Персональные данные</legend>
      <CustomInput label="Имя" name="name" @update-val="onUpdateName" />
      <CustomInput label="Возраст" name="age" @update-val="onUpdateAge" />
    </fieldset>
    <fieldset class="fieldset">
      <div class="head">
        <legend class="title">Дети (макс. 5)</legend>
        <div class="add" @click="add" v-if="arr.length < 5">
          <PlusIcon /><span>Добавить ребенка</span>
        </div>
      </div>
      <ChildRow
        v-for="item in arr"
        :key="item.label"
        :elems="item"
        :id="id"
        @update-childs="onUpdateChilds"
      />
    </fieldset>
    <button class="save" @submit="onSubmit">Сохранить</button>
  </form>
</template>

<style scoped lang="scss">
@import '../../assets/styles/vars.scss';
.fieldset {
  border: none;
}

legend {
  margin: 0 0 $spacing-s 0;
}

.add {
  padding: $spacing-xs $spacing-s;
  border: 2px solid $color-primary;
  border-radius: $radius-xl;
  display: flex;
  align-items: center;
  color: $color-primary;
  gap: 4px;
  background: $white;
  cursor: pointer;
  transition: opacity 0.3s ease;

  &:hover {
    opacity: 0.8;
  }
}

.head {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 0 0 $spacing-xs 0;
}

.save {
  padding: $spacing-xs $spacing-s;
  background: $color-primary;
  color: $white;
  border-radius: $radius-xl;
  border: none;
  transition: opacity 0.3s ease;
  cursor: pointer;

  &:hover {
    opacity: 0.7;
  }
}
</style>
