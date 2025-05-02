<template>
  <section class="card-top">
    <div class="tbl-detail-box">
      <div class="tbl-detail-title">
        조건 설정
        <div class="tbl-btns">
          <a class="btn-md btn-secondary">조회</a>
        </div>
      </div>
      <table class="tbl-detail">
        <colgroup>
          <col style="" />
          <col style="width: 33%" />
          <col style="" />
          <col style="width: 33%" />
          <col style="" />
          <col style="" />
        </colgroup>
        <tr>
          <th>기간</th>
          <td>
            <CallDateBox />
          </td>
          <th>전화번호</th>
          <td>
            <input type="text" placeholder="전화번호" class="w140px" />
          </td>
          <th>사원ID</th>
          <td>
            <input type="text" placeholder="사원ID" class="w140px" />
          </td>
        </tr>
      </table>
    </div>
  </section>

  <section class="card board-list-card">
    <q-table
      title="검색결과"
      style="height: 100%"
      flat
      separator="cell"
      :rows="rows"
      :columns="columns"
      row-key="name"
      :selected-rows-label="getSelectedString"
      v-model:selected="selected"
      virtual-scroll
      :hide-pagination="true"
      class="table-wrap type-data"
    >
      <template v-slot:top-right>
        <a class="btn-sm btn-soft">삭제</a>
      </template>

      <!-- 컬럼에 버튼 추가 -->
      <template v-slot:body-cell-download="props">
        <q-td key="download" :props="props">
            <a class="btn-sm btn-soft">다운</a>
        </q-td>
      </template>
    </q-table>
  </section>
</template>

<script setup>
  import { defineProps, defineEmits, ref, onMounted, watch } from 'vue';
  import { global } from 'assets/js/publish/global';
  import CallDateBox from 'components/CallDateBox.vue';

  //테이블
const columns = [    
    {
      name: 'download',
      align: 'center',
      label: '다운로드',
      field: 'download',
    },
    {
      name: 'id',
      align: 'center',
      label: '사용자 아이디',
      field: 'id',
    },
    {
      name: 'phone',
      align: 'center',
      label: '전화',
      field: 'phone',
    },
    {
      name: 'logDate',
      align: 'center',
      label: '로그일자',
      field: 'logDate',
    },
    {
      name: 'uploadTime',
      align: 'center',
      label: '업로드시간',
      field: 'uploadTime',
    },
    {
      name: 'logUrl',
      align: 'center',
      label: '로그전체경로',
      field: 'logUrl',
    },
  ];

  const rows = [
    {
      id: '9234',
      phone:'010-1111-2222',
      logDate:'2025-04-03',
      uploadTime:'2025-04-20 00:06:59',
      logUrl:'/mobilelog/20250402/log_9315_20250403_0.zip',      
    },
    {
      id: '9234',
      phone:'010-1111-2222',
      logDate:'2025-04-03',
      uploadTime:'2025-04-20 00:06:59',
      logUrl:'/mobilelog/20250402/log_9315_20250403_0.zip',      
    },
    {
      id: '9234',
      phone:'010-1111-2222',
      logDate:'2025-04-03',
      uploadTime:'2025-04-20 00:06:59',
      logUrl:'/mobilelog/20250402/log_9315_20250403_0.zip',      
    },
  ];
  const selected = ref([]);
  function getSelectedString() {
    return '';
  }
</script>

<style lang="scss" scoped>
  @import '/src/assets/css/set.scss';

  .period-box{
    width:140px;
  }
</style>
