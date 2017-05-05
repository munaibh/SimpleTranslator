<template>
  <section class="output">
    <div class="output__inner">
      <h1 v-if="!loading" class="result">{{translatedText}}</h1>
      <div class="actions" v-if="translatedText && !loading">
         <button class="action__copy btn" data-tooltip="Copy" @click="copy">
        <svg data-v-7108712b="" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 405.4 469.7"><path data-v-7108712b="" d="M85.4 277.3c0-49 .3-98-.1-147-.2-25.2 19.3-45 44.5-44.9 77.3.4 154.6.1 231.9.2 25.5 0 43.7 18.4 43.7 43.8v295.9c0 25.3-18.2 44.1-43.6 44.2-77.6.2-155.3.2-232.9 0-25.3-.1-43.4-18.9-43.4-44.3-.1-49.2-.1-98.6-.1-147.9zm277-148.9H128.5v298.1h233.9V128.4z"></path><path data-v-7108712b="" d="M42.8 341.4H.5c-.1-1.8-.3-3.5-.3-5.3 0-97 .3-193.9-.2-290.9C-.1 21.6 17.2 0 44.8 0c83 .1 165.9 0 248.9 0 1.5 0 2.9.2 4.6.3v42.4H42.8v298.7z"></path></svg>
        </button>
         <a class="action__share btn" :href="'https://twitter.com/intent/tweet?text=' + shareMessage" target="_blank" rel="nofollow" data-tooltip="Share">
          <svg data-v-7108712b="" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 48.7 47.9"><path data-v-7108712b="" d="M40.3 31.2c-2.4 0-4.5 1-6 2.6l-17.7-8.7c.1-.4.1-.8.1-1.2 0-.4 0-.8-.1-1.2L34.3 14c1.5 1.6 3.7 2.6 6.1 2.6 4.6 0 8.3-3.7 8.3-8.3C48.7 3.7 45 0 40.4 0S32 3.7 32 8.3c0 .4 0 .8.1 1.2l-17.7 8.6c-1.5-1.6-3.7-2.6-6.1-2.6-4.6 0-8.3 3.7-8.3 8.3 0 4.6 3.7 8.3 8.3 8.3 2.4 0 4.5-1 6-2.6L32 38.2v1.3c0 4.6 3.7 8.3 8.3 8.3s8.3-3.7 8.3-8.3c.1-4.6-3.7-8.3-8.3-8.3z"></path></svg>
        </a>
        <textarea ref="copyTextArea">{{translatedText}}</textarea>
      </div>
      <div v-if="loading" class="loader"></div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'translate-output',
  data () {
    return {
      originalText: '',
      translatedText: '',
      translatedLang: '',
      loading: true,
    }
  },
  methods: {
    translateText(text, from, to) {
      this.loading = true;
      this.originalText = text
      this.translatedLang = to
      axios.get(`https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20170428T183043Z.66775f62c06e5c81.d7f498c6dee3489a640909d96aaa394e0267bcb5&ui=${from}&text=${text}&lang=${to}`)
        .then(response => {
          this.translatedText = response.data.text[0]
          this.loading = false;
        })
    },
    copy(e) {
      this.$refs.copyTextArea.select()
      document.execCommand('copy');
      e.target.dataset.tooltip = "copied"
      setTimeout(() => {
        e.target.dataset.tooltip = "copy"
      }, 1500)
    }
  },

  computed: {
    shareMessage() {
      return `Did you know ${this.originalText} is ${this.translatedText} in ${this.translatedLang}? via @SimpleTranslator`
    }
  },

  mounted() {
    Events.$on('translate', this.translateText)
  }
}
</script>

<style>

</style>
