<template>
  <div id="app">

    <button v-if="!tableData" @click="generateDummyData(50)">СОЗДАТЬ</button>

    <table v-else class="table">
      <thead>
      <tr>
        <th>Наименование</th>
        <th>Цена</th>
        <th>Количество</th>
        <th>Стоимость</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="data in tableData" v-bind:key="data.name">
        <th>{{ data.name }}</th>
        <td>{{ data.price }}</td>
        <td align="center">{{ data.amount }}</td>
        <td>{{ data.value }}</td>
      </tr>
      <tr>
        <th></th>
        <td></td>
        <td>всего:</td>
        <td>{{ totalSum }}</td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>

export default {
  data() {
    return {
      ruLetters: ['а', 'б', 'в', 'г', 'д', 'е', 'ё', 'ж', 'з', 'и', 'й', 'к', 'л', 'м', 'н', 'о', 'п', 'р', 'с', 'т', 'у', 'ф', 'х', 'ц', 'ч', 'ш', 'щ', 'э', 'ю', 'я'],
      totalSum: 0,
      tableData: null,
    }
  },
  methods: {
    random(floor, max, min = 0) {
      return (floor) ? Math.floor(Math.random() * max) + min : Math.random() * max + min;
    },
    generateName(letters, lengthOfWord) {
      let result = "";
      const lengthOfAlphabet = letters.length;
      for (let i = 0; i < lengthOfWord; i++) {
        const randomIndex = this.random(true, lengthOfAlphabet);
        result += letters[randomIndex]
      }
      return result;
    },
    generatePrice(floor, max, min = 0) {
      return this.random(floor, max, min).toFixed(2)
    },
    generateAmount(floor, max, min = 0) {
      return this.random(floor, max, min)
    },
    generateDummyData(num) {
      const result = [];
      const values = [];
      for (let i = 0; i < num; i++) {
        const name = this.generateName(this.ruLetters, 5);
        const price = this.generatePrice(false, 1000, 0.01);
        const amount = this.generateAmount(true, 100, 1);
        const value = (price * amount).toFixed(2)
        const product = {
          name,
          price,
          amount,
          value,
        }
        values.push(+value)
        result.push(product)
      }
      this.totalSum = values.reduce((prev, next) => prev + next, 0).toFixed(2)
      this.tableData = result;
    }
  }
}
</script>

<style>

</style>
