<template>
  <form @submit.prevent="submit">
    <label for="email">Email</label>
    <input type="email" required v-model="email"/>

    <label for="password">Password</label>
    <input type="password" required v-model="password" />
    <p v-if="errorMsg" class="errmsg">{{errorMsg}}</p>

    <label>Roles:</label>
    <select v-model="role">
        <option value="web">Web Developer</option>
        <option value="app">App Developer</option>
    </select>

    <div>
        <label for="">Skills</label>
        <input type="text" @keyup="getText" v-model="skill"/>
    </div>  

    <div v-for="skill in skills" :key="skill">
        <p>{{skill}}<span class="skill" @click="deleteSkill(skill)"> &#x2716;</span></p>
    </div> 

    <div>
        <input type="checkbox" v-model="accept">
        <label for="">Accept Terms and Conditions</label>
    </div>  
    <div class="align">
        <button class="subButton">Submit</button>
    </div>  

    <!-- <label for="">Select Name</label> -->

    <!-- <div>
        <input type="checkbox" value="Alex" v-model="names">
        <label for="">Alex</label>
    </div>
    <div>
        <input type="checkbox" value="Zyan" v-model="names">
        <label for="">Zyan</label>
    </div>
    <div>
        <input type="checkbox" value="Khun" v-model="names">
        <label for="">Khun</label>
    </div> -->
    
  </form>
</template>

<script>
export default {
    data(){
        return{
            email:"",
            password:"",
            role:"",
            accept:false,
            names:[],
            skills:[],
            skill:"",
            errorMsg:""
        }
    },
    methods:{
        getText(e){
            // console.log(e.key);
            if(e.key === 'Enter' && this.skill){
                this.skills.push(this.skill);
                this.skill = ''
            }
            //  if(e.key === ','){
            //     this.skills.push(this.skill);
            //     this.skill = ''
            // }
        },
        deleteSkill(skill){
           this.skills=this.skills.filter(loopSkill=>{
                return loopSkill != skill;
           })
        },
        submit(){
            if(this.password.length<8){
                this.errorMsg = "The password should be 8 characters";
            }
        }
    }
}
</script>

<style>
    form{
        max-width: 420px;
        margin: 30px auto;
        background: white;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }
    label{
        color: #aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6em;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }
    input,select{
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ddd;
        color: #555;
    }
    input[type="checkbox"]{
        display: inline-block;
        margin: 0 10px 0 0;
        width: 50px;
        position: relative;
        top:2px;
    }
    .skill{
        cursor:pointer;
        color:red;        
    }
    .subButton{
        background: royalblue;
        padding: 8px 20px;
        color: white;
        border-radius: 10px;
        border: none;
    }
    .align{
        text-align: center;
    }
    .errmsg{
        color: red;
        font-size: 10px;
    }
</style>