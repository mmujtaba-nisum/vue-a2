<template>
  <div>
    <div >
      <div>{{ title }}</div>
      <div>
          <div >
            <label for="firstname" >First Name</label>
            <input
              type="text"
              id="firstname"
              v-model="firstname"
            />
          </div>
          <div >
            <label for="lastname" >Last Name</label>
            <input
              type="text"
              id="lastname"
              v-model="lastname"
            />
          </div>
          <div >
            <label for="email" >Email</label>
            <input
              type="email"
              id="email"
              v-model="email"
            />
          </div>
          <div >
            <label for="password">Password</label>
            <input
              type="password"
              id="password"
              v-model="password"
            />
          </div>
          <button type="button" @click="register" class="btn btn-primary">
            {{ title }}
          </button>
      </div>
    </div>
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
    }
  },
  methods: {
    async register(e) {
      e.preventDefault()
      let newUser = {
        firstname: this.firstname,
        lastname: this.lastname,
        email: this.email,
        password: this.password,
      }
      await this.fetchRandomRollNum(newUser)
        this.$emit('registerUser', newUser)
    },
    async fetchRandomRollNum(newUser) {
      const response = await fetch(
        'https://www.random.org/integers/?num=1&min=0&max=1000&col=1&base=10&format=plain&rnd=new'
      )
      if (response.status == 200) {
        let rollNum = await response.json()
        newUser['rollNo'] = rollNum
      }
    },
  },
}
</script>