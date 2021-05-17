<template>
  <h1>Home</h1>
  <p>
    <img src="../assets/logo.png" alt="logo" />
  </p>
  <button @click="state.count++">count is: {{ state.count }}</button>
  <Foo />
</template>

<script setup>
import { reactive, defineAsyncComponent } from 'vue'
let hydrate = () => {}
const promise = import.meta.env.SSR ? Promise.resolve() : new Promise((res) => { hydrate=res})
const Foo = defineAsyncComponent({
  loader: () => promise.then(() => import('../components/Foo')).then((mod) => mod.Foo),
  suspensible: false
})
if (!import.meta.env.SSR) {
  // window.setTimeout(hydrate, 1000)
}
const state = reactive({ count: 0 })
</script>

<style scoped>
h1,
a {
  color: green;
}
</style>
