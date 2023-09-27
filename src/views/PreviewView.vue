<script>
import {mapState, useStore} from "vuex";
import {computed} from "vue";
export default {
  computed: {
    ...mapState({
      name: state => state.name,
      age: state => state.age,
      childs: state => state.childs
    })
  }

}


</script>

<template>
  <div class="preview">
    <div class="container container--s">
      <div v-if="!name || !age">
        Пожалуйста, заполните даннные в форме
      </div>
      <div v-else>
        <div class="title">
          Персональные данные
        </div>
        <div class="preview__val">{{name}}, {{age}} лет</div>
        <div class="preview_sub">Дети</div>
        <div
            v-if="childs.length"
            v-for="{child, ind} in childs"
            :key="child.name + ind"
        >
          {{child.name}}, {{child.age}}
        </div>
      </div>
    </div>
  </div>

</template>
<style lang="scss">
@import '../assets/styles/vars.scss';
.preview {
  padding: $spacing-l 0;
  text-align: left;
}
</style>
