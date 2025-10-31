<!-- src/App.vue -->
<template>
  <div class="app">
    <!-- 상단 히어로 -->
    <header class="hero">
      <nav class="nav">
        <div class="logo">🌕 한가위</div>
        <div class="nav-links">
          <button class="nav-btn" @click="scrollTo('foods')">음식</button>
          <button class="nav-btn" @click="scrollTo('games')">전통놀이</button>
          <button class="nav-btn" @click="scrollTo('origin')">추석이야기</button>
          <button class="nav-btn" @click="scrollTo('events')">행사</button>
          <button class="nav-btn" @click="scrollTo('messages')">덕담보내기</button>
        </div>
      </nav>

      <div class="hero-body">
        <div class="hero-text">
          <p class="hero-tag">2025 Chuseok Special</p>
          <h1>
            풍요로운 한가위 되세요 🌾
          </h1>
          <p class="hero-sub">
            보름달처럼 밝고, 송편처럼 속이 꽉 찬 명절.
            가족과 친구들에게 마음을 전해보세요.
          </p>
          <div class="hero-actions">
            <button class="primary" @click="scrollTo('messages')">덕담 쓰기</button>
            <button class="ghost" @click="scrollTo('foods')">추석콘텐츠 보기</button>
          </div>
        </div>
        <div class="hero-visual" aria-label="보름달과 한복색 배경 일러스트">
          <div class="moon"></div>
          <div class="cloud c1"></div>
          <div class="cloud c2"></div>
          <div class="lamp l1"></div>
          <div class="lamp l2"></div>
        </div>
      </div>
    </header>

    <!-- 추석 음식 -->
    <section id="foods" class="section section-light">
      <header class="section-head">
        <h2>🥟 추석 음식 한상</h2>
        <p>지역마다 조금씩 다르지만, 이 음식들이 있으면 “우리집도 추석이네!” 하는 느낌 나죠.</p>
      </header>

      <div class="grid-3">
        <article v-for="food in foods" :key="food.id" class="card">
          <div class="card-icon">{{ food.emoji }}</div>
          <h3>{{ food.name }}</h3>
          <p>{{ food.desc }}</p>
          <div class="tagline">{{ food.note }}</div>
        </article>
      </div>
    </section>

    <!-- 전통 놀이 -->
    <section id="games" class="section section-colored">
      <header class="section-head">
        <h2>🎎 추석 전통 놀이</h2>
        <p>가족, 친척, 마을끼리 모이면 몸도 마음도 풀리는 놀이.</p>
      </header>

      <div class="grid-2">
        <article v-for="game in games" :key="game.id" class="card card-outline">
          <div class="card-top">
            <h3>{{ game.name }}</h3>
            <span class="badge">{{ game.level }}</span>
          </div>
          <p>{{ game.desc }}</p>
          <ul class="mini-list">
            <li v-for="tip in game.tips" :key="tip">
              {{ tip }}
            </li>
          </ul>
        </article>
      </div>
    </section>

    <!-- 추석의 기원 / 스토리 -->
    <section id="origin" class="section section-light">
      <header class="section-head">
        <h2>📜 추석은 왜 생겼을까?</h2>
        <p>풍요를 나누는 날, 중추절(仲秋節), 가배(嘉俳)라고도 불렸습니다.</p>
      </header>

      <div class="origin-wrap">
        <article class="origin-card">
          <h3>1. 한가위, “가운데 가을”</h3>
          <p>
            우리 조상들은 음력 8월을 가을 한가운데로 보았고, 그중에서도 보름날을 가장
            귀하게 여겼습니다. 추수한 곡식과 과일을 조상께 먼저 올리고, 이웃과도 나누며
            “올해 고생했다”는 마음을 전했죠.
          </p>
        </article>
        <article class="origin-card">
          <h3>2. 씨름·활쏘기와 함께</h3>
          <p>
            삼국시대 기록에 보면, 추석에 나라에서 여자들 길쌈 겨루기(길쌈놀이)를 시켜
            진 편이 음식을 대접하게 했다는 내용이 나옵니다. 지금의 ‘즐기기’와 ‘나누기’
            전통이 여기서도 보여요.
          </p>
        </article>
        <article class="origin-card">
          <h3>3. 보름달에 비는 소원</h3>
          <p>
            달이 가장 둥근 날이니, “우리 집도 이렇게 찼으면” 하고 기원한 거죠.
            그래서 지금도 가족의 건강, 풍년, 진학, 취업 같은 현실적인 소원을 많이 빌어요.
          </p>
        </article>
      </div>
    </section>

    <!-- 추석 행사 -->
    <section id="events" class="section section-colored">
      <header class="section-head">
        <h2>🎉 2025 추석에 이런 거 하면 좋겠어요</h2>
        <p>실제 일정이 아니니, 앱에선 이 리스트를 API로 바꿔도 돼요.</p>
      </header>

      <div class="timeline">
        <article v-for="event in events" :key="event.id" class="timeline-item">
          <div class="time-dot"></div>
          <div class="tl-body">
            <h3>{{ event.title }}</h3>
            <p class="tl-meta">{{ event.date }} · {{ event.place }}</p>
            <p>{{ event.desc }}</p>
            <div class="tl-tags">
              <span v-for="tag in event.tags" :key="tag" class="tl-tag">{{ tag }}</span>
            </div>
          </div>
        </article>
      </div>
    </section>

    <!-- 덕담 보내기 -->
    <section id="messages" class="section section-light">
      <header class="section-head">
        <h2>💌 추석 덕담 메시지 보내기</h2>
        <p>문자, 톡, 메신저에 바로 붙여넣을 수 있는 짧은 덕담들이에요.</p>
      </header>

      <div class="msg-wrap">
        <div class="msg-left">
          <label for="receiver" class="input-label">받는 사람</label>
          <input
              id="receiver"
              v-model="receiver"
              type="text"
              placeholder="예: 부모님, 팀장님, 친구 지민이"
              class="input"
          />

          <label for="template" class="input-label">메시지 템플릿</label>
          <select id="template" v-model="selectedTemplate" class="input">
            <option v-for="(m, idx) in messageTemplates" :key="idx" :value="idx">
              {{ m.title }}
            </option>
          </select>

          <label class="input-label">커스텀 수정</label>
          <textarea
              v-model="customMessage"
              rows="4"
              class="textarea"
          ></textarea>

          <button class="primary full" @click="copyMessage">
            메시지 복사하기
          </button>
          <p v-if="copied" class="copy-hint">📎 복사됐어요! 이제 메신저에 붙여넣으세요.</p>
        </div>

        <div class="msg-right">
          <p class="msg-preview-title">미리보기</p>
          <div class="msg-preview">
            <p class="to" v-if="receiver">To. {{ receiver }}</p>
            <p>{{ previewMessage }}</p>
            <p class="from">- 추석 웹페이지 드림 🌕</p>
          </div>

          <div class="quick-msg">
            <p class="quick-title">짧은 한 줄</p>
            <div class="chip-wrap">
              <button
                  v-for="short in shortMessages"
                  :key="short"
                  class="chip"
                  @click="applyShort(short)"
              >
                {{ short }}
              </button>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- footer -->
    <footer class="footer">
      <p>© {{ year }} 한가위 콘텐츠 페이지 · Vue + TS + Vite</p>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue'

