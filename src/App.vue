<template>
  <div class="container mt-5 d-md-flex justify-content-center">
    <div class="card col-md-5">
      <div class="card-body">
        <i class="fab fa-twitter fa-lg fa-fw"></i>
        <h1 class="display-6">Create your account</h1>
        <form v-on:submit.prevent="registerAccount">
          <div class="mb-3">
            <label for="name" class="form-label">Name</label>
            <span class="form-text font-monospace">
              {{ ` ${name.length}/${maxLength}` }}
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
              {{ ` ${email.length}/${maxLength}` }}
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
              {{ ` ${password.length}/${maxPassLength}` }}
            </span>
            <input
              type="password"
              class="form-control"
              v-model="password"
              maxlength="16"
              required
            />
          </div>
          <button type="submit" class="btn btn-primary">Register</button>
        </form>
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
    };
  },
  methods: {
    registerAccount() {
      // record user details
      if (this.name !== "" && this.email !== "" && this.password !== "") {
        this.userData.userId = ++this.userId
        console.log(this.userData);
        console.log(this.userId);
        this.userData.name = this.name;
        this.userData.email = this.email;
        this.userData.password = this.password;
      } else {
        this.error = "Complete all the form fields";
      }
      // add registration to localStorage
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
