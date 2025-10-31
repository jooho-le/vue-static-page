<template>
  <div class="app">
    <!-- Hero section -->
    <header class="hero">
      <div class="hero-overlay"></div>
      <nav class="top-nav">
        <div class="logo">한가위</div>
        <div class="nav-right">
          <button class="ghost-btn" @click="toggleWish">
            {{ showWish ? '인사 닫기' : '인사 보기' }}
          </button>
        </div>
      </nav>

      <div class="hero-content">
        <div class="hero-text">
          <p class="tag">2025 추석</p>
          <h1>풍성하고 밝은 한가위 보내세요 🌕</h1>
          <p class="subtitle">
            둥근 보름달처럼 마음도 둥글둥글해지는 날.<br />
            가족, 친구, 그리고 나에게도 수고했다고 말해요.
          </p>
          <div class="cta-group">
            <button class="primary-btn" @click="scrollToSection('food')">
              한가위 한상 보기
            </button>
            <button class="secondary-btn" @click="scrollToSection('message')">
              마음 전하기
            </button>
          </div>
        </div>
        <div class="moon-wrap">
          <div class="moon"></div>
          <div class="cloud cloud-1"></div>
          <div class="cloud cloud-2"></div>
        </div>
      </div>
    </header>

    <!-- Wish banner -->
    <transition name="fade">
      <section v-if="showWish" class="wish-banner">
        <p>
          🌕 올 추석엔 <strong>건강</strong>과 <strong>좋은 사람</strong>이 늘 곁에 있기를! – 당신의 Vue 페이지
        </p>
      </section>
    </transition>

    <!-- Food / items section -->
    <main class="content">
      <section id="food" class="section">
        <h2>한가위 한상</h2>
        <p class="section-desc">
          추석 하면 떠오르는 음식들을 담았어요. 실제 데이터 말고, 지금은 뷰 데모용 더미예요 🙂
        </p>
        <div class="card-grid">
          <article v-for="item in foods" :key="item.id" class="card">
            <div class="emoji">{{ item.emoji }}</div>
            <h3>{{ item.name }}</h3>
            <p>{{ item.desc }}</p>
            <small>{{ item.region }}</small>
          </article>
        </div>
      </section>

      <section id="message" class="section section-alt">
        <h2>가족에게 한마디</h2>
        <p class="section-desc">
          아래 메시지는 예시예요. 실제로는 폼이랑 연동해서 저장하거나, AI로 예쁜 문장 만들어도 돼요.
        </p>
        <div class="message-box">
          <textarea
              v-model="customMessage"
              class="message-input"
              rows="4"
              placeholder="올해도 고생 많으셨어요! 건강하세요 💛"
          ></textarea>
          <p class="preview-title">미리보기</p>
          <div class="message-preview">
            {{ customMessage || defaultMessage }}
          </div>
        </div>
      </section>
    </main>

    <footer class="footer">
      <p>© {{ new Date().getFullYear() }} 한가위 웹페이지 · made with Vue + TS + Vite</p>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const showWish = ref(true)

const foods = ref([
  {
    id: 1,
    name: '송편',
    desc: '갓 쪄서 뜨거운 쫀득쫀득',
    emoji: '🥟',
    region: '전국'
  },
  {
    id: 2,
    name: '전 & 산적',
    desc: '손이 많이 가도 빠질 수 없죠',
    emoji: '🥘',
    region: '집집마다'
  },
  {
    id: 3,
    name: '식혜',
    desc: '달달하고 시원하게',
    emoji: '🧃',
    region: '경상/강원'
  },
  {
    id: 4,
    name: '토란국',
    desc: '명절 아침에 따끈하게',
    emoji: '🍲',
    region: '충청/전라'
  }
])

const customMessage = ref('')
const defaultMessage =
    '풍성한 한가위 보내세요! 멀리 있어도 마음만은 함께해요 🍂'

const toggleWish = () => {
  showWish.value = !showWish.value
}

const scrollToSection = (id: string) => {
  const el = document.getElementById(id)
  if (el) {
    el.scrollIntoView({ behavior: 'smooth', block: 'start' })
  }
}
</script>

<style scoped>
:root {
  --bg: #0f172a;
  --accent: #f97316;
  --accent-soft: rgba(249, 115, 22, 0.12);
  --text: #0f172a;
  --light: #f8fafc;
  --muted: #64748b;
  --card: rgba(248, 250, 252, 0.85);
}

.app {
  min-height: 100vh;
  background: #0f172a;
  color: #0f172a;
  display: flex;
  flex-direction: column;
}

