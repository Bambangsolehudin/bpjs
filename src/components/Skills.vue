<template>
  <div class="Skills">
    
    <div class="row mb-5">
      <div class="col-12">
        <h5><b>Skills</b></h5>
        <p class="text-secondary">Choose 5 of the most impotant skills to show your talents! Make sure they match the keywords of the job listing if applying via online system</p>
      </div>
      
      <!-- Switch -->
      <div class="col-12">
        <div class="custom-control custom-switch">
          <input v-model="switch_button" type="checkbox" class="custom-control-input" id="customSwitch1" >
          <label class="custom-control-label text-dark" for="customSwitch1">Dont show experience level</label>
        </div>
      </div>

      <!-- Recomendation Skills -->
      <div class="col-12 my-4">
        <template v-for="(skill, index) of skills" >
          <button v-show="skill.button_of == false" data-toggle="collapse" class="btn btn-bg-skill mr-3 my-2" :disabled="collapse_on" :key="index" @click="changeButton(index)"> + {{ skill.name }}</button>
        </template>
      </div>
    
      <!-- Skill User-->
      <template v-for="(data, index) of skillsUser">
      <div v-if="switch_button == false" class="col-12 my-2" :key="index">
        <div class="card">
          <div class="pt-4 px-4 d-flex justify-content-between" data-toggle="collapse" href="#collapseExample" role="button" aria-expanded="false" aria-controls="collapseExample">
            <div class="note">
              <h6>{{ data.skill }}</h6>
              <p class="text-secondary">
                <span v-if="data.level == 1"> Beginner </span>
                <span v-if="data.level == 2"> Skilful </span>
                <span v-if="data.level == 3"> Experienced </span>
                <span v-if="data.level == 4"> Expert </span>
              </p>
            </div>
            <a href="" class="text-danger" @click.prevent="deleteData(index)">X</a>
          </div>
        </div>
      </div>
      </template>
     
      <div class="col-12 my-4">
        <a href="" @click.prevent="changeButton(index)">+ Add one more Skill</a>
      </div>

      <div class="col-12">
        <div class="card" v-if="collapse_on">
            <div class="row card-body">
              <div class="col-6">
                <div class="form-group">
                  <label for="skill">Skill</label>
                  <input v-model="form_data.skill" type="text" class="form-control" id="skill" >
                </div>
              </div> 
              <div class="col-6">
                <div class="form-group">
                  <label for="myRange">
                    Level -
                    <span v-if="form_data.level == 1" class="text-primary"> Beginner </span>
                    <span v-if="form_data.level == 2" class="text-warning"> Skilful </span>
                    <span v-if="form_data.level == 3" class="text-success"> Experienced </span>
                    <span v-if="form_data.level == 4" class="text-secondary"> Expert </span>
                  </label>
                  <div class="slidecontainer">
                    <input v-model="form_data.level" type="range" min="1" max="4" :class="`slider slider-${form_data.level}`" id="myRange" >
                  </div>
                  <input v-model="form_data.level" type="text" class="form-control" id="level" hidden >
                </div>
              </div>
              <div class="col-12 d-flex flex-row-reverse">
                <div class="sasa">
                  <button @click.prevent="cancel" class="btn btn-danger mr-2" >Cancel</button>
                  <button class="btn btn-primary" @click.prevent="addData">Add</button>
                </div>
              </div>
            </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  methods:{
    changeButton(index){
      this.collapse_on = true
      
      this.index = index
      this.form_data.skill = this.skills[index].name
      this.skills[this.index].button_of = true
    },
    addData(){
      let data = {
         skill : this.form_data.skill,
         level : this.form_data.level
      }
      this.skillsUser.push(data)
      this.$emit("data", this.skillsUser)

      // buat form data kosong
      this.collapse_on = false
      this.form_data = {
        skill : null,
        level : 1,
      }
      this.index = ''
    },
    deleteData(i){
      this.skillsUser.splice(i, 1)
      this.$emit("data", this.skillsUser)
    },
    cancel(){
      this.collapse_on = false
      this.skills[this.index].button_of = false

      this.form_data = {
        skill : null,
        level : 1,
      }
      this.index = ''
    }
  },
  data() {
    return{
      switch_button: false,
      index: null,
      collapse_on: false,
      form_data: {
        skill : null,
        level : 1,
      },
      skills : [
        {
          name : 'javascript',
          level : null,
          button_of : false
        },
        {
          name : 'Pyton',
          level : null,
          button_of : false
        },
        {
          name : 'Bootstrap',
          level : null,
          button_of : false
        },
        {
          name : 'Laravel',
          level : null,
          button_of : false
        },
        {
          name : 'React JS',
          level : null,
          button_of : false
        },
        {
          name : 'Nuxt JS',
          level : null,
          button_of : false
        },
      ],
      skillsUser : [
        // {
        //   skill : 'Bootstrap',
        //   level : 4,
        // }
      ]
    }
  }

}
</script>

<style scoped>

.btn-bg-skill{
  background-color: rgb(212, 206, 206);
}

.slidecontainer {
  width: 100%;
}

.slider {
  -webkit-appearance: none;
  width: 100%;
  height: 40px;
  background: #d3d3d3;
  outline: none;
  opacity: 0.7;
  -webkit-transition: .2s;
  transition: opacity .2s;
}

.slider:hover {
  opacity: 1;
}

.slider-1::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 100px;
  height: 40px;
  background: #3a38c7;
  cursor: pointer;
}
.slider-2::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 100px;
  height: 40px;
  background: #e4c150;
  cursor: pointer;
}
.slider-3::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 100px;
  height: 40px;
  background: #46e04e;
  cursor: pointer;
}
.slider-4::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 100px;
  height: 40px;
  background: #494949;
  cursor: pointer;
}


.slider-1::-moz-range-thumb {
  width: 100px;
  height: 40px;
  background: #3a38c7;
  cursor: pointer;
}
.slider-2::-moz-range-thumb {
  width: 100px;
  height: 40px;
  background: #e4c150;
  cursor: pointer;
}
.slider-3::-moz-range-thumb {
  width: 100px;
  height: 40px;
  background: #46e04e;
  cursor: pointer;
}
.slider-4::-moz-range-thumb {
  width: 100px;
  height: 40px;
  background: #494949;
  cursor: pointer;
}

</style>
