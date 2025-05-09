<template>
  <!-- 통계 레이아웃 case 1 -->
  <section class="card-top">
    <div class="tbl-detail-box">
      <div class="tbl-detail-title">
        조건 설정
        <div class="tbl-btns">
          <a class="btn-md btn-secondary">조회</a>
        </div>
      </div>
      <q-markup-table class="tbl-detail">
        <colgroup>
          <col style="" />
          <col style="width: 33%" />
          <col style="" />
          <col style="" />
        </colgroup>
        <tr>
          <th>기간</th>
          <td>
            <CallPeriodBox />
          </td>
          <th></th>
          <td></td>
        </tr>
        <tr>
          <th>대상조직</th>
          <td>
            <div class="form-mix">
              <select class="w150px">
                <option>인</option>
                <option>1</option>
                <option>2</option>
                <option>3</option>
              </select>
              <select class="w150px">
                <option>전체(D레벨)</option>
                <option>1</option>
                <option>2</option>
                <option>3</option>
              </select>
              <select class="w150px">
                <option>전체(E레벨)</option>
                <option>1</option>
                <option>2</option>
                <option>3</option>
              </select>
              <select class="w150px">
                <option>전체(사원)</option>
                <option>1</option>
                <option>2</option>
                <option>3</option>
              </select>
            </div>
          </td>
          <th></th>
          <td>
            <div class="form-mix">
              <select class="w150px">
                <option>전체</option>
                <option>1</option>
                <option>2</option>
                <option>3</option>
              </select>
              <select class="w150px">
                <option>전체</option>
                <option>1</option>
                <option>2</option>
                <option>3</option>
              </select>
              <select class="w150px">
                <option>전체</option>
                <option>1</option>
                <option>2</option>
                <option>3</option>
              </select>
            </div>
          </td>
        </tr>
      </q-markup-table>
    </div>
  </section>
  <section class="card card-column-auto">
    <h5>전체실적</h5>
    <div class="chart-box mt10">차트영역</div>
  </section>
  <section class="card-row mt10">
    <div class="card">
      <h5>2025년 4월</h5>
      <div class="calendar-box mt10">캘린더영역</div>
    </div>
    <div class="card">
      <h5>시간대별 통화건수</h5>
      <div class="chart-box mt10">차트영역</div>
    </div>
  </section>

  <!-- 통계 레이아웃 case 2 -->
  <!-- <section class="card-top">
    <div class="tbl-detail-box">
      <div class="tbl-detail-title">
        조건 설정
        <div class="tbl-btns">
          <a class="btn-md btn-secondary">조회</a>
        </div>
      </div>
      <q-markup-table class="tbl-detail">
        <colgroup>
          <col style="" />
          <col style="" />
        </colgroup>
        <tr>
          <th>기간</th>
          <td>
            <CallPeriodBox />
          </td>
        </tr>
        <tr>
          <th>대상조직</th>
          <td>
            <div class="form-mix">
              <select class="w150px">
                <option>인</option>
                <option>1</option>
                <option>2</option>
                <option>3</option>
              </select>
              <select class="w150px">
                <option>전체(D레벨)</option>
                <option>1</option>
                <option>2</option>
                <option>3</option>
              </select>
              <select class="w150px">
                <option>전체(E레벨)</option>
                <option>1</option>
                <option>2</option>
                <option>3</option>
              </select>
              <select class="w150px">
                <option>전체(사원)</option>
                <option>1</option>
                <option>2</option>
                <option>3</option>
              </select>
            </div>
          </td>
        </tr>
      </q-markup-table>
    </div>
  </section>
  <section class="card-row mt10">
    <div class="card">
      <h5>건당 평균 통화시간</h5>
      <div class="form-mix mt10">
        <select class="w150px">
          <option>전체</option>
          <option>1</option>
          <option>2</option>
          <option>3</option>
        </select>
        <select class="w150px">
          <option>전체</option>
          <option>1</option>
          <option>2</option>
          <option>3</option>
        </select>
      </div>
      <div class="chart-box mt10">
        <div>차트영역</div>
      </div>
    </div>
    <div class="card">
      <h5>대상 유형 비율</h5>
      <div class="form-mix mt10">
        <select class="w150px">
          <option>전체</option>
          <option>1</option>
          <option>2</option>
          <option>3</option>
        </select>
      </div>
      <div class="chart-box mt10">
        <div>차트영역</div>
      </div>
    </div>
  </section> -->
</template>

<script setup>
  import { defineProps, defineEmits, ref, onMounted, watch } from 'vue';
  import { global } from 'assets/js/publish/global';
  import CallPeriodBox from 'components/CallPeriodBox.vue';
</script>

<style lang="scss" scoped>
  .card-row {
    .card {
      height: 100%;
    }
  }
</style>
