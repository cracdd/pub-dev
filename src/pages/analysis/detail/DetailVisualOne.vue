<template>
  <!-- 통계 레이아웃 case 1 -->
<section class="card-top">
    <div class="tbl-detail-box">
      <div class="tbl-detail-title">
        조건 설정
        <div class="tbl-btns">
          <a class="btn-md btn-secondary">조회</a>
        </div>
      </div>
      <q-markup-table class="tbl-detail">
        <colgroup>
          <col style="" />
          <col style="width: 33%" />
          <col style="" />
          <col style="" />
        </colgroup>
        <tr>
          <th>기간</th>
          <td>
            <CallPeriodBox />
          </td>
          <th></th>
          <td></td>
        </tr>
        <tr>
          <th>대상조직</th>
          <td>
            <div class="form-mix">
              <select class="w120px">
                <option>인</option>
                <option>1</option>
                <option>2</option>
                <option>3</option>
              </select>
              <select class="w120px">
                <option>전체(D레벨)</option>
                <option>1</option>
                <option>2</option>
                <option>3</option>
              </select>
              <select class="w120px">
                <option>전체(E레벨)</option>
                <option>1</option>
                <option>2</option>
                <option>3</option>
              </select>
              <select class="w120px">
                <option>전체(사원)</option>
                <option>1</option>
                <option>2</option>
                <option>3</option>
              </select>
            </div>
          </td>
          <th></th>
          <td>
            <div class="form-mix">
              <select class="w120px">
                <option>전체</option>
                <option>1</option>
                <option>2</option>
                <option>3</option>
              </select>
              <select class="w120px">
                <option>전체</option>
                <option>1</option>
                <option>2</option>
                <option>3</option>
              </select>
              <select class="w120px">
                <option>전체</option>
                <option>1</option>
                <option>2</option>
                <option>3</option>
              </select>
            </div>
          </td>
        </tr>
      </q-markup-table>
    </div>
  </section>
  <section class="card card-column-auto">
    <h5>전체실적</h5>
    <div class="chart-box"><Line v-if="loaded" :data="chartData" :options="options2" /> </div>
  </section>
  <section class="card-row mt10">
    <div class="card">
      <h5>2025년 4월</h5>
      <div class="calendar-box mt10">

        <JobCalendar
            :events="eventList"
            :calendarCheck="calendarCheck"
            @day-click="onDayClick"
            @change-month="onMonthChange"
          />
      </div>
    </div>
    <div class="card">
      <h5>시간대별 통화건수</h5>
      <div class="chart-box mt10"><Line v-if="loaded" :data="chartData" :options="options2" /> </div>
    </div>
  </section>

</template>

<script setup>
import { defineProps, defineEmits, ref, onMounted, watch, computed } from 'vue';
import { global } from 'assets/js/publish/global';
import CallPeriodBox from 'components/CallPeriodBox.vue';
import { POPUP_TYPES } from 'assets/js/publish/popupTypes';
import JobCalendar from 'components/JobCalendar.vue'
import { Line } from 'vue-chartjs'
import { Chart as ChartJS, Title, ArcElement, Tooltip, Legend, BarElement, CategoryScale, LinearScale, PointElement, LineElement, PieController } from 'chart.js'
import ChartDataLabels from 'chartjs-plugin-datalabels'

const calendarCheck = false

// 전체 리스트
const allRows = ref([
  { id: 1, user_id: '1001', name: '120건\n02:55:01', date: '2025-05-01', time: '09:00~18:00', holiday: '사용' },
  { id: 2, user_id: '1002', name: '120건\n02:55:01', date: '2025-05-03', time: '09:00~18:00', holiday: '사용' },
  { id: 2, user_id: '1004', name: '120건\n02:55:01', date: '2025-05-07', time: '09:00~18:00', holiday: '사용' },
])

const eventList = computed(() =>
  allRows.value.map((row) => ({
    id: row.id,
    date: row.date,
    title: `${row.name}`,
    type: 'data'
  }))
)

// 필터된 행 (초기엔 전체)
const filteredRows = ref([...allRows.value])


// 날짜 클릭 시 필터링
const onDayClick = (date) => {
  filteredRows.value = allRows.value.filter(row => row.date === date)
}


function getSelectedString() {
  return '';
}


ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale, PointElement, ArcElement, LineElement, PieController, ChartDataLabels )

