<template>
    <div class="box_vacancy">
    <!-- <a :href="`../recruitmenthelper/recruitmenthelper/web/SWP/vacancies/${vacancy.id}`">
        <div class="vac_data">
            <p>{{ vacancy.comment }}</p>
        </div>
    </a> -->
    <RouterLink :to="`/vacancies/${vacancy.id}/`">
      <div class="vac_data">
            <p>{{ vacancy.comment }}</p>
        </div>
      </RouterLink>
    </div>
  </template>
  
  <script lang="ts">
  import { defineComponent, PropType } from 'vue';
  import {RouterLink} from 'vue-router';
  
  interface Vacancy {
    id: number;
    name: string;
    comment: string;
    // добавьте другие поля, если необходимо
  }
  
  export default defineComponent({
    name: 'VacancyBox',
    // это способ передачи данных от родительского компонента к дочернему компоненту в Vue.js.
    props: {
      vacancy: {
        type: Object as PropType<Vacancy>,
        required: true
      }
    },
    components:{
      RouterLink
    }
  });
  </script>
  
  <style scoped>
  .box_vacancy {
    padding: 0px;
    border: 1px solid #494949;
    margin-bottom: 20px;
    background-color: #494949;
    border-radius: 7px;
    width:470px;
    display: flex;
    justify-content: center;
    
  }
  
  .vac_data {
    color: white;
    font-family: Lato;
    font-size: 18px;
    font-weight: 400;
    line-height: 22px;
    
  }
  </style>
  