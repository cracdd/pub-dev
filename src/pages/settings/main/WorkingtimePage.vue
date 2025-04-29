<template>
  <div class="settings-mid">
    <div class="title-box">
      <div class="title">조건 설정</div>
      <div class="btns">
        <a href="javascript:;" class="btn-md btn-secondary">전체적용</a>
      </div>
    </div>
    <form class="form-box">
      <div class="form-mix">
        <label>기간</label>
        <CallTimeBox />
      </div>
    </form>
    <div class="tbl-box">
      <q-table
        title="근무 시간 변경"
        style="height: 100%"
        flat
        separator="cell"
        :rows="rows"
        :columns="columns"
        row-key="name"
        selection="single"
        v-model:selected="selected"
        :selected-rows-label="getSelectedString"
        virtual-scroll
        :hide-pagination="true"
        class="table-wrap type-data"
      >
        <template v-slot:top-right>
          <a class="btn-sm btn-basic" @click="openPopupWorkingTimeRegister()"
            >등록</a
          ><a class="btn-sm btn-basic ml6">삭제</a>
        </template>
        <template v-slot:body-cell-modify="props">
          <q-td key="modify" :props="props">
            <a class="btn-sm btn-soft">수정</a>
          </q-td>
        </template>
      </q-table>
    </div>
  </div>
</template>

<script setup>
  import { defineProps, defineEmits, ref, onMounted, watch } from 'vue';
  import { global } from 'assets/js/publish/global';
  import CallTimeBox from 'components/CallTimeBox.vue';
  import { usePopupStore } from 'stores/popup';
  import { POPUP_TYPES } from 'assets/js/publish/popupTypes';

  const columns = [
    {
      name: 'name',
      align: 'center',
      label: '등록날짜',
      field: 'name',
    },
    {
      name: 'time',
      align: 'center',
      label: '등록시간',
      field: 'time',
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
      name: '2022-04-01',
      time: '0900~13:00',
      modify: '',
    },
    {
      name: '2025-04-02',
      time: '0900~13:00',
      modify: '',
    },
  ];
  const selected = ref([]);
  function getSelectedString() {
    return selected.value.length === 0
      ? ''
      : `${selected.value.length} record${
          selected.value.length > 1 ? 's' : ''
        } selected of ${rows.length}`;
  }

  const popup = usePopupStore();

  const openPopupWorkingTimeRegister = () => {
    popup.open(POPUP_TYPES.REGISTER_WORKING, {});
  };
</script>
<style scoped>
  .tbl-box {
    margin-top: 64px;
  }
</style>
