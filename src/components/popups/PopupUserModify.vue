<template>
  <div class="popup-container" :class="visible ? 'active' : ''">
    <div class="popup-wrap w720px">
      <div class="popup-header">
        <b class="title">사용자 수정</b>
        <a href="#" class="close" @click.prevent="onClose"></a>
      </div>
      <div class="popup-body">
        <div class="form-col-wrap register-box">
          <form class="form-box">
            <div class="form-mix">
              <label>사용자 이름</label>
              <input type="text" placeholder="사용자 이름" class="w100p" />
            </div>
            <div class="form-mix">
              <label>이메일 주소</label>
              <input type="text" placeholder="이메일 주소" class="w100p" />
            </div>           
            <div class="form-mix">
              <label>소속그룹 - optional</label>
              <input type="text" placeholder="소속된 부서 정보를 입력해 주세요." class="w100p" />
            </div>
            <div class="form-mix">
              <label>권한</label>
              <select class="w100p">
                <option>선택</option>
              </select>
            </div>
            <div class="form-mix">
              <label>연락처 - optional</label>
              <input type="text" placeholder="모바일 연락처를 입력해 주세요." class="w100p" />
            </div>
            <div class="form-mix">
              <label>재직상태</label>
              <div class="form-mix__radio">
                <label class="radio-item">
                  <input type="radio" name="radio1" checked>
                  <span>재직중</span>
                </label>
                <label class="radio-item">
                  <input type="radio" name="radio1">
                  <span>퇴사</span>
                </label>
              </div>
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
          >수정</a
        >
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
