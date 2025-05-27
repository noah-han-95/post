<html>
  <head>
    <meta name="viewport" content="width=375, initial-scale=1, maximum-scale=1, user-scalable=no" />
    <link rel="preconnect" href="https://fonts.gstatic.com/" crossorigin="" />
    <link
      rel="stylesheet"
      href="https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/static/pretendard.css"
    />

    <title>스티치 디자인</title>
    <link rel="icon" type="image/x-icon" href="data:image/x-icon;base64," />

    <script src="https://cdn.tailwindcss.com?plugins=forms,container-queries"></script>
    <script type="module" src="https://ajax.googleapis.com/ajax/libs/model-viewer/1.12.0/model-viewer.min.js"></script>
    <style>
      /* 기존 input focus 스타일 삭제 */
      /* #searchInput:focus {
        outline: 2px solid #e82630;
        outline-offset: 0px;
      } */

      /* 커서 스타일 추가 */
      * {
        cursor: url('./mouse_icon.svg'), auto !important;
      }

      /* 클릭 가능한 요소들의 커서 스타일 */
      button, 
      a, 
      [role="button"],
      .cursor-pointer,
      .sticker-card,
      #modelViewerContainer,
      #benefitButton,
      #startButton,
      #detailBackBtn,
      #benefitPageBackBtn,
      #stickerPageBackBtn,
      #editButton,
      #saveButton,
      #prevImageBtn,
      #nextImageBtn,
      #changeImageButton,
      .tab-btn,
      #startPage,
      #myPage,
      #stickerPage,
      #benefitPage,
      #stickerContainer,
      .sticker-detail-image-container,
      #modelViewer,
      #glbFileInput,
      #imageFileInput,
      #searchInput,
      .sticker-detail-textarea,
      .sticker-detail-date-input,
      #detailStickerImage,
      #modelViewerContainer model-viewer {
        cursor: url('./mouse_icon.svg'), pointer !important;
      }

      /* input 요소들의 커서 스타일 */
      input,
      textarea,
      input[type="text"],
      input[type="file"],
      input[type="date"],
      input[type="search"],
      textarea.form-input {
        cursor: url('./mouse_icon.svg'), text !important;
      }

      /* input이 포커스될 때 부모 컨테이너에 아웃라인 적용 */
      .search-bar-container:has(#searchInput:focus) {
        outline: 1.2px solid #1D8BFF !important;
        outline-offset: 0px !important;
        border-color: #1D8BFF !important; /* 테두리 색상도 함께 변경 */
      }

      /* 검색 바 컨테이너 스타일 */
      .search-bar-container {
        position: relative;
      }

      /* 플레이스홀더 오버레이 스타일 */
      .placeholder-overlay {
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        pointer-events: none;
        display: flex;
        align-items: center;
        padding-left: 2.8rem; /* 사용자의 피드백에 따라 텍스트를 오른쪽으로 5px 이동 */
        color: #1b0e0f;
      }

      /* 파란색 텍스트 스타일 */
      .blue-text {
        color: #1D8BFF;
        font-weight: 600;
      }

      /* 네이티브 플레이스홀더 텍스트 색상 */
      #searchInput::placeholder {
        color: #C3C3C3 !important;
        opacity: 1; /* 일부 브라우저에서 기본 투명도 제거 */
      }

      /* 플레이스홀더 텍스트 중 특정 단어만 파란색으로 변경 */
      .placeholder-text {
        color: #1D8BFF;
      }

      /* 스티커 카드 클릭(active) 시 인터랙션 */
      .sticker-card:active {
        transform: scale(0.98);
        opacity: 0.95;
        transition: transform 0.1s ease, opacity 0.1s ease; /* 부드러운 전환 효과 */
      }

      /* 스티커 카드 포커스 시 아웃라인 제거 */
      .sticker-card:focus, .sticker-card:focus-visible {
          outline: none !important;
          box-shadow: none !important; /* 경우에 따라 그림자도 제거 */
      }

      /* 스티커 카드 마우스 오버 시 미세 회전 애니메이션 */
      .sticker-card {
        transition: transform 0.2s ease-out; /* 회전 애니메이션을 위한 트랜지션 추가 */
        position: relative; /* 가상 요소를 위한 기준점 설정 */
        overflow: hidden; /* 넘치는 가상 요소 숨김 */
      }

      /* 스티커 카드 빤짝이 효과 */
      .sticker-card::before {
        content: '';
        position: absolute;
        top: 0;
        left: -75%; /* 초기 위치: 카드 좌측 밖 */
        width: 50%; /* 빛 줄기 너비 */
        height: 100%;
        background: linear-gradient(
          to right,
          rgba(255, 255, 255, 0) 0%,
          rgba(255, 255, 255, .3) 75%,
          rgba(255, 255, 255, 0) 100%
        );
        transform: skewX(-25deg); /* 빛 줄기 기울임 */
        transition: transform 0.5s ease-in-out; /* 빤짝이 이동 애니메이션 */
        pointer-events: none; /* 마우스 이벤트 무시 */
      }

      /* 스티커 카드에 마우스 오버 시 빤짝이 효과 */
      .sticker-card:hover::before {
        transform: translate(150%, 0) skewX(-25deg); /* 마우스 오버 시 카드 우측으로 이동 */
      }

      /* 디테일 모달 입력 필드 focus 시 아웃라인 */
      .sticker-detail-textarea:focus,
      .sticker-detail-date-input:focus {
        outline: 1.2px solid #1D8BFF !important; /* 포커스 시 아웃라인 색상 변경 */
        outline-offset: 0px !important;
        border-color: #1D8BFF !important; /* 포커스 시 테두리 색상 변경 */
      }

      /* 입력 필드 기본 보더 스타일 유지 (Tailwind 충돌 방지) */
      .sticker-detail-textarea {
        border: 1px solid #A4A4A4 !important; /* 기본 테두리 색상 변경 (A4A4A4) */
      }

      /* 디테일 모달 입력 필드 플레이스홀더 색상 */
      .sticker-detail-textarea::placeholder {
        color: #A4A4A4 !important; /* 플레이스홀더 색상 변경 (A4A4A4) */
      }

      /* 여행 날짜 input 및 icon 영역의 개별 보더 제거 */
      .sticker-detail-date-input,
      .sticker-detail-date-container .border { /* .border 클래스 제거 */
          border: none !important;
      }

      /* 여행 날짜 컨테이너 focus 시 아웃라인 */
      .sticker-detail-date-container:has(.sticker-detail-date-input:focus) {
          outline: 1.2px solid #1D8BFF !important; /* 포커스 시 아웃라인 색상 변경 (1D8BFF) */
          outline-offset: 0px !important;
          border-color: #1D8BFF !important; /* 포커스 시 테두리 색상 변경 (1D8BFF) */
      }

      /* 여행 날짜 컨테이너 기본 테두리 색상 */
      .sticker-detail-date-container {
          border: 1px solid #A4A4A4 !important; /* 기본 테두리 색상 변경 (A4A4A4) */
      }

      /* 3D 모델 뷰어 스타일 */
      .model-viewer {
        width: 100%;
        height: 300px;
        background: #f3e7e8;
        border-radius: 0.75rem;
        overflow: hidden;
      }

      /* 스티커 카드 상세 모달 3D 뒤집기 스타일 */
      .sticker-detail-image-container {
        width: 100%; /* 이미지 컨테이너 너비 설정 */
        height: 100%; /* 이미지 컨테이너 높이 설정 */
        perspective: 1000px; /* 3D 효과를 위한 원근 설정 */
      }

      /* 새로운 스타일 */
      .transform-style-preserve-3d {
        transform-style: preserve-3d;
      }

      .transition-transform {
         transition: transform;
      }

      .duration-1000 {
        transition-duration: 0.7s; /* 속도를 700ms로 설정 */
      }

      .backface-hidden {
        backface-visibility: hidden;
      }

      .sticker-detail-image-container.is-flipped #detailStickerImage {
        transform: rotateY(180deg); /* 컨테이너가 뒤집히면 내부 이미지를 회전 */
      }

      /* 기존 스타일 유지 */
      .sticker-card {
        outline: none;
      }
      .sticker-card:focus {
        outline: none !important;
      }
      .sticker-card:focus-within {
        border-color: transparent !important;
      }
      .sticker-card:hover {
        outline: none !important;
      }
      .sticker-card:hover:focus-within {
        border-color: transparent !important;
      }
      .sticker-card:active {
        border: 1px solid transparent !important; /* active 상태의 테두리도 투명하게 */
      }
      .sticker-card:active:focus-within {
        background: #f3e7e8;
      }
      /* 배경색 변경 */
      .bg-\[#fcf8f8\] {
        background-color: #fcf8f8 !important;
      }
      /* 텍스트 색상 변경 */
      .text-\[#1b0e0f\] {
        color: #1b0e0f !important;
      }
      .text-\[#e82630\] {
        color: #e82630 !important;
      }
      .text-\[#974e52\] {
        color: #974e52 !important;
      }
      /* 테두리 색상 변경 */
      .border-\[#e7d0d1\] {
        border-color: #e7d0d1 !important;
      }
      /* 버튼 색상 변경 */
      .bg-\[#e82630\] {
        background-color: #e82630 !important;
      }
      .bg-\[#f5a7aa\] {
        background-color: #f5a7aa !important;
      }
      .bg-\[#f3e7e8\] {
        background-color: #f3e7e8 !important;
      }
      .bg-\[#FFE6E5\] {
        background-color: #FFE6E5 !important;
      }
      /* 탭 하단 바 색상 변경 */
      .border-b-\[#e82630\] {
        border-bottom-color: #1D8BFF !important;
      }

      /* 음악 아이콘 애니메이션 */
      @keyframes musicShake {
        0% { transform: rotate(0deg) translateX(1px); }
        25% { transform: rotate(-5deg) translateX(1px); }
        50% { transform: rotate(0deg) translateX(1px); }
        75% { transform: rotate(5deg) translateX(1px); }
        100% { transform: rotate(0deg) translateX(1px); }
      }

      @keyframes ripple {
        0% {
          transform: translate(-50%, -50%) scale(0.8);
          opacity: 0.8; /* 시작 투명도 증가 */
        }
        100% {
          transform: translate(-50%, -50%) scale(3.5); /* 더 크게 퍼지도록 스케일 증가 */
          opacity: 0;
        }
      }

      /* 음악이 재생 중일 때 토글 버튼 컨테이너에 적용 */
      #musicToggle.music-playing {
        position: relative;
        overflow: visible; /* 파장이 컨테이너 밖으로 퍼져나가도록 설정 */
      }

      /* 아이콘 자체의 흔들림 애니메이션 유지 */
      #musicIcon.music-playing {
          animation: musicShake 1s ease-in-out infinite;
      }

      #musicToggle.music-playing::before,
      #musicToggle.music-playing::after {
        content: '';
        position: absolute;
        top: 50%; 
        left: calc(50% + 12px); /* 아이콘 위치 고려하여 좌측 이동 */
        width: 24px; /* 아이콘 크기에 맞춰 시작 크기 설정 */
        height: 24px; /* 아이콘 크기에 맞춰 시작 크기 설정 */
        background: #E8F3FF; /* 파장 색상 */
        border-radius: 50%;
        transform: translate(-50%, -50%); /* 자체 크기의 중앙으로 이동 */
        z-index: -1;
        pointer-events: none; /* 파장 클릭 방지 */
      }

      #musicToggle.music-playing::before {
        animation: ripple 2s ease-out infinite;
      }

      #musicToggle.music-playing::after {
        animation: ripple 2s ease-out infinite 1s;
      }
    </style>
  </head>
  <body>
    <audio id="backgroundMusic" loop preload="auto">
      <source src="./Music/aimusic.mp3" type="audio/mpeg">
    </audio>
    <div
      class="relative flex size-full min-h-screen flex-col bg-[#fcf8f8] group/design-root overflow-x-hidden max-w-[375px] mx-auto"
      style='font-family: "Pretendard", sans-serif;'
    >
      <!-- Start Page Container -->
      <div id="startPage" class="w-full h-[812px] bg-cover bg-center" style="background-image: url('./images/startpage.png'); display: none;">
        <!-- Unseen Button (transparent overlay) -->
        <button id="startButton" class="absolute inset-0 w-full h-full"></button>
      </div>

      <!-- My Page Container (initially hidden) -->
      <div id="myPage" class="flex flex-col w-full h-[812px] bg-cover bg-center" style="display: none; background-image: url('./images/mypage.png');">
        <!-- 이 안의 내용은 모두 삭제하고 배경 이미지로 대체 -->
      </div>

      <!-- Sticker Page Container (initially hidden) -->
      <div id="stickerPage" class="flex flex-col w-full h-full" style="display: none;">
        <div>
          <div class="flex items-center bg-[#fcf8f8] px-4 pb-2 justify-center w-full max-w-[375px] mx-auto">
            <div class="text-[#1b0e0f] flex size-12 shrink-0 items-center cursor-pointer" id="stickerPageBackBtn">
              <svg xmlns="http://www.w3.org/2000/svg" width="24px" height="24px" fill="currentColor" viewBox="0 0 256 256">
                <path d="M224,128a8,8,0,0,1-8,8H59.31l58.35,58.34a8,8,0,0,1-11.32,11.32l-72-72a8,8,0,0,1,0-11.32l72-72a8,8,0,0,1,11.32,11.32L59.31,120H216A8,8,0,0,1,224,128Z"></path>
              </svg>
            </div>
            <h2 class="text-[#1b0e0f] text-lg font-bold leading-tight tracking-[-0.015em] flex-1 text-center">내 여행 기록</h2>
            <div class="text-[#1b0e0f] flex size-14 shrink-0 items-center justify-end cursor-pointer pr-2" id="musicToggle">
              <img src="./Music/music_off.svg" alt="music" class="w-6 h-6 translate-x-[1px]" id="musicIcon" style="filter: invert(33%) sepia(0%) saturate(0%) hue-rotate(0deg) brightness(0%) contrast(100%);">
            </div>
          </div>
          <div class="px-4 py-3 w-full max-w-[375px] mx-auto">
            <div class="flex flex-col p-4 w-full rounded-xl bg-[#E8F3FF] outline outline-1 outline-[#B4D8FF]">
              <div class="flex justify-between items-start">
                <div class="flex flex-col gap-0 flex-1 pr-2">
                  <p class="text-[#1b0e0f] text-base font-medium leading-normal"><span class="text-[#1D8BFF] font-bold">우표 20개를</span> 모으면</p>
                  <p class="text-[#1b0e0f] text-base font-medium leading-normal whitespace-nowrap">실물 스티커 우표를 드려요!</p>
                </div>
                <button
                  class="flex shrink-0 min-w-[84px] max-w-[480px] cursor-pointer items-center justify-center overflow-hidden rounded-full h-7 px-2 bg-transparent border border-[#1D8BFF] text-[#1D8BFF] text-sm font-bold leading-normal tracking-[0.015em]"
                  id="benefitButton"
                >
                <span class="truncate">혜택 보기</span>
                </button>
              </div>
              <div class="flex items-center gap-2 pt-2">
                <div class="w-full bg-[#8DC4FF] rounded-full h-2.5">
                  <div id="progressBarFill" class="bg-[#1D8BFF] h-2.5 rounded-full transition-all duration-1000 ease-out" style="width: 0%;"></div> <!-- 초기 너비 0% 설정 및 트랜지션 추가 -->
                </div>
                <p class="text-base leading-normal whitespace-nowrap text-[#974e52] font-normal"><span class="text-[#1D8BFF] font-bold">14</span><span class="text-[#232323]">/20</span></p>
              </div>
            </div>
          </div>
          <div class="px-4 py-3 w-full max-w-[375px] mx-auto">
            <label class="flex flex-col min-w-40 h-12 w-full">
              <div
                class="flex w-full flex-1 items-stretch rounded-xl h-full search-bar-container border border-[#424242]"
              >
                <div
                  class="text-[#1b0e0f] flex border-none items-center justify-center pl-4 border-r-0"
                  data-icon="MagnifyingGlass"
                  data-size="24px"
                  data-weight="regular"
                >
                  <svg
                    xmlns="http://www.w3.org/2000/svg"
                    width="24px"
                    height="24px"
                    fill="currentColor"
                    viewBox="0 0 256 256"
                  >
                    <path
                      d="M229.66,218.34l-50.07-50.06a88.11,88.11,0,1,0-11.31,11.31l50.06,50.07a8,8,0,0,0,11.32-11.32ZM40,112a72,72,0,1,1,72,72A72.08,72.08,0,0,1,40,112Z"
                    ></path>
                  </svg>
                </div>
                <input
                  id="searchInput"
                  placeholder="여행 했던 '장소' 를 입력해주세요."
                  class="form-input flex w-full min-w-0 flex-1 resize-none overflow-hidden text-[#1b0e0f] focus:outline-0 focus:ring-0 border-none focus:border-none h-full placeholder:text-[#797979] px-4 border-l-0 pl-2 text-base font-medium leading-normal" style="background-color: transparent; appearance: none;"
                  value=""
                  autofocus
                />
              </div>
            </label>
          </div>
          <div class="pb-3 w-full max-w-[375px] mx-auto">
            <div class="flex border-b border-[#D7D7D7] px-4 justify-between flex-row gap-2 whitespace-nowrap">
              <a class="flex flex-col items-center justify-center border-b-[3px] border-b-[#1D8BFF] text-[#1D8BFF] pb-[13px] pt-4 flex-1 tab-btn" data-tab="domestic" href="#">
                <p class="text-[#1D8BFF] text-base font-bold leading-normal tracking-[-0.015em]">국내 여행</p>
              </a>
              <a class="flex flex-col items-center justify-center border-b-[3px] border-b-transparent text-[#1b0e0f] pb-[13px] pt-4 flex-1 tab-btn" data-tab="international" href="#">
                <p class="text-[#1b0e0f] text-base font-bold leading-normal tracking-[-0.015em]">해외 여행</p>
              </a>
              <a class="flex flex-col items-center justify-center border-b-[3px] border-b-transparent text-[#1b0e0f] pb-[13px] pt-4 flex-1 tab-btn" data-tab="collection" href="#">
                <p class="text-[#1b0e0f] text-base font-bold leading-normal tracking-[-0.015em]">내 우표 모음</p>
              </a>
            </div>
          </div>
          <div id="stickerContainer" class="w-full max-w-[375px] mx-auto"></div>
          <script>
