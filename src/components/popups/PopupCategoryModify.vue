<template>
  <div class="popup-container" :class="visible ? 'active' : ''">
    <div class="popup-wrap w720px">
      <div class="popup-header">
        <b class="title">수정</b>
        <a href="#" class="close" @click.prevent="onClose"></a>
      </div>
      <div class="popup-body">
        <div class="form-col-wrap register-box">
          <form class="form-box">
            <div class="form-mix">
              <label>상위 부서</label>
              <input type="text" placeholder="상위 부서" class="w100p" />
            </div>
            <div class="form-mix">
              <label>부서ID</label>
              <input type="text" placeholder="부서ID" class="w100p" />
            </div>           
            <div class="form-mix">
              <label>부서명</label>
              <input type="text" placeholder="OB_1C(한고정)" class="w100p" />
            </div>
            <div class="form-mix">
              <label>Depth</label>
              <select class="w100p">
                <option>선택</option>
              </select>
            </div>
            <div class="form-mix">
              <label>Sort</label>
              <input type="text" placeholder="" class="w100p" />
            </div>
            <div class="form-mix">
              <label>만료 날짜</label>
              <CallDateBox />
            </div>
            <div class="form-mix">
              <label>사용여부</label>
              <div class="form-mix__radio">
                <label class="radio-item">
                  <input type="radio" name="radio1" checked>
                  <span>Y</span>
                </label>
                <label class="radio-item">
                  <input type="radio" name="radio1">
                  <span>N</span>
                </label>
              </div>
            </div>
            <div class="form-mix">
              <label>설명</label>
              <textarea class="w20p h150px" placeholder="설명을 입력해 주세요."></textarea>
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
          >초기화</a
        >
        <a
          href="javascript:;"
          class="btn-md btn-secondary close"
          data-dismiss="modalPopup"
          @click.prevent="onClose"
          >수정</a
        >
      </div>
    </div>
  </div>
</template>

<script setup>
  import { ref, watch, onMounted } from 'vue';
  import CallDateBox from 'components/CallDateBox.vue';
  

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

<style lang="scss" scoped>
  .register-box{
    .form-box{
      .form-mix{
        label{
          flex-basis: 200px;
        }
        &__radio{
          label{
            margin-right:24px;
          }
        }
      }
    }
  }
  .popup-wrap{
    &.w720px{
      width:720px;
    }
    .popup-footer{
      margin-top:20px;
    }
  }
</style>
