<template>
  <div id="app">
    <head>
        <title>Facebook</title>
        <link rel="icon" type="image/x-icon" href="https://icons.iconarchive.com/icons/yootheme/social-bookmark/512/social-facebook-box-blue-icon.png">
        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
    </head>
    <body>
        <header>
            <div class="header">
                <li class="sitename"><a href="http://Facebook.com">Facebook</a></li>
                <form @submit.prevent="formLogin" action="post">
                    <li>Email<br><input type="text" v-model="loginEmail" name="email" class="e">
                    <div class="error" v-if="loginEmailError">{{loginEmailError}}</div>
                    </li>
                    <li>Password<br><input type="password" v-model="loginPassword" name="password" class="p">
                    <div class="error" v-if="loginPasswordError" >{{loginPasswordError}}</div>
                    <br><a href="">Forgotten account?</a></li>
                    <li><input type="submit" name="login" value="Log In" class="b"></li>
                </form> 
            </div>
        </header>
        <div class="wrapper">
            <div class="div1">
                <p><B>Connect with friends and the <br>world around you on Facebook.</B></p>
                <br><br>
                <p><i class="fa fa-newspaper-o" aria-hidden="true"></i> <B>See photos and updates</B> from friends in New Feed </p><br><br>
                <p><i class="fa fa-television" aria-hidden="true"></i> <B>Share what's new</B> in your life on your Timeline.</p><br><br>
                <p><i class="fa fa-share-alt-square" aria-hidden="true"></i> <B>Find more</B> of what you're looking for with Facebook Search.</p>
            </div>
           <div class="div2">
                <h1>Sign Up</h1>
                <p>It's free and always will be.</p>
                <form @submit.prevent="checkSingUpForm" action="post">
                    <li>
                      <input type="text" v-model="username" placeholder="Username" name="Username" id="username">
                      <div class="error" v-if="usernameError">{{usernameError}}</div>
                    </li>
                    <li>
                      <input type="text" v-model="email" placeholder="Email" name="Email" id="email">
                      <div class="error" v-if="emailError">{{emailError}}</div>
                    </li>
                    <li>
                      <input type="password" v-model="password" placeholder="Password" name="Password" id="password">
                      <div class="error" v-if="passwordError">{{passwordError}}</div>
                    </li>
                    <li>
                      <input type="password" v-model="confirmpassword" placeholder="Confirm password" name="Password" id="confirm-password">
                      <div class="error" v-if="confirmPasswordError">{{confirmPasswordError}}</div>
                    </li>
                    <li>
                        <input type="radio" v-model="radioF" name="gender" value="male">
                        <label for="age1">Male</label>
                        <input type="radio" v-model="radioF" name="gender" value="female">
                        <label for="age1">Female</label>

                    </li>
                    <li class="terms">By clicking Sign Up,, you agree to our  <a href="">Teams. Data Police</a> and  <br><a href="">Cookies Policy </a>you may receive SMS Notification from us and <br>can opt out any time.</li>
                    <li>
                      <input type="submit" value="Sign Up" class="sub" id="signup">
                      <div id="submit-error-block"></div>
                    </li>
                </form>
            </div>
        </div>
        <footer>
            <p><a href="facebook.com">facebook.com</a></p>
        </footer>
    </body>

   <nav>
        <router-link to="/">Home</router-link> |||
        <router-link to="/signup">SignUp</router-link>|||
        <router-link to= "/dashboard">Dashboard</router-link>|||
        <router-link to= "/user">User</router-link>|||
    </nav>
    <router-view/>
  </div>
</template>