// 스티커 데이터 예시 (카테고리, 연도, 이름, 날짜, 이미지)
const stickers = [
  // 2025년 예시 4개 (국내)
  { category: 'domestic', year: 2025, name: '서울', date: '2025-01-15', images: ['./images/seoul_image.png', './images/selfi_01.png', './images/selfi_02.png'] },
  { category: 'domestic', year: 2025, name: '전주', date: '2025-02-20', images: ['./images/jeounju_image.png', './images/selfi_01.png', './images/selfi_02.png'] },
  { category: 'domestic', year: 2025, name: '강릉', date: '2025-03-01', images: ['./images/gangneung_image.png', './images/selfi_01.png', './images/selfi_02.png'] },
  { category: 'domestic', year: 2025, name: '경주', date: '2025-04-10', images: ['./images/gyeongju_image.png', './images/selfi_01.png', './images/selfi_02.png'] },
  // 2025년 해외 여행 3개
  { category: 'international', year: 2025, name: '일본', date: '2025-03-10', images: ['./images/japan_image.png', './images/selfi_01.png', './images/selfi_02.png'] },
  { category: 'international', year: 2025, name: '영국', date: '2025-03-20', images: ['./images/unitedkingdom_image.png', './images/selfi_01.png', './images/selfi_02.png'] },
  { category: 'international', year: 2025, name: '인도네시아', date: '2025-04-01', images: ['./images/indonesia_image.png', './images/selfi_01.png', './images/selfi_02.png'] },
  // 2024년 예시 4개 (국내)
  { category: 'domestic', year: 2024, name: '대구', date: '2024-05-12', images: ['./images/daegu_image.png', './images/selfi_01.png', './images/selfi_02.png'] },
  { category: 'domestic', year: 2024, name: '세종', date: '2024-08-15', images: ['./images/sejong_image.png', './images/selfi_01.png', './images/selfi_02.png'] },
  // 2024년 해외 여행 3개
  { category: 'international', year: 2024, name: '태국', date: '2024-06-22', images: ['./images/thailand_image.png', './images/selfi_01.png', './images/selfi_02.png'] },
  { category: 'international', year: 2024, name: '싱가포르', date: '2024-07-01', images: ['./images/singapore_image.png', './images/selfi_01.png', './images/selfi_02.png'] },
  { category: 'international', year: 2024, name: '브라질', date: '2024-08-25', images: ['./images/brazil_image.png', './images/selfi_01.png', './images/selfi_02.png'] },
];