let loaded= ref(true);
let chartData = ref({
      labels: ['강남보상센터', '구로보상센터', '강동보상센터', '강남스마트센터', '센터1', '센터2', '센터3', '센터4', '센터5', '센터7' ],  // 데이터가 없을 때 표시할 라벨
      datasets: [
        {
          type: 'bar', // 바 차트
          label: '총건수',
          backgroundColor:  ["#f4c448"],  // 부드러운 배경색
          borderColor: 'RGBA( 100, 149, 237, 1 )',
          data: [50,20,40,5,67,89,33,88,99,33]  // 기본 데이터
        },
        {
          type: 'bar', // 바 차트
          label: '총시간',
          backgroundColor:  ['#999'],
          borderColor: 'RGBA( 154, 205, 50, 1 )',
          data: [150,80,120,10,120,500,120,200,250,133] // 기본 데이터
        }
      ]
    });

let data1 = ref({
  labels: ['응답', '요청'],
  datasets: [
    {
      labels: '   ',
      data: [0, 100],
      backgroundColor: [
        '#1E88E5',
        'RGBA( 192, 192, 192, 1 )'
      ],
      borderColor: [
        'RGBA( 255, 255, 255, 1 )',
        'RGBA( 255, 255, 255, 1 )'
      ],
      hoverBorderColor: ["#1E88E5", "RGBA( 192, 192, 192, 1 )"],
      borderWidth: 5
    }
  ]
});



function chartData1(data){

  if(data){
    chartData.value = {
      labels: dashboard2Data.value.map(item => global.ymdFormat(item.sdate) +' '+item.stime.replace('00', '')+'시'),
      datasets: [
        {
          type: 'bar', // 바 차트
          label: '총건수',
          backgroundColor: ["#f4c448"],
          borderColor: 'RGBA( 100, 149, 237, 1 )',
          data: dashboard2Data.value.map(item => item.nOffered),
          // order: 2, // 바 차트를 뒤로 보냄
        },
        {
          type: 'bar', // 바 차트
          label: '총시간',
          backgroundColor: ['#999'],
          borderColor: 'RGBA( 154, 205, 50, 1 )',
          data: dashboard2Data.value.map(item => item.tAnswered == null?0:item.tAnswered),
          // order: 2, // 바 차트를 뒤로 보냄
        }
      ]
    }
  } else {
    chartData.value = {
      labels: ['No data'],  // 데이터가 없을 때 표시할 라벨
      datasets: [
        {
          label: '총건수',
          backgroundColor: ["#f4c448"],  // 부드러운 배경색
          borderColor: 'RGBA( 220, 220, 220, 1 )',
          data: [0.1]  // 기본 데이터
        },
        {
          label: '총시간',
          backgroundColor: ["#999"],
          borderColor: 'RGBA( 220, 220, 220, 1 )',
          data: [0.1]
        }
      ]
    };
  }


  loaded.value = true
}

let options2 = ref({
  animations: {
    radius: {
      duration: 400,
      easing: 'linear',
      loop: (context) => context.active
    }
  },
  hoverRadius: 12,
  interaction: {
    mode: 'nearest',
    intersect: false,
    axis: 'x'
  },
  plugins: {
    legend: {
      display: true,
      position: "bottom",
      labels: {
        boxWidth: 8,
        padding: 30,
        usePointStyle: true,
        pointStyle: "circle",
        font: {
          size: 14
        }
      },
      fullSize: true,
      align: "center"
    },
    tooltip: {
      // mode: 'index',  // 같은 인덱스에 있는 데이터 모두 표시
      // intersect: false,  // 교차 여부 무시
      // callbacks: {
      //   // 툴팁 정렬 콜백
      //   sort(a, b) {
      //     console.log("a : ", a);
      //     const order = { '요청호': 1, '응대호': 2, '응답률(%)': 3, '서비스레벨(%)': 4 };
      //     console.log("Sort callback - a:", a.dataset.label, ", b:", b.dataset.label);
      //     return order[a.dataset.label] - order[b.dataset.label];
      //   },
      //   label(tooltipItem) {
      //     console.log('Tooltip Item:', tooltipItem);
      //     return `${tooltipItem.dataset.label}: ${tooltipItem.raw}`;
      //   },
      // },
      boxWidth: 15,
      bodyFont: {
        size: 14
      },
    },
  },
  responsive: true,
  maintainAspectRatio: true,
  elements: {
    arc: {
      borderWidth: 2
    }
  },
  animation: {
    duration: 1000
  }
});

</script>

<style scoped>
  .card-row {
    .card {
      height: 100%;
    }
  }
    
</style>
