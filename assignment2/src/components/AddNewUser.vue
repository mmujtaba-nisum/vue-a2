<template>
  <div>
    <form>
      <div>
        <label for="firstname" class="form-label">First Name</label>
        <input
          type="text"
          class="form-control"
          id="firstname"
          v-model="firstname"
        />
      </div>
      <div>
        <label for="lastname" class="form-label">Last Name</label>
        <input
          type="text"
          class="form-control"
          id="lastname"
          v-model="lastname"
        />
      </div>
      <div >
        <label for="email" class="form-label">Email</label>
        <input type="email" class="form-control" id="email" v-model="email" />
      </div>
      <div >
        <label for="password" class="form-label">Password</label>
        <input
          type="password"
          class="form-control"
          id="password"
          v-model="password"
        />
      </div>
      <div class="btn-div">
        <button type="button" @click="addUser" >
          {{ title }}
        </button>
        <button type="button" @click="cancel">
          Cancel
        </button>
      </div>
    </form>
    <hr />
  </div>
</template>
<script>
export default {
  props: ['title'],
  data() {
    return {
      firstname: '',
      lastname: '',
      email: '',
      password: '',
      confirmPassword: '',
    }
  },
  methods: {
    async addUser(e) {
      e.preventDefault()
      let newUser = {
        firstname: this.firstname,
        lastname: this.lastname,
        email: this.email,
        password: this.password,
      }
      await this.fetchRandomRollNum(newUser)
        this.$emit('userAdded', newUser)
    },
    async fetchRandomRollNum(user) {
      const response = await fetch(
        'https://www.random.org/integers/?num=1&min=0&max=1000&col=1&base=10&format=plain&rnd=new'
      )
      if (response.status == 200) {
        let rollNum = await response.json()
        user['rollNo'] = rollNum
      }
    },
    cancel() {
      this.$emit('cancel', true)
    },
  },
}
</script>
<style scoped>
.error {
  color: red;
}
.btn-div {
  display: flex;
}
</style>