let currentTab = 'domestic';
let searchValue = '';

function renderStickers() {
  const container = document.getElementById('stickerContainer');
  let filtered = stickers;

  // 탭 필터링 추가
  if (currentTab && currentTab !== 'collection') {
    filtered = filtered.filter(s => s.category === currentTab);
  }

  if (searchValue) {
    filtered = filtered.filter(s => s.name.toLowerCase().includes(searchValue.toLowerCase()));
  }

  // 연도별로 그룹화
  const years = [...new Set(filtered.map(s => s.year))].sort((a, b) => b - a);
  container.innerHTML = years.map((year, index) => {
    const yearStickers = filtered.filter(s => s.year === year);
    // 첫 번째 연도 위에는 구분선을 추가하지 않음
    const divider = index > 0 ? `<div class="border-t border-[#D7D7D7] pt-4 mx-4"></div>` : '';
    return `
      ${divider} <!-- 연도 위에 얇은 구분선 (첫 번째 연도 제외) -->
      <h2 class="text-[#1b0e0f] text-[22px] font-bold leading-tight tracking-[-0.015em] px-4 pb-3 pt-5">${year}</h2>
      <div class="grid grid-cols-2 gap-3 p-4">
        ${yearStickers.map((sticker, idx) => `
          <div class="flex flex-col gap-3 pb-3 cursor-pointer sticker-card" data-sticker-index="${stickers.indexOf(sticker)}">
            <div class="w-full bg-center bg-no-repeat aspect-[3/4] bg-cover rounded-none" style="background-image: url('${sticker.images[0]}');"></div>
            <div>
              <p class="text-[#1b0e0f] text-base font-semibold leading-normal">${sticker.name}</p>
              <p class="text-[#232323] text-sm font-normal leading-normal">${sticker.date}</p>
            </div>
          </div>
        `).join('')}
      </div>
    `;
  }).join('');

  // 썸네일 클릭 이벤트(상세 모달)
  setTimeout(() => {
    document.querySelectorAll('.sticker-card').forEach(card => {
      card.addEventListener('click', function() {
        const idx = parseInt(card.getAttribute('data-sticker-index'));
        showStickerDetail(stickers[idx]);
      });

      // 마우스 위치에 따른 미세 회전 효과
      card.addEventListener('mousemove', function(e) {
        const rect = card.getBoundingClientRect();
        const centerX = rect.left + rect.width / 2;
        const centerY = rect.top + rect.height / 2;
        const moveX = e.clientX - centerX;
        const moveY = e.clientY - centerY;
        
        // 회전 각도 계산 (값은 미세하게 조정 가능)
        const rotateX = -moveY / (rect.height / 2) * 20; // 위아래 움직임에 따라 X축 회전 (최대 각도 20도로 증가)
        const rotateY = moveX / (rect.width / 2) * 20;  // 좌우 움직임에 따라 Y축 회전 (최대 각도 20도로 증가)
        
        card.style.transform = `perspective(500px) rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;
      });
      
      card.addEventListener('mouseleave', function() {
        card.style.transform = 'none'; // 마우스 벗어날 때 회전 초기화
      });
    });
  }, 0);
}

// 상세 모달 생성 함수
function showStickerDetail(sticker) {
  // 기존 모달 제거
  const old = document.getElementById('stickerDetailModal');
  if (old) old.remove();
  // 모달 HTML
  const modal = document.createElement('div');
  modal.id = 'stickerDetailModal';
  modal.className = 'fixed inset-0 z-[9999] flex items-center justify-center';
  modal.innerHTML = `
    <div class="absolute inset-0 bg-black bg-opacity-60 z-0"></div>
    <div class="relative bg-[#fcf8f8] rounded-xl w-full max-w-[375px] mx-auto shadow-lg z-10 max-h-[95vh] overflow-y-auto flex flex-col">
      <div class="flex items-center bg-[#fcf8f8] px-4 pb-2 justify-between sticky top-0 z-20">
        <div class="text-[#1b0e0f] flex size-12 shrink-0 items-center cursor-pointer" id="detailBackBtn">
          <svg xmlns="http://www.w3.org/2000/svg" width="24px" height="24px" fill="currentColor" viewBox="0 0 256 256"><path d="M224,128a8,8,0,0,1-8,8H59.31l58.35,58.34a8,8,0,0,1-11.32,11.32l-72-72a8,8,0,0,1,0-11.32l72-72a8,8,0,0,1,11.32,11.32L59.31,120H216A8,8,0,0,1,224,128Z"></path></svg>
        </div>
        <h2 class="text-[#1b0e0f] text-lg font-bold leading-tight tracking-[-0.015em] flex-1 text-center">${sticker.name}</h2>
        <div class="flex w-12 items-center justify-end"><p class="text-[#1D8BFF] text-base font-bold leading-normal tracking-[0.015em] shrink-0 cursor-pointer" id="editButton">편집</p></div>
      </div>
      <div class="flex w-full grow bg-[#fcf8f8] p-4 flex-col items-center">
        <div class="relative w-full gap-1 overflow-hidden bg-[#fcf8f8] aspect-[3/4] rounded-xl flex sticker-detail-image-container">
          <div id="detailStickerImage" class="w-full h-full transform-style-preserve-3d transition-transform duration-700">
            <!-- 이미지는 여기서 JavaScript로 동적으로 추가 -->
          </div>
          <!-- 좌우 인디케이터 버튼 -->
          <button id="prevImageBtn" class="absolute left-2 top-1/2 transform -translate-y-1/2 bg-white bg-opacity-50 rounded-full p-2 z-10 opacity-70">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" stroke="#000000" stroke-width="2" viewBox="0 0 24 24">
              <path d="M15 18l-6-6 6-6"></path>
            </svg>
          </button>
          <button id="nextImageBtn" class="absolute right-2 top-1/2 transform -translate-y-1/2 bg-white bg-opacity-50 rounded-full p-2 z-10 opacity-70">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" stroke="#000000" stroke-width="2" viewBox="0 0 24 24">
              <path d="M9 6l6 6-6 6"></path>
            </svg>
          </button>
           <!-- 이미지 변경 버튼 (처음에는 숨김) -->
           <button id="changeImageButton" class="absolute bottom-4 right-4 flex min-w-[84px] max-w-[480px] cursor-pointer items-center justify-center overflow-hidden rounded-full h-8 px-4 bg-[#1b0e0f] bg-opacity-50 text-[#fcf8f8] text-xs font-bold leading-normal tracking-[0.015em] opacity-0 pointer-events-none transition-all duration-200 ease-out transform scale-100">
              <span class="truncate">이미지 변경</span>
           </button>
        </div>
      </div>
      <div id="modelViewer" class="model-viewer" style="display: none;"></div>
      <p class="text-[#1b0e0f] text-lg font-bold leading-normal pb-3 pt-1 px-4 text-center">${sticker.name}</p>
      <input type="file" id="imageFileInput" accept="image/*" style="display: none;"/> <!-- 숨겨진 파일 입력 -->
      <div class="flex max-w-[480px] flex-wrap items-end gap-4 px-4 py-3">
        <label class="flex flex-col min-w-40 flex-1">
          <textarea placeholder="소중한 추억을 남겨보세요 (최대 200자)" class="form-input flex w-full min-w-0 flex-1 resize-none overflow-hidden rounded-xl text-[#1b0e0f] bg-[#fcf8f8] min-h-36 placeholder:text-[#974e52] p-[15px] text-base font-medium leading-normal sticker-detail-textarea"></textarea>
        </label>
      </div>
      <h3 class="text-[#1b0e0f] text-lg font-bold leading-tight tracking-[-0.015em] px-4 pb-2 pt-4">여행 날짜</h3>
      <div class="flex flex-col gap-4 max-w-[480px] px-4 py-3">
        <label class="flex flex-col min-w-40 flex-1">
          <div class="flex w-full flex-1 items-stretch rounded-xl sticker-detail-date-container border border-[#424242]">
            <input placeholder="여행 시작일 ~ 종료일 선택" class="form-input flex w-full min-w-0 flex-1 resize-none overflow-hidden rounded-xl text-[#1b0e0f] bg-[#fcf8f8] h-14 placeholder:text-[#974e52] p-[15px] rounded-r-none pr-2 text-base font-normal leading-normal sticker-detail-date-input" value="${sticker.date}" />
            <div class="text-[#232323] flex bg-[#fcf8f8] items-center justify-center pr-[15px] rounded-r-xl" data-icon="Calendar" data-size="24px" data-weight="regular"> <!-- 달력 아이콘 색상 변경 -->
              <svg xmlns="http://www.w3.org/2000/svg" width="24px" height="24px" fill="currentColor" viewBox="0 0 256 256"><path d="M208,32H184V24a8,8,0,0,0-16,0v8H88V24a8,8,0,0,0-16,0v8H48A16,16,0,0,0,32,48V208a16,16,0,0,0,16,16H208a16,16,0,0,0,16-16V48A16,16,0,0,0,208,32ZM72,48v8a8,8,0,0,0,16,0V48h80v8a8,8,0,0,0,16,0V48h24V80H48V48ZM208,208H48V96H208V208Zm-96-88v64a8,8,0,0,1-16,0V132.94l-4.42,2.22a8,8,0,0,1-7.16-14.32l16-8A8,8,0,0,1,112,120Zm59.16,30.45L152,176h16a8,8,0,0,1,0,16H136a8,8,0,0,1-6.4-12.8l28.78-38.37A8,8,0,1,0,145.07,132a8,8,0,1,1-13.85-8A24,24,0,0,1,176,136,23.76,23.76,0,0,1,171.16,150.45Z"></path></svg>
            </div>
          </div>
        </label>
      </div>
      <div class="flex flex-col px-4 pt-4">
        <h3 class="text-[#1b0e0f] text-lg font-bold leading-tight tracking-[-0.015em] pb-2">머물렀던 숙소</h3>
        <p class="text-[#1b0e0f] text-base font-normal leading-normal">삼성 신라스테이 호텔</p>
      </div>
      <div class="flex px-4 py-3">
        <button class="flex min-w-[84px] max-w-[480px] cursor-pointer items-center justify-center overflow-hidden rounded-full h-10 px-4 flex-1 bg-[#1D8BFF] text-[#fcf8f8] text-sm font-bold leading-normal tracking-[0.015em]" id="saveButton">
          <span class="truncate">저장</span>
        </button>
      </div>
      <div class="h-5 bg-[#fcf8f8]"></div>
    </div>
  `;
  document.body.appendChild(modal);

  // 요소들 가져오기
  const saveButton = document.getElementById('saveButton');
  const editButton = document.getElementById('editButton');

  // 저장 버튼 클릭 이벤트
  if (saveButton) {
    saveButton.addEventListener('click', function() {
      // 저장 로직 (현재는 없음)
      console.log('저장 버튼 클릭');
      // 저장 버튼 비활성화 및 스타일 변경
      saveButton.disabled = true;
      saveButton.classList.remove('bg-[#1D8BFF]', 'text-[#fcf8f8]', 'cursor-pointer');
      saveButton.classList.add('bg-[#cccccc]', 'text-[#666666]', 'cursor-not-allowed');
    });
  }

  // Edit 텍스트 클릭 이벤트
  if (editButton) {
    editButton.addEventListener('click', function() {
      console.log('Edit 버튼 클릭');
      // 저장 버튼 활성화 및 스타일 변경
      if (saveButton) {
        saveButton.disabled = false;
        saveButton.classList.remove('bg-[#cccccc]', 'text-[#666666]', 'cursor-not-allowed');
        saveButton.classList.add('bg-[#1D8BFF]', 'text-[#fcf8f8]', 'cursor-pointer');
      }
    });
  }

  // 닫기 버튼, 뒤로가기 버튼 이벤트
  const restoreScroll = () => { 
    document.body.style.overflow = ''; 
    modal.remove();
    // 프로그레스 바 애니메이션 재실행
    const progressBarFill = document.getElementById('progressBarFill');
    if (progressBarFill) {
      // 트랜지션 효과를 일시적으로 제거
      progressBarFill.style.transition = 'none';
      progressBarFill.style.width = '0%';
      
      // 강제 리플로우
      progressBarFill.offsetHeight;
      
      // 트랜지션 효과 복원 및 애니메이션 시작
      progressBarFill.style.transition = 'width 1s ease-out';
      setTimeout(() => {
        progressBarFill.style.width = '70%';
      }, 50);
    }
  };
  const backBtn = document.getElementById('detailBackBtn');
  if (backBtn) backBtn.onclick = restoreScroll;
  // 모달이 열릴 때 body 스크롤 방지
  document.body.style.overflow = 'hidden';

  const stickerImageContainer = document.querySelector('.sticker-detail-image-container');
  const detailStickerImageDiv = document.getElementById('detailStickerImage'); // 회전할 요소 선택 (이미지들을 담을 컨테이너)
  const prevImageBtn = document.getElementById('prevImageBtn');
  const nextImageBtn = document.getElementById('nextImageBtn');
  const changeImageButton = document.getElementById('changeImageButton'); // 이미지 변경 버튼 요소 가져오기
  const imageFileInput = document.getElementById('imageFileInput'); // 파일 입력 요소 가져오기

  let currentRotation = 0; // 현재 회전 각도를 저장할 변수
  let currentImageIndex = 0; // 현재 이미지 인덱스
  const images = sticker.images || [sticker.img]; // 스티커 이미지 배열 (images가 없으면 img 사용)

  // 이미지 표시 함수
  function displayImage(index) {
    if (detailStickerImageDiv && images.length > 0) {
      // 이미지 변경 시 회전 상태 및 트랜지션 초기화
      detailStickerImageDiv.style.transition = 'none'; // 트랜지션 비활성화
      detailStickerImageDiv.style.transform = 'rotateY(0deg)'; // 회전 각도 초기화
      currentRotation = 0; // 회전 각도 변수 초기화

      detailStickerImageDiv.innerHTML = `
        <div class="w-full h-full bg-center bg-no-repeat bg-cover rounded-none absolute top-0 left-0 backface-hidden" style="background-image: url('${images[index]}');"></div> <!-- 앞면 이미지 -->
        <div class="w-full h-full bg-center bg-no-repeat bg-cover rounded-none absolute top-0 left-0 backface-hidden" style="background-image: url('./images/platformdesignstudy_image.png'); transform: rotateY(180deg);"></div> <!-- 뒷면 이미지: platformdesignstudy_image.png 적용 -->
      `;

      // DOM 업데이트 후 트랜지션 다시 활성화 (약간의 지연 필요)
      setTimeout(() => {
        detailStickerImageDiv.style.transition = 'transform 0.7s'; // 트랜지션 다시 활성화 (CSS 클래스 사용시 해당 클래스 다시 추가)
      }, 50); // 짧은 지연 시간

    }
     // 좌우 버튼 표시/숨김 처리
     if (images.length > 1) { // 이미지가 1개보다 많을 때만 버튼 표시 로직 적용
        // 이전 버튼 표시/숨김
        if(prevImageBtn) {
            if (index === 0) {
                prevImageBtn.style.display = 'none';
            } else {
                prevImageBtn.style.display = 'block';
            }
        }
        // 다음 버튼 표시/숨김
        if(nextImageBtn) {
            if (index === images.length - 1) {
                nextImageBtn.style.display = 'none';
            } else {
                nextImageBtn.style.display = 'block';
            }
        }
     } else { // 이미지가 1개 이하일 때는 두 버튼 모두 숨김
        if(prevImageBtn) prevImageBtn.style.display = 'none';
        if(nextImageBtn) nextImageBtn.style.display = 'none';
     }

     // 이미지 변경 버튼 표시/숨김
     if (changeImageButton) {
       // 초기 상태 설정 (CSS에서 처리)
       changeImageButton.classList.add('opacity-0', 'pointer-events-none');
       changeImageButton.classList.remove('opacity-100', 'pointer-events-auto');
     }
  }

  // 초기 이미지 표시
  displayImage(currentImageIndex);

  // 스티커 이미지 영역 클릭 시 뒤집기 애니메이션 또는 버튼 표시
  if (detailStickerImageDiv) {
    detailStickerImageDiv.addEventListener('click', function() {
      // 현재 표시된 이미지가 첫 번째 이미지(인덱스 0)일 때만 회전 적용
      if (currentImageIndex === 0) {
        currentRotation += 180; // 180도 회전 각도 추가
        this.style.transform = `rotateY(${currentRotation}deg)`; // transform 스타일 업데이트
      } else if (currentImageIndex === 1 || currentImageIndex === 2) { // 두 번째 또는 세 번째 이미지일 때 버튼 표시 토글
         if (changeImageButton) {
           if (changeImageButton.classList.contains('opacity-0')) {
             // 버튼 나타나기: 투명도 및 클릭 활성화, 스케일 애니메이션 시작
             changeImageButton.classList.remove('opacity-0', 'pointer-events-none');
             changeImageButton.classList.add('opacity-100', 'pointer-events-auto');

             // 스케일 애니메이션: 원래 크기 -> 살짝 작게 -> 원래 크기
             changeImageButton.classList.remove('scale-95'); // 현재는 scale-100에서 시작
             setTimeout(() => {
                 changeImageButton.classList.add('scale-95');
             }, 10); // 아주 짧은 지연
             setTimeout(() => {
                 changeImageButton.classList.remove('scale-95');
             }, 210); // scale-95 상태 유지 시간 (200ms transition + 10ms 지연)

           } else {
             // 버튼 사라지기: 투명도 및 클릭 비활성화
             changeImageButton.classList.remove('opacity-100', 'pointer-events-auto');
             changeImageButton.classList.add('opacity-0', 'pointer-events-none');
              // 사라질 때는 스케일 초기 상태로 되돌림 (선택 사항)
              changeImageButton.classList.remove('scale-95'); // 원래 상태 (scale-100)

           }
         }
      }
    });
  }

  // 이전 이미지 버튼 클릭 이벤트
  if (prevImageBtn) {
    prevImageBtn.addEventListener('click', function(e) {
      e.stopPropagation(); // 이미지 클릭 이벤트 전파 방지
      currentImageIndex = (currentImageIndex - 1 + images.length) % images.length; // 이전 이미지 인덱스 계산 (순환)
      displayImage(currentImageIndex);
       // 이미지 변경 시 회전 상태 초기화 (선택 사항)
      // currentRotation = 0;
      // if(detailStickerImageDiv) detailStickerImageDiv.style.transform = `rotateY(0deg)`;
    });
  }

  // 다음 이미지 버튼 클릭 이벤트
  if (nextImageBtn) {
    nextImageBtn.addEventListener('click', function(e) {
      e.stopPropagation(); // 이미지 클릭 이벤트 전파 방지
      currentImageIndex = (currentImageIndex + 1) % images.length; // 다음 이미지 인덱스 계산 (순환)
      displayImage(currentImageIndex);
       // 이미지 변경 시 회전 상태 초기화 (선택 사항)
      // currentRotation = 0;
      // if(detailStickerImageDiv) detailStickerImageDiv.style.transform = `rotateY(0deg)`;
    });
  }

  // 이미지 변경 버튼 클릭 이벤트 (파일 입력 활성화)
  if (changeImageButton && imageFileInput) {
    changeImageButton.addEventListener('click', function() {
      imageFileInput.click(); // 숨겨진 파일 입력 요소 클릭
    });
  }

  // 파일 입력 변경 이벤트 (이미지 로드 및 표시)
  imageFileInput.addEventListener('change', function(event) {
    const file = event.target.files[0];
    
    if (file && file.type.startsWith('image/')) {
      const reader = new FileReader();
      
      reader.onload = function(e) {
        const imageUrl = e.target.result;
        
        // 현재 스티커 데이터의 이미지 URL 업데이트
        // 주의: 이 변경은 현재 모달에만 적용되며, 원본 stickers 배열을 영구적으로 바꾸지는 않습니다.
        if (sticker && sticker.images && currentImageIndex >= 0 && currentImageIndex < sticker.images.length) {
           sticker.images[currentImageIndex] = imageUrl; // 현재 표시된 이미지 교체
        }
        
        // 이미지 영역 업데이트
        const frontFace = detailStickerImageDiv.querySelector('.backface-hidden:not([style*="rotateY(180deg)"])');
        if (frontFace) {
            frontFace.style.backgroundImage = `url('${imageUrl}')`;
        }
      };
      
      reader.readAsDataURL(file); // 파일을 Data URL로 읽기
      
    } else if (file) {
      alert('유효한 이미지 파일을 선택해주세요.');
    }
  });
}

// 검색 이벤트
const searchInput = document.getElementById('searchInput');
searchInput.addEventListener('input', function(e) {
  searchValue = e.target.value;
  renderStickers();
});

// 모바일에서 검색 input 클릭 시 키보드가 확실히 올라오도록 focus 강제
searchInput.addEventListener('click', function() {
  searchInput.focus();
  // iOS에서 키보드가 확실히 올라오도록 하는 추가 코드
  searchInput.setAttribute('readonly', 'readonly');
  setTimeout(() => {
    searchInput.removeAttribute('readonly');
  }, 100);
});

// 탭 이벤트
Array.from(document.getElementsByClassName('tab-btn')).forEach(tab => {
  tab.addEventListener('click', function(e) {
    e.preventDefault();
    currentTab = tab.getAttribute('data-tab');
    // 모든 탭의 스타일 초기화 (하단 바 제거 및 텍스트 색상 변경)
    Array.from(document.getElementsByClassName('tab-btn')).forEach(t => {
      t.classList.remove('border-b-[#1D8BFF]'); // 파란색 바 클래스 제거
      t.classList.add('border-b-transparent'); // 투명 바 클래스 추가
      const p = t.querySelector('p');
      if (p) {
        p.classList.remove('text-[#1D8BFF]'); // 기존 파란색 텍스트 클래스 제거
        p.classList.add('text-[#1b0e0f]'); // 선택 해제된 탭 텍스트 색상 (#1b0e0f)
      }
    });
    // 선택된 탭의 스타일 적용
    tab.classList.remove('border-b-transparent'); // 투명 바 클래스 제거
    tab.classList.add('border-b-[#1D8BFF]'); // 파란색 바 클래스 추가
    const p = tab.querySelector('p');
    if (p) {
      p.classList.remove('text-[#1b0e0f]'); // 기본 텍스트 색상 제거
      p.classList.add('text-[#1D8BFF]'); // 선택된 탭 텍스트 색상 (#1D8BFF)
    }
    renderStickers();
  });
});

// 페이지 전환 함수 수정
function showPage(pageId) {
  // 모든 페이지 숨기기
  if (startPage) startPage.style.display = 'none';
  if (myPage) myPage.style.display = 'none';
  if (stickerPage) stickerPage.style.display = 'none';
  if (benefitPage) benefitPage.style.display = 'none';

  // 지정된 페이지 보여주기
  const targetPage = document.getElementById(pageId);
  if (targetPage) {
    targetPage.style.display = 'flex';

    // 스티커 페이지로 이동할 때 프로그레스 바 애니메이션 실행 및 음악 재생
    if (pageId === 'stickerPage') {
      const progressBarFill = document.getElementById('progressBarFill');
      if (progressBarFill) {
        // 트랜지션 효과를 일시적으로 제거
        progressBarFill.style.transition = 'none';
        progressBarFill.style.width = '0%';
        
        // 강제 리플로우
        progressBarFill.offsetHeight;
        
        // 트랜지션 효과 복원 및 애니메이션 시작
        progressBarFill.style.transition = 'width 1s ease-out';
        setTimeout(() => {
          progressBarFill.style.width = '70%';
        }, 50);
      }

      // 음악 재생
      const backgroundMusic = document.getElementById('backgroundMusic');
      const musicIcon = document.getElementById('musicIcon');
      const musicToggle = document.getElementById('musicToggle'); // musicToggle 요소 가져오기
      if (backgroundMusic && musicIcon && musicToggle) {
        backgroundMusic.volume = 0.5;
        backgroundMusic.play().catch(function(error) {
          console.error('음악 재생 실패:', error);
        });
        musicIcon.src = './Music/music_on.svg';
        musicIcon.style.filter = 'invert(40%) sepia(100%) saturate(1000%) hue-rotate(190deg) brightness(100%) contrast(100%)';
        musicIcon.classList.add('music-playing'); // 애니메이션 클래스 추가
      }
    }
  }
}

// DOMContentLoaded 이벤트 리스너 수정
window.addEventListener('DOMContentLoaded', function() {
  // 초기 상태 설정 (마이 페이지 보이기)
  showPage('startPage');

  // 시작 페이지 버튼 클릭 이벤트: 마이 페이지로 이동
  if (startButton) {
    startButton.addEventListener('click', function() {
      showPage('myPage');
    });
  }

  // 마이 페이지 클릭 이벤트: 내 스티커 페이지로 이동
  if (myPage) {
    myPage.classList.add('cursor-pointer');
    myPage.addEventListener('click', function() {
      showPage('stickerPage');
      renderStickers();
    });
  }

  // 혜택보기 버튼 클릭 이벤트: 혜택 페이지로 이동
  const benefitButton = document.getElementById('benefitButton');
  if (benefitButton) {
    benefitButton.addEventListener('click', function() {
      showPage('benefitPage');
    });
  }

  // 혜택 페이지 뒤로가기 버튼 클릭 이벤트: 스티커 페이지로 이동
  const benefitPageBackBtn = document.getElementById('benefitPageBackBtn');
  if (benefitPageBackBtn) {
    benefitPageBackBtn.addEventListener('click', function() {
      showPage('stickerPage');
    });
  }

  // 스티커 페이지 뒤로가기 버튼 클릭 이벤트: 마이 페이지로 이동
  const stickerPageBackBtn = document.getElementById('stickerPageBackBtn');
  if (stickerPageBackBtn) {
    stickerPageBackBtn.addEventListener('click', function() {
      showPage('myPage');
    });
  }
});

// 음악 토글 기능 추가
document.addEventListener('DOMContentLoaded', function() {
  const musicToggle = document.getElementById('musicToggle');
  const musicIcon = document.getElementById('musicIcon');
  const backgroundMusic = document.getElementById('backgroundMusic');
  let isMusicOn = false;

  // 초기 볼륨 설정
  if (backgroundMusic) {
    backgroundMusic.volume = 0.5;
  }

  if (musicToggle && musicIcon) {
    musicToggle.addEventListener('click', function() {
      isMusicOn = !isMusicOn;
      musicIcon.src = isMusicOn ? './Music/music_on.svg' : './Music/music_off.svg';
      
      if (isMusicOn) {
        musicIcon.style.filter = 'invert(40%) sepia(100%) saturate(1000%) hue-rotate(190deg) brightness(100%) contrast(100%)';
        musicIcon.classList.add('music-playing'); // 애니메이션 클래스 추가
        backgroundMusic.volume = 0.5;
        backgroundMusic.play().catch(function(error) {
          console.error('음악 재생 실패:', error);
        });
      } else {
        musicIcon.style.filter = 'invert(33%) sepia(0%) saturate(0%) hue-rotate(0deg) brightness(0%) contrast(100%)';
        musicIcon.classList.remove('music-playing'); // 애니메이션 클래스 제거
        backgroundMusic.pause();
      }
    });
  }
});
          </script>
        </div>
        <div><div class="h-5 bg-[#fcf8f8]"></div></div>
      </div>
    </div>

    <!-- Benefit Page Container (initially hidden) -->
    <div id="benefitPage" class="flex flex-col w-full h-full max-w-[375px] mx-auto" style="display: none;">
      <!-- Fixed Header -->
      <div class="flex items-center bg-[#fcf8f8] px-4 py-2 justify-between sticky top-0 z-10 w-full">
        <div class="text-[#1b0e0f] flex size-12 shrink-0 items-center cursor-pointer" id="benefitPageBackBtn">
          <svg xmlns="http://www.w3.org/2000/svg" width="24px" height="24px" fill="currentColor" viewBox="0 0 256 256">
            <path d="M224,128a8,8,0,0,1-8,8H59.31l58.35,58.34a8,8,0,0,1-11.32,11.32l-72-72a8,8,0,0,1,0-11.32l72-72a8,8,0,0,1,11.32,11.32L59.31,120H216A8,8,0,0,1,224,128Z"></path>
          </svg>
        </div>
        <h2 class="text-[#1b0e0f] text-lg font-bold leading-tight tracking-[-0.015em] flex-1 text-center pr-12">이벤트</h2>
      </div>

      <!-- Scrollable Content -->
      <div class="flex-1 overflow-y-auto">
        <div class="@container">
          <div id="modelViewerContainer" class="w-full bg-[#fcf8f8] overflow-hidden aspect-[3/4] min-h-[300px] cursor-pointer">
            <model-viewer
              alt="A 3D model"
              ar
              auto-rotate
              auto-rotate-delay="0"
              camera-controls
              auto-rotate-speed="30"
              autoplay
              poster="./images/event_main_image.png"
              style="width: 100%; height: 100%; background-color: black; object-fit: contain;"
              exposure="1.0"
            ></model-viewer>
          </div>
        </div>
        <h1 class="text-[#1b0e0f] text-[22px] font-bold leading-tight tracking-[-0.015em] px-4 text-left pb-3 pt-2">디지털 우표를 모아보세요!</h1>
        <p class="text-[#1b0e0f] text-base font-normal leading-normal pb-3 pt-1 px-4">
          숙소를 예약하고 디지털 우표를 받으세요. 20개의 우표를 모으면 실물 스티커 세트를 받을 수 있습니다.
        </p>
        <h3 class="text-[#1b0e0f] text-lg font-bold leading-tight tracking-[-0.015em] px-4 pb-2 pt-4">참여 방법</h3>
        <div class="flex items-center gap-4 bg-[#fcf8f8] px-4 min-h-[72px] py-2">
          <div class="text-[#1b0e0f] flex items-center justify-center rounded-lg bg-[#f3e7e8] shrink-0 size-12" data-icon="Calendar" data-size="24px" data-weight="regular">
            <svg xmlns="http://www.w3.org/2000/svg" width="24px" height="24px" fill="currentColor" viewBox="0 0 256 256">
              <path d="M208,32H184V24a8,8,0,0,0-16,0v8H88V24a8,8,0,0,0-16,0v8H48A16,16,0,0,0,32,48V208a16,16,0,0,0,16,16H208a16,16,0,0,0,16-16V48A16,16,0,0,0,208,32ZM72,48v8a8,8,0,0,0,16,0V48h80v8a8,8,0,0,0,16,0V48h24V80H48V48ZM208,208H48V96H208V208Zm-96-88v64a8,8,0,0,1-16,0V132.94l-4.42,2.22a8,8,0,0,1-7.16-14.32l16-8A8,8,0,0,1,112,120Zm59.16,30.45L152,176h16a8,8,0,0,1,0,16H136a8,8,0,0,1-6.4-12.8l28.78-38.37A8,8,0,1,0,145.07,132a8,8,0,1,1-13.85-8A24,24,0,0,1,176,136,23.76,23.76,0,0,1,171.16,150.45Z"></path>
            </svg>
          </div>
          <div class="flex flex-col justify-center">
            <p class="text-[#1b0e0f] text-base font-medium leading-normal line-clamp-1">숙소 예약</p>
            <p class="text-[#974e52] text-sm font-normal leading-normal line-clamp-2">앱을 통해 숙소를 예약하세요.</p>
          </div>
        </div>
        <div class="flex items-center gap-4 bg-[#fcf8f8] px-4 min-h-[72px] py-2">
          <div class="text-[#1b0e0f] flex items-center justify-center rounded-lg bg-[#f3e7e8] shrink-0 size-12" data-icon="Stamp" data-size="24px" data-weight="regular">
            <svg xmlns="http://www.w3.org/2000/svg" width="24px" height="24px" fill="currentColor" viewBox="0 0 256 256">
              <path d="M224,224a8,8,0,0,1-8,8H40a8,8,0,0,1,0-16H216A8,8,0,0,1,224,224Zm0-80v40a16,16,0,0,1-16,16H48a16,16,0,0,1-16-16V144a16,16,0,0,1,16-16h56.43L88.72,54.71A32,32,0,0,1,120,16h16a32,32,0,0,1,31.29,38.71L151.57,128H208A16,16,0,0,1,224,144ZM120.79,128h14.42l16.43-76.65A16,16,0,0,0,136,32H120a16,16,0,0,0-15.65,19.35ZM208,184V144H48v40H208Z"></path>
            </svg>
          </div>
          <div class="flex flex-col justify-center">
            <p class="text-[#1b0e0f] text-base font-medium leading-normal line-clamp-1">우표 받기</p>
            <p class="text-[#974e52] text-sm font-normal leading-normal line-clamp-2">숙박 후 디지털 우표를 받으세요.</p>
          </div>
        </div>
        <div class="flex items-center gap-4 bg-[#fcf8f8] px-4 min-h-[72px] py-2">
          <div class="text-[#1b0e0f] flex items-center justify-center rounded-lg bg-[#f3e7e8] shrink-0 size-12" data-icon="Gift" data-size="24px" data-weight="regular">
            <svg xmlns="http://www.w3.org/2000/svg" width="24px" height="24px" fill="currentColor" viewBox="0 0 256 256">
              <path d="M216,72H180.92c.39-.33.79-.65,1.17-1A29.53,29.53,0,0,0,192,49.57,32.62,32.62,0,0,0,158.44,16,29.53,29.53,0,0,0,137,25.91a54.94,54.94,0,0,0-9,14.48,54.94,54.94,0,0,0-9-14.48A29.53,29.53,0,0,0,97.56,16,32.62,32.62,0,0,0,64,49.57,29.53,29.53,0,0,0,73.91,71c.38.33.78.65,1.17,1H40A16,16,0,0,0,24,88v32a16,16,0,0,0,16,16v64a16,16,0,0,0,16,16H200a16,16,0,0,0,16-16V136a16,16,0,0,0,16-16V88A16,16,0,0,0,216,72ZM149,36.51a13.69,13.69,0,0,1,10-4.5h.49A16.62,16.62,0,0,1,176,49.08a13.69,13.69,0,0,1-4.5,10c-9.49,8.4-25.24,11.36-35,12.4C137.7,60.89,141,45.5,149,36.51Zm-64.09.36A16.63,16.63,0,0,1,96.59,32h.49a13.69,13.69,0,0,1,10,4.5c8.39,9.48,11.35,25.2,12.39,34.92-9.72-1-25.44-4-34.92-12.39a13.69,13.69,0,0,1-4.5-10A16.6,16.6,0,0,1,84.87,36.87ZM40,88h80v32H40Zm16,48h64v64H56Zm144,64H136V136h64Zm16-80H136V88h80v32Z"></path>
            </svg>
          </div>
          <div class="flex flex-col justify-center">
            <p class="text-[#1b0e0f] text-base font-medium leading-normal line-clamp-1">스티커 교환</p>
            <p class="text-[#974e52] text-sm font-normal leading-normal line-clamp-2">20개의 우표를 모아 스티커 세트를 받으세요.</p>
          </div>
        </div>
        <h3 class="text-[#1b0e0f] text-lg font-bold leading-tight tracking-[-0.015em] px-4 pb-2 pt-4">이벤트 상세</h3>
        <div class="p-4 grid grid-cols-[auto_1fr] gap-x-6">
          <div class="col-span-2 grid grid-cols-subgrid border-t border-t-[#e7d0d1] py-5">
            <p class="text-[#974e52] text-sm font-normal leading-normal">이벤트 기간</p>
            <p class="text-[#1b0e0f] text-sm font-normal leading-normal">2024년 7월 1일 - 2024년 8월 31일</p>
          </div>
          <div class="col-span-2 grid grid-cols-subgrid border-t border-t-[#e7d0d1] py-5">
            <p class="text-[#974e52] text-sm font-normal leading-normal">참여 대상</p>
            <p class="text-[#1b0e0f] text-sm font-normal leading-normal">숙소를 예약한 모든 사용자</p>
          </div>
          <div class="col-span-2 grid grid-cols-subgrid border-t border-t-[#e7d0d1] py-5">
            <p class="text-[#974e52] text-sm font-normal leading-normal">상품</p>
            <p class="text-[#1b0e0f] text-sm font-normal leading-normal">실물 스티커 세트 (20개 우표)</p>
          </div>
        </div>
        <h3 class="text-[#1b0e0f] text-lg font-bold leading-tight tracking-[-0.015em] px-4 pb-2 pt-4">자주 묻는 질문</h3>
        <div class="flex flex-col p-4">
          <details class="flex flex-col border-t border-t-[#e7d0d1] py-2 group" open="">
            <summary class="flex cursor-pointer items-center justify-between gap-6 py-2">
              <p class="text-[#1b0e0f] text-sm font-medium leading-normal">디지털 우표는 어떻게 받나요?</p>
              <div class="text-[#1b0e0f] group-open:rotate-180" data-icon="CaretDown" data-size="20px" data-weight="regular">
                <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" fill="currentColor" viewBox="0 0 256 256">
                  <path d="M213.66,101.66l-80,80a8,8,0,0,1-11.32,0l-80-80A8,8,0,0,1,53.66,90.34L128,164.69l74.34-74.35a8,8,0,0,1,11.32,11.32Z"></path>
                </svg>
              </div>
            </summary>
            <p class="text-[#974e52] text-sm font-normal leading-normal pb-2">숙박 완료 후 앱에서 디지털 우표를 받으실 수 있습니다.</p>
          </details>
          <details class="flex flex-col border-t border-t-[#e7d0d1] py-2 group">
            <summary class="flex cursor-pointer items-center justify-between gap-6 py-2">
              <p class="text-[#1b0e0f] text-sm font-medium leading-normal">스티커 세트는 언제 받을 수 있나요?</p>
              <div class="text-[#1b0e0f] group-open:rotate-180" data-icon="CaretDown" data-size="20px" data-weight="regular">
                <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" fill="currentColor" viewBox="0 0 256 256">
                  <path d="M213.66,101.66l-80,80a8,8,0,0,1-11.32,0l-80-80A8,8,0,0,1,53.66,90.34L128,164.69l74.34-74.35a8,8,0,0,1,11.32,11.32Z"></path>
                </svg>
              </div>
            </summary>
            <p class="text-[#974e52] text-sm font-normal leading-normal pb-2">20개의 우표를 모두 모으신 후 2주 이내에 발송됩니다.</p>
          </details>
        </div>
      </div>
      <!-- Sticky Footer -->
      <div class="fixed bottom-0 left-0 right-0 z-10 w-full max-w-[375px] mx-auto bg-[#fcf8f8] py-3">
        <button
          class="flex min-w-[84px] max-w-[480px] cursor-pointer items-center justify-center overflow-hidden rounded-full h-12 px-5 flex-1 bg-[#e82630] text-[#fcf8f8] text-base font-bold leading-normal tracking-[0.015em]"
        >
          <span class="truncate">숙소 예약하기</span>
        </button>
      </div>
    </div>

    <!-- Hidden file input for GLB -->
    <input type="file" id="glbFileInput" accept=".glb" style="display: none;"/>

    <script>
      document.addEventListener('DOMContentLoaded', function() {
        const modelViewerContainer = document.getElementById('modelViewerContainer');
        const glbFileInput = document.getElementById('glbFileInput');
        const modelViewer = modelViewerContainer.querySelector('model-viewer');

        let isModelLoadedFromUser = false; // 사용자가 파일을 업로드했는지 추적하는 변수

        if (modelViewerContainer && glbFileInput && modelViewer) {
          // 모델 뷰어 영역 클릭 시 파일 입력 창 열기
          modelViewerContainer.addEventListener('click', function() {
            // 사용자가 파일을 업로드하지 않은 경우에만 파일 선택 창 열기
            if (!isModelLoadedFromUser) {
              glbFileInput.click();
            }
          });

          // 파일 선택 시 모델 로드
          glbFileInput.addEventListener('change', function(event) {
            const file = event.target.files[0];
            if (file && file.name.endsWith('.glb')) {
              const objectUrl = URL.createObjectURL(file);
              modelViewer.src = objectUrl;
              // 파일 로드 성공 후 상태 업데이트
              isModelLoadedFromUser = true;

              // 기존 URL 해제 (메모리 관리)
              modelViewer.addEventListener('load', () => {
                URL.revokeObjectURL(objectUrl);
              }, { once: true });
            } else {
              alert('GLB 파일을 선택해주세요.');
            }
          });
        }
      });
    </script>
    <script>
      document.addEventListener('DOMContentLoaded', function() {
        const modelViewer = document.querySelector('#modelViewerContainer model-viewer');

        if (modelViewer) {
          // 모델 로드 완료 후 애니메이션 재생
          modelViewer.addEventListener('load', () => {
            // 모델에 애니메이션 클립이 있는지 확인
            if (modelViewer.availableAnimations && modelViewer.availableAnimations.length > 0) {
              // 첫 번째 애니메이션 재생 (예시)
              const animation1Name = modelViewer.availableAnimations[0]; // 실제 애니메이션 이름으로 변경하세요
              modelViewer.animationName = animation1Name;
              modelViewer.play();

              // 첫 번째 애니메이션 종료 후 두 번째 애니메이션 재생 (예시)
              modelViewer.addEventListener('animation-finished', () => {
                // 두 번째 애니메이션 이름 확인 및 재생
                if (modelViewer.availableAnimations.length > 1) {
                  const animation2Name = modelViewer.availableAnimations[1]; // 실제 애니메이션 이름으로 변경하세요
                   // 현재 재생된 애니메이션과 다를 경우에만 재생
                   if (modelViewer.animationName !== animation2Name) {
                       modelViewer.animationName = animation2Name;
                       modelViewer.play();
                   }
                } else {
                  console.log('두 번째 애니메이션이 없습니다.');
                   // 두 번째 애니메이션이 없을 경우 다시 첫 번째 애니메이션 재생 (선택 사항)
                   // modelViewer.animationName = animation1Name;
                   // modelViewer.play();
                }
              }, { once: true }); // 첫 번째 애니메이션 종료 시 한 번만 실행
            }
          });
        }
      });
    </script>
    <script>
      document.addEventListener('DOMContentLoaded', function() {
        const searchInput = document.getElementById('searchInput');
        const searchContainer = searchInput.closest('.search-bar-container');
        const placeholderTexts = ['장소', '나라', '여행지'];
        let textIndex = 0;
        const basePlaceholder = "여행했던 ";
        const endPlaceholder = " 를 입력해주세요.";

        // 플레이스홀더 오버레이 생성
        const overlay = document.createElement('div');
        overlay.className = 'placeholder-overlay';
        searchContainer.appendChild(overlay);

        function animatePlaceholder() {
          // 입력 필드가 포커스되지 않은 상태일 때만 애니메이션 실행
          if (searchInput !== document.activeElement) {
            const currentText = placeholderTexts[textIndex];
            searchInput.placeholder = ' '; // 빈 플레이스홀더로 설정
            
            // 오버레이 텍스트 업데이트
            overlay.innerHTML = `${basePlaceholder}<span class="blue-text">'${currentText}'</span>${endPlaceholder}`;
            
            textIndex = (textIndex + 1) % placeholderTexts.length;
          }
        }

        let placeholderInterval = null; // Interval ID를 저장할 변수

        function startPlaceholderAnimation() {
          if (!placeholderInterval) { // 애니메이션이 이미 실행 중이 아니면 시작
            animatePlaceholder(); // 첫 프레임 즉시 표시
            placeholderInterval = setInterval(animatePlaceholder, 1000);
          }
        }

        function stopPlaceholderAnimation() {
          clearInterval(placeholderInterval);
          placeholderInterval = null;
        }

        // 입력 필드 포커스 시 애니메이션 중지 및 기본 플레이스홀더 표시
        searchInput.addEventListener('focus', function() {
          stopPlaceholderAnimation(); // 포커스 시 애니메이션 중지
          overlay.style.display = 'none'; // 오버레이 숨김
          searchInput.placeholder = '여행할 때 여기어때'; // 네이티브 플레이스홀더 텍스트 변경
        });

        // 입력 필드 포커스 해제 시 애니메이션 재개
        searchInput.addEventListener('blur', function() {
          if (!searchInput.value) {
            searchInput.placeholder = ' '; // 네이티브 플레이스홀더 초기화
            overlay.style.display = 'flex'; // 오버레이 다시 표시
            startPlaceholderAnimation(); // 포커스 해제 시 애니메이션 재개 (입력값이 없을 경우)
          }
        });

        // 입력값이 변경될 때 오버레이 표시/숨김 처리
        searchInput.addEventListener('input', function() {
          // 입력값이 있을 때는 오버레이 숨김
          if (this.value) {
            overlay.style.display = 'none';
            searchInput.placeholder = ''; // 입력값이 있을 때 네이티브 플레이스홀더 숨김
          } else {
            // 입력값이 없을 때는 오버레이 표시
            overlay.style.display = 'flex';
            searchInput.placeholder = ' '; // 입력값이 없을 때 네이티브 플레이스홀더 초기화
          }
        });

        // 초기 로드 시 애니메이션 시작
        startPlaceholderAnimation();
      });
    </script>
  </body>
</html>