const year = new Date().getFullYear()

const foods = ref([
  { id: 1, name: '송편', desc: '반달 모양에 소원 담기', note: '찹쌀 + 콩/깨/밤', emoji: '🥟' },
  { id: 2, name: '전/부침', desc: '가족들 먹을 만큼 한가득 부쳐서', note: '산적, 동그랑땡', emoji: '🥘' },
  { id: 3, name: '과일/대추', desc: '가을 햇과일 + 차례상', note: '사과·배·감', emoji: '🍐' },
  { id: 4, name: '토란국', desc: '따뜻하게 속 풀리는 국', note: '지역별로 레시피 다른 편', emoji: '🍲' },
  { id: 5, name: '식혜/수정과', desc: '느끼함 잡아주는 후식', note: '차게 해서 내기', emoji: '🧉' },
  { id: 6, name: '잡채', desc: '명절에 빠질 수 없죠', note: '고기/야채 듬뿍', emoji: '🍜' }
])

const games = ref([
  {
    id: 1,
    name: '강강술래',
    desc: '여럿이 손잡고 둥글게 돌면서 노래하기. 보름달 아래서 하면 최고.',
    level: '난이도 ★',
    tips: ['마당/야외에서 하기', '가운데에 아이 넣어서 춤추게 해도 재밌음']
  },
  {
    id: 2,
    name: '줄다리기 / 씨름',
    desc: '힘 겨루기도 명절의 재미. 큰아이 vs 어른 팀으로 나눠보세요.',
    level: '난이도 ★★☆',
    tips: ['안전하게 매트 깔기', '지는 팀이 전 부치기']
  },
  {
    id: 3,
    name: '윷놀이',
    desc: '세대 불문, 앉아서 할 수 있는 국민놀이.',
    level: '난이도 ★☆',
    tips: ['팀전으로 하면 경쟁심 UP', '상품 하나 걸면 집중도 올라감']
  },
  {
    id: 4,
    name: '연 만들기',
    desc: '아이들이랑 하면 좋은 아날로그 콘텐츠.',
    level: '난이도 ★★',
    tips: ['실내에서는 종이연으로', '이름/소원 적기']
  }
])

