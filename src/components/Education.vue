<template>
  <div class="EmployeHistory">
     <!-- Employement History -->
     <div class="row mb-5">
      <div class="col-12">
        <h5><b>Education</b></h5>
        <p class="text-secondary">A varried education youre resume sums up the value that your learnings and background will bring ti job</p>
      </div>
      <div class="col-12">
        <template v-for="(data, index) of datas">
        <div class="card my-2" :key="index">
          <div class="pt-4 px-4 d-flex justify-content-between">
            <h6>
              {{ data.school }}
              <p class="text-muted mt-2">{{ moment(data.start_date).format('MMMM, YYYY')  }} - {{ moment(data.end_date).format('MMMM, YYYY') }}</p>
            </h6>
            <a href="" class="text-danger" @click.prevent="deleteData(index)">X</a>
          </div>
          </div>
        </template>

        <a v-if="!colapse_on" class="" data-toggle="collapse" href="#education" role="button" aria-expanded="false" aria-controls="education" @click.prevent="changeColapseOn">
          + Add one more education
        </a>
        <div v-if="colapse_on" class="collapse" id="education">
          <div class="card card-body">
            <div class="row">
              <div class="col-12">
                (Not Specified)
              </div>
              <div class="col-6">
              <div class="form-group">
                <label for="job_title">School</label>
                <input v-model="form_data.school"  type="text" class="form-control" id="job_title" >
              </div>
            </div> 
            <div class="col-6">
              <div class="form-group">
                <label for="employer">Degree</label>
                <input v-model="form_data.degree"  type="text" class="form-control" id="employer" >
              </div>
            </div> 
            <div class="col-6">
              <div class="form-group">
                <label for="start_date">Start and End date</label>
                <div class="d-flex">
                  <input v-model="form_data.start_date"  type="month" class="form-control mr-2" id="start_date" >
                  <input v-model="form_data.end_date"  type="month" class="form-control" id="end_date" >
                </div>
              </div>
            </div> 
            <div class="col-6">
              <div class="form-group">
                <label for="city">City</label>
                <input v-model="form_data.city"  type="text" class="form-control" id="city" >
              </div>
            </div> 
            <div class="col-12">
              <vue-editor v-model="content"></vue-editor>
            </div>
            <div class="col-12 my-2">
              <button class="btn btn-danger mr-2" @click.prevent="colapse_on = false">Cancel</button>
              <button class="btn btn-primary" @click.prevent="addData">Add Data</button>
            </div>
            </div>
          </div>
        </div>
        </div>
      </div>
  </div>
</template>

<script>
import { VueEditor } from "vue2-editor";

export default {
   components: {
    VueEditor,
  },
  methods:{
    changeColapseOn() {
      this.colapse_on = !this.colapse_on
    },
    addData() {
      let data = {
        school: this.form_data.school,
        degree: this.form_data.degree,
        start_date: this.form_data.start_date,
        end_date: this.form_data.end_date,
        city: this.form_data.city,
        desc : this.content
      }
      this.datas.push(data)

      this.$emit("data", this.datas)

      this.form_data = {}
      this.content = "<h1>Some initial content</h1>"
      this.colapse_on = !this.colapse_on
    },
    
    deleteData(i){
      this.datas.splice(i, 1)
      this.$emit("data", this.datas)
    },
  },
  data() {
    return {
      colapse_on: false,
      content: "<h1>Some initial content</h1>",
      form_data: {},
      datas: [
        // {
        //   school: "Universitas Gunadarma",
        //   degree: "Pt Astra",
        //   start_date: "Jan 2021",
        //   end_date: "jul 2022",
        //   city: "Jakarta",
        //   desc : "Hai"
        // }
      ],
    };
  }

}
</script>

<style>

</style>