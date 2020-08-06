<template>
  <div>
    <div class="wrapper">
      <link
        rel="stylesheet"
        href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css"
      />

      <div class="loginForm">
        <div class="leftPage">
          <div class="slidershow">
            <div class="slides">
              <input type="radio" name="r" id="r1" checked @click="firstSlideActive()" />
              <input type="radio" name="r" id="r2" @click="secondSlideActive()" />

              <div class="slide s1">
                <img src="@/assets/Slide1.png" alt />
              </div>
              <div class="slide">
                <img src="@/assets/Slide2.png" alt />
              </div>

              <div class="navigation">
                <label for="r1" class="bar sliderButtonActive" id="navLabel1"></label>
                <label for="r2" class="bar" id="navLabel2"></label>
              </div>
            </div>
          </div>
        </div>
        <div class="rightPage">
          <img src="@/assets/ros-logo.png" class="rightPageContentLogo" />
          <div class="rightPageContent">
            <div class="loginActive" id="rightPageContentLogin">
              <h1>Willkommen zurück!</h1>
              <br />

              <p class="rightPageContentGrey" id="rightPageContentLoginEmailfield">E-Mail</p>
              <input
                @blur="validOrInvalidEmail"
                v-model="email"
                class="rightPageContentInputfield"
                type="text"
                placeholder
                required
                id="email"
              />
              <p class="rightPageContentGrey">Passwort</p>
              <input
                @blur="validOrInvalidPassword"
                v-on:input="passwordStrongTestLogin"
                v-model="passwordlogin"
                class="rightPageContentInputfield"
                type="password"
                placeholder
                required
                id="password"
              />
              <br />
              <button
                :disabled="this.passwordStrong != true"
                class="rightPageContentLoginbutton"
              >LOGIN</button>
              <button @click="oauthLogin()" value="G+" class="rightPageContentGooglebutton">
                <i class="fa fa-google-plus" style="color: #db4a39; font-size: 26px"></i>
              </button>
              <p class="rightPageContentText">
                Noch keinen Account?
                <span
                  style="color:#002c6b; cursor: pointer;"
                  id="createAccountButton"
                  @click="createSwitch()"
                >
                  Erstelle
                  einen!
                </span>
              </p>
            </div>

            <div class="registerInactive" id="rightPageContentRegister">
              <h1>Willkommen!</h1>
              <br />

              <p class="rightPageContentGrey">Name</p>
              <input
                v-model="name"
                id="name"
                class="rightPageContentInputfield"
                type="text"
                placeholder
                required
                @blur="validOrInvalidName"
              />
              <p class="rightPageContentGrey">E-Mail</p>
              <input
                @blur="validOrInvalidEmailCreate"
                v-model="emailCreate"
                class="rightPageContentInputfield"
                type="text"
                placeholder
                required
                id="emailCreate"
              />
              <p class="rightPageContentGrey">Passwort</p>
              <input
                v-on:input="passwordStrongTestCreate"
                class="rightPageContentInputfield"
                v-model="password1"
                type="password"
                placeholder
                required
                id="password1"
                @blur="validOrInvalidPasswordCreate1"
              />
              <p class="rightPageContentGrey">Passwort wiederholen</p>
              <input
                v-on:input="passwordStrongTestCreate"
                class="rightPageContentInputfield"
                v-model="password2"
                type="password"
                placeholder
                required
                id="password2"
                                @blur="validOrInvalidPasswordCreate2"

              />
              <br />
              <button
                :disabled="this.passwordStrongCreate != true"
                class="rightPageContentLoginbutton"
                style="width: 304px;"
              >REGISTRIEREN</button>

              <p class="rightPageContentText">
                Du hast schon einen Account?
                <span
                  style="color:#002c6b; cursor: pointer;"
                  id="loginAccountButton"
                  @click="loginSwitch()"
                >Zum Login!</span>
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="footer">
      <div class="geomap">
        <iframe
          src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d2659.810763052766!2d16.39565561632648!3d48.19099747922772!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x476d075e036ac393%3A0x9326dcbe2d63c038!2sHTL%20Rennweg!5e0!3m2!1sde!2sat!4v1596491956547!5m2!1sde!2sat"
          width="100%"
          height="300"
          frameborder="0"
          style="border:0;"
          allowfullscreen
          aria-hidden="false"
          tabindex="0"
        ></iframe>
      </div>
      <div class="copyright">
        © ROS 2020
        <span style="margin: 5px;">|</span>
        <a href="#">Impressum</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      passwordlogin: "",
      password1: "",
      password2: "",
      email: "",
      emailCreate: "",
      name: "",
      regexPassword: /^(?=.*?[A-Z])(?=.*?[a-z])(?=.*?[0-9])(?=.*?[#?!@$%^&*-]).{8,}$/,
      regexEmail: /^\S+@\S+\.\S+$/,
      regexName: /^[a-z ,.'-]+$/i,
      passwordStrong: false,
      passwordStrongCreate: false,
      emailStrong: false,
      nameValid: false
    };
  },
  methods: {
    firstSlideActive() {
      document.getElementById("navLabel1").classList.add("sliderButtonActive");
      document
        .getElementById("navLabel2")
        .classList.remove("sliderButtonActive");
    },
    secondSlideActive() {
      document
        .getElementById("navLabel1")
        .classList.remove("sliderButtonActive");
      document.getElementById("navLabel2").classList.add("sliderButtonActive");
    },
    createSwitch() {
      document
        .getElementById("rightPageContentLogin")
        .classList.remove("loginActive");
      document
        .getElementById("rightPageContentLogin")
        .classList.add("loginInactive");

      document
        .getElementById("rightPageContentRegister")
        .classList.remove("registerInactive");
      document
        .getElementById("rightPageContentRegister")
        .classList.add("registerActive");
    },
    loginSwitch() {
      document
        .getElementById("rightPageContentLogin")
        .classList.remove("loginInactive");
      document
        .getElementById("rightPageContentLogin")
        .classList.add("loginActive");

      document
        .getElementById("rightPageContentRegister")
        .classList.remove("registerActive");
      document
        .getElementById("rightPageContentRegister")
        .classList.add("registerInactive");
    },
    passwordStrongTestLogin() {
      if (this.regexPassword.test(this.passwordlogin)) {
        this.passwordStrong = true;
      } else {
        this.passwordStrong = false;
      }
    },
    passwordStrongTestCreate() {
      if (
        this.regexPassword.test(this.password1) &&
        this.regexPassword.test(this.password2)
      ) {
        this.passwordStrongCreate = true;
        console.log("true");
      } else {
        this.passwordStrongCreate = false;
        console.log("false");
      }
    },

    validOrInvalidEmail() {
      if (this.regexEmail.test(this.email)) {
        document.getElementById("email").classList.add("inputValid");
        document.getElementById("email").classList.remove("inputInvalid");
      } else {
        document.getElementById("email").classList.add("inputInvalid");
        document.getElementById("email").classList.remove("inputValid");
      }
    },
    validOrInvalidPassword() {
      if (this.regexPassword.test(this.passwordlogin)) {
        document.getElementById("password").classList.add("inputValid");
        document.getElementById("password").classList.remove("inputInvalid");
      } else {
        document.getElementById("password").classList.add("inputInvalid");
        document.getElementById("password").classList.remove("inputValid");
      }
    },
    validOrInvalidName() {
      if (this.regexName.test(this.name)) {
        document.getElementById("name").classList.add("inputValid");
        document.getElementById("name").classList.remove("inputInvalid");
      } else {
        document.getElementById("name").classList.add("inputInvalid");
        document.getElementById("name").classList.remove("inputValid");
      }
    },
    validOrInvalidEmailCreate() {
      if (this.regexName.test(this.name)) {
        document.getElementById("emailCreate").classList.add("inputValid");
        document.getElementById("emailCreate").classList.remove("inputInvalid");
      } else {
        document.getElementById("emailCreate").classList.add("inputInvalid");
        document.getElementById("emailCreate").classList.remove("inputValid");
      }
    },
    validOrInvalidPasswordCreate1() {
      if (this.regexPassword.test(this.password1)) {
        document.getElementById("password1").classList.add("inputValid");
        document.getElementById("password1").classList.remove("inputInvalid");
      } else {
        document.getElementById("password1").classList.add("inputInvalid");
        document.getElementById("password1").classList.remove("inputValid");
      }
    },
    validOrInvalidPasswordCreate2() {
      if (this.regexPassword.test(this.password2)) {
        document.getElementById("password2").classList.add("inputValid");
        document.getElementById("password2").classList.remove("inputInvalid");
      } else {
        document.getElementById("password2").classList.add("inputInvalid");
        document.getElementById("password2").classList.remove("inputValid");
      }
    }
  }
};
</script>


