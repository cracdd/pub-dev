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
          <col style="width: 20%" />
          <col style="width: 80%" />
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
            <CallDateBox />
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
                <input type="radio" name="radio1" checked />
                <span>Y</span>
              </label>
              <label class="radio-item">
                <input type="radio" name="radio1" />
                <span>N</span>
              </label>
            </div>
          </td>
        </tr>
        <tr>
          <th class="memo">설명</th>
          <td class="memo">
            <textarea
              class="h150px"
              placeholder="설명을 입력해주세요."
            ></textarea>
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
  import CallDateBox from 'components/CallDateBox.vue';
</script>

<style lang="scss" scoped>
  @import '/src/assets/css/set.scss';
</style>
