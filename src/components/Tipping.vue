<template>
  <div class="pt-12 pl-12 w-auto">
    <h1 class="font-black">Tipping Totals - 2023</h1>
    <table class="table-auto border mt-6">
      <thead>
        <tr class="bg-gray-200">
          <th class="px-4">Name</th>
          <th class="px-4">Total</th>
          <th class="px-4 font-bold" v-for="(item, key) in getSortedTips()[0].tips" :key="key">Rd {{ getSortedTips()[0].tips.length - key }}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="tipper in getSortedTips()" :key="tipper.name">
          <td class="px-4">{{ tipper.name }}</td>
          <td class="px-4">{{ tipper.total }}</td>
          <td class="px-4" :class="{ 'bg-yellow-300': round === 9 }" v-for="round in tipper.reversedTips" :key="round.id">{{ round }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import Tips from '@/tips.json';

export default {
  name: 'Tipping',
  methods: {
    getSortedTips() {
      const tips = Tips.map((element) => {
        element.total = element.tips.reduce((result, item) => {
          return result + item;
        }, 0);
        element.reversedTips = [...element.tips]
        element.reversedTips.reverse();
        return element;
      });
      tips.sort((a, b) => {
        if (a.total < b.total) {
          return 1;
        }
        if (a.total > b.total) {
          return -1;
        }
        return 0;
      });
      console.log(tips);

      return tips;
    }
  }
}
</script>

<style scoped>
  tbody tr:nth-child(odd) {
    @apply bg-gray-100;
  }
</style>
