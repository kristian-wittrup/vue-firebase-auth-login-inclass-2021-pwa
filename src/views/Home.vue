<template>
  <div class="home">
    <h1>Welcome {{ name }}</h1>

    <button @click="logout">
      Logout
    </button>
  </div>
</template>

<script>
import firebase from 'firebase'
import { ref, onBeforeMount } from 'vue'

export default {
  name: 'Home',


  setup() {
    const name = ref("")
    
    onBeforeMount(() => {
      const user = firebase.auth().currentUser
      console.log("testUserInfo", user.email)
      if (user ) {
        name.value = user.email.split('@')[0]
      }
    })

    const logout = () => {
      firebase
      .auth()
      .signOut()
      .then(() =>{
        // sign out succes
      }).catch((error) => {
        console.log("err", error.message)
      })
    }

    return { logout, name }
  }

}
</script>
