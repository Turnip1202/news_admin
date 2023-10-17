<template>
  <router-view />
</template>

<style lang="less">
// 全局样式
* {
  margin: 0;
  padding: 0;
}
// 设置滚动条的样式
::-webkit-scrollbar {
  width: 5px;
  height: 5px;
  position: absolute;
}
::-webkit-scrollbar-thumb {
  // 滚动条上的滚动滑块的颜色
  background-color: #1890ff;
}
::-webkit-scrollbar-track {
  // 滚动条轨道的颜色
  background: #ddd;
}
</style>
<script setup>
const debounce = (fn, delay) => {
  let timer = null;

  return function () {
    let context = this;

    let args = arguments;

    clearTimeout(timer);

    timer = setTimeout(function () {
      fn.apply(context, args);
    }, delay);
  };
};

// 解决ERROR ResizeObserver loop completed with undelivered notifications.

//问题的

const _ResizeObserver = window.ResizeObserver;

window.ResizeObserver = class ResizeObserver extends _ResizeObserver {
  constructor(callback) {
    callback = debounce(callback, 16);

    super(callback);
  }
};
</script>
