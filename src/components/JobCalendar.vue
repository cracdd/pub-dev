<template>
  <div class="calendar-container">
    <div class="caldendar-title" v-show="calendarMode">
      <q-btn flat icon="chevron_left" @click="prev" />
      <div class="text-h6">{{ yearMonthLabel }}</div>
      <q-btn flat icon="chevron_right" @click="next" />
      <q-btn flat label="Today" @click="moveToToday" class="btn-today" />
    </div>

    <q-calendar-month
      ref="calendarRef"
      v-model="selectedDate"
      :now="nowDate"
      locale="ko-kr"
      animated
      no-active-date
      view="month"
      :key="calendarMode"
      :day-height="calendarMode ? '' : 75"
      :hoverable="true"
      :focusable="true"
      :focus-type="['day']"
      transition-prev="slide-right"
      transition-next="slide-left"
      @click-day="handleClickDay"
      @change="handleMonthChange"
    >
      <template #day="{ scope }">
        <div
          v-for="(event, idx) in getVisibleEvents(scope.timestamp.date)"
          :key="event.id + '-' + idx"
        >
          <q-chip
            v-show="calendarMode"
            dense
            square
            size="12px"
            :color="getColor(event)"
            text-color="white"
          >
            {{ event.title }}
          </q-chip>
          <div
            v-show="!calendarMode"
            class="event-content"
            :style="{ backgroundColor: getColor(event) }"
          >
            {{ event.title }}
          </div>
        </div>

        <q-chip
          v-if="getHiddenCount(scope.timestamp.date) > 0"
          dense
          square
          size="12px"
          color="grey"
          text-color="white"
        >
          +{{ getHiddenCount(scope.timestamp.date) }} more
        </q-chip>
      </template>
    </q-calendar-month>
  </div>
</template>

<script setup>
  import { ref, computed, onMounted } from 'vue';
  import { today, parseTimestamp } from '@quasar/quasar-ui-qcalendar';

  const props = defineProps({
    events: {
      type: Array,
      default: () => [],
    },
    calendarCheck: Boolean,
  });

  const calendarMode = computed(() => props.calendarCheck);

  const emit = defineEmits(['day-click', 'change-month']);

  const selectedDate = ref(today());
  const nowDate = today();
  const calendarRef = ref(null);

  const yearMonthLabel = ref('');

  const updateLabel = (dateStr) => {
    const parsed = parseTimestamp(dateStr);
    yearMonthLabel.value = `${parsed.year}년 ${parsed.month}월`;
  };

  const eventsMap = computed(() => {
    const map = {};
    props.events.forEach((event) => {
      if (!map[event.date]) {
        map[event.date] = [];
      }
      map[event.date].push(event);
    });
    return map;
  });

  const getVisibleEvents = (date) => {
    return eventsMap.value[date]?.slice(0, 2) || [];
  };

  const getHiddenCount = (date) => {
    const total = eventsMap.value[date]?.length || 0;
    return total > 2 ? total - 2 : 0;
  };

  const handleClick = (event) => {
    const date = event?.scope?.timestamp?.date;
    if (date) {
      emit('day-click', date);
    } else {
      console.warn(
        '❗ 캘린더 클릭 이벤트 오류: scope 또는 timestamp 없음',
        event,
      );
    }
  };

  const handleClickDay = ({ scope }) => {
    if (!scope?.timestamp?.date) {
      console.warn('❗ 날짜 클릭 오류', scope);
      return;
    }
    emit('day-click', scope.timestamp.date);
  };

  const handleMonthChange = ({ start, end }) => {
    emit('change-month', start);
    updateLabel(selectedDate.value); //현재 중심 날짜로 연/월 표시
  };

  const getColor = (event) => {
    if (event.type === 'dept') return 'red';
    if (event.type === 'employee') return 'grey-8';
    if (event.type === 'data') return '';
    return 'primary';
  };

  const moveToToday = () => {
    calendarRef.value.moveToToday();
  };

  const prev = () => {
    calendarRef.value.prev();
  };

  const next = () => {
    calendarRef.value.next();
  };

  onMounted(() => {
    updateLabel(selectedDate.value);
  });
</script>
<style lang="scss" scoped>
  .calendar-container {
    width: 100%;
    height: 100%;
    max-width: 1000px;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    .caldendar-title {
      position: relative;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 15px 0;
      .btn-today {
        position: absolute;
        right: 20px;
        font-size: 13px;
        color: #f89902;
        text-decoration: underline;
      }
    }
  }

  .event-content {
    white-space: pre-line;
    line-height: 1.2;
    font-size: 9px;
    color: #e34d4d;
    background: none;
    padding: 3px 10px;
    margin-top: 20px;
  }

  .q-chip {
    width: 100%;
    height: 20px;
    padding: 0;
    margin: 0;
    border-radius: 0;
    justify-content: center;
    :deep(.q-chip__content) {
      justify-content: center;
      text-align: center;
    }
  }
  .q-calendar {
    :deep(.q-calendar-month__head) {
      border-top: 1px solid #e0e0e0;
      background-color: #f5f5f7;
      .q-calendar-month__head--weekday {
        padding: 7px 0;
      }
    }
    :deep(.q-calendar-month__body) {
      .q-calendar-month__week--wrapper {
        //min-height: 120px !important;
        flex-grow: 1;
        .q-calendar-month__day {
          &.q-current-day {
            .q-calendar__button {
              margin: 2px 0;
              min-width: 30px;
              min-height: 30px;
              border: 2px solid #4a4840;
            }
          }
        }
      }
    }
  }
</style>
