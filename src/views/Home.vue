<template>
  <div class="body">
    <div class="header">
      <Header />

      <div class="row tabs_wrap">
        <div class="col s2 tabs" id="DSLR"><button @click="getAssets(1)">{{this.$parent.categories[1].name}}</button></div>
        <div class="col s2 tabs" id=""><button @click="getAssets(2)">{{this.$parent.categories[2].name}}</button></div>
        <div class="col s2 tabs" id=""><button @click="getAssets(3)">{{this.$parent.categories[3].name}}</button></div>
        <div class="col s2 tabs" id=""><button @click="getAssets(4)">{{this.$parent.categories[4].name}}</button></div>
        <div class="col s2 tabs" id=""><button @click="getAssets(5)">{{this.$parent.categories[5].name}}</button></div>
        <div class="col s2 tabs" id=""><button @click="getAssets(6)">{{this.$parent.categories[6].name}}</button></div>
      </div>

    </div>
    <div clas="main">
<p>{{this.pageHeading}}</p>
      <div class="container con">
        <div class="row table_heading">
          <div class="col s3"><h2>Serial number</h2></div>
          <div class="col s3"><h2>Product Name</h2></div>
          <div class="col s3"><h2>Quantity</h2></div>
          <div class="col s3"><h2></h2></div>
        </div>

        <div class="" v-for="(item, index) in this.$parent.assets" :key="index" >
        <div class="divider"></div>
        <div class="section row table_content">
          <div class="col s3  "><p>{{index + 1}}.</p></div>
          <div class="col s3  "><p>{{item.asset_description}}</p></div>
          <div class="col s3  "><p>{{item.assets_count_available}}</p></div>

          <div class="button col s3 " @click="addCart(item.asset_description, item.assets_count_available)" ><button>Add to cart</button></div>

        </div>
        </div>
        <div class="row table_heading">
          <div class="col s12"></div>
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
  data (){
    return{
      
    }
  },
    methods: {
    getAssets(id) {
      this.$emit("changeState",{state:"category",category:id});
    },
    addCart (asset, available) {
      if (available > 0) {
        this.$emit("changeState",{state:"addToCart",asset:asset});
      } else {
        console.log("Too bad");
      }
    }
  },
  mounted () {
    this.$emit("changeState",{state:"home"});
    
  }
}
</script>
<style scoped>
  h1, h2, h3{
    margin: 0;
  }
  .tabs_wrap{
    text-align: center;
    box-shadow: 2px 2px 5px rgba(0,0,0,.2);
  }
  .tabs{
    height: 3.0rem;
    background-color: #ffffff;
    margin-top: -1.5rem;
    transition: all .5s;
  }
  .tabs:hover, .tabs button:hover{
    background-color: #008265;
    color: #ffffff;
    font-size: 22px;
    cursor: pointer;
  }
  .tabs button:focus{
    background-color: #008265;
    color: #ffffff;
  }
  .tabs button:visited{
    background-color: #008265;
    color: #ffffff;
  }
  .tabs button{
    font-family: Helvetica Neue;
    background-color: #ffffff;
    font-weight: 300;
    color:#727272;
    font-size: 20px;
    line-height: 3.0rem;
    width: 100%;
    border: 0;
    border-radius: 0;
    transition: all .5s;
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
.table_heading{
  margin-top: 0;
}
.con{
  background-color: #ffffff;
  box-shadow: 5px 5px 5px rgba(0,0,0,.2);
}
.equipment_heading{
  height: 3.0rem;
} 
.table_content{
  height: 5.0rem;
  margin-top: 1.0rem;
}
</style>