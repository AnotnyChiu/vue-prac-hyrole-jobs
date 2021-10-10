<template>
    <div class="job-list">
        <p>Ordered by {{ order }}</p>
        <!-- doing some animation -->
        <transition-group name="list" tag="ul">
            <li v-for="job in orderedJobs" :key="job.id">
                <h2>{{ job.title }} in {{ job.location }}</h2>
                <div class="salary">
                    <p>{{ job.salary }} rupees</p>
                </div>
                <div class="descriprion">
                    no description yet
                </div>
            </li>
        </transition-group>
    </div>
</template>

<script lang="ts">
import OrderTerm from '@/types/orderTerm'
import { computed, defineComponent, PropType } from 'vue'
import Job from '../types/job'

export default defineComponent({
    props: {
        'jobs': {
            required: true,
            // here is a runtime check by vue using js
            // thus can't use ts syntax here
            // have to use "PropType" from vue
            type: Array as PropType<Job[]>
        },
        'order': {
            required: true,
            type: String as PropType<OrderTerm>
        }
    },
    setup(props) {
        const orderedJobs = computed(() => {
            // notice do not change the original array
            // use spread
            return [...props.jobs].sort( (j1: Job, j2: Job): number => {
                return j1[props.order] > j2[props.order] ? 1 : -1
            })
        })

        return {
            orderedJobs
        }
    }
})
</script>

<style scoped>
  .job-list {
    max-width: 960px;
    margin: 40px auto;
  }
  .job-list ul {
    padding: 0;
  }
  .job-list li {
    list-style-type: none;
    background: white;
    padding: 16px;
    margin: 16px 0;
    border-radius: 4px;
  }
  .job-list h2 {
    margin: 0 0 10px;
    text-transform: capitalize;
  }
  .salary {
    display: flex;
  }
  .salary img {
    width: 30px;
  }
  .salary p {
    color: #17bf66;
    font-weight: bold;
    margin: 10px 4px;
  }
  .list-move{
      transition: all 1s;
  }
</style>
