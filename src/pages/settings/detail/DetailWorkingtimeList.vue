<template>
  <div class="split-box">
    <section class="left">
      <div class="card">
        <q-table
          title=" 휴가 사용자 등록"
          style="height: 100%"
          flat
          separator="cell"
          :rows="filteredRows"
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
            <a class="btn-sm btn-basic" @click="openPopupHolidayRegister()"
              >등록</a
            ><a class="btn-sm btn-basic ml6">삭제</a>
          </template>
          <template v-slot:body-cell-modify="props">
            <q-td key="modify" :props="props">
              <a class="btn-sm btn-soft" @click="openPopupHolidayRegister()"
                >수정</a
              >
            </q-td>
          </template>
          <!-- 데이터 없을 때 빈 영역 처리 -->
          <template v-slot:no-data>
            <!-- 아무것도 안 넣으면 완전히 숨김 -->
          </template>

          <template v-slot:no-results>
            <!-- 필터 검색 결과 없을 때도 숨김 -->
          </template>
        </q-table>
      </div>
    </section>
    <section class="right">
      <div class="card">
        <div class="card-title">휴일설정</div>
        <div class="calendar-box type-full">
          <JobCalendar
            :events="eventList"
            :calendarCheck="calendarCheck"
            @day-click="onDayClick"
            @change-month="onMonthChange"
          />
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
  import {
    defineProps,
    defineEmits,
    ref,
    onMounted,
    watch,
    computed,
  } from 'vue';
  import { global } from 'assets/js/publish/global';
  import { usePopupStore } from 'stores/popup';
  import { POPUP_TYPES } from 'assets/js/publish/popupTypes';
  import JobCalendar from 'components/JobCalendar.vue';

  const calendarCheck = true;

  // 전체 리스트
  const allRows = ref([
    {
      id: 1,
      user_id: '1001',
      name: '홍길동',
      date: '2025-05-01',
      time: '09:00~18:00',
      holiday: '사용',
    },
    {
      id: 2,
      user_id: '1002',
      name: '강대리',
      date: '2025-05-03',
      time: '09:00~18:00',
      holiday: '사용',
    },
    {
      id: 3,
      user_id: '1003',
      name: '김대리',
      date: '2025-05-03',
      time: '09:00~18:00',
      holiday: '사용',
    },
    {
      id: 4,
      user_id: '1004',
      name: '홍과장',
      date: '2025-05-07',
      time: '09:00~18:00',
      holiday: '사용',
    },
    {
      id: 5,
      user_id: '1005',
      name: '곽차장',
      date: '2025-05-07',
      time: '09:00~18:00',
      holiday: '사용',
    },
    {
      id: 6,
      user_id: '1006',
      name: '홍과장',
      date: '2025-05-07',
      time: '09:00~18:00',
      holiday: '사용',
    },
    {
      id: 7,
      user_id: '1007',
      name: '곽차장',
      date: '2025-05-07',
      time: '09:00~18:00',
      holiday: '사용',
    },
    {
      id: 8,
      user_id: '1008',
      name: '홍과장',
      date: '2025-05-07',
      time: '09:00~18:00',
      holiday: '사용',
    },
    {
      id: 9,
      user_id: '1009',
      name: '곽차장',
      date: '2025-05-07',
      time: '09:00~18:00',
      holiday: '사용',
    },
  ]);

  const eventList = computed(() =>
    allRows.value.map((row) => ({
      id: row.id,
      date: row.date,
      title: `${row.name} 연차`,
      type: 'employee',
    })),
  );

  // 필터된 행 (초기엔 전체)
  const filteredRows = ref([...allRows.value]);

  const selected = ref([]);

  const columns = [
    { name: 'user_id', label: '사번', field: 'user_id', align: 'center' },
    { name: 'name', label: '이름', field: 'name', align: 'center' },
    { name: 'date', label: '날짜', field: 'date', align: 'center' },
    { name: 'time', label: '시간', field: 'time', align: 'center' },
    { name: 'holiday', label: '휴일여부', field: 'holiday', align: 'center' },
    { name: 'modify', align: 'center', label: '수정', field: 'modify' },
  ];

  // 날짜 클릭 시 필터링
  const onDayClick = (date) => {
    filteredRows.value = allRows.value.filter((row) => row.date === date);
  };

  // 전체보기
  const resetFilter = () => {
    filteredRows.value = [...allRows.value];
  };

  function getSelectedString() {
    return '';
  }

  const popup = usePopupStore();

  const openPopupHolidayRegister = () => {
    popup.open(POPUP_TYPES.REGISTER_HOLIDAY, {});
  };

  const onMonthChange = (startDate) => {
    console.log('달 변경됨:', startDate);
  };
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
    flex: 1 1 45%;
  }
  .split-box section.right {
    flex: 1 1 55%;
  }
  .card {
    height: 100%;
  }
  .card-title {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
</style>
