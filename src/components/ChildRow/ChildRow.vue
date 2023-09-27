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
    },
    id: {
      type: Number,
    }
  },
  emits: ['updateChilds', 'deleteChild'],
  methods: {
    onUpdateVal(val) {
      const name = val['value']
      const field = val['name']
      let type = this.checkType(field)

      const isInList = this.child.filter(item => item.id === this.id)
      const res = { id: this.id, [type]: name }
      if (!isInList.length) {
        this.child.push(res)
      } else {
        isInList[0][type] = name
      }
      console.log('child',this.child)
      this.$emit('updateChilds', res)
    },
    checkType(type) {
      if (type === 'name') {
        return 'name'
      } else {
        return 'age'
      }
    },
    onDelete() {
      console.log('delete', this.child)
      this.$emit('deleteChild', this.child)
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
    <button class="delete" @click="onDelete">Удалить</button>
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