<style scoped>
.wrapper {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  box-shadow: 0px 0px 13px 1px rgba(0, 0, 0, 0.75);
}

.loginForm {
  width: 80vw;
  height: 70vh;
}

.leftPage {
  width: 50%;
  height: 100%;
  background-color: #0044b2;
  /*  background-color: grey; */
  float: left;
  display: flex;
}

.rightPage {
  width: 50%;
  height: 100%;
  background-color: #eee;
  margin-left: 50%;
}

.rightPageContent {
  position: relative;
  top: 50%;
  transform: translateY(-50%);
  display: grid;
  align-content: center;
  justify-content: center;
}

.rightPageContentGrey {
  color: #000;
  margin-bottom: 4px;
  font-size: 18px;
  font-weight: 300;
}

.rightPageContentInputfield {
  width: 300px;
  border-color: #adadad;
  border-top: none;
  border-left: none;
  border-right: none;
  outline: none;
  background-color: #eee;
  font-size: 16px;
  color: black;
  padding: 2px;
}

::placeholder {
  color: black;
}

.rightPageContentLoginbutton {
  width: 150px;
  height: 40px;
  margin-top: 20px;
  margin-right: 0.1vw;
  border-radius: 5px;
  color: #0044b2;
  border-color: #0044b2;
  border-width: 1.4px;
  font-weight: 300;
  font-size: 18px;
  cursor: pointer;
  transition: opacity 0.5s ease-out;
  -moz-transition: opacity 0.5s ease-out;
  -webkit-transition: opacity 0.5s ease-out;
  -o-transition: opacity 0.5s ease-out;
}
.rightPageContentLoginbutton:disabled {
  opacity: 40%;
}
.rightPageContentGooglebutton {
  width: 150px;
  height: 40px;
  margin-top: 21px;
  border-radius: 5px;
  border-color: #db4a39;
  border-width: 1.5px;
  position: relative;
  top: 3px;
  cursor: pointer;
}

