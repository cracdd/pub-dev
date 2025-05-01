<template>
  <section class="contents-c-body">
    <div class="titleBox">
      <div class="text-title lg">단말기</div>
      <div class="titleBox__btns">
        <a href="javascript:;" class="btn-sm btn-ghost">초기화</a>
        <a href="javascript:;" class="btn-sm btn-basic">등록/수정</a>
      </div>
    </div>
    <div class="formBox">
      <ol>
        <dt>전화번호</dt>
        <dd>
          <input type="text" placeholder="010-111-2222" class="w140" />
        </dd>
        <dt>사원ID</dt>
        <dd>
          <input type="text" placeholder="Test01" class="w140" />
        </dd>
        <dt>핸드폰유무</dt>
        <dd>
          <select class="w140">
            <option>선택</option>
          </select>
        </dd>
      </ol>
    </div>
    
  </section>
</template>

<script setup>
import { defineProps, defineEmits, ref, onMounted, watch, computed, reactive } from 'vue'
import { global } from 'assets/js/publish/global'

</script>

<style lang="scss" scoped>
  @import "/src/assets/css/set.scss";
</style>
