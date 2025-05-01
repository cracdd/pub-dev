<template>
  <div class="settings-mid">
    <div class="title-box">
      <div class="title">시스템 설정</div>
      <div class="btns">
        <a href="javascript:;" class="btn-sm btn-basic">적용</a>
      </div>
    </div>
    <form class="form-box">
      <div class="form-mix">
        <label class="radio-item">
          <input type="radio" name="radio1" checked />
          <span>스위치1</span>
        </label>
        <label class="radio-item">
          <input type="radio" name="radio1" />
          <span>스위치2</span>
        </label>
        <label class="radio-item">
          <input type="radio" name="radio1" />
          <span>스위치3</span>
        </label>
      </div>
    </form>
  </div>
</template>

<script setup>
  import { defineProps, defineEmits, ref, onMounted, watch } from 'vue';
  import { global } from 'assets/js/publish/global';
</script>
