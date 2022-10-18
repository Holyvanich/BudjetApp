<template>
  <div id="app">
    <FormApp @submitForm="onFormsSubmit" />
    <TotalBalance :total="TotalBalance" />
    <BudjetList :list="list" @deleteitem="onDeleteItem" />
  </div>
</template>

<script>
import BudjetList from '@/components/BudgetList.vue';
import TotalBalance from '@/components/TotalBalance.vue';
import FormApp from '@/components/Form.vue';

export default {
  name: 'App',
  components: {
    BudjetList,
    TotalBalance,
    FormApp,
  },
  data: () => ({
    list: {
      1: {
        type: 'INCOME',
        value: 100,
        comment: 'Some comment',
        id: 1,
      },
      2: {
        type: 'OUTCOME',
        value: -50,
        comment: 'Some outcome comment',
        id: 2,
      },
    },
  }),
  computed: {
    TotalBalance() {
      return Object.values(this.list).reduce(
        (acc, item) => acc + item.value,
        0
      );
    },
  },
  methods: {
    onDeleteItem(id) {
      this.$delete(this.list, id);
    },
    onFormsSubmit(data) {
      const newObj = {
        ...data,
        id: String(Math.random()),
      };

      this.$set(this.list, newObj.id, newObj);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
