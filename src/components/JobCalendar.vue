<template>
  <div class="calendar-container">
    <div class="row items-center justify-between q-pa-sm" v-show="calendarMode">
      <div class="text-h6">{{ yearMonthLabel }}</div>
      <div>
        <q-btn flat icon="chevron_left" @click="prev" />
        <q-btn flat icon="chevron_right" @click="next" />
        <q-btn flat label="Today" @click="moveToToday" />
      </div>
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
        :day-height="calendarMode?100:75"
        :hoverable="true"
        :focusable="true"
        :focus-type="['day']"
        transition-prev="slide-right"
        transition-next="slide-left"
        @click-day="handleClickDay"
        @change="handleMonthChange"

      >
      <template #day="{ scope }">
        <div v-for="(event, idx) in getVisibleEvents(scope.timestamp.date)" :key="event.id + '-' + idx">
          <q-chip
            v-show="calendarMode"
            dense
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
import { ref, computed, onMounted } from 'vue'
import {
  today,
  parseTimestamp
} from '@quasar/quasar-ui-qcalendar'

const props = defineProps({
  events: {
    type: Array,
    default: () => []
  },
  calendarCheck: Boolean,
})

const calendarMode = computed(() => props.calendarCheck)

const emit = defineEmits(['day-click', 'change-month'])

const selectedDate = ref(today())
const nowDate = today()
const calendarRef = ref(null)

const yearMonthLabel = ref('')

const updateLabel = (dateStr) => {
  const parsed = parseTimestamp(dateStr)
  yearMonthLabel.value = `${parsed.year}년 ${parsed.month}월`
}

const eventsMap = computed(() => {
  const map = {}
  props.events.forEach(event => {
    if (!map[event.date]) {
      map[event.date] = []
    }
    map[event.date].push(event)
  })
  return map
})

const getVisibleEvents = (date) => {
  return eventsMap.value[date]?.slice(0, 2) || []
}

const getHiddenCount = (date) => {
  const total = eventsMap.value[date]?.length || 0
  return total > 2 ? total - 2 : 0
}

const handleClick = (event) => {
  const date = event?.scope?.timestamp?.date
  if (date) {
    emit('day-click', date)
  } else {
    console.warn('❗ 캘린더 클릭 이벤트 오류: scope 또는 timestamp 없음', event)
  }
}

const handleClickDay = ({ scope }) => {
  if (!scope?.timestamp?.date) {
    console.warn('❗ 날짜 클릭 오류', scope)
    return
  }
  emit('day-click', scope.timestamp.date)
}

const handleMonthChange = ({ start, end }) => {
  emit('change-month', start)
  updateLabel(selectedDate.value) //현재 중심 날짜로 연/월 표시
}

const getColor = (event) => {
  if (event.type === 'dept') return 'red'
  if (event.type === 'employee') return 'indigo'
  if (event.type === 'data') return ''
  return 'primary'
}

const moveToToday = () => {
  calendarRef.value.moveToToday()
}

const prev = () => {
  calendarRef.value.prev()
}

const next = () => {
  calendarRef.value.next()
}

onMounted(() => {
  updateLabel(selectedDate.value)
})

</script>
<style scoped>
.calendar-container {
  width: 100%;
  max-width: 1000px;
  margin: 0 auto;
  height : 100%;
  /* height: 700px; */
  border: 1px solid #dedede;
}

.event-content {
  white-space: pre-line;
  line-height: 1.2;
  font-size: 9px;
  color: #e34d4d;
  background: none;
  padding:3px 10px;
  margin-top:20px;
}


</style>
