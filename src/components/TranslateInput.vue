<template>
  <section class="input" :class="{ 'large': showOutput}">
    <div class="input__inner">
      <form @submit.prevent="onSubmit">
        <input v-model="inputText" placeholder="Enter a text and hit enter..." type="text" />
        <button>Submit</button>
      </form>
      <div class="filter">
       <div class="filter__item">
          <a href="#" :data-code="selectedInput.code" class="filter__active">{{selectedInput.name}}</a>
          <ul class="filter__submenu">
            <li v-for="(val, key) in availableLangs" :value="key">
              <a href="#" :data-code="key" @click="selectInput" class="filter__link">{{val}}</a>
            </li>
          </ul>
        </div>
        <button @click="swapLanguages" class="filter__btn">
          <svg data-v-413a05e0="" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 503 389.8">
            <path data-v-413a05e0="" d="M0 277.4c1.4-1.2 2.8-2.3 4.1-3.5l103.2-103.2c1.3-1.3 2.1-2.9 3.2-4.4.5.3 1 .6 1.4.9v82.6H308v56.3H112.2v83.8c-2.1-2-3.5-3.1-4.7-4.3-34.5-34.7-69.2-69.3-103.8-104-1.2-1.2-2.5-2.2-3.7-3.3v-.9zM392.7 81.5V0c36.7 36.8 73.7 73.7 110.2 110.3L393 220.2V138H196.8V81.5h195.9z"></path>
          </svg>
        </button>
        <div class="filter__item">
           <a href="#" :data-code="selectedOutput.code" class="filter__active">{{selectedOutput.name}}</a>
           <ul class="filter__submenu">
             <li v-for="(val, key) in availableLangs" :value="key">
               <a href="#" :data-code="key" @click="selectOutput" class="filter__link">{{val}}</a>
             </li>
           </ul>
         </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'translate-input',
  data () {
    return {
      inputText: '',
      selectedInput: {
        code: 'en',
        name: 'English'
      },
      selectedOutput: {
        code: 'en',
        name: 'English'
      },
      availableLangs: []
    }
  },
  methods: {
    getLanguages() {
      axios.get('https://translate.yandex.net/api/v1.5/tr.json/getLangs?key=trnsl.1.1.20170428T183043Z.66775f62c06e5c81.d7f498c6dee3489a640909d96aaa394e0267bcb5&ui=en')
      .then(response => {
        this.availableLangs = response.data.langs
      })
    },

    swapLanguages() {
      const selectedInput = this.selectedInput;
      this.selectedInput = this.selectedOutput
      this.selectedOutput = selectedInput
    },

    selectInput(e) {
      e.preventDefault();
      this.selectedInput.code = e.target.dataset.code;
      this.selectedInput.name = e.target.innerHTML;
    },

    selectOutput(e) {
      e.preventDefault();
      this.selectedOutput.code = e.target.dataset.code;
      this.selectedOutput.name = e.target.innerHTML;
    },

    onSubmit() {
      if(this.inputText.trim().length !== 0) {
        Events.$emit('translate', this.inputText, this.selectedOutput.code, this.selectedOutput.code);
      }
    }
  },
  watch: {
    'selectedInput.code': 'onSubmit',
    'selectedOutput.code': 'onSubmit',
  },
  computed: {
    showOutput() {
      return this.inputText.trim().length == 0
    }
  },
  mounted() {
    this.getLanguages()
  }
}
</script>

<style>

</style>
