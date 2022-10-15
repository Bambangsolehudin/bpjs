<template>
  <div class="ProfesionalSummary">
     <!-- Profesional Summary -->
     <div class="row mb-5">
      <div class="col-12">
        <h5><b>Professional Summary</b></h5>
        <p class="text-secondary">Write 2-4 short & energetic sentence the reader! Mention your role, experience & most importanly - your biggest achievements, best qualities and skills.</p>
      </div>
      <div class="col-12">
        <vue-editor :disabled="disabled_form" v-model="content"></vue-editor>
      </div>
      <div class="col-12 d-flex flex-row-reverse my-4">
        <button v-if="disabled_form" class="btn btn-warning" @click.prevent="disabled_form = false">Edit</button>
        <button v-else class="btn btn-primary" @click.prevent="submit">Save</button>
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
  data() {
    return {
      disabled_form: false,
      content: "<h1>Some initial content</h1>"
    };
  },
  methods:{
    submit(){
      this.$emit("data", this.content)
      this.disabled_form = true
    }
  }
}
</script>

<style>

</style>