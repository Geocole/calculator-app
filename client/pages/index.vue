<template>
  <div class="container">
    <div class="header">
      <h2>Calculator</h2>
    </div>
    <div class="main">
      <div class="card mt-4">
        <div class="w-100 flex align-center flex-column">
          <form @submit.prevent="submit">
            <label for="password">Enter the number please</label>
            <input
              v-model="number1"
              type="number"
              placeholder="Number 1"
              required="required"
              class="mt-2 mb-2 py-2 py-3"
            />
            <input
              v-model="number2"
              type="number"
              placeholder="Number 2"
              required="required"
              class="py-2 py-3"
            />

            <button
              type="submit"
              class="submit-btn mt-2"
              :disabled="!number1 || !number2"
            >
              Sum
            </button>
          </form>

          <div class="divisor"></div>

          <div class="flex justify-center align-center flex-column w-100">
            <label for="result" class="block mt-4">Results</label>

            <input
              id="result"
              v-model="result"
              readonly
              name="result"
              type="number"
              required="required"
              class="py-2 py-3 mt-2"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      number1: null,
      number2: null,
      result: null,
    }
  },
  watch: {
    number1() {
      if (this.result) {
        this.result = null
      }
    },
    number2() {
      if (this.result) {
        this.result = null
      }
    },
  },
  methods: {
    submit() {
      const { number1, number2 } = this
      this.$axios
        .post('/calculate', {
          number1,
          number2,
        })
        .then(({ data }) => {
          this.result = data.result
        })
        .catch((error) => {
          console.log(error)
        })
    },
  },
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}

.header {
  display: flex;
  justify-content: center;
  padding: 1rem;
  background-color: #b91c1c;
  color: white;
  font-size: 1.5rem;
  font-weight: 500;
}

.main {
  display: flex;
  justify-content: center;
  padding: 1rem;
}

.card {
  padding: 1rem;
  min-width: 50%;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
}

form {
  display: flex;
  flex-direction: column;
  padding: 1rem;
  align-items: center;
  max-width: 28rem;
  width: 100%;
}
input {
  font-size: 0.875rem;
  line-height: 1.25rem;
  border-radius: 0.375rem;
  border-width: 1px;
  border-radius: 0.375rem;
  padding-top: 0.5rem;
  padding-right: 0.75rem;
  padding-bottom: 0.5rem;
  padding-left: 0.75rem;
  border-color: #e5e7eb !important;
  width: 15rem;
}

.mt-2 {
  margin-top: 1rem;
}
.mb-2 {
  margin-bottom: 1rem;
}

.mt-4 {
  margin-top: 2rem;
}

.submit-btn {
  background-color: #b91c1c;
  color: white;
  font-size: 1rem;
  width: 15rem;
  border-color: transparent;
  border-width: 1;
  border-radius: 0.375rem;
  padding: 0.5rem;
}

.py-2 {
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
}
.px-3 {
  padding-left: 0.75rem;
  padding-right: 0.75rem;
}
.divisor {
  height: 1px;
  width: 100%;
  background-color: #b91c1c;
  margin-top: 10px;
  margin-bottom: 10px;
}
.w-100 {
  width: 100%;
}

.flex {
  display: flex;
}

.flex-column {
  flex-direction: column;
}

.justify-center {
  justify-content: center;
}
.align-center {
  align-items: center;
}
#result {
  border-color: #b91c1c;
}
.block {
  display: block;
}

*,
::after,
::before {
  box-sizing: border-box;
  border-width: 0;
  border-style: solid;
  border-color: #e5e7eb;
}
</style>
