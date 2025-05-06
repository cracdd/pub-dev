<template>
  <div class="player-box">
    <p class="player-info">
      <b
        ><i
          >{{ callDetail?.name ? callDetail?.name + ' 님' : ''
          }}{{ callDetail?.callId ? ' ( ' + callDetail?.callId + ' )' : '' }}
          / 2025-0101_12345.wav
        </i></b
      >
      <a href="javascript:;" class="btn-sm btn-ghost">청취</a>
    </p>

    <!-- 청취 시 활성화 : active -->
    <ul class="player-item active">
      <li>
        <a
          href="#"
          class="play-btn"
          @click="play = !play"
          :class="play ? 'play' : 'pause'"
        ></a>
      </li>
      <li class="timer">
        <span>2:47</span>
        <i>/</i>
        <em>3:29</em>
      </li>
      <li class="bar">
        <span><i style="width: 60%"></i></span>
      </li>
      <li>
        <a
          href="#"
          class="play-btn"
          @click="volume = !volume"
          :class="volume ? 'volume' : 'mute'"
        ></a>
      </li>
    </ul>
  </div>
</template>

<script setup>
  import { ref } from 'vue';

  //오디오 play/pause 버튼
  const play = ref(false);
  //오디오 volume/mute 버튼
  const volume = ref(false);
</script>
