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
          <input type="text" id="fname" autocomplete="off" name="fname" @input="fnamecheck" v-model="fname"><br>
          <span >{{fnamee}}</span><br>
          <label for="lname">Last name:</label>
          <input type="text" id="lname" autocomplete="off" name="lname" @input="lnamecheck" v-model="lname"><br>
          <span>{{lnamee}}</span><br>
           <span>select gender</span><br>       
          <input type="radio" id="male" name="gender" value="male" v-model="gender">
          <label for="male">Male</label>
          <input type="radio" id="female" name="gender" value="female" v-model="gender">
          <label for="female">Female</label>
          <input type="radio" id="other" name="gender" value="other" v-model="gender">
          <label for="other">Other</label><br>
          <label for="email">Enter your email:</label>
          <input type="email" id="email" autocomplete="off" name="email" @input="emailcheck" v-model="email"><br>
          <span>{{emaile}}</span><br>
          <label for="pwd">Password:</label>
          <input type="password" id="pwd" name="pwd" @input="pcheck"  v-model="pwd"><br>
          <span>{{pwde}}</span><br>
          <label for="cpwd">Confirm Password:</label>
          <input type="password" id="cpwd" @input="cpcheck" name="cpwd"><br>
          <span>{{cpwde}}</span><br>
          <input type="checkbox" id="agecheck" name="agecheck" value="agecheck" @change="agecheckf" v-model="agecheck">
          <label for="agecheck">are you above 18</label><br>
          <span>{{agee}}</span><br>
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
    activedata: false,
     fnamee: '',
    lnamee: '',
    pwde:'',
    cpwde:'',
    agee:'',
    emaile:''
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
    
    

  },
   fnamecheck() {

      if (!this.fname) {

        this.fnamee = 'first name cannot be empty'
         document.getElementById("submit").disabled = true;

      } else if (this.fname.length < 3) {

        this.fnamee = 'name must be greater than 2 characters'
         document.getElementById("submit").disabled = true;

      } else {
        this.fnamee = ''
         document.getElementById("submit").disabled = false;
      }
    },
    lnamecheck() {

      if (!this.lname) {

        this.lnamee = 'last name cannot be empty'
        document.getElementById("submit").disabled = true;


      } else if (this.lname.length < 3) {

        this.lnamee = 'last name must be greater than 2 characters'
        document.getElementById("submit").disabled = true;


      } else {
        this.lnamee = ''
         document.getElementById("submit").disabled = false;

      }
    },
    pcheck(){
        if (!this.pwd) {

        this.pwde = 'password cannot be empty'
         document.getElementById("submit").disabled = true;


      } else if (this.pwd.length < 5) {

        this.pwde = 'password must be greater than 5 characters'
         document.getElementById("submit").disabled = true;


      } else {
        this.pwde = ''
         document.getElementById("submit").disabled = false;

      }
      

    },
    cpcheck(){
        if(!document.getElementById('cpwd').value){
          this.cpwde='cannot be empty'
           document.getElementById("submit").disabled = true;
         
        }
        else if(document.getElementById('cpwd').value!==document.getElementById('pwd').value){
          this.cpwde="Passwords don't match"
           document.getElementById("submit").disabled = true;
          
        }
        else{
          this.cpwde=''
           document.getElementById("submit").disabled = false;
        }
      },
      agecheckf(){
      if(  document.getElementById('agecheck').checked){
        this.agee=''
         document.getElementById("submit").disabled = false;
      }else{
        this.agee='only above 18 allowed'
         document.getElementById("submit").disabled = true;
      }
      },
      emailcheck(){
        console.log('q');
        if (/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(document.getElementById('email').value)){ // eslint-disable-line
          this.emaile=''
           document.getElementById("submit").disabled = false;
        }else{
           document.getElementById("submit").disabled = true;
          this.emaile='inavlid email'
        }
      }
 
}
}
</script>

<style>

</style>