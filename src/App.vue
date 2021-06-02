<template>
  <div class="container my-5 d-md-flex justify-content-center">
    <div class="card col-md-5">
      <div class="card-body">
        <i class="fab fa-twitter d-block text-center display-1 my-3"></i>
        <!-- register an account -->
        <div v-if="!registered" class="register">
          <button
            form="register"
            type="submit"
            class="btn btn-primary mb-3 d-flex m-auto"
          >
            Register
          </button>
          <h2 class="display-6 text-center mb-3">Create your account</h2>
          <form id="register" v-on:submit.prevent="registerAccount">
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
          <h2 class="display-6 text-center mb-3">
            Welcome
            <span class="fw-bold text-capitalize">{{ userData.name }}</span>
            write your first Tweet
          </h2>
          <form v-on:submit.prevent="sendTweet">
            <div class="mb-3">
              <label for="tweet" class="form-label">
                Send your tweet
                <span class="form-text font-monospace">
                  {{ `${tweetMsg.length}/${maxTweet}` }}</span
                >
              </label>
              <textarea
                class="form-control"
                name="tweet"
                id="tweet"
                cols="30"
                rows="10"
                v-model="tweetMsg"
                maxlength="200"
                required
              ></textarea>
            </div>
            <button type="submit" class="btn btn-primary">Tweet</button>
          </form>
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
      name: "",
      email: "",
      password: "",
      maxLength: 25,
      maxPassLength: 16,
      maxTweet: 200,
      error: "",
      registered: false,
      tweetMsg: "",
      tweets: [],
    };
  },
  created() {
    // check if the user is registered and set the reigstered to true
    if (localStorage.getItem("simpleTweetRegistered") === "true") {
      this.registered = true;
    }
    // repopulate the userData object
    if (localStorage.getItem("simpleTweetRegisteredUser")) {
      this.userData = JSON.parse(
        localStorage.getItem("simpleTweetRegisteredUser")
      );
    }
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
    sendTweet() {
      // store the tweet in the tweets property
      this.tweets.unshift({
        text: this.tweetMsg,
        date: new Date().toLocaleTimeString(),
      });
      // empty the tweetMsg property
      this.tweetMsg = "";
      // add to the localStorage the stringified tweet object
      localStorage.setItem("simpleTweetTweets", JSON.stringify(this.tweets));
    },
  },
};
</script>

<style>
body {
  background: linear-gradient(to right, #00d2ff, #3a7bd5);
}
</style>
