<template>
    <div class="body">
        <Header />
        
        <div class="main">
            <div class="container">
            <div class="container row login_wrapper">
                <div class="col s6 offset-s1 heading_login">
                    <h1>Login</h1>
                    <p>Enter you id and Password</p>
                </div>

                <div class="col s10 offset-s1 id_text">
                    <input type="text" v-model="login.student_id" id="student_id" placeholder="Id or Username">
                </div>

                <div class="col s10 offset-s1 password_text">
                    <input type="text" v-model="login.password" id="password" placeholder="Enter your password">
                </div>

                <div class="col s4 offset-s4 login_button">
                    <button v-on:click="checkCredentials">Login</button>
                </div>

                <div class="col s2 offset-s5 or_text">0r</div>

                <div class="col s4 offset-s4 signup_button">
                    <button>signup</button>
                </div>

                <div class="col s6 offset-s3 forgot_text"><a>forgot the password</a></div>
            </div>
            </div>
        </div>
    </div>
</template>


<script>
import Header from "../components/header.vue";

export default {
    name: 'Login',
    components: {
        Header
        
    },
    data(){
        return{
        login: {
            student_id: '900000009',
            password: 'dingo'
        }
        }
    },
    methods: {
        checkCredentials () {
        // send info to service
        console.log("STUDENT ID: "+this.login.student_id);
        this.$emit("changeState",{state:"login",student_id:this.login.student_id,password:this.login.password});
        }
    }
}
</script>

<style scoped>
.login_wrapper{
    margin-top: 5.0rem;
    margin-bottom: 10.0rem;
    background-color: #ffffff;
    border: 1px #707070 solid;
    width: 60%;
    box-shadow: 5px 5px 3px #707070;
}
.heading_login{
    height: 4.0rem;
    margin-top: 2.5rem;
}
.heading_login h1{
    font-family: Helvetica Neue;
    font-size: 50px;
    color: #0B4E44;
    font-weight: 600;
}
.heading_login p{
    font-family: Helvetica Neue;
    font-size: 15px;
    color: #000000;
    font-weight: 200;
    margin-top: -20px;
}
.id_text{
    height: 3.0rem;
    margin-top: 7.0rem ;
}
.password_text{
    height: 3.0rem;
    margin-top: 4.0rem ;
}
.login_button{
    height: 3.0rem;
    margin-top: 2.5rem ;
}
.login_button button{
    border-radius: 0;
    background-color: #0B4E44;
    color: #ffffff;
    border: 0;
    width: 100%;
    height: 100%;
    transition: all .2s ease-in-out;
}
.login_button button:hover{
    background-color: grey;
    color: #ffffff;
    font-size: 17px;
    cursor: pointer;
}
.or_text{
    text-align: center;
    height: 3.0rem;
    margin-top: 1.5rem;
}
.signup_button, .forgot_text{
    height: 3.0rem;
    margin-top: 1.5rem;
    text-align: center;
}
.forgot_text a:hover{
    text-decoration: underline;
    cursor: pointer;
}
.signup_button button{
    border-radius: 0;
    background-color: #0B1D4E;
    color: #ffffff;
    border: 0;
    width: 100%;
    height: 100%;
    transition: all .2s ease-in-out;
}
.signup_button button:hover{
    background-color: grey;
    color: #ffffff;
    font-size: 17px;
    cursor: pointer;
}
.login_wrapper{
    height: 45.0rem;
}
.body{
    height: 60.0rem;
}
</style>