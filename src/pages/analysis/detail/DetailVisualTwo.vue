<template>
  <!-- 통계 레이아웃 case 2 -->
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
          <col style="" />
        </colgroup>
        <tr>
          <th>기간</th>
          <td>
            <CallPeriodBox />
          </td>
        </tr>
        <tr>
          <th>대상조직</th>
          <td>
            <div class="form-mix">
              <select class="w150px">
                <option>인</option>
                <option>1</option>
                <option>2</option>
                <option>3</option>
              </select>
              <select class="w150px">
                <option>전체(D레벨)</option>
                <option>1</option>
                <option>2</option>
                <option>3</option>
              </select>
              <select class="w150px">
                <option>전체(E레벨)</option>
                <option>1</option>
                <option>2</option>
                <option>3</option>
              </select>
              <select class="w150px">
                <option>전체(사원)</option>
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
  <section class="card-row mt10">
    <div class="card">
      <h5>건당 평균 통화시간</h5>
      <div class="form-mix mt10">
        <select class="w150px">
          <option>전체</option>
          <option>1</option>
          <option>2</option>
          <option>3</option>
        </select>
        <select class="w150px">
          <option>전체</option>
          <option>1</option>
          <option>2</option>
          <option>3</option>
        </select>
      </div>
      <div class="chart-box">
        <Line v-if="loaded" :data="chartData" :options="options_bar1" />
      </div>
    </div>
    <div class="card">
      <h5>대상 유형 비율</h5>
      <div class="form-mix mt10">
        <select class="w150px">
          <option>전체</option>
          <option>1</option>
          <option>2</option>
          <option>3</option>
        </select>
      </div>
      <div class="chart-box">
        <Pie :data="dataAgent1" :options="options_pie1" />
      </div>
    </div>
  </section>
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
  import { Line, Doughnut, Pie } from 'vue-chartjs';
  import {
    Chart as ChartJS,
    Title,
    ArcElement,
    Tooltip,
    Legend,
    BarElement,
    CategoryScale,
    LinearScale,
    PointElement,
    LineElement,
    PieController,
  } from 'chart.js';
  import ChartDataLabels from 'chartjs-plugin-datalabels';
  import { global } from 'assets/js/publish/global';
  import CallPeriodBox from 'components/CallPeriodBox.vue';

  ChartJS.register(
    Title,
    Tooltip,
    Legend,
    BarElement,
    CategoryScale,
    LinearScale,
    PointElement,
    ArcElement,
    LineElement,
    PieController,
    ChartDataLabels,
  );

  let loaded = ref(true);
  let chartData = ref({
    labels: [
      '강남보상센터',
      '구로보상센터',
      '강동보상센터',
      '강남스마트센터',
      '센터1',
      '센터2',
      '센터3',
      '센터4',
      '센터5',
      '센터7',
    ], // 데이터가 없을 때 표시할 라벨
    datasets: [
      {
        type: 'bar', // 바 차트
        label: '총건수',
        backgroundColor: ['#f4c448'], // 부드러운 배경색
        borderColor: 'RGBA( 100, 149, 237, 1 )',
        data: [50, 20, 40, 5, 67, 89, 33, 88, 99, 33], // 기본 데이터
      },
      {
        type: 'bar', // 바 차트
        label: '총시간',
        backgroundColor: ['#999'],
        borderColor: 'RGBA( 154, 205, 50, 1 )',
        data: [150, 80, 120, 10, 120, 500, 120, 200, 250, 133], // 기본 데이터
      },
    ],
  });

  let data1 = ref({
    labels: ['응답', '요청'],
    datasets: [
      {
        labels: '   ',
        data: [0, 100],
        backgroundColor: ['#1E88E5', 'RGBA( 192, 192, 192, 1 )'],
        borderColor: ['RGBA( 255, 255, 255, 1 )', 'RGBA( 255, 255, 255, 1 )'],
        hoverBorderColor: ['#1E88E5', 'RGBA( 192, 192, 192, 1 )'],
        borderWidth: 5,
      },
    ],
  });

  function chartData1(data) {
    if (data) {
      chartData.value = {
        labels: dashboard2Data.value.map(
          (item) =>
            global.ymdFormat(item.sdate) +
            ' ' +
            item.stime.replace('00', '') +
            '시',
        ),
        datasets: [
          {
            type: 'bar', // 바 차트
            label: '총건수',
            backgroundColor: ['#6495ed'],
            borderColor: 'RGBA( 100, 149, 237, 1 )',
            data: dashboard2Data.value.map((item) => item.nOffered),
            // order: 2, // 바 차트를 뒤로 보냄
          },
          {
            type: 'bar', // 바 차트
            label: '총시간',
            backgroundColor: ['#9acd32'],
            borderColor: 'RGBA( 154, 205, 50, 1 )',
            data: dashboard2Data.value.map((item) =>
              item.tAnswered == null ? 0 : item.tAnswered,
            ),
            // order: 2, // 바 차트를 뒤로 보냄
          },
        ],
      };
    } else {
      chartData.value = {
        labels: ['No data'], // 데이터가 없을 때 표시할 라벨
        datasets: [
          {
            label: '총건수',
            backgroundColor: ['#f0f0f0'], // 부드러운 배경색
            borderColor: 'RGBA( 220, 220, 220, 1 )',
            data: [0.1], // 기본 데이터
          },
          {
            label: '총시간',
            backgroundColor: ['#f0f0f0'],
            borderColor: 'RGBA( 220, 220, 220, 1 )',
            data: [0.1],
          },
        ],
      };
    }

    loaded.value = true;
  }

  //bar차트 - 건당 평균 통화시간 option
  let options_bar1 = ref({
    scales: {
      x: {
        beginAtZero: true,
        grid: {
          color: 'transparent',
        },
      },
    },
    animations: {
      radius: {
        duration: 400,
        easing: 'linear',
        loop: (context) => context.active,
      },
    },
    hoverRadius: 12,
    interaction: {
      mode: 'nearest',
      intersect: false,
      axis: 'x',
    },
    plugins: {
      legend: {
        display: true,
        position: 'bottom',
        labels: {
          boxWidth: 12,
          boxHeight: 12,
          usePointStyle: true,
          pointStyle: 'rect',
          font: {
            size: 12,
          },
        },
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
          size: 14,
        },
      },
    },
    responsive: true,
    maintainAspectRatio: false,
    elements: {
      arc: {
        borderWidth: 2,
      },
    },
    animation: {
      duration: 1000,
    },
  });

  onMounted(() => {
    dataAgent1.value = {
      labels: ['고객', '파트너', '제외번호', '임직원'],
      datasets: [
        {
          borderWidth: 5,
          backgroundColor: [
            '#77a6b8',
            '#e85a70',
            '#999999',
            '#f4c448',
            '#FDD835',
          ],
          hoverBackgroundColor: [
            '#77a6b8',
            '#e85a70',
            '#999999',
            '#f4c448',
            '#FDD835',
          ],
          hoverBorderColor: [
            '#77a6b8',
            '#e85a70',
            '#999999',
            '#f4c448',
            '#FDD835',
          ],
          data: [
            Number(10) || 0,
            Number(20) || 0,
            Number(30) || 0,
            Number(40) || 0,
          ],
        },
      ],
    };
  });

  // 도넛 데이터 시작-----------------------------------------------------------------

  let dataAgent1 = ref({
    labels: ['No data'],
    datasets: [
      {
        data: [0.1], // 기본 도넛 데이터
        backgroundColor: ['#f0f0f0'], // 부드러운 배경색
        hoverBackgroundColor: ['#f0f0f0'], // hover 시에도 동일한 색상 유지
        hoverBorderColor: ['#f0f0f0'],
      },
    ],
  });

  //pie차트 - 대상 유형 비율 option
  let options_pie1 = {
    radius: '100%',
    plugins: {
      datalabels: {
        color: '#000', //'#fff',
        font: {
          weight: 'bold',
          size: 18,
        },
        formatter: (value, context) => {
          const data = context.chart.data.datasets[0].data;
          const total = data.reduce((a, b) => a + b, 0);
          const percent = total > 0 ? ((value / total) * 100).toFixed(1) : 0;
          return `${percent}%`;
        },
      },
      legend: {
        display: true,
        position: 'bottom',
        labels: {
          boxWidth: 12,
          boxHeight: 12,
          usePointStyle: true,
          pointStyle: 'rect',
          font: {
            size: 12,
          },
        },
      },
      tooltip: {
        boxWidth: 15,
        bodyFont: {
          size: 12,
        },
        displayColors: false,
        callbacks: {
          title: () => '',
          label: (context) => `${context.label} : ${context.parsed}`,
        },
      },
    },
    responsive: true,
    maintainAspectRatio: false,
    elements: {
      arc: {
        borderWidth: 2,
      },
    },
    animation: {
      duration: 1000,
    },
  };
</script>

<style scoped>
  .card-row {
    .card {
      height: 100%;
    }
  }
  .chart-box {
    margin-top: 30px;
  }
</style>
