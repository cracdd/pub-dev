<template>
  <section class="card-top" :class="open ? 'active' : ''">
    <div class="tbl-detail-box">
      <div class="tbl-detail-title">
        조회 조건
        <div class="tbl-btns">
          <a class="btn-md btn-secondary">조회</a>
          <a
            class="btn-md btn-basic ico-arrow"
            @click="open = !open"
            :class="open ? 'active' : ''"
            >상세검색</a
          >
        </div>
      </div>
      <q-markup-table class="tbl-detail">
        <colgroup>
          <col style="" />
          <col style="width: 33%" />
          <col style="" />
          <col style="width: 33%" />
          <col style="" />
          <col style="" />
        </colgroup>
        <tr>
          <th>사용자이름</th>
          <td><input type="text" placeholder="사용자이름" class="w140px" /></td>
          <th>사용자ID</th>
          <td><input type="text" placeholder="사용자ID" class="w140px" /></td>
          <th></th>
          <td></td>
        </tr>
      </q-markup-table>
    </div>

    <div class="tbl-detail-box mt40 toggle-box" v-show="open">
      <div class="tbl-detail-title">조건 설정</div>
      <q-markup-table class="tbl-detail">
        <colgroup>
          <col style="" />
          <col style="width: 33%" />
          <col style="" />
          <col style="width: 33%" />
          <col style="" />
          <col style="" />
        </colgroup>
        <tr>
          <th>사원명</th>
          <td>
            <input type="text" placeholder="사용자이름" class="w140px" />
          </td>
          <th>사원ID</th>
          <td><input type="text" placeholder="사용자ID" class="w140px" /></td>
          <th>부서</th>
          <td>
            <select class="w140px">
              <option>보상</option>
              <option>1</option>
              <option>2</option>
              <option>3</option>
            </select>
          </td>
        </tr>
      </q-markup-table>
    </div>
  </section>

  <section class="card">
    <q-table
      title="검색결과"
      style="height: 100%"
      flat
      separator="cell"
      :rows="rows"
      :columns="columns"
      row-key="name"
      virtual-scroll
      :rows-per-page-options="[0]"
      :pagination-label="getTotal"
      class="table-wrap type-data"
    >
    </q-table>
  </section>
</template>

<script setup>
  import { defineProps, defineEmits, ref, onMounted, watch } from 'vue';
  import { global } from 'assets/js/publish/global';

  const open = ref(false);
  //테이블
  const columns = [
    {
      name: 'date',
      align: 'center',
      label: '발생일',
      field: 'date',
    },
    {
      name: 'connectionID',
      align: 'center',
      label: '접속ID',
      field: 'connectionID',
    },
    {
      name: 'ip',
      align: 'center',
      label: 'IP',
      field: 'ip',
    },
    {
      name: 'screenID',
      align: 'center',
      label: '화면ID',
      field: 'screenID',
    },
    {
      name: 'note',
      align: 'center',
      label: '비고',
      field: 'note',
    },
  ];

  const rows = [
    {
      date: '2025-01-01 00:00:01',
      connectionID: '12345678',
      ip: '1.1.1.1',
      screenID: '화면01',
      note: 'My Phone',
    },
    {
      date: '2025-01-01 00:00:02',
      connectionID: '12345678',
      ip: '1.1.1.1',
      screenID: '화면01',
      note: 'My Phone',
    },
    {
      date: '2025-01-01 00:00:03',
      connectionID: '12345678',
      ip: '1.1.1.1',
      screenID: '화면01',
      note: 'My Phone',
    },
    {
      date: '2025-01-01 00:00:04',
      connectionID: '12345678',
      ip: '1.1.1.1',
      screenID: '화면01',
      note: 'My Phone',
    },
    {
      date: '2025-01-01 00:00:05',
      connectionID: '12345678',
      ip: '1.1.1.1',
      screenID: '화면01',
      note: 'My Phone',
    },
    {
      date: '2025-01-01 00:00:06',
      connectionID: '12345678',
      ip: '1.1.1.1',
      screenID: '화면01',
      note: 'My Phone',
    },
    {
      date: '2025-01-01 00:00:07',
      connectionID: '12345678',
      ip: '1.1.1.1',
      screenID: '화면01',
      note: 'My Phone',
    },
  ];

  function getTotal(start, end, total) {
    return `총 ${total} 건`;
  }
</script>

<style lang="scss" scoped>
  @import '/src/assets/css/set.scss';
  .toggle-box {
    position: absolute;
    left: 0;
    top: 92px;
    z-index: 10;
    width: 100%;
    border-radius: 0 0 10px 10px;
  }
</style>
