<template>
  <v-app class="app">
    <h1>Quotes</h1>
    <Quotes :quotes="quoteInfo" v-if="quoteInfo.length"
      @removingQuote="updateQuotes" />

    <div class="buttons-container">
      <button class="buttons" @click="getQuote">Request Quote</button>
      <button class="buttons" @click="removeAllQuotes">Remove Quotes</button>
    </div>
  </v-app>
</template>

<script lang="ts">
import {
  Component,
  Vue,
} from 'vue-property-decorator';
import axios from 'axios';

import Quotes from './components/Quotes.vue';

import { IQuote } from './settings/types';

@Component({
  components: {
    Quotes,
  },
})
export default class App extends Vue {
  private quoteInfo: IQuote[] = [];

  getQuote(): void {
    axios.get<IQuote>('https://api.kanye.rest').then((res) => {
      this.quoteInfo.push(res.data);
    });
  }

  updateQuotes(newQuotesList: IQuote[]): void {
    this.quoteInfo = newQuotesList;
  }

  removeAllQuotes(): void {
    this.quoteInfo = [];
  }
}
</script>

<style>
body, html {
  margin: 0;
  padding: 0;
}

.app {
  width: 600px;
  margin: 0 auto;
  display: flex;
  text-align: center;
}

.buttons-container {
  display: flex;
  justify-content: center;
}

.buttons-container button {
  background: #000;
  color: #fff;
  padding: 5px;
  border-radius: 4px;
}

.buttons-container button:first-child {
  margin-right: 10px;
}
</style>
