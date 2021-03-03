<template>
  <div>
    <Header />
    <main class="md:w-4/12 p-10">
      <h1 class="my-4 text-xl font-bold">
        How well do you know the world’s capital cities?
      </h1>
      <p class="mb-4">
        In this quiz you’ll be presented with the names of
        {{ countries.length }} countries. You’ll need to match them to their
        capital city.
      </p>
      <form v-on:submit="validateAnswers">
        <div class="mb-4">
          <label
            class="block mb-2 text-sm font-bold text-gray-700"
            for="country"
          >
            Choose a country from the list:</label
          >
          <select
            id="country"
            class="px-3 py-2 leading-tight text-gray-700 border rounded shadow focus:outline-none focus:shadow-outline w-full"
            @change="changeCountry($event)"
            required
          >
            <option value="">Select country</option>
            <option
              v-for="country in countries"
              :value="country.alpha2Code"
              :key="country.alpha2Code"
            >
              {{ country.name }}
            </option>
          </select>
        </div>

        <div class="mb-4">
          <label
            class="block mb-2 text-sm font-bold text-gray-700"
            for="capital"
          >
            What is the capital?
          </label>
          <input
            type="text"
            id="capital"
            class="px-3 py-2 leading-tight text-gray-700 border rounded shadow focus:outline-none focus:shadow-outline w-full"
            v-model="answer"
            autocomplete="off"
            required
          />
        </div>
        <button
          type="submit"
          class="px-4 py-2 font-bold text-white bg-green-600 rounded hover:bg-green-900"
        >
          Check
        </button>
      </form>
      <div class="mt-6" v-show="showResults">
        <p class="flex">
          <img
            width="24"
            class="mr-2"
            :src="selectedCountry.flag"
            :alt="selectedCountry.name"
          />{{ selectedCountry.name }}
        </p>
        <p><strong>Capital:</strong> {{ selectedCountry.capital }}</p>
        <hr class="mt-2 mb-2" />
        <p>{{ message }}</p>
      </div>
    </main>
  </div>
</template>
<script>
import Header from '../components/Header.vue'
export default {
  name: 'App',
  data() {
    return {
      countries: [],
      showResults: false,
      message: '',
      selectedCountry: {},
      answer: '',
    }
  },
  created() {
    this.getCountries()
  },
  components: {
    Header,
  },
  methods: {
    async getCountries() {
      const res = await fetch('https://restcountries.eu/rest/v2/all')
      const data = await res.json()
      this.countries = data
    },
    validateAnswers: function (e) {
      e.preventDefault()
      this.showResults = true
      if (this.answer === this.selectedCountry.capital) {
        this.message = '🥳 Your answer is correct.'
      } else {
        this.message = '😕 Your answer is not correct. You can try again!'
      }
    },
    changeCountry(event) {
      this.selectedCountry = this.countries.find(
        (country) => country.alpha2Code === event.target.value
      )
      this.showResults = false
      this.answer = ''
    },
  },
}
</script>
