<template>
    <div v-if="activeform" >
        <div>
            <h2>Form</h2>
        </div>
        <p v-if="errors.length">
            <b>Please correct the following error(s):</b>
            <ul>
                <li v-for="error in errors" v-bind:key="error.id">{{ error }}{{error.id}}</li>
            </ul>
        </p>

        <form @submit="runf">


            <label for="fname">First name:</label>
            <input type="text" id="fname" name="fname" v-model="fname"><br>
            <label for="lname">Last name:</label>
            <input type="text" id="lname" name="lname" v-model="lname"><br>
            <span>select gender</span><br>
            <input type="radio" id="male" name="gender" value="male" v-model="gender">
            <label for="male">Male</label>
            <input type="radio" id="female" name="gender" value="female" v-model="gender">
            <label for="female">Female</label>
            <input type="radio" id="other" name="gender" value="other" v-model="gender">
            <label for="other">Other</label><br>
            <label for="email">Enter your email:</label>
            <input type="email" id="email" name="email" v-model="email"><br>
            <label for="pwd">Password:</label>
            <input type="password" id="pwd" name="pwd" v-model="pwd"><br>
            <label for="cpwd">Confirm Password:</label>
            <input type="password" id="cpwd" name="cpwd"><br>

            <input type="checkbox" id="agecheck" name="agecheck" value="agecheck" v-model="agecheck">
            <label for="agecheck">are you above 18</label><br>
            <input type="submit" id="submit" value="Submit">
        </form>
    </div>
    <div v-if="activedata">
        <span>FullName: {{fname}} {{lname}}</span><br>
        <span>Gender:{{gender}}</span><br>
        <span>Email: {{email}}</span><br>
    </div>
</template>

<script>
export default {

  data(){
    return{
    errors:[],
    fname: null,
    lname: null,
    gender:null,
    email:null,
    pwd:null,
    
    agecheck:null,
    activeform: true,
    activedata: false
    }
  },
methods:{
  displayinfo(){
    
    
    this.activeform=false
    this.activedata=true
    

  },
  runf(e){
    e.preventDefault()
    
    this.errors=[]
    if(this.fname && this.lname&&this.gender&&this.email&&this.pwd&&this.agecheck&&document.getElementById('pwd').value ==
            document.getElementById('cpwd').value){
              console.log('login success');
              this.displayinfo()
            }
            else{
    if(!this.fname){
      
      this.errors.push("Enter first name")
    }
    if(!this.lname){
      this.errors.push("Enter last name")
    }
   
    if(!this.gender){
      this.errors.push("select gender")
    }
    if(!this.email){
      this.errors.push("email required")
    }
     if(!this.pwd){
      this.errors.push("password required")
    }
     if(!this.agecheck){
      this.errors.push("only 18+ allowed")
    }
     if (document.getElementById('pwd').value !==
            document.getElementById('cpwd').value) {
        this.errors.push("passwords don't match")
    }
            }
   
    console.warn('errors',this.errors);
    
    

  }
 
}
}
</script>

<style>

</style>