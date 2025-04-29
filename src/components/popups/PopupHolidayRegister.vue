<template>
  <div class="popup-container" :class="visible ? 'active' : ''">
    <div class="popup-wrap">
      <div class="popup-header">
        <b class="title">휴가 사용자 등록 및 수정</b>
        <a href="#" class="close" @click.prevent="onClose"></a>
      </div>
      <div class="popup-body">
        <div class="form-col-wrap register-box">
          <form class="form-box">
            <div class="form-mix">
              <label>사용자ID</label>
              <input type="text" placeholder="사용자ID" class="w100p" />
            </div>
            <div class="form-mix">
              <label>사용자명</label>
              <input type="text" placeholder="사용자명" class="w100p" />
            </div>
            <div class="form-mix">
              <label>등록 날짜</label>
              <CallDateBox />
            </div>
            <div class="form-mix">
              <label>등록 시간</label>
              <CallTimeBox />
            </div>
            <div class="form-mix">
              <label>휴일사용</label>
              <label class="checkbox-item">
                <input type="checkbox" checked />
                <span></span>
              </label>
            </div>
            <div class="form-mix">
              <label>사유</label>
              <input type="text" placeholder="사유" class="w100p" />
            </div>
          </form>
        </div>
      </div>
      <div class="popup-footer">
        <a
          href="javascript:;"
          class="btn-md btn-ghost close"
          data-dismiss="modalPopup"
          @click.prevent="onClose"
          >취소</a
        >
        <a
          href="javascript:;"
          class="btn-md btn-secondary close"
          data-dismiss="modalPopup"
          @click.prevent="onClose"
          >등록</a
        >
      </div>
    </div>
  </div>
</template>

<script setup>
  import { ref, watch, onMounted } from 'vue';
  import CallDateBox from 'components/CallDateBox.vue';
  import CallTimeBox from 'components/CallTimeBox.vue';

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
