<template>
  <div class="container">
    <h1>writerslife.app</h1>
    <h2>{{ msgH2 }}</h2>    
    <div class="email-form">
      Enter your email here to receive a notification when we are live !
      <br />
      <input type="text" placeholder="writer@bestseller.com" v-model="email" />
      <div v-on:click="onSubmit" class="box-1">
        <div class="btn btn-one">
          <span>SUBMIT</span>
        </div>
      </div>
    </div>
    <div class="footer-credits">
      <p>Photo by Klaas on Unsplash</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "ComingSoon",
  data() {
    return {
      email: "",
      msgH2:
        "You are a writer. You write. Maybe for yourself, maybe to share with friends and fans, maybe for profit or for passion, or  maybe for fame. Do all that and more. You are a writer. This is your life. Writerslife. Coming soon."
    };
  },
  methods: {
    onSubmit: function(event) {
      var dataJson = {
        email: this.email
      };

      var $ = require("jquery");
      var Swal = require("sweetalert2");

      $.ajax({
        url: "http://52.198.61.205:8081/api/subscribe",
        dataType: "json",
        type: "POST",
        contentType: "application/json; charset=utf-8",
        data: JSON.stringify(dataJson),

        success: function(data) {
          Swal.fire("", data.result.message, "success");
        },

        error: function(xhr, status, err) {
          var errJson = JSON.parse(xhr.responseText);
          Swal.fire({
            icon: "error",
            title: "Woah... something feels off..",
            text: errJson.result.message,
            footer: ""
          });
        }
      });
    }
  }
};
</script>

<style scoped>
div.container {
  position: relative;  
  top: 20%;
  color: beige;
}
h1 {
  position: relative;  
  left: 10%;
  right: 10%;
  color: beige;
}
h2 {
  position: relative;  
  left: 10%;
  margin-right: 20%;
  color: beige;
}
div.email-form {
  position: relative;  
  left: 10%;
  margin-right: 20%;
  color: beige;
}
div.footer-credits {
  position: fixed;
  top: 95%;
  left: 85%;
  color: beige;
}
input {
  display: block;
  width: 300px;
  padding: 15px 0 15px 12px;
  font-family: monospace;
  color: beige;
  background: rgba(0, 0, 0, 0.3);
  border: 1px;
  outline: none;
  text-shadow: 1px 1px 1px rgba(0, 0, 0, 0.3);
  border: 1px solid beige;
  border-radius: 4px;
  box-shadow: inset 0 -5px 45px rgba(100, 100, 100, 0.2),
    0 1px 1px rgba(255, 255, 255, 0.2);
  position: relative;
  font-size: 18px;
  margin-top: 5%;
  margin-right: 10px;
  float: left;
}
div[class*="box"] {
  height: 33.33%;
  width: 20%;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 5%;
}
.box-1 {
  background-color: #1b1310;
  border: 1px solid beige;
  border-radius: 4px;
  font-family: monospace;
}
.btn {
  line-height: 50px;
  height: 50px;
  width: 100%;
  text-align: center;  
  cursor: pointer;
}
.btn-one {
  color: #fff;
  transition: all 0.3s;
  position: relative;
}
.btn-one span {
  transition: all 0.3s;
}
.btn-one::before {
  content: "";
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
  opacity: 0;
  transition: all 0.3s;
  border-top-width: 1px;
  border-bottom-width: 1px;
  border-top-style: solid;
  border-bottom-style: solid;
  border-top-color: rgba(255, 255, 255, 0.5);
  border-bottom-color: rgba(255, 255, 255, 0.5);
  transform: scale(0.1, 1);
}
.btn-one:hover span {
  letter-spacing: 2px;
}
.btn-one:hover::before {
  opacity: 1;
  transform: scale(1, 1);
}
.btn-one::after {
  content: "";
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
  transition: all 0.3s;
  background-color: rgba(255, 255, 255, 0.1);
}
.btn-one:hover::after {
  opacity: 0;
  transform: scale(0.1, 1);
}
</style>
