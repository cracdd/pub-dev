<template>
  <div class="period-box">
    <div class="form-mix">
      <!-- 시작시간 -->
      <div class="input-mix type-timepicker w130px">
        <span class="unit">
          <a
            href="javascript:;"
            class="btn-ico type-text"
            @click="showStartTime"
          ></a>
        </span>
        <input
          type="text"
          :value="localizedStartTime"
          placeholder="00:00"
          readonly
          @click="showStartTime"
        />
        <q-popup-proxy cover transition-show="scale" transition-hide="scale">
          <q-time color="grey-7" v-model="startTime" mask="A hh:mm" />
        </q-popup-proxy>
      </div>

      <span>-</span>

      <!-- 종료시간 -->
      <div class="input-mix type-timepicker w130px">
        <span class="unit">
          <a
            href="javascript:;"
            class="btn-ico type-text"
            @click="showEndTime"
          ></a>
        </span>
        <input
          type="text"
          :value="localizedEndTime"
          placeholder="00:00"
          readonly
          @click="showEndTime"
        />
        <q-popup-proxy cover transition-show="scale" transition-hide="scale">
          <q-time color="grey-7" v-model="endTime" mask="A hh:mm" />
        </q-popup-proxy>
      </div>
    </div>
  </div>
</template>

<script setup>
  import { ref, computed } from 'vue';

  const today = new Date().toLocaleTimeString().slice(0, 8);

  const startTime = ref(today);
  const endTime = ref(today);

  const startRef = ref(null);
  const endRef = ref(null);

  const showStartTime = () => {
    setTimeout(() => startRef.value?.show(), 0);
  };
  const showEndTime = () => {
    setTimeout(() => endRef.value?.show(), 0);
  };

  // 한글 표기로 포맷
  const localizedStartTime = computed(() =>
    startTime.value.replace('AM', '오전').replace('PM', '오후'),
  );
  const localizedEndTime = computed(() =>
    endTime.value.replace('AM', '오전').replace('PM', '오후'),
  );
</script>
