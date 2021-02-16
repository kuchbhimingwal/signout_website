<template>
    <div class="body">
        <Header />

    <div class="main">
        <div class="row equipment_heading">
            <div class="green_nav row">
            <div class="col s12 heading_equipment"><h1>Profile page</h1></div>
            <div class="col s3 heading_allItem"><h2>Your profile details and equipment summary is shown</h2></div>
            </div>
        </div>

        <div class="container con">
            <div class="row table_heading ">
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
                <div class="col s6 equi_taken">
                    <div class="col s12 equipment_held">Equipment Held by student</div>
                    <div class="col s12 detail_equipment" v-for="(item, index) in this.$parent.cart" :key="index" >
                        {{item}}
                    </div>
                </div>
            </div>

            <div class="row table_heading">
            <div class="col s12"></div>
            </div>
            </div>

        <div class="container">
        <div class="row button_wrap">
            <div class="col s2 but "><button v-on:click="goToUpdate">Update</button></div>
            <div class="col s2 offset-s8 but "><button v-on:click="goToLogin">Signout</button></div>
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
    name: 'Profile',
    components: {
        Header,
        Footer
    },
    methods: {
        goToUpdate () {
            this.$router.push('Update');
        },
        goToLogin () {
            this.$router.push('/');
        }
    }
}
</script>

<style scoped>

.con{
    background-color: #ffffff;
}
.equipment_heading{
    margin-top: 2.0rem;
}
h1,h2,h3{
    margin: 0;
}
.table_heading{
    height: 4.0rem;
    margin-top: 4.0rem;
}
.table_heading h1{
    margin-top: 1.0rem;
}
.detail_equipment{
    height: 4.0rem;
}
.equipment_held{
    font-size: 25px;
    font-weight: bold;
}
.info h1{
    font-family: Helvetica Neue;
    font-size: 60px;
    margin-bottom: 40px;
    color: #008265;
}
.but{
    margin-top: 4.0rem;
    text-align: center;
    height: 3.0rem;
}
.foot{
    margin-top: 4.0rem;
    margin-bottom: 0;
}
</style>