.hero {
  position: relative;
  min-height: 60vh;
  background: linear-gradient(160deg, #0f172a 0%, #1e293b 40%, #f97316 130%);
  color: white;
  overflow: hidden;
  padding-bottom: 3rem;
}

.hero-overlay {
  position: absolute;
  inset: 0;
  background-image: radial-gradient(
      circle at 15% 20%,
      rgba(249, 115, 22, 0.4),
      transparent 45%
  ),
  radial-gradient(circle at 80% 10%, rgba(255, 255, 255, 0.15), transparent 50%);
  pointer-events: none;
}

.top-nav {
  position: relative;
  z-index: 2;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1.4rem 1.8rem;
}

.logo {
  font-weight: 700;
  letter-spacing: -0.03em;
  font-size: 1.3rem;
}

.nav-right {
  display: flex;
  gap: 0.75rem;
}

.ghost-btn {
  background: rgba(15, 23, 42, 0.1);
  border: 1px solid rgba(248, 250, 252, 0.25);
  padding: 0.4rem 1rem;
  border-radius: 9999px;
  color: white;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s;
}
.ghost-btn:hover {
  background: rgba(15, 23, 42, 0.4);
}

.hero-content {
  position: relative;
  z-index: 2;
  display: grid;
  grid-template-columns: 1.1fr 0.9fr;
  gap: 1.5rem;
  padding: 1rem 1.8rem 0;
  align-items: center;
}

.hero-text .tag {
  display: inline-block;
  background: rgba(15, 23, 42, 0.12);
  border: 1px solid rgba(248, 250, 252, 0.25);
  padding: 0.25rem 0.7rem;
  border-radius: 999px;
  font-size: 0.7rem;
  margin-bottom: 0.9rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
}

.hero-text h1 {
  font-size: clamp(2.6rem, 3.5vw, 3.1rem);
  line-height: 1.05;
  margin-bottom: 1rem;
}
.hero-text .subtitle {
  max-width: 32rem;
  line-height: 1.5;
  color: rgba(248, 250, 252, 0.78);
  margin-bottom: 1.3rem;
}

.cta-group {
  display: flex;
  gap: 0.8rem;
  flex-wrap: wrap;
}

.primary-btn {
  background: #f97316;
  border: none;
  color: white;
  padding: 0.55rem 1.3rem;
  border-radius: 9999px;
  font-weight: 600;
  cursor: pointer;
  transition: transform 0.2s;
}
.primary-btn:hover {
  transform: translateY(-2px);
}

.secondary-btn {
  background: rgba(15, 23, 42, 0.08);
  border: 1px solid rgba(248, 250, 252, 0.25);
  color: white;
  padding: 0.55rem 1.2rem;
  border-radius: 9999px;
  cursor: pointer;
}

.moon-wrap {
  position: relative;
  min-height: 260px;
}
.moon {
  position: absolute;
  right: 12%;
  top: 0.8rem;
  width: 170px;
  height: 170px;
  border-radius: 9999px;
  background: radial-gradient(circle at 25% 20%, #fff, #ffe6ad 65%, #f97316 130%);
  box-shadow: 0 0 60px rgba(249, 115, 22, 0.4);
}
.cloud {
  position: absolute;
  background: rgba(15, 23, 42, 0.36);
  border-radius: 999px;
  filter: blur(1px);
}
.cloud-1 {
  width: 120px;
  height: 26px;
  top: 7.4rem;
  right: 2rem;
}
.cloud-2 {
  width: 75px;
  height: 20px;
  top: 6.1rem;
  right: 10rem;
}

.wish-banner {
  background: #f97316;
  color: white;
  text-align: center;
  padding: 0.9rem 1.2rem;
  font-weight: 500;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.25s;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.content {
  background: #f8fafc;
  flex: 1;
}

.section {
  max-width: 1100px;
  margin: 0 auto;
  padding: 3.2rem 1.3rem 2.3rem;
}
.section-alt {
  background: #e2e8f0;
  border-radius: 2rem 2rem 0 0;
}
.section h2 {
  font-size: 1.5rem;
  margin-bottom: 0.5rem;
}
.section-desc {
  color: #64748b;
  margin-bottom: 1.8rem;
}

.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
  gap: 1.3rem;
}
.card {
  background: white;
  border: 1px solid rgba(15, 23, 42, 0.03);
  border-radius: 1.4rem;
  padding: 1rem 1rem 1rem;
  box-shadow: 0 10px 30px rgba(15, 23, 42, 0.04);
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
}
.card .emoji {
  font-size: 2.2rem;
  margin-bottom: 0.4rem;
}
.card h3 {
  margin-bottom: 0.2rem;
  font-size: 1.02rem;
}
.card p {
  color: #64748b;
  font-size: 0.85rem;
  flex: 1;
}
.card small {
  color: #94a3b8;
  font-size: 0.72rem;
}

.message-box {
  background: rgba(248, 250, 252, 0.85);
  border: 1px solid rgba(148, 163, 184, 0.35);
  border-radius: 1.2rem;
  padding: 1.3rem 1.3rem 1.1rem;
}
.message-input {
  width: 100%;
  border: 1px solid rgba(148, 163, 184, 0.6);
  border-radius: 0.7rem;
  padding: 0.7rem 0.6rem;
  font-family: inherit;
  resize: vertical;
  margin-bottom: 0.9rem;
  background: white;
}
.preview-title {
  font-weight: 600;
  margin-bottom: 0.5rem;
}
.message-preview {
  background: white;
  border-radius: 0.8rem;
  padding: 0.7rem 0.65rem;
  border: 1px dashed rgba(15, 23, 42, 0.08);
  line-height: 1.4;
}

.footer {
  background: #0f172a;
  color: rgba(248, 250, 252, 0.6);
  text-align: center;
  padding: 1.5rem 1rem 2.5rem;
  font-size: 0.78rem;
}

/* responsive */
@media (max-width: 960px) {
  .hero-content {
    grid-template-columns: 1fr;
  }
  .moon-wrap {
    min-height: 180px;
  }
  .moon {
    right: 4rem;
  }
}
@media (max-width: 640px) {
  .top-nav {
    padding-inline: 1rem;
  }
  .hero-text h1 {
    font-size: 2.35rem;
  }
  .cta-group {
    flex-direction: column;
    align-items: flex-start;
  }
  .section {
    padding-inline: 1rem;
  }
}
</style>
