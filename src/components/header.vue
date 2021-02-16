<template>

      <div class="row nav">
        <div class="col s2 logo" v-on:click="goToHome">
          <img src="../assets/logo@2x.png" alt="logo">
        </div>

        <div class="col s2 offset-s3 nav_equipment"><h1>Equipment signout</h1></div>

        <div class="col s2 offset-s3 proCart">
          <img src="../assets/profile@2x.png" alt="profile" v-on:click="goToProfile">
            <img src="../assets/cart@2x.png" alt="cart" v-on:click="goToCart">
            <div id="dot">{{this.$parent.$parent.cartItems}}</div>
        </div>
      </div>
</template>

<script>
export default {
    name: 'Header',
    components: {
    
    },
    methods: {
        goToHome () {
            this.$router.push('Home');
        },
        goToProfile () {
            this.$router.push('Profile');
        },
        goToCart () {
            this.$router.push('Cart');
        }
    }
}
</script>
<style scoped>
#dot{
  width: 20px;
  height: 20px;
  border-radius: 50%;
  position: absolute;
  top: 35px;
  right: 10px;
  text-align: center;
  line-height: 20px;
  background-color: red;
}
h1, h2, h3{
    margin: 0;
}
</style>
<style>
  .proCart{
    text-align: right;
  }
  .proCart img{
    width: 30px;
    height: 25px;
    margin: 5px;
    margin-top: 1.0rem;
    mix-blend-mode: multiply;
  }
  .proCart img:hover{
    mix-blend-mode:color;
  }
  .logo img{
    mix-blend-mode: color-burn;
    width: 100px;
    height: 30px;
    margin-top: 1.0rem;
  }

  .nav_equipment h1{
    margin-top: 1.0rem;
    font-family: Helvetica Neue;
    color: #ffffff;
    font-size: 25px;
  }
  .nav{
    height: 4.0rem;
    background-color: #008265;
    line-height: 3.0rem;
  }
</style>