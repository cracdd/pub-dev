<template>
  <section class="card-top">
    <div class="tbl-detail-box">
      <div class="tbl-detail-title">
        조회 조건
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
          <th>사번</th>
          <td><input type="text" placeholder="사번" class="w140px" /></td>
          <th>전화번호</th>
          <td><input type="text" placeholder="전화번호" class="w140px" /></td>
          <th></th>
          <td></td>
        </tr>
      </table>
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
      :selected-rows-label="getSelectedString"
      selection="multiple"
      v-model:selected="selected"
      virtual-scroll
      :hide-pagination="true"
      class="table-wrap type-data"
    >
    <template v-slot:top-right>
      <a class="btn-sm btn-soft">삭제</a>
    </template>
    </q-table>
  </section>
</template>

<script setup>
import { defineProps, defineEmits, ref, onMounted, watch } from 'vue'
import { global } from 'assets/js/publish/global'

//테이블
const columns = [    
    {
      name: 'phone',
      align: 'center',
      label: '전화번호',
      field: 'phone',
    },
    {
      name: 'id',
      align: 'center',
      label: '아이디',
      field: 'id',
    },
    {
      name: 'mobileCarrier',
      align: 'center',
      label: '통신사',
      field: 'mobileCarrier',
    },
    {
      name: 'model',
      align: 'center',
      label: '모델명',
      field: 'model',
    },
    {
      name: 'android',
      align: 'center',
      label: 'Android OS',
      field: 'android',
    },
    {
      name: 'version',
      align: 'center',
      label: '앱 버전',
      field: 'version',
    },
    {
      name: 'date',
      align: 'center',
      label: '생성일자',
      field: 'date',
    }
  ];

  const rows = [
    {
      phone: '010-1234-5432',
      id: '1234567',
      mobileCarrier: 'SK Telecom',
      model: 'Samsung SM-S908N',
      android:'14',
      version: '1.0.0',
      date: '2025-04-30 13:21'
    },
    {
      phone: '010-1234-5432',
      id: '1234567',
      mobileCarrier: 'SK Telecom',
      model: 'Samsung SM-S908N',
      android:'14',
      version: '1.0.0',
      date: '2025-04-30 13:21'
    },
    {
      phone: '010-1234-5432',
      id: '1234567',
      mobileCarrier: 'SK Telecom',
      model: 'Samsung SM-S908N',
      android:'14',
      version: '1.0.0',
      date: '2025-04-30 13:21'
    },
    {
      phone: '010-1234-5432',
      id: '1234567',
      mobileCarrier: 'SK Telecom',
      model: 'Samsung SM-S908N',
      android:'14',
      version: '1.0.0',
      date: '2025-04-30 13:21'
    },
    {
      phone: '010-1234-5432',
      id: '1234567',
      mobileCarrier: 'SK Telecom',
      model: 'Samsung SM-S908N',
      android:'14',
      version: '1.0.0',
      date: '2025-04-30 13:21'
    },
  ];
  const selected = ref([]);

  function getSelectedString() {
    return '';
  }

</script>

<style lang="scss" scoped>
  @import "/src/assets/css/set.scss";
</style>
