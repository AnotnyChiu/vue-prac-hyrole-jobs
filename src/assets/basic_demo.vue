<template>
  <div class="app">
    <!-- hello, hyrule
    <p>{{ name }} - {{ age }}</p>
    <input type="text" v-model="inputName">
    <button @click="changeName(inputName)"> change name </button>
    <br>
    <input type="text" v-model="inputAge">
    <button @click="changeAge(inputAge)"> change age </button> -->
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, toRefs, ref } from 'vue';

// typescript way of defining a component
export default defineComponent({
  name: 'App',
  components: {},
  setup() {
    const state = reactive({
      name: 'Link' as string,
      age: 25 as number | string
    })

    // demo on ref (use generic arguments)
    const birthYear = ref<number| string>(1996)

    const changeName = (name: string): void => {
      state.name = name
    }

    const changeAge = (age: number | string): void => {
      state.age = age
    }

    return {
      // #region : entity
      /*
        note: rather than return the whole state, try use spread with toRefs

        Converts a reactive object to a plain object
        where each property of the resulting object is a ref
        pointing to the corresponding property of the original object.
      */
      ...toRefs(state),
      birthYear,
      // #endregion

      // #region : function
      changeName,
      changeAge,
      // #endregion
    }
  },
});
</script>

<style>

</style>
