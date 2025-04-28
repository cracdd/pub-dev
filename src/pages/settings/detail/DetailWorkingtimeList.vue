<template>
  <div class="split-box">
    <section class="left">
      <div class="card">
        <q-table
          title=" 휴가 사용자 등록"
          style="height: 100%"
          flat
          separator="cell"
          :rows="rows"
          :columns="columns"
          row-key="name"
          :selected-rows-label="getSelectedString"
          selection="single"
          v-model:selected="selected"
          virtual-scroll
          :hide-pagination="true"
          class="table-wrap type-data"
        >
          <template v-slot:top-right>
            <a class="btn-sm btn-basic">등록</a
            ><a class="btn-sm btn-basic ml6">삭제</a>
          </template>
          <template v-slot:body-cell-modify="props">
            <q-td key="modify" :props="props">
              <a class="btn-sm btn-soft">수정</a>
            </q-td>
          </template>
        </q-table>
      </div>
    </section>
    <section class="right">
      <div class="card">
        <div class="card-title">휴일설정</div>
        <div class="calendar-box"></div>
      </div>
    </section>
  </div>
</template>

<script setup>
  import { defineProps, defineEmits, ref, onMounted, watch } from 'vue';
  import { global } from 'assets/js/publish/global';

  const columns = [
    {
      name: 'user_id',
      align: 'center',
      label: '사용자ID',
      field: 'user_id',
    },
    {
      name: 'name',
      align: 'center',
      label: '사용자명',
      field: (row) => row.name,
      format: (val) => `${val}`,
      //sortable: true,
    },
    {
      name: 'date',
      align: 'center',
      label: '등록날짜',
      field: 'date',
    },
    {
      name: 'time',
      align: 'center',
      label: '등록시간',
      field: 'time',
    },
    {
      name: 'holiday',
      align: 'center',
      label: '휴일사용',
      field: 'holiday',
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
      user_id: '12341234',
      name: '홍길동',
      date: '2025-04-01',
      time: '0900~13:00',
      holiday: '사용',
    },
    {
      user_id: '12341234',
      name: '홍길김',
      date: '2025-04-01',
      time: '0900~13:00',
      holiday: '사용',
    },
  ];
  const selected = ref([]);
  function getSelectedString() {
    return '';
  }
</script>

<style scoped>
  .split-box {
    display: flex;
    gap: 10px;
    height: 100%;
  }
  .split-box section {
    height: inherit;
  }
  .split-box section.left {
    flex: 1 1 40%;
  }
  .split-box section.right {
    flex: 1 1 60%;
  }
  .split-box section .card {
    height: inherit;
  }
  .split-box section .card .card-title {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .calendar-box {
    height: 100%;
    border: 1px solid #dedede;
  }
</style>
