<template>
  <div id="app">

    <router-view @changeState="setState"/>
  </div>
</template>

<script>

  import M from 'materialize-css'

  export default {
    data() {
      return {
        student_id: "",
        password: "",
        categories: {},
        assets: {},
        cart: [],
        cartItems: 0,
        borrower: {
          firstName: "",
          lastName: "",
          borrower_id: "",
          student_id: "",
          dc_email: "",
          other_email: "",
          program_name: "",
          program_year: ""
        }
      }
      },
      methods: {
        setState(e) {
            console.log(e);
            switch (e.state) {
              case "login":
                this.student_id = e.student_id;
                this.password = e.password;
                this.getLogIn(e);
                break;
              case "home":
                this.getAssets();
                break;
              case "category":
                this.assets = this.categories[e.category].assets;
                break;
              case "addToCart":
                this.cart[this.cart.length] = e.asset;
                console.log("START");
                console.log(this.cart);
                this.cartItems = this.cart.length;
                console.log("Cart Length: "+this.cart.length);
                console.log("Cart Items: "+this.cartItems);
                break;
              case "checkOut":
                this.doCheckOut();
                break;
              case "itemDelete":
                this.deleteItem(e);
                break;
              case "update":
                this.updateData(e);
                break;
            }
          },
          updateData(e){
            console.log(e);

            const options = {
              url: 'https://dca.durhamcollege.ca/~mingwalshubham/signout/dynamic_site/services/update_borrower.php',
              method: 'POST',
              data: {
                student_id: this.student_id,
              }
            }
            this.$axios(options)
              .then((res) => {
                switch (res.data.error.id) {
                  case 0 :

                    (e.first_name).val(res.data.name_first);
                    (e.last_name).val(res.data.name_last);
                    (e.other_email).val(res.data.email_other);
                    (e.old_password).val(res.data.password_old);
                    (e.new_password).val(res.data.password_new);
                    break;
                /* add other responses here */
                  default:
                    alert("Something went wrong please try again.");
                    document.getElementById('#student_id').focus();
                    break;
                }
              })
              .catch((err) => {
                console.error('Login failed.'+err);
              })
          },
          deleteItem(e){
            this.cart.splice(e.index, 1);
            this.cartItems = this.cart.length;
          },
          doCheckOut() {
            let asset_string = "EMPTY";
            this.cart.forEach(function(entry) {
              console.log(entry);
              if (asset_string == "EMPTY") {
                asset_string = entry;
              } else {
                asset_string += "|"+entry;
              }
            });
            console.log(asset_string);
            const options = {
            }
            this.$axios(options)
              .then((res) => {
                console.log(res.data);
                switch (res.data.error.id) {
                  case 0 :
                    // ? push down to home
                    console.log("Yahoo");
                    this.$router.push('CheckOut');
                    break;
                  default:
                    break;
                }
              })
              .catch((err) => {
                console.error('Login failed.'+err);
              })
          },
          getAssets() {
            console.log(this.borrower.student_id);
            const options = {
              url: 'https://dca.durhamcollege.ca/~mingwalshubham/signout/dynamic_site/services/get_assets.php',
              method: 'POST',
              data: {
                student_id: this.student_id
              }
            }
            this.$axios(options)
              .then((res) => {
                console.log(res.data);
                switch (res.data.error.id) {
                  case 0 :
                    // ? push down to home
                    this.categories = res.data.categories;
                    console.log(this.categories);
                    break;
                  default:
                    break;
                }
              })
              .catch((err) => {
                console.error('Login failed.'+err);
              })
          },

          getLogIn(e) {
            console.log(e.student_id);
            const options = {
              url: 'https://dca.durhamcollege.ca/~mingwalshubham/signout/dynamic_site/services/login.php',
              method: 'POST',
              data: {
                student_id: e.student_id,
                password: e.password
              }
            }
            this.$axios(options)
              .then((res) => {
                switch (res.data.error.id) {
                  case 0 :
                    this.borrower.firstName = res.data.borrower.first_name;
                    this.borrower.lastName = res.data.borrower.last_name;
                    this.borrower.borrower_id = res.data.borrower.borrower_id;
                    this.borrower.dc_email = res.data.borrower.dc_email;
                    this.borrower.other_email = res.data.borrower.other_email;
                    this.borrower.program_name = res.data.borrower.program_name;
                    this.borrower.program_year = res.data.borrower.program_year;
                    this.borrower.student_id = res.data.borrower.student_id;
                    //alert("route");
                    console.log(this.borrower);
                    this.$router.push('Home');
                    break;
                /* add other responses here */
                  default:
                    alert("Something went wrong please try again.");
                    document.getElementById('#student_id').focus();
                    break;
                }
              })
              .catch((err) => {
                console.error('Login failed.'+err);
              })
      
          }
      },

      mounted () {
      M.AutoInit()
    }
  }
