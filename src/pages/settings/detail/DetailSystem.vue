<template>
  <section class="card-top">
    <div class="tbl-detail-box">
      <div class="tbl-detail-title">
        조회 설정
        <div class="tbl-btns">
          <a class="btn-md btn-secondary">조회</a>
        </div>
      </div>
      <table class="tbl-detail">
        <colgroup>
          <col style="" />
          <col style="width: 33%" />
          <col style="" />
          <col style="width: 33%" />
          <col style="" />
          <col style="" />
        </colgroup>
        <tr>
          <th>코드북 코드</th>
          <td><input type="text" placeholder="" class="w140px" /></td>
          <th>사용여부</th>
          <td>
            <select class="w140px">
              <option>사용중</option>
              <option></option>
            </select>
          </td>
          <th></th>
          <td></td>
        </tr>
      </table>
    </div>
  </section>

  <section class="card multi">
    <!--검색결과-->
    <div class="card__conts">
      <q-table
          title="검색결과"
          style="height: 300px"
          flat
          separator="cell"
          :rows="resultRows"
          :columns="resultColumns"
          row-key="name"
          :selected-rows-label="getSelectedString"
          v-model:selected="selected"
          :hide-pagination="true"
          :rows-per-page-options="[0]"
          class="table-wrap type-data"
        >
          <template v-slot:top-right>
            <a class="btn-sm btn-ghost">초기화</a>
            <a class="btn-sm btn-basic ml5">수정</a>
          </template>
        </q-table>
        <div class="settings-mid pd0">
          <h5 class="mt25">코드셋 정보 등록/수정</h5>
          <form class="form-box mt20">
            <div class="form-mix">
              <label>코드셋 코드</label>
              <input type="text" placeholder="" value="AGT001" class="w100p" />
            </div>
            <div class="form-mix">
              <label>코드셋 설명</label>
              <input type="text" placeholder="코드셋 설명" value="" class="w100p" />
            </div>
            <div class="form-mix">
              <label>코드셋명</label>
              <input type="text" placeholder="" value="상담사 상태코드" class="w100p" />
            </div>
            <div class="form-mix">
              <label>사용여부</label>
              <div class="h40px pt10 w100p">
                <label class="radio-item">
									<input type="radio" name="radio1" checked>
									<span>Y</span>
								</label>
								<label class="radio-item ml25">
									<input type="radio" name="radio1">
									<span>N</span>
								</label>
              </div>
            </div>
          </form>
        </div>
    </div>

    <!--상세결과-->
    <div class="card__conts">
      <q-table
          title="상세결과"
          style="height: 300px"
          flat
          separator="cell"
          :rows="detailRows"
          :columns="detailColumns"
          row-key="name"
          :selected-rows-label="getSelectedString"
          v-model:selected="selected"
          :hide-pagination="true"
          :rows-per-page-options="[0]"
          class="table-wrap type-data"
        >
          <template v-slot:top-right>
            <a class="btn-sm btn-ghost">초기화</a>
            <a class="btn-sm btn-basic ml5">수정</a>
          </template>
      </q-table>

      <div class="card__conts__codeInfo">
        <div class="settings-mid pd0">
          <form class="form-box mt20">
            <div class="form-mix">
              <label>코드</label>
              <input type="text" placeholder="" value="01" class="w100p" />
            </div>
            <div class="form-mix">
              <label>코드 설명</label>
              <input type="text" placeholder="코드 설명" value="" class="w100p" />
            </div>
            <div class="form-mix">
              <label>기타1</label>
              <input type="text" placeholder="" value="" class="w100p" />
            </div>
            <div class="form-mix">
              <label>기타3</label>
              <input type="text" placeholder="" value="" class="w100p" />
            </div>
            <div class="form-mix">
              <label>기타5</label>
              <input type="text" placeholder="" value="" class="w100p" />
            </div>
          </form>
        </div>
        <div class="settings-mid pd0">
          <form class="form-box mt20">
          <div class="form-mix">
            <label>코드명</label>
            <input type="text" placeholder="" value="" class="w100p" />
          </div>
          <div class="form-mix">
            <label>사용여부</label>
            <div class="h40px pt10 w100p">
              <label class="radio-item">
                <input type="radio" name="radio1" checked>
                <span>Y</span>
              </label>
              <label class="radio-item ml25">
                <input type="radio" name="radio1">
                <span>N</span>
              </label>
            </div>
          </div>
          <div class="form-mix">
            <label>기타2</label>
            <input type="text" placeholder="" value="" class="w100p" />
          </div>
          <div class="form-mix">
            <label>기타4</label>
            <input type="text" placeholder="" value="" class="w100p" />
          </div>
          <div class="form-mix">
            <label>기타6</label>
            <input type="text" placeholder="" value="" class="w100p" />
          </div>
          </form>
        </div>
      </div>

    </div>
  </section>
  
</template>

<script setup>
import { defineProps, defineEmits, ref, onMounted, watch } from 'vue'
import { global } from 'assets/js/publish/global'

const resultColumns = [
    {
      name: 'code',
      align: 'center',
      label: '코드셋 코드',
      field: 'code',
    },
    {
      name: 'name',
      align: 'center',
      label: '코드셋명',
      field: 'name',
    },
    {
      name: 'explanation',
      align: 'center',
      label: '설명',
      field: 'explanation',
      style: 'width:40%'
    },
    {
      name: 'use',
      align: 'center',
      label: '사용여부',
      field: 'use',
    },
  ];

  const resultRows = [
    {
      code:'AGT001',
      name:'상담사 상태코드',
      explanation:'',
      use:'사용중',
    },
    {
      code:'AGT001',
      name:'상담사 상태코드',
      explanation:'',
      use:'사용중',
    },
    {
      code:'AGT001',
      name:'상담사 상태코드',
      explanation:'',
      use:'사용중',
    },
    {
      code:'AGT001',
      name:'상담사 상태코드',
      explanation:'',
      use:'사용중',
    },
    {
      code:'AGT001',
      name:'상담사 상태코드',
      explanation:'',
      use:'사용중',
    },
    {
      code:'AGT001',
      name:'상담사 상태코드',
      explanation:'',
      use:'사용중',
    },
  ];

  const detailColumns = [
  {
      name: 'code',
      align: 'center',
      label: '코드셋 코드',
      field: 'code',
    },
    {
      name: 'name',
      align: 'center',
      label: '코드셋명',
      field: 'name',
    },
    {
      name: 'explanation',
      align: 'center',
      label: '설명',
      field: 'explanation',
      style: 'width:40%'
    },
    {
      name: 'use',
      align: 'center',
      label: '사용여부',
      field: 'use',
    },
  ];
  const detailRows = [
    {
      code:'11',
      name:'점심식사',
      explanation:'',
      use:'사용중',
    },
    {
      code:'11',
      name:'점심식사',
      explanation:'',
      use:'사용중',
    },
    {
      code:'11',
      name:'점심식사',
      explanation:'',
      use:'사용중',
    },
  ];

  const selected = ref([]);

  function getSelectedString() {
    return '';
  }
</script>

<style lang="scss" scoped>
  @import "/src/assets/css/set.scss";

  .card{
    &.multi{
      .card__conts{
        .settings-mid{
          .form-box{
            padding:0;
            .form-mix{
              label{
                font-size:12px;
                font-weight: 600;
                color:#333;
              }
            }
          }
        }
      }
    }
  }

</style>

<style>
.table-wrap.type-data thead th{
    position:sticky;
    top:0;
    z-index:2;
}
</style>


