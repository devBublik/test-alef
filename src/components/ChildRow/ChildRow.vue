<script>
import CustomInput from '../CustomInput/CustomInput.vue'

export default {
  components: {
    CustomInput
  },
  data() {
    return {
      child: []
    }
  },
  props: {
    elems: {
      type: Object,
      default: () => {}
    },
    id: {
      type: Number,
      default: () => 0
    }
  },
  emits: ['updateChilds'],
  methods: {
    onUpdateVal(val) {
      const name = val['value']
      const field = val['name']
      console.log('this.child', this.child)

      let type = this.checkType(field)

      for (let i = 0; i < this.child.length; i++) {
        console.log('list', this.child[i])
      }

      if (this.child.length == 0) {
        this.child.push({ id: this.id, [type]: name })
        console.log(this.child)
      } else {
        const isHere = this.child.filter((item) => item.id === val.id)
        if (isHere) {
          console.log('isHere', isHere)
          isHere[type] = name
        }
      }

      console.log('this.child', this.child)

      //   console.log(ind)

      //   if (!isInList.length) {
      //     this.child.push({ id: this.id, [type]: name })
      //     console.log('res', this.child)
      //   } else {
      //     isInList[0][type] = name
      //     console.log(isInList[0])
      //     console.log('res 2', this.child)
      //   }

      //   console.log('in row', this.child)
      this.$emit('updateChilds', this.child)
    },
    checkType(type) {
      if (type === 'name') {
        return 'name'
      } else {
        return 'age'
      }
    }
  }
}
</script>

<template>
  <div class="row">
    <CustomInput
      v-for="elem in elems"
      :key="elem.name"
      :label="elem.label"
      :name="elem.name"
      @update-val="onUpdateVal"
    />
    <button class="delete">Удалить</button>
  </div>
</template>
<style lang="scss" scoped>
@import '../../assets/styles/vars.scss';

.row {
  display: flex;
  align-items: center;
  gap: 18px;
}

.delete {
  background: $white;
  color: $color-primary;
  color: var(--colors-primary, #01a7fd);
  font: normal 400 14px / 171% Montserrat;
  border: none;
}
</style>
