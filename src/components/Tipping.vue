<template>
  <div class="pt-12 pl-12 w-auto">
    <h1 class="font-black">Tipping Totals - 2021</h1>
    <table class="table-auto border mt-6">
      <thead>
        <tr class="bg-gray-200">
          <th class="px-4">Name</th>
          <th class="px-4">Total</th>
          <th class="px-4 font-bold" v-for="(item, key) in getSortedTips()[0].tips" :key="key">Rd {{ key + 1 }}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="tipper in getSortedTips()" :key="tipper.name">
          <td class="px-4">{{ tipper.name }}</td>
          <td class="px-4">{{ tipper.total }}</td>
          <td class="px-4" v-for="round in tipper.tips" :key="round.id">{{ round }}</td>
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