<script>
export default{
  name:"SignUp",
  
  data(){
    return{
       error:[],
       username:null,
       email:null,
       password:null,
       confirmpassword:null,
       usernameError: null,
       emailError:null,
       passwordError: null,
       confirmPasswordError: null, 
       radioF:null,
       radioM:null,
       data:[],
       loginEmail:null,
       loginPassword:null,
       loginEmailError:null,
       loginPasswordError:null
    }
  },
    methods: {
    checkSingUpForm(e) {
        const userObj ={
            emailInput:this.email,
            passwordInput:this.password
        }
        console.log('Form submitted', this.username, this.email, this.password, this.confirmpassword);
        this.error=[];
        const regexUsername= /[A-Za-z][A-Za-z0-9_]{7,29}$/;
        const regexEmail= /^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+$/;
        const regexPassword=/^(?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?=.*[^a-zA-Z0-9])(?!.*\s).{8,20}$/;
        if (!this.username)   {
            this.usernameError = 'Username is required';
        } 
        else if(!regexUsername.test(this.username)){
            this.usernameError='Username is not valid';
        }
        else {
            this.usernameError = ''
        }
        if (!this.email)   {
            this.emailError = 'Email is required';
        }
        else if(!regexEmail.test(this.email)){
            this.emailError='Email is not valid';
        } 
        else {
            this.emailError = ''
        }
        if (!this.password)   {
            this.passwordError = 'Password is required';
        }
        else if(!regexPassword.test(this.password)){
            this.passwordError='Password is not valid';
        }
        else {
            this.passwordError = ''
        }
        if (!this.confirmpassword){
            this.confirmPasswordError = 'Confirm password is required';
        }
        else if(this.password !=this.confirmpassword){
            this.confirmPasswordError = 'Password does not match';
        }
        else {
            this.confirmPasswordError = ''
        }

        if(this.usernameError == null &&
            this.emailError == null &&
            this.passwordError == null &&
            this.confirmPasswordError == null
        ){  
           alert("successfully Signed Up");   
        }
        if(localStorage.data){
                let localUsers=localStorage.data;
                this.data=JSON.parse(localUsers);
        }
        console.log("Validations successfully");

        this.data.push(userObj);
        localStorage.setItem('data',JSON.stringify(this.data));
        this.email=null;
        this.password=null;
        this.username=null;
        this.confirmpassword=null;
        console.warn("errors",this.error)
        e.preventDefault()
       
    },
  
  formLogin(){
    console.log('Form submitted', this.loginEmail, this.loginPassword)
    let security={
           emailLogin : this.loginEmail,
            passwordLogin: this.loginPassword
    } 
    if (!this.loginEmail)   {
            this.loginEmailError = 'Email can not be empty';
    }
    else{
        this.loginEmailError= ''
    }
    if(!this.loginPassword){
        this.loginPasswordError = 'Password can not be empty';
    }
    else{
        this.loginPasswordError= ''
    }
    if(
        this.loginEmailError == null && 
        this.loginPasswordError == null){
            let localStorageLoginUsers = localStorage.data;
            localStorageLoginUsers = JSON.parse(localStorageLoginUsers);
            this.emailLogin = localStorageLoginUsers.findIndex(
                (userObj) => userObj.emailInput === security.emailLogin
            )
            console.log("hello");
            if(this.emailLogin>-1){
                this.passwordLogin = localStorageLoginUsers.findIndex(
                    (userObj) => userObj.passwordInput === security.passwordLogin
                )
                if(this.loginPassword>-1){
                    this.$router.push("/DashBoard");
                }
                else{
                    this.loginPasswordError = 'Password does not match'
                }
            }
            else{
                this.loginEmailError='user does not match';
            }
        }
    } 
  }
}