.rightPageContentLogo {
  height: 80px;
  margin: 10px;
  position: absolute;
}

.rightPageContentText {
  font-size: 12px;
  position: relative;
  left: 50px;
}

.loginActive {
  display: inline;
}

.registerActive {
  display: inline;
}

.loginInactive {
  display: none;
}

.registerInactive {
  display: none;
}

.slidershow {
  position: relative;
  width: 700px;
  height: 400px;
  overflow: hidden;
  margin: auto;
}

.navigation {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
}

.bar {
  width: 12px;
  height: 12px;
  border: 0.5px solid #000;
  background: #002c6b;
  border-radius: 100px;
  margin: 380px 10px 0px;
}

.bar:hover {
  background-color: #eee;
  cursor: pointer;
}

input[name="r"] {
  position: absolute;
  visibility: hidden;
}

.slides {
  width: 500%;
  height: 100%;
  display: flex;
}

.slide {
  width: 20%;
  transition: 0.6s;
  min-width: 20%;
}

.slide img {
  width: 100%;
  height: 100%;
  object-fit: contain;
}
h1 {
  margin-bottom: 0;
  text-align: center;
}
#r1:checked ~ .s1 {
  margin-left: 0;
}

#r2:checked ~ .s1 {
  margin-left: -20%;
}

.sliderButtonActive {
  background-color: #eee;
}
.footer {
  position: absolute;
  bottom: -400px;
  left: 0;
  background-color: #10222e;
  width: 100%;
  height: 400px;
  margin: 0px;
  -webkit-box-shadow: 0px -5px 10px 0px rgba(0, 0, 0, 0.75);
  -moz-box-shadow: 0px -5px 10px 0px rgba(0, 0, 0, 0.75);
  box-shadow: 0px -5px 10px 0px rgba(0, 0, 0, 0.75);
}

.geomap {
  display: flex;
  justify-content: center;
  margin: 15px;
}

.copyright {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 60px;
  letter-spacing: 1px;
  color: #eee;
}

a {
  text-decoration: none;
  color: #eee;
}

.inputValid {
  border-color: #0044b2;
  transition: ease-in-out 0.5s;
}
.inputInvalid {
  border-color: #cc0000;
  transition: ease-in-out 0.5s;
}
</style>