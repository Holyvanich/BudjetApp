<template>
  <div class="budget-list-wrap">
    <ElCard :header="header">
      <template v-if="isEmpty">
        <div class="list-item" v-for="(item, prop) in list" :key="prop">
          <span class="budget-comment">{{ item.comment }}</span>
          <span class="budget-value">{{ item.value }}</span>
          <ElButton type="danger" size="mini" @click="deleteitem(item.id)"
            >Delete</ElButton
          >
        </div>
      </template>
      <ElAlert
        v-else
        type="info"
        :title="emptyTitle"
        :closable="false"
      ></ElAlert>
    </ElCard>
  </div>
</template>

<script>
export default {
  name: 'BudgetList',
  props: {
    list: {
      type: Object,
      default: () => ({}),
    },
  },
  data: () => ({
    header: 'Budget List',
    emptyTitle: 'Empty List',
  }),
  computed: {
    isEmpty() {
      return Object.keys(this.list).length;
    },
  },
  methods: {
    deleteitem(id) {
      this.$emit('deleteitem', id);
    },
  },
};
</script>

<style scoped>
.budget-list-wrap {
  max-width: 500px;
  margin: auto;
}

.list-item {
  display: flex;
  align-items: center;
  padding: 10px 15px;
}
.budget-value {
  font-weight: bold;
  margin-left: auto;
  margin-right: 20px;
}
</style>
