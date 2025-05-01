<template>
  <!--admin-->
  <section class="card">
    <div class="titleBox mb30">
      <div class="text-title lg">메뉴관리</div>
      <div class="titleBox__btns">
        <a href="javascript:;" class="btn-sm btn-soft">메뉴추가</a>
      </div>
    </div>

    <div class="adminBox">
      <table>
        <colgroup>
          <col style="width:20%"/>
          <col style="width:80%"/>
        </colgroup>
        <tr>
          <th>상위메뉴</th>
          <td><input type="text" class="w400px" value="" /></td>
        </tr>
        <tr>
          <th>메뉴ID</th>
          <td><input type="text" class="w400px" value="" /></td>
        </tr>
        <tr>
          <th>메뉴명</th>
          <td><input type="text" class="w400px" value="" /></td>
        </tr>
        <tr>
          <th>Depth</th>
          <td><input type="text" class="w400px" value="" /></td>
        </tr>
        <tr>
          <th>화면경로</th>
          <td><input type="text" class="w400px" value="" /></td>
        </tr>
        <tr>
          <th>만료날짜</th>
          <td>
            <div class="form-mix">
              <div class="input-mix type-datepicker w400px">
                <span class="unit">
                  <a href="javascript:;" class="btn-ico type-text"></a>
                </span>
                <input type="text" placeholder="yyyy-mm-dd" value="2022-11-01" readonly />
              </div>
            </div>
          </td>
        </tr>
        <tr>
          <th>사용권한</th>
          <td>
            <select class="w400px">
              <option>선택</option>
            </select>
          </td>
        </tr>
        <tr>
          <th>사용여부</th>
          <td>
            <div class="radioBox">
              <label class="radio-item">
                <input type="radio" name="radio1" checked>
                <span>Y</span>
              </label>
              <label class="radio-item">
                <input type="radio" name="radio1">
                <span>N</span>
              </label>
            </div>
          </td>
        </tr>
        <tr>
          <th class="memo">설명</th>
          <td class="memo">
            <textarea class="h150px" placeholder="설명을 입력해주세요."></textarea>
          </td>
        </tr>
      </table>
    </div>
  </section>
  <div class="form-mix flex-end mt15">
    <a href="javascript:;" class="btn-md btn-ghost">초기화</a>
    <a href="javascript:;" class="btn-md btn-secondary">수정</a>
  </div>
</template>

<script setup>
  import { defineProps, defineEmits, ref, onMounted, watch } from 'vue';
  import { global } from 'assets/js/publish/global';
</script>

<style lang="scss" scoped>
  @import '/src/assets/css/set.scss';
</style>