</script>

<style>
  .body{
    background-color: #EFF0F1;
    background-size: cover;
  }
  .heading{
      height: 3.5rem;
      text-align: center;
      font-size: 40px;
  }
  .heading h1{
      font-family: Helvetica Neue;
      font-size: 50px;
      font-weight: 300;
      color: #ffffff;
  }
  .equipment{
      height: 10.0rem;
      margin-top: 4.0rem;
      background-color: #ffffff;
      text-align: center;
      box-shadow: 1px 3px 5px #707070;
  }
  .equipment h1{
      font-family: Helvetica Neue;
      font-size: 30px;
      font-weight: 200;
      color: #727272;
  }
  .equipment p{
      font-family: Helvetica Neue;
      font-size: 20px;
      font-weight: 200;
      color: #727272;
  }
  .button{
      height: 2.0rem;
      text-align: center;
      margin-top: 1.0rem;
  }
  .button button{
      height: 100%;
      width: 60%;
      border-radius: 0;
      background-color: #008265;
      border: none;
      color: #ffffff;
      transition: all .2s ease-in;
  }
  .button button:hover{
      background-color: #ffffff;
      color: #008265;
      font-size: 17px;
      cursor: pointer;
  }
  .no_left{
      opacity: .4;
  }
  .noleft_but{
      opacity: .4;
  }
  .noleft_but button:hover{
      background-color: #008265;
      color: #ffffff;
      font-size: 15px;
      cursor: unset;
  }
  .green_nav{
    width: 75%;
    text-align: left;
    height: 4.0rem;
    background-color: #008265;
    box-shadow: 0px 5px 3px #707070;
  }
  .heading_equipment h1{
    font-family: Helvetica Neue;
    font-size: 30px;
    margin-top: 5px;
    color: #ffffff;
  }
  .heading_totalItem{
    font-size: 10px;
    text-align: right;
  }
  .heading_totalItem h2{
    font-family: Helvetica Neue;
    font-size: 10px;
    margin-top: 5px;
    color: #ffffff;
  }
  .heading_allItem h2{
    font-family: Helvetica Neue;
    font-size: 10px;
    margin-top: 5px;
    color: #ffffff;
  }
  .table_heading{
    height: 4.0rem;
    margin-top: 5.0rem;
    background-color: #008265;
  }
  .table_heading h2{
    font-family: Helvetica Neue;
    font-size: 15px;
    margin-top: 2.0rem;
    color: #ffffff;
  }
  .table_heading h1{
    font-family: Helvetica Neue;
    font-size: 30px;
    margin-top: 2.0rem;
    color: #ffffff;
  }
  .but{
    text-align: center;
    height: 3.0rem;
    margin-top: 2.0rem;
  }
  .but button{
    border: 0;
    width: 100%;
    height: 100%;
    background-color: #008265;
    color: #ffffff;
    font-size: 15px;
    font-family: Helvetica Neue;
  }
  .but button:hover{
    background-color: #ffffff;
    color: #008265;
    font-size: 17px;
    cursor: pointer;
  }

</style>