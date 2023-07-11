<template>
  <form @submit.prevent="validateForm">
    <label>Email</label>
    <input type="email" required v-model="Email"/>

    <label>Password</label>
    <input type="password" required v-model="Password"/>
    <div v-if="PasswordError" class="error">{{PasswordError}}</div>
    <label>Role</label>
    <select v-model="Role">
        <option value="Webdeveloper">Web developer</option>
        <option value="WebDesigner">Web Designer</option>
    </select>
    <label>Skills</label>
    <input type="text"  v-model="tempSkill" @keyup="addSkill"/>
    <div v-for="skill in skills" :key="skill" class="pill">
       <span @click="removeSkill(skill)"> {{skill}}</span>
    </div>

    <div class="terms">
        <input type="checkbox" required v-model="Terms">
        <label>Accept Terms And Condition</label>
    </div>

    <div class="submit">
        <button class="button">Create an account</button>
    </div>
    <!-- <div>
        <input type="checkbox" value="Saun" v-model="names">
        <label>Saun</label>
    </div>
     <div>
        <input type="checkbox" value="Smith" v-model="names">
        <label>Smith</label>
    </div>
     <div>
        <input type="checkbox" value="Yommy" v-model="names">
        <label>Yommy</label>
    </div> -->
  </form>
</template>

<script>
export default {
    data(){
        return{
            Email:'',
            Password:'',
            Role:'',
            Terms:false,
            tempSkill:'',
            skills:[],
            PasswordError:''
        }
    },
    methods:{
        addSkill(e){
            if(e.key===','&&this.tempSkill){
                if(this.tempSkill.length>1){
                       if(!this.skills.includes(this.tempSkill)){
                    var skValue=this.tempSkill.replace(",","");
                    this.skills.push(skValue);
                    this.tempSkill='';
                }
                }
                this.tempSkill='';
            }
        },
        removeSkill(skill){
            this.skills=this.skills.filter((item)=>{
                return item!==skill;}
            )
        },
        validateForm(){
            this.PasswordError=this.Password.length>6 ?" ":"Password length must be greater than 7";
        }
    }
}
</script>

<style>
form{
    max-width:420px ;
    margin:30px auto ;
    background:white ;
    text-align: left;
    padding: 40px;
    border-radius:10px ;
}
label{
    color: #aaa;
    display:inline-block ;
    margin:25px 0 15px ;
    font-size:0.6em ;
    text-transform: uppercase;
    letter-spacing:1px ;
    font-weight:bold ;

}
input, select{
    color: #555;
    display:block ;
    padding: 10px 6px;
    width: 100%;
    box-sizing:border-box ;
    border: none;
    border-bottom:1px solid #ddd ;
}
input[type="checkbox"]{
display:inline-block ;
width: 16px;
margin: 0 10px 0 0;
position:relative ;
top:2px ;
}
.pill{
    display:inline-block;
    margin:20px 10px 0 0 ;
    padding:6px 12px ;
    background: #eee;
    border-radius:20px ;
    font-size: 12px;
    letter-spacing:1px ;
    font-weight:bold ;
    color:#777 ;
    cursor: pointer;
}

.submit{
    text-align: center;
}

.button{
    background:blue ;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
}

.error {
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
}
</style>