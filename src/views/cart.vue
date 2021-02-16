<template>
  <div class="body">
    <Header />

  <div class="main">
      <div class="row equipment_heading">
        <div class="green_nav row">
        <div class="col s12 heading_equipment"><h1>EQUIPMENT CART</h1> </div>
        <div class="col s3 heading_allItem"><h2>All the items for checkout will be listed here</h2></div>
        <div class="col s2 offset-s7 heading_totalItem"><h2>Total items = {{this.$parent.cartItems}}</h2></div>
        </div>
      </div>

      <div class="container con">
        <div class="row table_heading">
          <div class="col s4"><h2>Serial number</h2></div>
          <div class="col s4"><h2>Equipment</h2></div>
          <div class="col s4"><h2>Delete item</h2></div>
        </div>

        <div class="" v-for="(item, index) in this.$parent.cart" :key="index" >
        <div class="divider"></div>
        <div class="section row table_content">
          <div class="col s4"><p>{{index + 1}}.</p></div>
          <div class="col s4"><p>{{item}}</p></div>
          <div class="col s4" @click="deleteItem(index)"><p>X</p></div>
        </div>
        </div>
        <div class="row table_heading">
          <div class="col s12"><h2>{{this.Msg}}</h2></div>
        </div>

      </div>
        <div class="container row button_wrap">
          <div class="col s2  but" v-on:click="homePage"><button>back</button></div>
          <div class="col offset-s8 s2 but"><button v-on:click="checkOutMsg">checkout</button></div>
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
  data: function(){
    return {
      Msg: ""
    }
  },
  methods: {
    checkOutMsg(){
      if(this.$parent.cartItems != 0){
        this.Msg = "You have 20 min to take your equipment from L123 room.";
      }else{
        this.Msg = "Tou have not selected anything";
      }
    },
    deleteItem(index){
      this.$emit("changeState",{state:"itemDelete",index:index});
    },
    homePage(){
      this.$router.push('Home');
    }
  }
}
</script>
<style scoped>

h1,h2,h3{
  margin: 0;
}
.table_heading h2{
    font-family: Helvetica Neue;
  text-align: center;
    font-size: 20px;
    font-weight: 300;
    margin-top: 1.0rem;
    color: #ffffff;
}
.table_content p{
    font-family: Helvetica Neue;
    text-align: center;
    font-size: 15px;
    font-weight: 350;
    color: #000000;
}
.con{
  background-color: #ffffff;
}
.equipment_heading{
  height: 3.0rem;
} 
.table_content{
  height: 5.0rem;
  margin-top: 3.0rem;
}
  .foot{
    margin-bottom: 0;
  }
</style>