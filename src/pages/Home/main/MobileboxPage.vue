<template>
  <section class="contents-c-body">
    <div class="text-title text-lg">모바일 Box</div>
    <div class="mBox-wrap">
      <div class="mBox-title">고애주님(2025-0101012345)</div>
      <div class="inner">
        <div class="prev" @click="openPopupImageZoom()">
          <p class="item type-img active">
            <img src="../../../assets/images/ex-img.png" alt="" />
          </p>
          <p class="item type-file">
            <i class="file-ico lg type4"></i>
            <span>PDF 파일입니다.</span>
          </p>
        </div>
      </div>
      <div class="inner">
        <p class="text-title font-b">파일 상세정보</p>
        <ul class="ul-list-row">
          <li>
            <b>고객명</b>
            <span>홍길동님</span>
          </li>
          <li>
            <b>전화번호</b>
            <span>010-2325-5628</span>
          </li>
          <li>
            <b>접수번호</b>
            <span>2025-0101012345</span>
          </li>
          <li>
            <b>파일명</b>
            <span>KakaoTalk_Photo_2025-03-31.jpg</span>
          </li>
          <li>
            <b>종류</b>
            <span>이미지</span>
          </li>
          <li>
            <b>확장자</b>
            <span>JPG</span>
          </li>
          <li>
            <b>크기</b>
            <span>2.3 MB</span>
          </li>
          <li>
            <b>생성 날짜</b>
            <span>2025. 03. 31. 오후 8:22</span>
          </li>
        </ul>
      </div>
    </div>
  </section>
</template>
<script setup>
  import { ref, onMounted, watch, computed } from 'vue';
  import { usePopupStore } from 'stores/popup';
  import { POPUP_TYPES } from 'assets/js/publish/popupTypes';
  const popup = usePopupStore();

  const openPopupImageZoom = () => {
    popup.open(POPUP_TYPES.IMAGE_ZOOM, {
      message: '직접선택에서 열었어요!',
      from: '직접선택',
    });
  };

  // 팝업 결과 수신
  watch(
    () => popup.result,
    (newVal) => {
      if (newVal) {
        console.log('팝업에서 받은 결과:', newVal);
        // popup.result = null  // 필요 시 초기화
      }
    },
  );
</script>
