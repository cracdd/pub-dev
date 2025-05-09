<template>
  <section class="card-top">
    <div class="tbl-detail-box">
      <div class="tbl-detail-title">
        조회 조건
        <div class="tbl-btns">
          <a class="btn-md btn-secondary">조회</a>
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
          <td><input type="text" placeholder="사번" class="w140px" /></td>
          <th>사용자ID</th>
          <td><input type="text" placeholder="전화번호" class="w140px" /></td>
          <th></th>
          <td></td>
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
      :selected-rows-label="getSelectedString"
      v-model:selected="selected"
      virtual-scroll
      :hide-pagination="true"
      class="table-wrap type-data"
    >
      <!-- 컬럼에 버튼 추가 -->
      <template v-slot:body-cell-modify="props">
        <q-td key="modify" :props="props">
          <a class="btn-sm btn-soft" @click="openPopupUserModify()">수정</a>
        </q-td>
      </template>
    </q-table>
    <a class="btn-sm btn-secondary" @click="openPopupSearchDepartment()"
      >모달 - 부서검색</a
    >
  </section>
</template>

<script setup>
  import { defineProps, defineEmits, ref, onMounted, watch } from 'vue';
  import { global } from 'assets/js/publish/global';
  import { usePopupStore } from 'stores/popup';
  import { POPUP_TYPES } from 'assets/js/publish/popupTypes';

  //테이블
  const columns = [
    {
      name: 'name',
      align: 'center',
      label: '사용자 이름',
      field: 'name',
    },
    {
      name: 'mail',
      align: 'center',
      label: '이메일 주소',
      field: 'mail',
    },
    {
      name: 'group',
      align: 'center',
      label: '소속 그룹',
      field: 'group',
      style: 'width: 260px;',
    },
    {
      name: 'phone',
      align: 'center',
      label: '연락처',
      field: 'phone',
    },
    {
      name: 'authority',
      align: 'center',
      label: '권한',
      field: 'authority',
    },
    {
      name: 'employment',
      align: 'center',
      label: '재직상태',
      field: 'employment',
    },
    {
      name: 'modify',
      align: 'center',
      label: '수정',
      field: 'modify',
    },
  ];

  const rows = [
    {
      name: 'GSN Test_PCH(비번:Test123!)',
      mail: 'gsntest@gsneotek.com',
      group: '-',
      phone: '010-1111-2222',
      authority: 'USER',
      employment: '재직중',
    },
    {
      name: 'GSN Test_PCH(비번:Test123!)',
      mail: 'gsntest@gsneotek.com',
      group: '-',
      phone: '010-1111-2222',
      authority: 'USER',
      employment: '재직중',
    },
    {
      name: 'GSN Test_PCH(비번:Test123!)',
      mail: 'gsntest@gsneotek.com',
      group: '-',
      phone: '010-1111-2222',
      authority: 'USER',
      employment: '재직중',
    },
    {
      name: 'GSN Test_PCH(비번:Test123!)',
      mail: 'gsntest@gsneotek.com',
      group: '-',
      phone: '010-1111-2222',
      authority: 'USER',
      employment: '재직중',
    },
  ];
  const selected = ref([]);
  function getSelectedString() {
    return '';
  }

  const popup = usePopupStore();

  const openPopupUserModify = () => {
    popup.open(POPUP_TYPES.USER_MODIFY, {});
  };

  const openPopupSearchDepartment = () => {
    popup.open(POPUP_TYPES.SEARCH_DEPARTMENT, {});
  };
</script>

<style lang="scss" scoped>
  @import '/src/assets/css/set.scss';
</style>
