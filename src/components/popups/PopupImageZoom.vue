<template>
  <div class="popup-container" :class="visible ? 'active' : ''">
    <div class="popup-wrap">
      <div class="popup-header">
        <b class="title">이미지 확대보기</b>
        <a href="#" class="close" @click.prevent="onClose"></a>
      </div>
      <div class="popup-body">
        <div class="image-box">
          <img src="../../assets/images/ex-img.png" alt="" />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
  import { ref, watch, onMounted } from 'vue';

  const props = defineProps({
    visible: Boolean,
    initData: Object,
  });

  onMounted(() => {
    console.log('팝업에 전달된 데이터:', props.initData);
  });

  watch(
    () => props.initData,
    (val) => {
      if (val) {
        console.log('💡 새로운 팝업 데이터 감지:', val);
      }
    },
    { immediate: true },
  );

  const emit = defineEmits(['update:visible', 'submit']);

  const onClose = () => {
    emit('update:visible', false);
  };
</script>

<style scoped></style>
