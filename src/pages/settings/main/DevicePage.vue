<template>
  <div class="settings-mid">
    <div class="title-box">
      <div class="title">단말기</div>
      <div class="btns">
        <a href="javascript:;" class="btn-sm btn-ghost">초기화</a>
        <a href="javascript:;" class="btn-sm btn-basic">등록/수정</a>
      </div>
    </div>
    <form class="form-box">
      <div class="form-mix">
        <label>전화번호</label>
        <input type="text" placeholder="010-111-2222" class="w150px" />
      </div>
      <div class="form-mix">
        <label>사원ID</label>
        <input type="text" placeholder="Test01" class="w150px" />
      </div>
      <div class="form-mix">
        <label>핸드폰유무</label>
        <select class="w150px">
          <option>선택</option>
        </select>
      </div>
    </form>
  </div>
</template>

<script setup>
  import {
    defineProps,
    defineEmits,
    ref,
    onMounted,
    watch,
    computed,
    reactive,
  } from 'vue';
  import { global } from 'assets/js/publish/global';
</script>

<style lang="scss" scoped>
  @import '/src/assets/css/set.scss';
</style>
