<template>
  <div class="period-box">
    <div class="form-mix">
      <!-- 시작시간 -->
      <div class="input-mix type-timepicker w130px">
        <span class="unit">
          <a href="javascript:;" class="btn-ico type-text"></a>
        </span>
        <input type="text" placeholder="00:00" v-model="startTime" readonly />
        <q-popup-proxy cover transition-show="scale" transition-hide="scale">
          <q-time color="grey-7" v-model="startTime" today-btn />
        </q-popup-proxy>
      </div>

      <span>-</span>

      <!-- 종료시간 -->
      <div class="input-mix type-timepicker w130px">
        <span class="unit">
          <a href="javascript:;" class="btn-ico type-text"></a>
        </span>
        <input type="text" placeholder="00:00" v-model="endTime" readonly />
        <q-popup-proxy cover transition-show="scale" transition-hide="scale">
          <q-time color="grey-7" v-model="endTime" today-btn />
        </q-popup-proxy>
      </div>
    </div>
  </div>
</template>

<script setup>
  import { ref } from 'vue';

  const startTime = ref();
  const endTime = ref();
</script>