const events = ref([
  {
    id: 1,
    title: '도심 한가위 공연',
    date: '9/6 (토) 오후 5시',
    place: '시청 광장',
    desc: '사물놀이, 부채춤, 어린이 한복 패션쇼',
    tags: ['무료', '가족']
  },
  {
    id: 2,
    title: '전통음식 만들기 체험',
    date: '9/7 (일) 오전 11시',
    place: '문화센터 2층',
    desc: '송편 빚기, 전 부치기, 아이들 체험 가능',
    tags: ['체험', '요리']
  },
  {
    id: 3,
    title: '보름달 소원등 달기',
    date: '9/7 (일) 오후 8시',
    place: '한강 공원',
    desc: '가족 이름 적은 소원등 띄우기',
    tags: ['야간', '포토']
  }
])

const messageTemplates = ref([
  {
    title: '가족에게',
    body: '올해도 건강하게 함께해줘서 고마워요. 보름달처럼 꽉 찬 한가위 보내요 💛'
  },
  {
    title: '지인/친구에게',
    body: '풍성한 한가위 보내고, 남은 한 해도 서로 힘내요! 🍂'
  },
  {
    title: '회사/선배님께',
    body: '항상 이끌어주셔서 감사합니다. 명절 잘 보내시고 가족분들과 즐거운 시간 되세요 🙇'
  }
])

const shortMessages = ref([
  '풍요로운 한가위 되세요 🌕',
  '가족과 따뜻한 시간 보내세요 🧡',
  '멀리 있어도 마음만은 가까이 🤎',
  '올해 소원도 꼭 이루세요 ✨'
])

const receiver = ref('')
const selectedTemplate = ref(0)
const customMessage = ref('')

const previewMessage = computed(() => {
  if (customMessage.value.trim().length > 0) return customMessage.value.trim()
  const base = messageTemplates.value[selectedTemplate.value]?.body ?? ''
  if (receiver.value.trim().length > 0) {
    return `${receiver.value.trim()}님, ${base}`
  }
  return base
})

const copied = ref(false)

const scrollTo = (id: string) => {
  const el = document.getElementById(id)
  if (!el) return
  el.scrollIntoView({ behavior: 'smooth', block: 'start' })
}

const copyMessage = async () => {
  try {
    await navigator.clipboard.writeText(previewMessage.value)
    copied.value = true
    setTimeout(() => (copied.value = false), 2800)
  } catch (e) {
    console.warn('copy failed', e)
  }
}

const applyShort = (msg: string) => {
  customMessage.value = msg
}
</script>

<style scoped>
:root {
  --bg: #0f172a;
  --chuseok-yellow: #ffdf6b;
  --chuseok-pink: #f4acb7;
  --chuseok-blue: #406882;
  --offwhite: #f7f3ee;
  --ink: #1f2937;
  --muted: #718096;
}

/* 레이아웃 기본 */
.app {
  min-height: 100vh;
  background: var(--offwhite);
  color: var(--ink);
  display: flex;
  flex-direction: column;
}

/* 히어로 */
.hero {
  background: radial-gradient(circle at 10% 10%, #ffe9a7 0%, #f5a2b8 41%, #1f2937 98%);
  color: #fff;
  padding-bottom: 3rem;
  position: relative;
  overflow: hidden;
}

.nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.2rem 2rem 0.8rem;
  gap: 1.2rem;
  position: relative;
  z-index: 2;
}

.logo {
  font-weight: 700;
  letter-spacing: -0.03em;
  font-size: 1.3rem;
}

.nav-links {
  display: flex;
  gap: 0.5rem;
  flex-wrap: wrap;
}

.nav-btn {
  background: rgba(15, 23, 42, 0.12);
  border: 1px solid rgba(247, 243, 238, 0.35);
  border-radius: 999px;
  color: #fff;
  padding: 0.35rem 0.9rem;
  font-size: 0.78rem;
  cursor: pointer;
  transition: 0.15s;
}
.nav-btn:hover {
  background: rgba(15, 23, 42, 0.3);
}

