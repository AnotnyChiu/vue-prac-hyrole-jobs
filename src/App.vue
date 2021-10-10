<template>
  <div class="app">
    <header>
      <div class="title">
        <h1>Hyrule Jobs</h1>
      </div>
      <div class="order">
        <button @click="handleClick('title')">order by title</button>
        <button @click="handleClick('salary')">order by salary</button>
        <button @click="handleClick('location')">order by location</button>
      </div>
    </header>
    <JobList :jobs="jobs" :order="order"/>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import Job from './types/job'
import OrderTerm from './types/orderTerm'
// notice! when using ts, have to say .vue extension while import
import JobList from './components/jobList.vue'

// typescript way of defining a component
export default defineComponent({
  name: 'App',
  components: { JobList },
  setup() {
    
    const jobs = ref<Job[]>([
      { title: 'farm worker', location: 'lon lon ranch', salary: 30000, id: '1' },
      { title: 'quarryman', location: 'death mountain', salary: 40000, id: '2' },
      { title: 'flute player', location: 'the lost woods', salary: 35000, id: '3' },
      { title: 'fisherman', location: 'lake hylia', salary: 21000, id: '4' },
      { title: 'prison guard', location: 'gerudo valley', salary: 32000, id: '5' }
    ])

    const order = ref<OrderTerm>('title')

    // use "type" (enum) to limit the options! >> see orderTerm.ts
    const handleClick = (term: OrderTerm) => {
      order.value = term      
    }



    return {
      //#region : entities
      jobs, order,
      //#endregion

      //#region : functions
      handleClick
      //#endregion 
    }
  },
});
</script>

<style>
  header {
    text-align: center;
  }
  header .order {
    margin-top: 20px;
  }
  button {
    margin: 0 10px;
    color: #1195c9;
    border: 3px solid #1195c9;
    background: #d5f0ff;
    padding: 8px 16px;
    border-radius: 4px;
    cursor: pointer;
    font-weight: bold;
  }
</style>
