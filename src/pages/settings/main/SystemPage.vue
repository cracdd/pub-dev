<template>
  <div class="settings-mid">
    <div class="title-box">
      <div class="title">시스템 설정</div>
      <div class="btns">
        <a href="javascript:;" class="btn-sm btn-basic">적용</a>
      </div>
    </div>
    <form class="form-box">
      <h5 class="mt25 mb25">녹취 업로드 옵션</h5>
      <div class="form-mix">
        <label class="radio-item">
          <input type="radio" name="radio1" checked />
          <span>
            스위치1
            <span class="subText">전체 업로드</span>
          </span>
        </label>
        <label class="radio-item">
          <input type="radio" name="radio1" />
          <span>
            스위치2
            <span class="subText">매핑정보 있는 파일만 업로드</span>
          </span>
        </label>
        <label class="radio-item">
          <input type="radio" name="radio1" />
          <span>
            스위치3
            <span class="subText">매핑정보+녹취 동의 있는 파일만 업로드</span>
          </span>
        </label>
      </div>
    </form>
  </div>
</template>

<script setup>
  import { defineProps, defineEmits, ref, onMounted, watch } from 'vue';
  import { global } from 'assets/js/publish/global';
</script>

<style lang="scss" scoped>
.form-mix{
  flex-direction: column;
  align-items: flex-start;
  gap:16px;
  .radio-item{
    width:100% !important;
    span{
      .subText{
        font-size:13px; color:#999;
        padding-left:24px;
      }
    }
  }
}
</style>