.hero-body {
  display: grid;
  grid-template-columns: 1.1fr 0.9fr;
  gap: 2rem;
  padding: 2.2rem 2rem 0;
  align-items: center;
  position: relative;
  z-index: 2;
}

.hero-text .hero-tag {
  display: inline-block;
  background: rgba(15, 23, 42, 0.2);
  border: 1px solid rgba(247, 243, 238, 0.35);
  border-radius: 999px;
  padding: 0.25rem 0.6rem;
  font-size: 0.65rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  margin-bottom: 0.85rem;
}

.hero-text h1 {
  font-size: clamp(2.6rem, 3.3vw, 3.4rem);
  line-height: 1.1;
  margin-bottom: 0.6rem;
}

.hero-sub {
  max-width: 31rem;
  line-height: 1.5;
  margin-bottom: 1.2rem;
}

.hero-actions {
  display: flex;
  gap: 0.7rem;
  flex-wrap: wrap;
}

.primary {
  background: #ffdf6b;
  color: #1f2937;
  border: none;
  border-radius: 999px;
  padding: 0.6rem 1.1rem;
  font-weight: 600;
  cursor: pointer;
  transition: transform 0.12s;
}
.primary:hover {
  transform: translateY(-2px);
}

.ghost {
  background: rgba(15, 23, 42, 0.11);
  color: #fff;
  border: 1px solid rgba(247, 243, 238, 0.4);
  border-radius: 999px;
  padding: 0.6rem 1.1rem;
  cursor: pointer;
}

