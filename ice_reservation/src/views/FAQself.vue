<template>
  <div class="faq">
    <h2>자주 묻는 질문</h2>
    <div class="search-section">
      <!--필터링-->
      <input
        type="text"
        v-model="searchQuery"
        placeholder="검색어를 입력하세요"
        @input="filterFAQs" />
    </div>

    <div class="faq-categories">
      <!-- 클릭시 활성화를 위하여 :class="['category-btn'-클라스명 , {active : seletedCategory === category.id}]" -->
      <button
        v-for="category in categories"
        :key="category.id"
        :class="['category-btn', { active: seletedCategory === category.id }]"
        @click="seletedCategory1(category.id)">
        {{ category.name }}
      </button>
    </div>
    <div class="faq-list">
        <div v-for="faq in faqs" :key="faq.id" class="faq-item" >
            <div @click="toggleFAQ(faq.id)" class="faq-question">
                <h3>{{ faq.question }}</h3>
                <span class="toggle-icon">
                    {{ activeIndex === faq.id ? "▼" : "▶" }}<!--isOpen 모두 false ▶-->
                </span>
            </div>
            <div v-show="activeIndex === faq.id" class="faq-answer">
                <p>{{faq.answer}}</p>
            </div>
        </div>
    </div>
  </div>
</template>

<script setup>
import { ref , reactive } from "vue";
const activeIndex = ref(null)
// 검색어와 선택된 카테고리 상태 정의(전체를 메인으로)
const searchQuery = ref(""); //처음 상태는 빈배열로
const seletedCategory = ref("all");

// 카테고리 목록 정의
const categories = [
  { id: "all", name: "전체" },
  { id: "reservation", name: "예약 관련" },
  { id: "service", name: "서비스 관련" },
  { id: "payment", name: "결제 관련" },
  { id: "cancellation", name: "취소/환불" },
];
function seletedCategory1(categoryId){
    seletedCategory.value = categoryId;
}
// FAQ 목록 정의
const faqs = reactive([
  {
    id: 1,
    category: "reservation",
    question: "예약은 어떻게 해야 하나요?",
    answer:
      "홈페이지에서 예약하기 버튼을 클릭하여 예약 폼을 작성하시면 됩니다. 예약 시 희망 날짜와 시간을 선택할 수 있습니다.",
    isOpen: false,
  },
  {
    id: 2,
    category: "reservation",
    question: "예약 변경이 가능한가요?",
    answer:
      "예약일 24시간 전까지는 예약 변경이 가능합니다. 마이페이지에서 예약 내역을 확인하고 변경할 수 있습니다.",
    isOpen: false,
  },
  {
    id: 3,
    category: "service",
    question: "청소 소요 시간은 얼마나 걸리나요?",
    answer:
      "제빙기 종류에 따라 다르지만, 일반적으로 1-2시간 정도 소요됩니다. 심층 청소의 경우 2-3시간 정도 소요될 수 있습니다.",
    isOpen: false,
  },
  {
    id: 4,
    category: "service",
    question: "청소 후 얼음을 바로 사용할 수 있나요?",
    answer:
      "청소 후 1-2시간 정도 기다린 후 사용하시는 것을 권장합니다. 이는 청소제 잔여물이 완전히 제거되기 위한 시간입니다.",
    isOpen: false,
  },
  {
    id: 5,
    category: "payment",
    question: "결제 방법은 어떻게 되나요?",
    answer:
      "현장에서 현금 또는 카드로 결제하실 수 있습니다. 신용카드, 체크카드 모두 사용 가능합니다.",
    isOpen: false,
  },
  {
    id: 6,
    category: "payment",
    question: "영수증 발급이 가능한가요?",
    answer:
      "네, 현장에서 영수증을 발급해드립니다. 필요하시다면 이메일로도 발송 가능합니다.",
    isOpen: false,
  },
  {
    id: 7,
    category: "cancellation",
    question: "예약 취소 시 환불 규정은 어떻게 되나요?",
    answer:
      "예약일 24시간 전까지는 전액 환불이 가능합니다. 24시간 이내 취소 시에는 취소 수수료가 발생할 수 있습니다.",
    isOpen: false,
  },
  {
    id: 8,
    category: "cancellation",
    question: "기사가 방문하지 않을 경우 어떻게 하나요?",
    answer:
      "기사가 예약 시간에 방문하지 않을 경우, 즉시 고객센터로 연락주시면 빠른 조치를 도와드리겠습니다.",
    isOpen: false,
  },
]); // reactive로 객체 배열 전체를 반응형으로 처리
// 질문 열고 닫기(토글기능만 만듦)
//f는 {}임 어느 것을 클릭할지 몰라 담아놓고 씀 다음 if넣어 토글 기능만 만듦-> 내용 보이고는 따로 설정해야 함
function toggleFAQ(id){
    activeIndex.value = activeIndex.value === id ? null :IdleDeadline 
}
const filterFAQs = ()=>{}
</script>

<style lang="scss" scoped>
.faq {
  max-width: 800px;
  margin: 0 auto;
  padding: 2rem;
}

h2 {
  text-align: center;
  margin-bottom: 2rem;
  color: #333;
}

.search-section {
  margin-bottom: 2rem;
}

.search-section input {
  width: 100%;
  padding: 0.75rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 1rem;
}

.faq-categories {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 2rem;
  overflow-x: auto;
  padding-bottom: 0.5rem;
}

.category-btn {
  padding: 0.5rem 1rem;
  border: 1px solid #ddd;
  border-radius: 20px;
  background: white;
  cursor: pointer;
  white-space: nowrap;
  transition: all 0.3s;
}

.category-btn.active {
  background: #4caf50;
  color: white;
  border-color: #4caf50;
}
.faq-list {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.faq-item {
  border: 1px solid #ddd;
  border-radius: 8px;
  overflow: hidden;
}

.faq-question {
  padding: 1rem;
  background: #f8f9fa;
  display: flex;
  justify-content: space-between;
  align-items: center;
  cursor: pointer;
}

.faq-question h3 {
  margin: 0;
  font-size: 1.1rem;
  color: #333;
}

.toggle-icon {
  color: #666;
}

.faq-answer {
  padding: 1rem;
  background: white;
  border-top: 1px solid #ddd;
}

.faq-answer p {
  margin: 0;
  line-height: 1.6;
  color: #666;
}

</style>
