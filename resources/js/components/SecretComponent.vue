<template>
  <div class="container">
    <!--login form -->
    <div class="row mt-4">
      <div class="col-6 offset-3">
        <form action="#" @submit.prevent="handleLogin">
          <h3>Sign in for secrets</h3>

          <div class="form-row">
            <input
              v-model="formData.email"
              type="email"
              name="email"
              class="form-control"
              placeholder="Email Address"
            />
          </div>
          <div class="form-row">
            <input
              v-model="formData.password"
              type="password"
              name="password"
              class="form-control"
              placeholder="Password"
            />
          </div>
          <div class="form-row">
            <button type="submit" name="Submit" class="btn btn-primary">
              Sign In
            </button>
          </div>
        </form>
      </div>
    </div>

    <!-- Secret List -->
  </div>
</template>

<script>
export default {
  data() {
    return { secrets: [], formData: { emai: "", password: "" } };
  },
  methods: {
    handleLogin() {
      // send axios request to the login
      axios.get("/sanctum/csrf-cookie").then((response) => {
        // Login...
        axios.post("login", this.formData).then((response) => {
          //console.log(response);
          this.getSecrets();
        });
      });
    },
    getSecrets() {
      axios.get("/api/secrets").then((response) => {
        console.log(response);
      });
    },
  },
};
</script>
<style>
.form-control {
  margin-bottom: 5px;
}
</style>