.hero-visual {
  position: relative;
  height: 280px;
}
.moon {
  position: absolute;
  right: 1.5rem;
  top: 0.6rem;
  width: 170px;
  height: 170px;
  background: radial-gradient(circle at 35% 25%, #fffceb 0%, #ffdf6b 65%, rgba(249, 116, 22, 0) 100%);
  border-radius: 50%;
  box-shadow: 0 0 60px rgba(255, 222, 138, 0.7);
}
.cloud {
  position: absolute;
  background: rgba(15, 23, 42, 0.25);
  border-radius: 999px;
  filter: blur(1px);
}
.c1 {
  right: 1.5rem;
  top: 7rem;
  width: 110px;
  height: 22px;
}
.c2 {
  right: 7.5rem;
  top: 5.8rem;
  width: 80px;
  height: 18px;
}
.lamp {
  position: absolute;
  width: 40px;
  height: 70px;
  background: linear-gradient(180deg, #fff 0%, rgba(255, 223, 107, 0) 80%);
  border-radius: 60px 60px 24px 24px;
  border: 1px solid rgba(255, 223, 107, 0.6);
  box-shadow: 0 10px 30px rgba(31, 41, 55, 0.25);
}
.l1 {
  right: 5rem;
  top: 9rem;
}
.l2 {
  right: 2.1rem;
  top: 10.1rem;
  height: 58px;
}

/* 공통 섹션 */
.section {
  max-width: 1100px;
  margin: 0 auto;
  padding: 3.2rem 1.4rem 3.3rem;
  width: 100%;
}

.section-head {
  margin-bottom: 2rem;
}
.section-head h2 {
  font-size: 1.6rem;
  margin-bottom: 0.5rem;
}
.section-head p {
  color: #64748b;
}

.section-light {
  background: #fdfaf3;
}
.section-colored {
  background: linear-gradient(120deg, rgba(255, 223, 107, 0.08), rgba(244, 172, 183, 0.08));
  border-top: 1px solid rgba(255, 223, 107, 0.15);
  border-bottom: 1px solid rgba(64, 104, 130, 0.08);
}

/* 그리드 */
.grid-3 {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(190px, 1fr));
  gap: 1.2rem;
}

.grid-2 {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 1.2rem;
}

/* 카드 */
.card {
  background: #fff;
  border-radius: 1.25rem;
  padding: 1.05rem 1.05rem 1rem;
  box-shadow: 0 10px 30px rgba(15, 23, 42, 0.04);
  border: 1px solid rgba(255, 223, 107, 0.09);
}
.card-icon {
  font-size: 2.2rem;
  margin-bottom: 0.4rem;
}
.card h3 {
  margin-bottom: 0.4rem;
}
.card p {
  color: #64748b;
}
.card .tagline {
  font-size: 0.75rem;
  margin-top: 0.5rem;
  color: #94a3b8;
}

.card-outline {
  background: rgba(255, 255, 255, 0.1);
  border: 1px solid rgba(31, 41, 55, 0.08);
  backdrop-filter: blur(4px);
}
.card-top {
  display: flex;
  justify-content: space-between;
  gap: 1rem;
  margin-bottom: 0.75rem;
}
.badge {
  background: rgba(255, 223, 107, 0.2);
  border: 1px solid rgba(255, 223, 107, 0.5);
  border-radius: 999px;
  padding: 0.15rem 0.6rem;
  font-size: 0.68rem;
}

/* origin */
.origin-wrap {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 1.1rem;
}
.origin-card {
  background: #fff;
  border-radius: 1.25rem;
  padding: 1.1rem 1.05rem 1rem;
  border: 1px solid rgba(244, 172, 183, 0.16);
}
.origin-card h3 {
  margin-bottom: 0.5rem;
}

/* timeline */
.timeline {
  display: flex;
  flex-direction: column;
  gap: 1.1rem;
}
.timeline-item {
  display: flex;
  gap: 0.75rem;
}
.time-dot {
  width: 10px;
  height: 10px;
  background: #ffdf6b;
  border-radius: 999px;
  margin-top: 0.4rem;
}
.tl-body {
  background: rgba(255, 255, 255, 0.7);
  border-radius: 1rem;
  padding: 0.6rem 0.85rem 0.75rem;
  border: 1px solid rgba(64, 104, 130, 0.08);
  width: 100%;
}
.tl-meta {
  font-size: 0.72rem;
  color: #637285;
  margin-bottom: 0.35rem;
}
.tl-tags {
  display: flex;
  gap: 0.4rem;
  flex-wrap: wrap;
  margin-top: 0.35rem;
}
.tl-tag {
  background: rgba(244, 172, 183, 0.33);
  border-radius: 999px;
  padding: 0.15rem 0.55rem;
  font-size: 0.63rem;
}

/* messages */
.msg-wrap {
  display: grid;
  grid-template-columns: minmax(260px, 0.6fr) 1fr;
  gap: 1.3rem;
}
.input-label {
  display: block;
  font-weight: 600;
  margin-bottom: 0.3rem;
}
.input,
.textarea,
select {
  width: 100%;
  border-radius: 0.6rem;
  border: 1px solid rgba(99, 119, 133, 0.4);
  padding: 0.45rem 0.5rem;
  background: #fff;
  margin-bottom: 0.65rem;
  font-family: inherit;
}
.textarea {
  resize: vertical;
}
.full {
  width: 100%;
}
.copy-hint {
  font-size: 0.7rem;
  margin-top: 0.5rem;
  color: #64748b;
}

.msg-right {
  background: #fff;
  border-radius: 1.25rem;
  border: 1px solid rgba(255, 223, 107, 0.12);
  padding: 1rem 1rem 0.9rem;
}
.msg-preview-title {
  font-weight: 600;
  margin-bottom: 0.5rem;
}
.msg-preview {
  background: #fdfaf3;
  border: 1px solid rgba(244, 172, 183, 0.3);
  border-radius: 0.8rem;
  padding: 0.8rem 0.75rem 0.7rem;
  margin-bottom: 0.9rem;
}
.msg-preview .to {
  font-weight: 600;
  margin-bottom: 0.3rem;
}
.msg-preview .from {
  margin-top: 0.6rem;
  font-size: 0.65rem;
  color: #64748b;
}

.quick-msg {
  background: #f9f7f5;
  border-radius: 0.7rem;
  padding: 0.5rem;
  margin-bottom: 0.8rem;
}
.quick-title {
  font-size: 0.7rem;
  margin-bottom: 0.4rem;
  color: #6b7280;
}
.chip-wrap {
  display: flex;
  gap: 0.35rem;
  flex-wrap: wrap;
}
.chip {
  background: #fff;
  border: 1px solid rgba(244, 172, 183, 0.4);
  border-radius: 999px;
  font-size: 0.7rem;
  padding: 0.2rem 0.5rem;
  cursor: pointer;
}
.chip:hover {
  background: rgba(244, 172, 183, 0.22);
}

/* footer */
.footer {
  background: #1f2937;
  color: rgba(255, 255, 255, 0.35);
  text-align: center;
  padding: 1.5rem 1rem 2.1rem;
  font-size: 0.75rem;
}

/* responsive */
@media (max-width: 960px) {
  .hero-body {
    grid-template-columns: 1fr;
  }
  .msg-wrap {
    grid-template-columns: 1fr;
  }
  .nav {
    flex-wrap: wrap;
  }
}
@media (max-width: 600px) {
  .nav-links {
    gap: 0.3rem;
  }
  .hero {
    padding-bottom: 2.2rem;
  }
  .section {
    padding-inline: 1rem;
  }
}
</style>
