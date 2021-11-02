<template>
  <div class="popup-bg">
    <div class="popup-wizard">
      <div class="popup-wizard-content">
        <svg
          data-v-71dcf00a=""
          width="17"
          height="17"
          viewBox="0 0 17 17"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
          class="close-button"
          @click="close()"
        >
          <path
            data-v-71dcf00a=""
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M11.5046 8.19899L16.3769 3.49921C17.2077 2.69781 17.2077 1.40245 16.3769 0.601051C15.5461 -0.20035 14.2031 -0.20035 13.3723 0.601051L8.5 5.30083L3.62768 0.601051C2.79686 -0.20035 1.45394 -0.20035 0.623117 0.601051C-0.207706 1.40245 -0.207706 2.69781 0.623117 3.49921L5.49544 8.19899L0.623117 12.8988C-0.207706 13.7002 -0.207706 14.9955 0.623117 15.7969C1.03747 16.1966 1.58143 16.3975 2.1254 16.3975C2.66936 16.3975 3.21333 16.1966 3.62768 15.7969L8.5 11.0972L13.3723 15.7969C13.7867 16.1966 14.3306 16.3975 14.8746 16.3975C15.4186 16.3975 15.9625 16.1966 16.3769 15.7969C17.2077 14.9955 17.2077 13.7002 16.3769 12.8988L11.5046 8.19899Z"
            fill="#3C3C3C"
          ></path>
        </svg>
        <div class="" v-if="pageState === 0">
          <h2 class="delete-header">Please, login to proceed</h2>
          <div class="links">
            <span>Don't have an account?</span>
            <a @click="changePage(1)">Sign up now</a>
          </div>
          <ul
            v-if="loginError"
            role="alert"
            class="woocommerce-error"
            style="margin-bottom: 0"
          >
            <li>
              <strong>Error:</strong>
              {{ loginErrorMessage }}
            </li>
          </ul>

          <div class="form-wrapper">
            <p class="form-group">
              <label for="username">Email address</label>
              <input name="email" id="username" />
            </p>
            <p style="margin-bottom: 0px" class="form-group">
              <label for="password">Password</label>
              <input name="password" type="password" id="password" />
            </p>

            <div class="remember">
              <input type="checkbox" id="remember_me" />
              <label for="remember_me">Remember me</label>
              <a>Lost your password?</a>
            </div>
          </div>

          <div class="button-row">
            <button
              class="ms-button-wide ms-outlined-button txt-center"
              @click="close()"
            >
              CANCEL
            </button>
            <button
              class="ms-button-wide ms-filled-button btn-second"
              @click="login()"
            >
              LOGIN
            </button>
          </div>
        </div>
        <div class="" v-if="pageState === 1">
          <h2 class="delete-header">Sign up</h2>
          <div class="links">
            <span>Already have an account?</span>
            <a @click="changePage(0)">Login here</a>
          </div>

          <ul
            v-if="signupError"
            role="alert"
            class="woocommerce-error"
            style="margin-bottom: 0"
          >
            <li>
              <strong>Error:</strong>
              {{ signupErrorMessage }}
            </li>
          </ul>

          <div class="form-wrapper">
            <p class="form-group">
              <label for="email">Email address</label>
              <input name="email" id="reg_email" />
            </p>
            <p style="margin-bottom: 0px" class="form-group">
              <label for="password">Password</label>
              <input name="password" type="password" id="reg_password" />
            </p>

            <div class="remember" style="margin-right: -30px">
              <input type="checkbox" id="receive" checked />
              <label for="receive">
                I want to receive updates about products & promotions.</label
              >
            </div>
          </div>

          <div class="button-row">
            <button
              class="ms-button-wide ms-outlined-button txt-center"
              @click="close()"
            >
              CANCEL
            </button>
            <button
              class="ms-button-wide ms-filled-button btn-second"
              @click="register()"
            >
              SIGN UP
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { loginAndGetJwt } from '../../components/apiFunctions.js'

export default {
  data() {
    return {
      newEmail: '',
      password: '',
      pageState: 0, /// login
      loginError: false,
      loginErrorMessage: 'No error.',
      signupError: false,
      signupErrorMessage: 'No error.',
    }
  },
  mounted() {},
  beforeDestroy() {},
  methods: {
    close() {
      console.log('close auth popup')
      $nuxt.$emit('close-auth-popup')
    },
    changePage(state) {
      this.pageState = state
    },
    async register() {
      const registerStatus = await this.$axios.$post(
        this.$store.state.apiConfiguration.baseUrl +
          this.$store.state.apiConfiguration.urlRegister,
        {
          email: document.getElementById('reg_email').value,
          password: document.getElementById('reg_password').value,
          status: 'active',
        }
      )
      // the result
      if (registerStatus.status === 1) {
        // login the user
        if (
          loginAndGetJwt(
            document.getElementById('reg_email').value,
            document.getElementById('reg_password').value,
            this.$axios,
            this.$store
          )
        ) {
          $nuxt.$emit('close-auth-popup')
          this.$router.push({
            path: '/wizard',
          })
        }
      } else {
        // show the error
        this.signupError = true
        this.signupErrorMessage = 'Account with this email already exists.'
      }
    },
    login() {
      if (
        loginAndGetJwt(
          document.getElementById('username').value,
          document.getElementById('password').value,
          this.$axios,
          this.$store
        )
      ) {
        $nuxt.$emit('close-auth-popup')
        this.$router.push({
          path: '/wizard',
        })
      } else {
        this.loginError = true
        this.loginErrorMessage = 'Wrong credentials'
      }
    },
  },
}
</script>

<style scoped>
.delete-header {
  font-family: Nunito;
  font-style: normal;
  font-weight: 800;
  font-size: 32px;
  line-height: 38px;
  text-align: left;
  letter-spacing: -0.9856px;
  color: #3c3c3c;
  display: block;
  margin-left: auto;
  margin-right: auto;
}

h2 {
  font-family: Nunito;
  font-style: normal;
  font-weight: 800;
  font-size: 44px;
  line-height: 54px;
  max-width: 516px;
  color: #3c3c3c;
  margin-top: 0;
  margin-bottom: 5px;
}

.links {
  font-size: 15px;
  letter-spacing: 0.5px;
}

.links a {
  cursor: pointer;
  margin-left: 10px;
  text-decoration: underline;
  font-weight: bold;
}

a:hover,
a:active {
  color: #3cbb8a;
}

.form-wrapper {
  padding: 30px;
}

.form-group label {
  font-family: Nunito;
  font-style: normal;
  font-weight: 800;
  font-size: 16px;
  line-height: 22px;
  color: #a4b6c0;
}

.form-group input {
  background: #ffffff;
  border: 2px solid #e0e9ef;
  box-sizing: border-box;
  border-radius: 8px;
  transition: 200ms ease;
  font-weight: 800;
  font-size: 14px;
  line-height: 19px;
  letter-spacing: -0.4032px;
  color: #3c3c3c;
  height: 48px;
  caret-color: #34bc89;
  width: 100%;
}

.form-wrapper input[type='checkbox'] {
  width: 16px;
  height: 16px;
  vertical-align: sub;
}

.form-wrapper p {
  margin-bottom: 10px;
}

.remember label {
  font-size: 15px;
  margin-left: 10px;
}

.remember a {
  cursor: pointer;
  margin-left: 10px;
  text-decoration: underline;
  font-weight: bold;
  float: right;
  font-size: 15px;
  margin-top: 5px;
}

.ms-button-wide {
  width: 215px;
  text-align: center;
}
.btn-second {
  margin-left: 20px;
}
</style>