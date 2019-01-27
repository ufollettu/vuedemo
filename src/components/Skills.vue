<template>
  <div class="hello">
    <div class="holder">
      <form @submit.prevent="addSkill">

      <input type="text" name="skill" id="" placeholder="enter skill" 
      v-model="skill" v-validate="'min:5'">
      <transition name="alert-in" enter-active-class="animated flipInX" leave-active-class="animated flipOutX">  
        <p class="alert" v-if="errors.has('skill')">{{errors.first('skill')}}</p>
      </transition>  
      </form>
      <ul>
        <transition-group name="list" enter-active-class="animated bounceInUp" leave-active-class="animated bounceInOut">
        <li v-for="(data, index) in skills" :key="data.skill">
           <span @click="goToSkill(data.skill)">{{data.skill}}</span>
           
           <i class="fa fa-minus-circle" v-on:click="remove(index)"></i>
        </li>
        </transition-group>
      </ul>
      <p>skills possedute</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Skills',
    data() {
      return {
        skill :"",
        skills: [
          {"skill": "vue"},
          {"skill": "frontesnd"}
        ], 
      }
    },
    methods: {
      addSkill() {
        this.$validator.validateAll().then(result => {
          if (result) {
            this.skills.push({skill : this.skill});
            this.skill = "";
          } else {
            console.log('nope')
          }
        })
      },
      remove(id) {
        this.skills.splice(id, 1);
      },
      goToSkill(skill) {
        this.$router.push({ name: 'about', params: { name: skill } })
      }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style src="./Skills.css" scoped>

</style>
