<template>
  <div class="demo">
    <bk-select
      v-model="selectedValue"
      class="bk-select"
      multiple
      filterable
      :filter-option="filterOption"
    >
      <bk-option
        v-for="(item, index) in datasource"
        :id="item.value"
        :key="index"
        :name="item.label"
      />
    </bk-select>
    <bk-select
      v-model="selectedValue"
      class="bk-select"
      :input-search="false"
      :list="searchList"
      multiple
      filterable
      :filter-option="filterOption"
      :remote-method="searchDataSource"
    />
    <bk-select
      v-model="selectedValue"
      class="bk-select"
      :input-search="false"
      multiple
      filterable
      multiple-mode="tag"
    >
      <bk-option
        v-for="(item, index) in datasource"
        :id="item.value"
        :key="index"
        :name="item.label"
      />
    </bk-select>
    <bk-select
      v-model="selectedValue"
      class="bk-select"
      multiple
      filterable
      allow-create
      multiple-mode="tag"
    >
      <bk-option
        v-for="(item, index) in datasource"
        :id="item.value"
        :key="index"
        :name="item.label"
      />
    </bk-select>
    <bk-select
      class="bk-select"
      multiple
      filterable
      :remote-method="remoteMethod"
      multiple-mode="tag"
    >
      <bk-option
        v-for="(item, index) in list"
        :id="item.value"
        :key="item.value"
        :name="item.label"
        :order="index"
      />
    </bk-select>
  </div>
</template>
<script setup>
  import { onMounted, ref } from 'vue';
  const datasource = ref([
    {
      value: 'climbing',
      label: '爬山',
    },
    {
      value: 'running',
      label: '跑步',
    },
    {
      value: 'unknow',
      label: '未知',
    },
    {
      value: 'fitness',
      label: '健身',
    },
    {
      value: 'bike',
      label: '骑车',
    },
    {
      value: 'dancing',
      label: '跳舞',
    },
    {
      value: 'sleep',
      label: '睡觉',
      disabled: true,
    },
  ]);
  const selectedValue = ref('dancing');
  const list = ref([]);
  const remoteMethod = async value => new Promise((resolve) => {
    if (!value)  {
      list.value = [];
      resolve('ok');
    } else {
      setTimeout(() => {
        list.value = new Array(10).fill('')
          .map((_, i) => ({
            value: `${i}-${value}`,
            label: `label-${value}-${i}`,
          }));
        resolve('ok');
      }, 1000);
    };
  });
  const filterOption = (input, options) => options.name?.includes(input);

  const searchList = ref();
  const searchDataSource = (key) => {
    searchList.value = datasource.value.filter(item => item.label.includes(key));
  };

  onMounted(() => {
    setTimeout(() => {
      searchList.value = JSON.parse(JSON.stringify(datasource.value));
    }, 1000);
  });
</script>
<style scoped>
.demo {
  display: flex;
}

.bk-select {
  width: 300px;
  margin-right: 20px;
}
</style>

