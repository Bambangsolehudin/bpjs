<template>
  <div class="EmployeHistory">
    <!-- Employement History -->
    <div class="row mb-5">
      <div class="col-12">
        <h5><b>Employement History</b></h5>
        <p class="text-secondary">Show your relevant experience (last 10 years). use bullet points to note your achievments. if possible - use numbers/facts (Achieved X, measured by Y. by doing Z). </p>
      </div>
      <div class="col-12">
        <template v-for="(data, index) of datas">
        <div class="card my-2" :key="index">
          <div class="pt-4 px-4 d-flex justify-content-between">
            <h6>
              {{ data.title }}
              <p class="text-muted mt-2">{{ data.start_date }} - {{ data.end_date }}</p>
            </h6>
            <a href="" class="text-danger" @click.prevent="deleteData(index)">X</a>
          </div>
        </div>
        </template>

        <a v-if="!colapse_on" class="" data-toggle="collapse" href="#employee" role="button" aria-expanded="false" aria-controls="employee" @click.prevent="changeColapseOn">
          + Add one more employment
        </a>
        <div v-if="colapse_on" class="collapse" id="employee">
          <div class="card card-body">
            <div class="row">
              <div class="col-12 my-4">
                (Not Specified)
              </div>
              <div class="col-6">
              <div class="form-group">
                <label for="job_title">Job Title</label>
                <input v-model="form_data.job"  type="text" class="form-control" id="job_title" >
              </div>
            </div> 
            <div class="col-6">
              <div class="form-group">
                <label for="employer">Employer</label>
                <input v-model="form_data.employer"  type="text" class="form-control" id="employer" >
              </div>
            </div> 
            <div class="col-6">
              <div class="form-group">
                <label for="start_date">Start and End date</label>
                <div class="d-flex">
                  <input v-model="form_data.start_date"  type="date" class="form-control mr-2" id="start_date" >
                  <input v-model="form_data.end_date"  type="date" class="form-control" id="end_date" >
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
      this.colapse_on = true
    },
    addData() {
      this.colapse_on = false
      let data = {
        title: this.form_data.job,
        employer: this.form_data.employer,
        start_date: this.form_data.start_date,
        end_date: this.form_data.end_date,
        city: this.form_data.city,
        desc : this.content
      }
      this.datas.push(data)

      this.$emit("data", this.datas)

      this.form_data = {}
      this.content = "<h1>Some initial content</h1>"
      this.disabled_form = true
    },
    deleteData(i){
      this.datas.splice(i, 1)
      this.$emit("data", this.datas)
    }
  },
  data() {
    return {
      colapse_on: false,
      disabled_form: false,
      content: "<h1>Some initial content</h1>",
      form_data: {},
      datas: [],
    };
  }

}
</script>

<style>

</style>