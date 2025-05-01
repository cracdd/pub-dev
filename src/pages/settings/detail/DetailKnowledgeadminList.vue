<template>

  <!--admin-->
  <section class="card">
    <div class="titleBox mb30">
      <div class="text-title lg">지식창고 메뉴관리</div>
      <div class="titleBox__btns">
        <a href="javascript:;" class="btn-sm btn-soft">메뉴추가</a>
        <a href="javascript:;" class="btn-sm btn-ghost">게시물 관리</a>
      </div>
    </div>

    <div class="adminBox">
      <table>
        <colgroup>
          <col style="width:20%"/>
          <col style="width:80%"/>
        </colgroup>
        <tr>
          <th>상위메뉴</th>
          <td><input type="text" class="w400px" value="" /></td>
        </tr>
        <tr>
          <th>메뉴ID</th>
          <td><input type="text" class="w400px" value="" /></td>
        </tr>
        <tr>
          <th>메뉴명</th>
          <td><input type="text" class="w400px" value="" /></td>
        </tr>
        <tr>
          <th>Depth</th>
          <td><input type="text" class="w400px" value="" /></td>
        </tr>
        <tr>
          <th>화면경로</th>
          <td><input type="text" class="w400px" value="" /></td>
        </tr>
        <tr>
          <th>만료날짜</th>
          <td>
            <div class="form-mix">
              <div class="input-mix type-datepicker w400px">
                <span class="unit">
                  <a href="javascript:;" class="btn-ico type-text"></a>
                </span>
                <input type="text" placeholder="yyyy-mm-dd" value="2022-11-01" readonly />
              </div>
            </div>
          </td>
        </tr>
        <tr>
          <th>사용권한</th>
          <td>
            <select class="w400px">
              <option>선택</option>
            </select>
          </td>
        </tr>
        <tr>
          <th>사용여부</th>
          <td>
            <div class="radioBox">
              <label class="radio-item">
                <input type="radio" name="radio1" checked>
                <span>Y</span>
              </label>
              <label class="radio-item">
                <input type="radio" name="radio1">
                <span>N</span>
              </label>
            </div>
          </td>
        </tr>
        <tr>
          <th class="memo">설명</th>
          <td class="memo">
            <textarea class="h150px" placeholder="내용을 입력하세요."></textarea>
          </td>
        </tr>
      </table>
    </div>
  </section>
  <div class="form-mix flex-end mt15">
    <a href="javascript:;" class="btn-md btn-ghost">초기화</a>
    <a href="javascript:;" class="btn-md btn-secondary">수정</a>
  </div>

  <!--List-->
  <section class="card">
    <div class="titleBox mb30">
      <div class="text-title lg">지식창고 메뉴관리</div>
      <div class="titleBox__btns">
        <a href="javascript:;" class="btn-sm btn-soft">메뉴추가</a>
        <a href="javascript:;" class="btn-sm btn-ghost">게시물 관리</a>
      </div>
    </div>

    <div class="form-mix mb10">
      <select class="w130px">
        <option>선택</option>
      </select>
      <input type="text" class="w100p">
      <a href="javascript:;" class="btn-md btn-basic">검색</a>
    </div>

    <q-table
      style="height: 100%"
      flat
      separator="cell"
      :rows="rows"
      :columns="columns"
      row-key="name"
      :selected-rows-label="getSelectedString"
      selection="multiple"
      v-model:selected="selected"
      virtual-scroll
      :hide-pagination="true"
      class="table-wrap type-data"
    >
    </q-table>
  </section>
  <div class="form-mix flex-end mt15">
    <a href="javascript:;" class="btn-md btn-secondary">등록</a>
  </div>

  <!--view-->
  <section class="card">
    <div class="titleBox mb30">
      <div class="text-title lg">지식창고 메뉴관리</div>
      <div class="titleBox__btns">
        <a href="javascript:;" class="btn-sm btn-soft">메뉴추가</a>
        <a href="javascript:;" class="btn-sm btn-ghost">게시물 관리</a>
      </div>
    </div>

    <div class="viewBox">
      <h1>주택화재 손해 인정 기준 요약</h1>
      <p class="date">2025-03-14</p>
      <div class="viewBox__content">
        본문 내용 <br />
        본문 내용 
      </div>
      <div class="viewBox__file">
        <div class="viewBox__file__title">첨부파일</div>
        <div class="viewBox__file__list">
          주택화재 손해 인정 기준 안내.docx
          <a href="javascript:;" class="btn-sm btn-ghost"><span class="upload"></span> 내려받기</a>
        </div>
      </div>
    </div>
  </section>
  <div class="form-mix flex-end mt15">
    <a href="javascript:;" class="btn-md btn-ghost">목록</a>
    <a href="javascript:;" class="btn-md btn-secondary">수정</a>
  </div>

  <!--write-->
  <section class="card">
    <div class="titleBox mb30">
      <div class="text-title lg">지식창고 메뉴관리</div>
      <div class="titleBox__btns">
        <a href="javascript:;" class="btn-sm btn-soft">메뉴추가</a>
        <a href="javascript:;" class="btn-sm btn-ghost">게시물 관리</a>
      </div>
    </div>
    <div class="editBox">
      <h4>제목</h4>
      <input type="text" class="w100p"/>

      <h4>내용</h4>
      <q-editor
        v-model="content"
        label="내용을 작성하세요"
        :definitions="{}"
        height="300px"
        :toolbar="[
          ['bold', 'italic', 'underline', 'strike'],
          ['quote', 'unordered', 'ordered'],
          ['undo', 'redo'],
          ['link', 'image']
        ]"
      />
      
      <h4>첨부파일</h4>
      <!--등록전-->
      <div class="editBox__file">
        <a href="javascript:;" class="btn-sm btn-ghost">파일 선택</a>
        <p>업로드 할 파일을 선택해 주세요.</p>
      </div>
      <!--등록후-->
      <div class="editBox__file--list">
        <ul>
          <li>
            주택화제 손해 인정 기준 안내.docx
            <button type="button" class="Btn-delete">삭제</button>
          </li>
          <li>
            담보안내.docx
            <button type="button" class="Btn-delete">삭제</button>
          </li>
          <li>
            KakaoTalk_20220710_200746461_05.png
            <button type="button" class="Btn-delete">삭제</button>
          </li>
          <li>
            KakaoTalk_20220710_200746461_08.png
            <button type="button" class="Btn-delete">삭제</button>
          </li>
        </ul>
      </div>
      <div class="editBox__radio">
        <label class="radio-item">
          <input type="radio" name="radio1" checked>
          <span>내용등록</span>
        </label>
        <label class="radio-item">
          <input type="radio" name="radio1">
          <span>PDF 등록</span>
        </label>
      </div>
    </div>
  </section>
  <div class="form-mix flex-end mt15">
    <a href="javascript:;" class="btn-md btn-ghost">취소</a>
    <a href="javascript:;" class="btn-md btn-secondary">저장</a>
  </div>

