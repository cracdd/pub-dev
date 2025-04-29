<template>
  <div class="period-box">
    <div class="form-mix">
      <!-- 시작일자 -->
      <div class="input-mix type-datepicker">
        <span class="unit">
          <a
            href="javascript:;"
            class="btn-ico type-text"
            @click="showStartDate"
          ></a>
        </span>
        <input
          type="text"
          placeholder="yyyy-mm-dd"
          v-model="startDate"
          readonly
          @click="showStartDate"
        />

        <q-popup-proxy
          ref="startRef"
          cover
          transition-show="none"
          transition-hide="none"
        >
          <q-date
            color="grey-7"
            v-model="startDate"
            mask="YYYY-MM-DD"
            today-btn
            @update:model-value="onStartSelect"
          />
        </q-popup-proxy>
      </div>
    </div>
  </div>
</template>

<script setup>
  import { ref } from 'vue';

  // ✅ 날짜 초기값은 오늘로
  const today = new Date().toISOString().slice(0, 10);

  const startDate = ref(today);

  const startRef = ref(null);

  const showStartDate = () => {
    setTimeout(() => startRef.value?.show(), 0);
  };

  const onStartSelect = () => startRef.value?.hide();
</script>
