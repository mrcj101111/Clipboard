<template>
    <div class="tile" style="margin:auto;">
        <div class="tile-header">
        <h2 >SIGN UP</h2>
    </div>
    <div class="tile-body">
        <form id="form">
            <label class="form-input">
                    <input type="text" v-model="userName" autofocus="true" required />
                    <span class="label">Username</span>
                <span class="underline"></span>
            </label>
            <label class="form-input">
                    <input type="text" v-model="email" autofocus="true" required />
                    <span class="label">Email</span>
                <span class="underline"></span>
            </label>
            <label class="form-input">
                    <input type="password" v-model="password" required />
                    <span class="label">New Password</span>
                <div class="underline"></div>
            </label>
            <div class="submit-container clearfix" style="margin-top: 2rem;">
                <div v-on:click="SignUp" id="submit" role="button" type="button" class="btn btn-irenic float-right" tabindex="0">
                    <span>SIGN UP</span>
                </div>
                <p style="padding-top: 40px;">Or click <router-link to="/Home">here</router-link> to go back to Sign in.</p>
                    <div class="login-pending">
                        <div class=spinner>
                            <span class="dot1"></span>
                            <span class="dot2"></span>
                        </div>
                    <div class="login-granted-content">
                        <i class="material-icons">done</i>
                    </div>
                </div>
            </div>
        </form>
    </div>
</div>
</template>

<script>
import firebase from 'firebase'
import db from './firebaseInit'

export default {
  name: 'Signup',
  data () {
    return {
      userName: '',
      email: '',
      password: ''
    }
  },
  methods: {
    SignUp () {
      firebase.auth().createUserWithEmailAndPassword(this.email, this.password).then(
        (user) => {
          db.collection('users').doc(firebase.auth().currentUser.uid).set({
              userName: this.userName,
              email: this.email
          })
          firebase.auth().currentUser.displayName = this.userName
          this.$router.replace('Dashboard')
        },
        (err) => {
          alert('Oops. ' + err.message)
        }
      )
    }
  }
}
</script>
