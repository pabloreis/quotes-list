<template>
  <div class="quotes">
    <ul>
      <li v-for="(quoteItem, i) in quotesList" :key="quoteItem.quote">
        <p>
          {{ quoteItem.quote }}
          <button @click="removeQuote(i)">X</button>
        </p>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import {
  Component,
  Prop,
  Emit,
  Vue,
} from 'vue-property-decorator';

import { IQuote } from '../settings/types';

@Component
export default class Quotes extends Vue {
  @Prop({ required: true, type: Array }) public quotes!: IQuote[];

  private quotesList: IQuote[] = this.quotes;

  @Emit('removingQuote')
  removeQuote(quoteIndex: number): IQuote[] | [] {
    this.quotesList.splice(quoteIndex, 1);

    return this.quotesList;
  }
}
</script>

<style>
.quotes ul {
  list-style: none;
}

.quotes ul li button {
  background: #000;
  color: #fff;
  padding: 5px;
  border-radius: 4px;
}
</style>