</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
body
{
    text-align:center;
    width:100%;
    margin:0 auto;
    padding:0px;
    font-family:"lucida grande",tahoma,verdana,arial,sans-serif;
    background: linear-gradient(white, #D3D8E8);
}
header
{
    width:100%;
    min-width:980px;
    background-color:#4c66a4;
}
.header
{
    width:980px;
    margin:0px auto;
    padding:0px;
    height:85px;
    }
.header li
{
    list-style-type:none;
    float:left;
    text-align:left;
    color:white;
}
.header .sitename
{
    margin-top:25px;
}
.header .sitename a
{
    color:white;
    text-decoration:none;
    font-size:30px;
    font-weight:900;   
}
.header form
{
    margin-top:15px;
    float:right;
}
.header form li
{
    font-size:13px;
    margin-left:15px;
}
.header form li a
{
    color:#A9BCF5;
    text-decoration:none;
}
.e
{
    margin-top:3px;
    margin-bottom:3px;
    width:150px;
    border:1px solid #08298A;
    height:25px;
    padding-left:3px;
}
.p
{
    margin-top:3px;
    margin-bottom:3px;
    width:150px;
    border:1px solid #08298A;
    height:25px;
    padding-left:30px;
}
.b
{
    height:25px;
    margin-top:20px;
    background-color:#084B8A;
    color:white;
    border:1px solid #08298A;
}
.wrapper
{
    margin:0 auto;
    padding:0px;
    text-align:center;
    width:990px;
}
.wrapper div
{
    float:left;
    font-family: helvetica, arial, sans-serif;
}
.wrapper .div1
{
    margin-top:30px;
    width:590px;
    text-align:left;
}
.wrapper .div1 p
{
    font-size:20px;
    font-family:arial;
    font-weight:bold;
    margin:0px;
    color:#000000;
}
.wrapper .div2
{
    margin-top:10px;
    width:390px;
    text-align:left;
}
.wrapper .div2 h1
{
    margin:0px;
    font-size:37px;
    color:#2E2E2E;
}
.wrapper .div2 p
{
    font-size:18px;
    color:#2E2E2E;
    
}
.wrapper .div2 li
{
    list-style-type:none;
    margin-top:10px;
}
.error{
    color:red;
    font-size: small;
}
#username
{
    width:100%;
    height:40px;
    border-radius:5px;
    padding-left:10px;
    font-size:18px;
    border:1px solid #BDBDBD;
}
#email
{
    width:100%;
    height:40px;
    border-radius:5px;
    padding-left:10px;
    font-size:18px;
    border:1px solid #BDBDBD;
}
#password
{
    width:100%;
    height:40px;
    border-radius:5px;
    padding-left:10px;
    font-size:18px;
    border:1px solid #BDBDBD;
}
#confirm-password
{
    width:100%;
    height:40px;
    border-radius:5px;
    padding-left:10px;
    font-size:18px;
    border:1px solid #BDBDBD;
}
.wrapper .div2 li select
{
    padding:4px;
    float:left;
}
.wrapper .div2 li a
{
    margin-left:10px;
    width:150px;
    color:#045FB4;
    text-decoration:none;
    font-size:11px;
    display: inline-block;
    vertical-align: middle;
    line-height:15px;
}
.wrapper .div2 li a:hover
{
    text-decoration:underline;
}
.wrapper .div2 li
{
    color:#2E2E2E;
    font-size:18px;
}
.wrapper .div2 li.terms 
{
    color:#424242;
    font-size:11px;
}.wrapper .div2 li.terms a
{
    display:inline;
    margin:0px;
    font-size:11px;
}
.sub
{
    width:205px;
    height:45px;
    text-align:center;
    font-size:19px;
    margin-top: 10px;
    margin-bottom: 10px;
    font-family: 'Freight Sans Bold', helvetica, arial, sans-serif !important;
    font-weight: bold !important;
    background: linear-gradient(#67ae55, #578843);
    background-color: #69a74e;
    box-shadow: inset 0 1px 1px #a4e388;
    border-color: #3b6e22 #3b6e22 #2c5115;
    border: 1px solid;
    border-radius: 5px;
    color: #fff;
    cursor: pointer;
    display: inline-block;
    position: relative;
    text-shadow: 0 1px 2px rgba(0,0,0,.5);
}
footer
{
    margin-top:47%;
    width:100%;
    min-width:980px;
    background-color:#4c66a4;
    text-align: center;
    height: 50px;
    padding-top: 15px;
    padding-bottom: 15px;
    
}
</style>