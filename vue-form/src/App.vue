<template>
  <div>
    <!-- <progress-bar></progress-bar> -->
    <ProgressBar></ProgressBar>
    <form v-on:submit.prevent="submitForm">
      <div>
        <label for="username">ID:</label>
        <input
          id="username"
          type="text"
          v-model="username"
          class="username-input"
          v-bind:class="{ 'error': isError}"
        />
      </div>
      <div>
        <label for="password">PW:</label>
        <input id="password" type="password" v-model="password" />
      </div>
      <button v-bind:disabled="!isUsernameValid" type="submit">LOGIN</button>
    </form>
    <p v-if="isSuccess">로그인이 되었습니다</p>
    <!-- <p v-if="isError">옳바르지 않은 ID 입니다</p>
    <p v-if="isUsernameValid">이메일 형식이 맞습니다</p>-->
    <toast-popup v-bind:open="isSuccess" v-on:close="isSuccess = false"></toast-popup>
  </div>
</template>

<script>
import ToastPopup from "@/components/ToastPopup.vue";
import ProgressBar from "@/components/ProgressBar.vue";

function validateEmail(email) {
  const re = /^(([^<>()[\]\\.,;:\s@\"]+(\.[^<>()[\]\\.,;:\s@\"]+)*)|(\".+\"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
  return re.test(email);
}

export default {
  components: {
    ToastPopup,
    ProgressBar
  },
  data() {
    return {
      username: "",
      password: "",
      isError: false,
      isSuccess: false
    };
  },
  computed: {
    isUsernameValid() {
      return validateEmail(this.username);
    }
  },
  methods: {
    submitForm() {
      console.log("log in");
      // axios.post().then().catch(err => { this.isError = true})
      // this.isError = true;
      // this.initForm();
      this.isSuccess = true;
    },
    initForm() {
      this.username = "";
      this.password = "";
    }
  }
};
</script>

<style>
body {
  margin: 0;
}
form {
  padding: 5px 10px;
}
.username-input {
  outline: none;
}
.username-input.error {
  border: 1px solid red;
}
</style>