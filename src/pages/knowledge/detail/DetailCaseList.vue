<template>
  <div>
    <q-btn color="primary" @click="showTextLoading">로딩보기</q-btn>
    <q-inner-loading
      :showing="visible"
      color="grey-6"
      label="텍스트 변환중입니다."
      label-style="font-size: 14px; color:#999;"
    />
  </div>
</template>

<script setup>
  import { defineProps, defineEmits, ref, onMounted, watch } from 'vue';
  import { global } from 'assets/js/publish/global';
  import { useQuasar } from 'quasar';

  const visible = ref(false);
  const showSimulatedReturnData = ref(false);

  function showTextLoading() {
    visible.value = true;
    showSimulatedReturnData.value = false;
  }
</script>
