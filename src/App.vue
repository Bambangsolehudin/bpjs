<template>
  <div class="Home container">
    <div v-if="validationParent" class="alert alert-danger my-2" role="alert">
      Terdapat data yang belum terisi, silahkan isi terlebih dahulu !
    </div>
    <PersonalDetail @datas="detail" />

    <ProfesionalSummary @data="getDataPS" />
   
   <EmployeHistory @data="getDataEH" />

   <Education @data="getEducation" />

   <Skills @data="getSkill" />

   <div class="row">
    <div class="col-12 d-flex flex-row-reverse my-4">
      <button class="btn btn-primary" @click="saveAll">Simpan Semua</button>
    </div>
   </div>

  </div>
</template>

<script>
import PersonalDetail from "../src/components/PersonalDetail.vue"
import ProfesionalSummary from "../src/components/ProfesionalSummary.vue"
import EmployeHistory from "../src/components/EmployeHistory.vue"
import Education from "../src/components/Education.vue"
import Skills from '../src/components/Skills.vue'
import $ from "jquery";


export default {
  components: {
    PersonalDetail,
    ProfesionalSummary,
    EmployeHistory,
    Education,
    Skills,
  },
  methods : {
    detail(e){
      this.personalDetail = e
      console.log('personal detail', this.personalDetail);
    },
    getDataPS(e){
      this.profesionalSummary = e
      console.log('profesional summary', this.profesionalSummary);
    },
    getDataEH(el){
      this.EmployeHistory = el
      console.log('employment history', this.EmployeHistory);
    },
    getEducation(e){
      this.Education = e
      console.log('education', this.Education);
    },
    getSkill(e){
      this.skills = e
      console.log('skills', this.skills);
    },
    saveAll(){
      if(this.personalDetail == null || this.profesionalSummary == null || this.EmployeHistory == null || this.Education == null || this.skills == null){
        $('html, body').animate({
            scrollTop: 0
        }, 1000); 
        this.validationParent = true
      }else{
        this.validationParent = false
        console.log("All Data", {personal_detail: this.personalDetail, prefesional_sumary: this.profesionalSummary, employe_history: this.EmployeHistory, education: this.Education, skills: this.skills, });
      }
    },
  },

  data() {
    return {
      validationParent: false,
      personalDetail : null,
      profesionalSummary:null,
      EmployeHistory: null,
      Education: null,
      skills: null,

    };
  }
}
</script>

<style>

/* .btn-bg-skill{
  background: rgb(221, 216, 216);
} */



</style>