</template>

<script setup>
import { defineProps, defineEmits, ref, onMounted, watch } from 'vue'
import { global } from 'assets/js/publish/global'
const content = ref('')

//테이블
const columns = [
    {
      name: 'no',
      align: 'center',
      label: 'No.',
      field: 'no',
    },
    {
      name: 'title',
      align: 'left',
      headerClasses: 'text-center',
      label: '제목',
      field: 'title',
      style: 'width: 660px;',
    },
    {
      name: 'date',
      align: 'center',
      label: '등록일',
      field: 'date',
    },
    {
      name: 'count',
      align: 'center',
      label: '조회수',
      field: 'count',
    },
  ];

  const rows = [
    {
      no:'1',
      title:'게시글 제목',
      date:'2025.04.10',
      count:'12'
    },
    {
      no:'1',
      title:'게시글 제목',
      date:'2025.04.10',
      count:'12'
    },
  ];
  const selected = ref([]);

  function getSelectedString() {
    return '';
  }

</script>

<style lang="scss" scoped>
  @import '/src/assets/css/set.scss';
</style>



<style>
/* ★ 한 화면에 리스트, 뷰, 쓰기 다 보이게 하기 위해서 임시로 넣은 스타일, 개발시 삭제 */
.contents-r{ display:inline;}
</style>

