<template>
  
  <div class="container-fluid">
    
    <main class="form-signin">
      <div class="form-floating">
        <form v-on:submit.prevent="processLogInUser">
          <h1 class="h3 mb-3 fw-normal">Iniciar Sesión</h1>
          <div class="">
            <input type="text" class="form-control" placeholder="Nombre de Usuario" v-model="user.username"/>
            <br />
          </div>
          <div class="">
            <input type="password" class="form-control" placeholder="Contraseña" v-model="user.password"/>
            <br />
          </div>
          <button class="w-100 btn btn-lg btn-primary" type="submit">
            Ingresar
          </button>
          <p class="mt-5 mb-3 text-muted">&copy; 2021</p>
        </form>
      </div>
    </main>
  </div>
  
</template>

<script>
import axios from "axios";

export default {
  name: "LogIn",

  data: function () {
    return {
      user: {
        username: "",
        password: "",
      },
    };
  },

  methods: {
    processLogInUser: function () {
      axios
        .post("http://127.0.0.1:8000/login/", this.user, { headers: {} })
        .then((result) => {
          let dataLogIn = {
            username: this.user.username,
            token_access: result.data.access,
            token_refresh: result.data.refresh,
          };

          this.$emit("completedLogIn", dataLogIn);
        })
        .catch((error) => {
          if (error.response.status == "401")
            alert("ERROR 401: Credenciales Incorrectas.");
        });
    },
  },
};
</script>

<style>
body{
  background-position: 25%;
  background-size: 75%;
  background-repeat: no-repeat;
  /* background-attachment: fixed; */
  background-image: url(~@/assets/mujer-embarazada-1.jpg);
}

.btn-primary{
  color: black;
  background-color: #a4d8ed;
  border-color: #a4d8ed;
}

.btn-primary:hover{
  color: white;
  background-color: #7a87aa;
  border-color: #7a87aa;
}

.btn-primary:focus{
  background-color: #7a87aa;
  border-color: #7a87aa;
}

.main-component{
  background: transparent;
}

.container-fluid{
  position: absolute;
	top: 50%;
	left: 50%;
	margin: -150px 0 0 -150px;
	width:300px;
	height:300px;

  background: transparent;
  }

.form-control{
  line-height: 2.0;
}

/* .container-fluid{
  width: 30%;
  margin-right: auto;
  margin-left: auto;
} */



.logIn_user {
  margin: 0;
  padding: 0%;
  height: 100%;
  width: 100%;

  display: flex;
  justify-content: center;
  align-items: center;
}

.container_logIn_user {
  border: 3px solid #283747;
  border-radius: 10px;
  width: 25%;
  height: 60%;

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.logIn_user h2 {
  color: #283747;
}

.logIn_user form {
  width: 70%;
}

.logIn_user input {
  height: 40px;
  width: 100%;

  box-sizing: border-box;
  padding: 10px 20px;
  margin: 5px 0;

  border: 1px solid #283747;
}

.logIn_user button {
  width: 100%;
  height: 40px;

  color: #e5e7e9;
  background: #283747;
  border: 1px solid #e5e7e9;

  border-radius: 5px;
  padding: 10px 25px;
  margin: 5px 0;
}

.logIn_user button:hover {
  color: #e5e7e9;
  background: crimson;
  border: 1px solid #283747;
}
</style>