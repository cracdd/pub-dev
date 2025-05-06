<template>
  <component
    :is="componentMap[popup.name]"
    v-if="popup.visible"
    :visible="popup.visible"
    :init-data="popup.initData"
    @submit="popup.submit"
    @update:visible="popup.close"
  />
</template>

<script setup>
  import { usePopupStore } from 'stores/popup';
  import PopupForm from 'components/popups/PopupForm.vue';
  import PopupFormDirect from 'components/popups/PopupFormDirect.vue';
  import popupAlert from 'components/popups/popupAlert.vue';
  import PopupHistory from 'components/popups/PopupHistory.vue';
  import PopupWorkingTimeRegister from 'components/popups/PopupWorkingTimeRegister.vue';
  import PopupHolidayRegister from 'components/popups/PopupHolidayRegister.vue';
  import { POPUP_TYPES } from 'assets/js/publish/popupTypes';
  import PopupUserModify from './popups/PopupUserModify.vue';
  import PopupCategoryModify from './popups/PopupCategoryModify.vue';
  import PopupImageZoom from './popups/PopupImageZoom.vue';

  const popup = usePopupStore();

  // 등록 가능한 팝업 컴포넌트
  const componentMap = {
    [POPUP_TYPES.FORM]: PopupForm,
    [POPUP_TYPES.DIRECT]: PopupFormDirect,
    [POPUP_TYPES.ALERT]: popupAlert,
    [POPUP_TYPES.HISTORY]: PopupHistory,
    [POPUP_TYPES.REGISTER_WORKING]: PopupWorkingTimeRegister,
    [POPUP_TYPES.REGISTER_HOLIDAY]: PopupHolidayRegister,
    [POPUP_TYPES.USER_MODIFY]: PopupUserModify,
    [POPUP_TYPES.CATEGORY_MODIFY]: PopupCategoryModify,
    [POPUP_TYPES.IMAGE_ZOOM]: PopupImageZoom,
  };
</script>
