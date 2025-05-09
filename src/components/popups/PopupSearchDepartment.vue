<template>
  <div class="popup-container" :class="visible ? 'active' : ''">
    <div class="popup-wrap">
      <div class="popup-header">
        <b class="title">부서 검색</b>
        <a href="#" class="close" @click.prevent="onClose"></a>
      </div>
      <div class="popup-body">
        <div class="form-col-wrap search-box">
          <form class="form-box w100p">
            <div class="form-mix">
              <select class="w100px">
                <option>부서명</option>
              </select>
              <input
                type="text"
                placeholder="검색어를 입력해 주세요."
                class=""
              />
              <a class="btn-md btn-basic">검색</a>
            </div>
          </form>
        </div>
        <div class="box-item type-line h400px treeList">
          <ul class="tree depth1">
            <TreeNode
              v-for="node in treeData"
              :key="node.id"
              :node="node"
              :depth="1"
              :selected-id="selectedId"
              @select="handleSelect"
            />
          </ul>
        </div>
      </div>
      <div class="popup-footer">
        <a
          href="javascript:;"
          class="btn-md btn-ghost close"
          data-dismiss="modalPopup"
          @click.prevent="onClose"
          >취소</a
        >
        <a
          href="javascript:;"
          class="btn-md btn-secondary close"
          data-dismiss="modalPopup"
          @click.prevent="onClose"
          >선택</a
        >
      </div>
    </div>
  </div>
</template>

<script setup>
  import { ref, watch, onMounted, reactive } from 'vue';
  import TreeNode from 'components/TreeNode.vue';

  const treeData = reactive([
    {
      id: 'cat01',
      name: 'Category 01',
      isOpen: true,
      children: [
        {
          id: 'group01',
          name: 'Group 01',
          isOpen: true,
          children: [
            { id: 'sub01a', name: 'Sub Group 01' },
            { id: 'sub01b', name: 'Sub Group 01' },
          ],
        },
        {
          id: 'group02',
          name: 'Group 02',
          isOpen: true,
          children: [
            { id: 'sub02a', name: 'Sub Group 01' },
            { id: 'sub02b', name: 'Sub Group 01' },
          ],
        },
        {
          id: 'group03',
          name: 'Group 03 - 자식없음',
        },
      ],
    },
    {
      id: 'cat02-1',
      name: 'Category 02',
      children: [{ id: 'group04', name: 'Group 01' }],
    },
    {
      id: 'cat02-2',
      name: 'Category 02',
      children: [{ id: 'group05', name: 'Group 01' }],
    },
    {
      id: 'cat02-3',
      name: 'Category 02',
      children: [{ id: 'group06', name: 'Group 01' }],
    },
    {
      id: 'cat02-4',
      name: 'Category 02',
      children: [{ id: 'group07', name: 'Group 01' }],
    },
    {
      id: 'cat02-5',
      name: 'Category 02',
      children: [{ id: 'group08', name: 'Group 01' }],
    },
  ]);

  const props = defineProps({
    visible: Boolean,
    initData: Object,
  });

  onMounted(() => {
    console.log('팝업에 전달된 데이터:', props.initData);
  });

  watch(
    () => props.initData,
    (val) => {
      if (val) {
        console.log('💡 새로운 팝업 데이터 감지:', val);
      }
    },
    { immediate: true },
  );

  const emit = defineEmits(['update:visible', 'submit']);

  const onClose = () => {
    emit('update:visible', false);
  };
</script>

<style lang="scss" scoped>
  .register-box {
    .form-box {
      .form-mix {
        label {
          flex-basis: 200px;
        }
        &__radio {
          label {
            margin-right: 24px;
          }
        }
      }
    }
  }
  .popup-wrap {
    &.w720px {
      width: 720px;
    }
    .popup-footer {
      margin-top: 20px;
    }
  }
</style>
