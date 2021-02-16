<template>
    <div class="body">
        <Header />

    <div class="main">
        <div class="row equipment_heading">
            <div class="green_nav row">
            <div class="col s10 heading_equipment"><h1>Update page</h1></div>
            <div class="col s10 heading_allItem"><h2>Fill below to update your info</h2></div>
            </div>
        </div>

        <div class="container con">
            <div class="row table_heading">
            <div class="col s12"><h1>{{this.$parent.borrower.firstName}} {{this.$parent.borrower.lastName}}</h1></div>
            </div>

            <div class="row">
                <div class="col s6 info">
                    <div class="col s12 name"><h1>My Info</h1></div>
                    <div class="col s12 name">First Name: {{this.$parent.borrower.firstName}}</div>
                    <div class="col s12 name">Last Name: {{this.$parent.borrower.lastName}}</div>
                    <div class="col s12 name">Student number: {{this.$parent.borrower.student_id}}</div>
                    <div class="col s12 name">DC mail: {{this.$parent.borrower.dc_email}}</div>
                    <div class="col s12 name">Alternative mail: {{this.$parent.borrower.other_email}}</div>
                    <div class="col s12 name">Program of student: {{this.$parent.borrower.program_name}}</div>
                </div>

                <div class="col s5 input_fields">
                    <div class="col s12 name"><input type="text" v-model="update.first_name" placeholder="First Name"></div>
                    <div class="col s12 name"><input type="text" v-model="update.last_name" placeholder="Last Name"></div>
                    <div class="col s12 name"><input type="text" v-model="update.old_password" placeholder="Old Password"></div>
                    <div class="col s12 name"><input type="text" v-model="update.new_password" placeholder="New Password"></div>
                    <div class="col s12 name"><input type="text" v-model="update.other_email" placeholder="Other mail"></div>
                    <div class="col s12 name"><input type="text" v-model="update.student_number" placeholder="Student Number"></div>
                </div>
            </div>

            <div class="row table_heading">
            <div class="col s12"><h2>By pressing the update button your information will be updated</h2></div>
            </div>
            </div>

        <div class="container">
        <div class="row button_wrap">
            <div class="col s2 offset-s5 but"><button v-on:click="updateInfo">Update</button></div>
        </div>
        </div>
    </div>

        
        <Footer />
    </div>
</template>
<script>
import Header from "../components/header.vue";
import Footer from "../components/footer.vue";

export default {
    name: 'Home',
    components: {
        Header,
        Footer
    },
    data(){
        return{
        update: {
            first_name: this.$parent.borrower.firstName,
            last_name: this.$parent.borrower.lastName,
            student_number: this.$parent.borrower.student_id,
            other_email: this.$parent.borrower.other_email,
            old_password: '',
            new_password: ''
        }
        }
    },
    methods: {
        updateInfo(){
            if (this.update.old_password == this.$parent.password){
                this.$emit("changeState",{state:"update",first_name:this.update.first_name, last_name:this.update.last_name, student_number:this.update.student_number, other_email:this.update.other_email, old_password:this.update.old_password, new_password:this.update.new_password});
                this.$router.push('Profile');
            }else{
                console.log("your old password is not right");
            }
        }
    }
}
</script>
<style scoped>

.con{
    background-color: #ffffff;
}
h1,h2,h3{
    margin: 0;
}
.table_heading{
    height: 4.0rem;
}
.table_heading h1,h2{
    margin-top: 1.0rem;
}
.detail_equipment{
    height: 4.0rem;
}
.info{
    margin-top: 2.0rem;
}
.info h1{
    font-family: Helvetica Neue;
    font-size: 60px;
    margin-bottom: 40px;
    color: #008265;
}
.input_fields{
    background-color: #008265;
    margin-top: 2.0rem;
}
::placeholder {
    color: #ffffff;
    opacity: 1; /* Firefox */
}
:-ms-input-placeholder { /* Internet Explorer 10-11 */
    color: #ffffff;
}
::-ms-input-placeholder { /* Microsoft Edge */
    color: #ffffff;
}
.but{
    text-align: center;
    height: 3.0rem;
}
.foot{
    margin-bottom: 0;
}
</style>