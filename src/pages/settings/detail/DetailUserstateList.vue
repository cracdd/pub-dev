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
          <th>사원명</th>
          <td><input type="text" placeholder="사원명" class="w140px" /></td>
          <th>사번</th>
          <td><input type="text" placeholder="사번번" class="w140px" /></td>
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
      </table>
    </div>
  </section>
  
  <div class="flex-row realtime__title">
    <p class="text-title text-md">실시간 현황</p>
    <div class="time">
      2022-08-08 10:45:25
      <button type="button" class="play"></button>
      <button type="button" class="refresh"></button>
      <button type="button" class="setting"></button>
    </div>
  </div>
  <section class="realTimeStatus">
      <div>로그인<span>1</span></div>
      <div>대기<span>0</span></div>
      <div>통화중<span>0</span></div>
      <div>후처리<span>1</span></div>
      <div>IN<span>0</span></div>
      <div>OUT<span>0</span></div>
      <div>자리비움<span>0</span></div>
      <div>미등록<span>0</span></div>
  </section>

  <section class="card">
    <p class="card-title">지속시간설정</p>
    <div class="durationSetting">
      <div class="durationSetting__time">
        <span class="colorbox__black"></span>
        <input type="text" value="180" class="w50px">
      </div>
      <div class="durationSetting__time">
        <span class="colorbox__red"></span>
        <input type="text" value="180" class="w50px">
      </div>
      <div class="durationSetting__time">
        <span class="colorbox__yellow"></span>
        <input type="text" value="180" class="w50px">
      </div>
      <a href="javascript:;" class="btn-md btn-basic">적용</a>
    </div>
    
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
      <template v-slot:body-cell-logout="props">
        <q-td key="logout" :props="props">
            <a class="btn-sm btn-soft">로그아웃</a>
        </q-td>
      </template>

      <!-- 컬럼에 배경색 추가 -->
      <template v-slot:body-cell-userState="props">
        <q-td :props="props" class="bg-red text-white">
          {{ props.value }}
        </q-td>
      </template>

    </q-table>
  </section>
  
</template>

<script setup>
import { defineProps, defineEmits, ref, onMounted, watch } from 'vue'
import { global } from 'assets/js/publish/global'

const columns = [    
    {
      name: 'ID',
      align: 'center',
      label: '사용자 ID',
      field: 'id',
    },
    {
      name: 'name',
      align: 'center',
      label: '사용자명',
      field: 'name',
    },
    {
      name: 'department',
      align: 'center',
      label: '부서',
      field: 'department',
    },
    {
      name: 'phone',
      align: 'center',
      label: '연락처',
      field: 'phone',
    },
    {
      name: 'userState',
      align: 'center',
      label: '사용자 상태',
      field: 'userState',
    },
    {
      name: 'deviceState',
      align: 'center',
      label: '디바이스 상태',
      field: 'deviceState',
    },
    {
      name: 'Direction',
      align: 'center',
      label: 'Direction',
      field: 'direction',
    },
    {
      name: 'processTime',
      align: 'center',
      label: '진행시간',
      field: 'processTime',
    },
    {
      name: 'logout',
      align: 'center',
      label: '',
      field: 'logout',
    }
  ];

  const rows = [
    {
      id: 'Test01',
      name: '홍길동',
      department: '보상',
      phone: '010-1234-3456',
      userState: '후처리',
      deviceState: '대기중',
      direction: 'OUTTOUND',
      processTime: '00:08:22',
    }
  ];
  const selected = ref([]);

  function getSelectedString() {
    return '';
  }

</script>

<style lang="scss" scoped>
@import "/src/assets/css/set.scss";

</style>
