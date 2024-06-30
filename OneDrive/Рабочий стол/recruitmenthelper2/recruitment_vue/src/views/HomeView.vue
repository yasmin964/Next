<template>
  <div class="appproc">
    <div class="logo">
      <h2 class="logo_p1">Recruitment</h2>
      <img class="logo_p2" src="@/img/iu_logo_green 1.svg" alt="university logo ">
    </div>
    <h2 class="title" style="color: white;">Applications</h2>

  <div class="tables">
    <div class="vac">
      <VacancyBox 
        v-for="vacancy in latestVacancies" 
        :key="vacancy.id" 
        :vacancy="vacancy" 
        class="column is-4"
      />
    </div>
    <!-- <div class="vacInPr">
      <VacancyInPr
        v-for="vacancy in VacanciesInProcessing" 
        :key="vacancy.id" 
        :vacancy="vacancy" 
        class="column is-4"
      />
    </div> -->
  </div>
   
  </div>
  
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import axios from 'axios';
import VacancyBox from '@/components/VacancyBox.vue'; // Импорт дочернего компонента

interface Vacancy {
  id: number;
  name: string;
  comment: string;
  // добавьте другие поля, если необходимо
}

// OPTIONS API
export default defineComponent({
  name: 'HomeView',
  components: {
    VacancyBox // Регистрация дочернего компонента
  },
  data() {
    return {
      latestVacancies: [] as Vacancy[],// Начальное состояние для экземпляра компонента 
      VacanciesInProcessing: [] as Vacancy[]
    }
  },
  mounted() {
    this.getLatestVacancies();
    // this.getVacanciesInPr();
    document.title = 'Home | Vacancies';
  },
  methods: {// Здесь лучше не использовать функции со стрелками, у них не будет доступа через this
    async getLatestVacancies() {
      try {
        const response = await axios.get('main/');
        this.latestVacancies = response.data as Vacancy[];
      } catch (error) {
        console.error(error);
      }
    },
    // async getVacanciesInPr(){
    //   try {
    //     const response = await axios.get('main/vacInPr');
    //     this.VacanciesInProcessing = response.data as Vacancy[];
    //   } catch (error) {
    //     console.error(error);
    //   }
    //}
  }
});
</script>

<style scoped>
.appproc {
  background-color: #236F00;
  width: 1440px;
  height: 1024px;
  
}
.logo_p1{
  font-family: Lato;
  font-size: 27px;
  font-weight: 900;
  line-height: 32px;
  color:#FFFFFF;
  margin-left: 91px;
    margin-right: -79px;
    padding-top: 60px;
 
}
.logo{
  display: flex;
    flex-direction: row;
    justify-content: flex-start;
}
.title{
  padding-left: 150px;
  padding-top: 220px;
  font-family: League Spartan;
  font-size: 40px;
  font-weight: 500;
  line-height: 37px;
  padding: 49px;
}
.tables{
  display: flex;
  justify-content: space-around;
}
.vac{
  background-color: white;
  width: 536px;
  height: 464px;
  display: flex;
  flex-direction: column;
  align-items: center;
  overflow-y: scroll;
  margin-left: 190px;
  padding-top: 31px;
  padding-bottom: 31px;
  border-radius: 3px;
}
.vacInPr{
  background-color: white;
  width: 475px;
  height: 343px;
  display: flex;
  flex-direction: column;
  align-items: center;
  overflow-y: scroll;
  border-radius: 3px;
  padding-top: 31px;
  padding-bottom: 31px;
  margin-right: 153px;
  margin-left: 120px;
}

</style>
