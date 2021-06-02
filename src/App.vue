<template>
  <div class="container mt-5 d-md-flex justify-content-center">
    <div class="card col-md-5">
      <div class="card-body">
        <i class="fab fa-twitter d-block text-center display-1 m-3"></i>
        <!-- register an account -->
        <div v-if="!registered" class="register">
          <button type="submit" class="btn btn-primary mb-3 d-flex m-auto">
            Register
          </button>
          <h2 class="display-6 text-center">Create your account</h2>
          <form v-on:submit.prevent="registerAccount">
            <div class="mb-3">
              <label for="name" class="form-label">Name</label>
              <span class="form-text font-monospace">
                {{ ` ${name.length}/` }}
              </span>
              <input
                type="text"
                class="form-control"
                v-model="name"
                maxlength="25"
                required
              />
            </div>
            <div class="mb-3">
              <label for="email" class="form-label">Email</label>
              <span class="form-text font-monospace">
                {{ ` ${email.length}/` }}
              </span>
              <input
                type="email"
                class="form-control"
                v-model="email"
                maxlength="25"
                required
              />
            </div>
            <div class="mb-3">
              <label for="password" class="form-label">Password</label>
              <span class="form-text font-monospace">
                {{ ` ${password.length}/` }}
              </span>
              <input
                type="password"
                class="form-control"
                v-model="password"
                maxlength="16"
                required
              />
            </div>
            <div
              v-if="error.length > 0"
              class="text-danger mb-3 fw-bold form-text"
            >
              {{ error }}
            </div>
          </form>
        </div>
        <!-- add tweet -->
        <div v-else class="tweet-box">
          <h2>Welcome {{ name }} write your first Tweet</h2>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      userData: {},
      userId: 0,
      name: "test",
      email: "test@test.com",
      password: "test",
      maxLength: 25,
      maxPassLength: 16,
      error: "",
      registered: false,
    };
  },
  methods: {
    registerAccount() {
      // record user details
      if (this.name !== "" && this.email !== "" && this.password !== "") {
        this.userData.userId = ++this.userId;
        this.userData.name = this.name;
        this.userData.email = this.email;
        this.userData.password = this.password;
      } else {
        this.error = "Complete all the form fields";
      }
      // add registration to localStorage
      localStorage.setItem("simpleTweetRegistered", true);
      // add the whole userData object as JSON string
      localStorage.setItem(
        "simpleTweetRegisteredUser",
        JSON.stringify(this.userData)
      );
      // clear the registration fields
      this.name = "";
      this.email = "";
      this.password = "";
    },
  },
};
</script>

<style>
</style>
