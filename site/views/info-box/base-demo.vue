<template>
  <div>
    <bk-button
      theme="primary"
      @click="handleDefault1"
    >
      默认配置的提示框1
    </bk-button>
    <bk-button
      theme="primary"
      style="margin-left: 15px;"
      @click="handleDefault2"
    >
      默认配置的提示框2
    </bk-button>
  </div>
</template>

<script setup>

  import { InfoBox } from 'bkui-vue';
  const handleDefault1 = () => {
    InfoBox({
      title: '确认要删除？',
      confirmFn() {},
    });
  };
  const handleDefault2 = () => {
    InfoBox({
      title: '请确认是否重置',
      subTitle: '重置SecureKey，需要自行修改templates中的callback地址字段！',
      confirmText: '按钮1',
      cancelText: '按钮2',
      onConfirm() {},
    });
  };
</script>
