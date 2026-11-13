# AccessBoard-Rang-Kontrasti
Plaintext
accessboard/
├── index.html
├── style.css
└── app/
    ├── db.js
    └── main.js
1. index.html
Ushbu faylda semantik teglar va holat indikatorlari uchun rangdan tashqari matn hamda belgilar (ikonkalar) ishlatilgan.

HTML
<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>AccessBoard — WCAG AA + IndexedDB</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <header class="app-header">
    <h1>AccessBoard</h1>
    <p class="subtitle">WCAG AA (4.5:1+) Kontrast va IndexedDB Offline Taxta</p>
  </header>

  <main class="container">
    <!-- Yangi karta qo'shish formasi -->
    <section class="form-section" aria-labelledby="form-heading">
      <h2 id="form-heading">Yangi vazifa qo'shish</h2>
      <form id="card-form" class="card-form">
        <div class="form-group">
          <label for="card-title">Vazifa nomi:</label>
          <input type="text" id="card-title" placeholder="Masalan: Kontrastni tekshirish" required>
        </div>

        <div class="form-group">
          <label for="card-status">Holati:</label>
          <select id="card-status">
            <option value="todo">⏳ Kutilmoqda (Todo)</option>
            <option value="progress">⚙️ Jarayonda (In Progress)</option>
            <option value="done">✅ Bajarildi (Done)</option>
          </select>
        </div>

        <button type="submit" class="btn-primary">+ Kartani saqlash</button>
      </form>
    </section>

    <!-- Kartalar ro'yxati -->
    <section class="board-section" aria-labelledby="board-heading">
      <div class="board-header">
        <h2 id="board-heading">Vazifalar taxtasi</h2>
        <span id="db-status" class="db-badge" role="status">💾 IndexedDB tayyor</span>
      </div>
      <div id="cards-container" class="cards-grid"></div>
    </section>
  </main>

  <script type="module" src="app/main.js"></script>
</body>
</html>
2. style.css
Barcha rang juftliklari WCAG AA (kamida 4.5:1) kontrast nisbatidan yuqori qilib tanlangan (ko'pchiligi 7:1 (AAA) darajasida):

Asosiy matn #111827 va oq fon #ffffff — 17.7:1

Kutilmoqda (Todo): Matn #78350f / Fon #fef3c7 — 8.2:1

Jarayonda (Progress): Matn #1e3a8a / Fon #dbeafe — 8.6:1

Bajarildi (Done): Matn #064e3b / Fon #d1fae5 — 8.9:1

CSS
:root {
  --bg-page: #f3f4f6;
  --bg-card: #ffffff;
  --text-main: #111827;     /* 17.7:1 kontrast oq fonda */
  --text-muted: #374151;    /* 10.3:1 kontrast oq fonda */
  --border-color: #9ca3af;
  
  --primary-bg: #1d4ed8;    /* 6.7:1 kontrast oq matn bilan */
  --primary-hover: #1e40af;
  --primary-text: #ffffff;

  /* Holat ranglari (WCAG AA/AAA tasdiqlangan) */
  --todo-bg: #fef3c7;
  --todo-text: #78350f;     /* 8.2:1 kontrast */
  --todo-border: #b45309;

  --progress-bg: #dbeafe;
  --progress-text: #1e3a8a; /* 8.6:1 kontrast */
  --progress-border: #1d4ed8;

  --done-bg: #d1fae5;
  --done-text: #064e3b;     /* 8.9:1 kontrast */
  --done-border: #047857;
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: system-ui, -apple-system, sans-serif;
  background-color: var(--bg-page);
  color: var(--text-main);
  line-height: 1.6;
}

.app-header {
  background-color: #111827;
  color: #ffffff; /* 17.7:1 kontrast */
  padding: 1.5rem 2rem;
  text-align: center;
}

.subtitle {
  color: #e5e7eb; /* 14.5:1 kontrast #111827 fonda */
  font-size: 0.95rem;
  margin-top: 0.25rem;
}

.container {
  max-width: 960px;
  margin: 2rem auto;
  padding: 0 1rem;
  display: grid;
  gap: 2rem;
}

.form-section, .board-section {
  background: var(--bg-card);
  padding: 1.5rem;
  border-radius: 8px;
  border: 2px solid #d1d5db;
}

h2 {
  font-size: 1.25rem;
  margin-bottom: 1rem;
  color: var(--text-main);
}

.card-form {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  align-items: flex-end;
}

.form-group {
  display: flex;
  flex-direction: column;
  flex: 1;
  min-width: 200px;
}

label {
  font-weight: 600;
  margin-bottom: 0.35rem;
  color: var(--text-main);
}

input, select {
  padding: 0.65rem;
  font-size: 1rem;
  border: 2px solid #4b5563;
  border-radius: 6px;
  background-color: #ffffff;
  color: var(--text-main);
}

input:focus, select:focus, button:focus {
  outline: 3px solid #2563eb;
  outline-offset: 2px;
}

.btn-primary {
  background-color: var(--primary-bg);
  color: var(--primary-text);
  border: none;
  padding: 0.72rem 1.25rem;
  font-size: 1rem;
  font-weight: 600;
  border-radius: 6px;
  cursor: pointer;
}

.btn-primary:hover {
  background-color: var(--primary-hover);
}

.board-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
}

.db-badge {
  background-color: #e5e7eb;
  color: #111827; /* 14.5:1 kontrast */
  padding: 0.3rem 0.75rem;
  border-radius: 999px;
  font-size: 0.85rem;
  font-weight: 600;
  border: 1px solid #6b7280;
}

.cards-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  gap: 1rem;
}

.task-card {
  background: #ffffff;
  border: 2px solid #9ca3af;
  border-radius: 8px;
  padding: 1rem;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  gap: 1rem;
}

.task-title {
  font-size: 1.1rem;
  font-weight: 700;
  color: var(--text-main);
}

/* Holat indikatorlari: Rang + Belgi + Matn */
.status-badge {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.35rem 0.65rem;
  border-radius: 6px;
  font-size: 0.9rem;
  font-weight: 700;
  width: fit-content;
}

.status-todo {
  background-color: var(--todo-bg);
  color: var(--todo-text);
  border: 2px solid var(--todo-border);
}

.status-progress {
  background-color: var(--progress-bg);
  color: var(--progress-text);
  border: 2px solid var(--progress-border);
}

.status-done {
  background-color: var(--done-bg);
  color: var(--done-text);
  border: 2px solid var(--done-border);
}

.card-actions {
  display: flex;
  gap: 0.5rem;
  margin-top: 0.5rem;
}

.btn-small {
  padding: 0.4rem 0.65rem;
  font-size: 0.85rem;
  font-weight: 600;
  border-radius: 4px;
  cursor: pointer;
  background-color: #f9fafb;
  color: #111827; /* 16.9:1 kontrast */
  border: 1.5px solid #374151;
}

.btn-small:hover {
  background-color: #e5e7eb;
}

.btn-delete {
  background-color: #fee2e2;
  color: #7f1d1d; /* 8.5:1 kontrast */
  border-color: #991b1b;
}

.btn-delete:hover {
  background-color: #fecaca;
}
3. app/db.js
Talabda so'ralganidek createObjectStore, put va getAll metodlari bilan ishlaydigan IndexedDB moduli:

JavaScript
const DB_NAME = 'AccessBoardDB';
const DB_VERSION = 1;
const STORE_NAME = 'cards';

// Bazani ochish va kerak bo'lsa ObjectStore yaratish
export function openDB() {
  return new Promise((resolve, reject) => {
    const request = indexedDB.open(DB_NAME, DB_VERSION);

    request.onupgradeneeded = (event) => {
      const db = event.target.result;
      if (!db.objectStoreNames.contains(STORE_NAME)) {
        db.createObjectStore(STORE_NAME, { keyPath: 'id' });
      }
    };

    request.onsuccess = () => resolve(request.result);
    request.onerror = () => reject(request.error);
  });
}

// Kartani qo'shish yoki yangilash (put)
export async function saveCard(card) {
  const db = await openDB();
  return new Promise((resolve, reject) => {
    const tx = db.transaction(STORE_NAME, 'readwrite');
    const store = tx.objectStore(STORE_NAME);
    const request = store.put(card);

    request.onsuccess = () => resolve(request.result);
    request.onerror = () => reject(request.error);
  });
}

// Barcha saqlangan kartalarni o'qish (getAll)
export async function getAllCards() {
  const db = await openDB();
  return new Promise((resolve, reject) => {
    const tx = db.transaction(STORE_NAME, 'readonly');
    const store = tx.objectStore(STORE_NAME);
    const request = store.getAll();

    request.onsuccess = () => resolve(request.result);
    request.onerror = () => reject(request.error);
  });
}

// Kartani o'chirish
export async function deleteCard(id) {
  const db = await openDB();
  return new Promise((resolve, reject) => {
    const tx = db.transaction(STORE_NAME, 'readwrite');
    const store = tx.objectStore(STORE_NAME);
    const request = store.delete(id);

    request.onsuccess = () => resolve();
    request.onerror = () => reject(request.error);
  });
}
4. app/main.js
Sahifa yuklanganda IndexedDB'dan kartalarni yuklab olish va ularni ekranda holat belgisi + matni bilan chiqarish logikasi:

JavaScript
import { saveCard, getAllCards, deleteCard } from './db.js';

const cardForm = document.getElementById('card-form');
const cardTitleInput = document.getElementById('card-title');
const cardStatusSelect = document.getElementById('card-status');
const cardsContainer = document.getElementById('cards-container');
const dbStatusBadge = document.getElementById('db-status');

// Har bir holat uchun rang klassi, belgi (ikonka) va matn
const STATUS_CONFIG = {
  todo: {
    label: 'Kutilmoqda',
    icon: '⏳',
    className: 'status-todo',
    next: 'progress'
  },
  progress: {
    label: 'Jarayonda',
    icon: '⚙️',
    className: 'status-progress',
    next: 'done'
  },
  done: {
    label: 'Bajarildi',
    icon: '✅',
    className: 'status-done',
    next: 'todo'
  }
};

// Sahifa yuklanganda saqlangan kartalarni chiqarish
async function renderCards() {
  try {
    const cards = await getAllCards();
    cardsContainer.innerHTML = '';

    if (cards.length === 0) {
      cardsContainer.innerHTML = '<p>Hozircha vazifalar yoʻq. Yuqoridan yangi karta qoʻshing.</p>';
      return;
    }

    cards.forEach((card) => {
      const statusInfo = STATUS_CONFIG[card.status] || STATUS_CONFIG.todo;

      const cardEl = document.createElement('article');
      cardEl.className = 'task-card';
      cardEl.innerHTML = `
        <div>
          <span class="status-badge ${statusInfo.className}">
            <span aria-hidden="true">${statusInfo.icon}</span>
            <span>${statusInfo.label}</span>
          </span>
          <h3 class="task-title" style="margin-top: 0.75rem;">${escapeHTML(card.title)}</h3>
        </div>
        <div class="card-actions">
          <button type="button" class="btn-small btn-next" data-id="${card.id}">
            🔄 Holatni o'zgartirish
          </button>
          <button type="button" class="btn-small btn-delete" data-id="${card.id}">
            🗑️ O'chirish
          </button>
        </div>
      `;

      // Holatni o'zgartirish tugmasi
      cardEl.querySelector('.btn-next').addEventListener('click', async () => {
        card.status = statusInfo.next;
        await saveCard(card);
        dbStatusBadge.textContent = '💾 Yangilandi (Offline)';
        renderCards();
      });

      // O'chirish tugmasi
      cardEl.querySelector('.btn-delete').addEventListener('click', async () => {
        await deleteCard(card.id);
        dbStatusBadge.textContent = '🗑️ Oʻchirildi';
        renderCards();
      });

      cardsContainer.appendChild(cardEl);
    });
  } catch (err) {
    dbStatusBadge.textContent = '⚠️ Xatolik yuz berdi';
    console.error(err);
  }
}

// Yangi karta qo'shish
cardForm.addEventListener('submit', async (e) => {
  e.preventDefault();
  const title = cardTitleInput.value.trim();
  if (!title) return;

  const newCard = {
    id: Date.now(),
    title,
    status: cardStatusSelect.value
  };

  await saveCard(newCard);
  dbStatusBadge.textContent = '💾 IndexedDB ga saqlandi';
  cardTitleInput.value = '';
  renderCards();
});

// XSS himoyasi uchun matnni tozalash
function escapeHTML(str) {
  const div = document.createElement('div');
  div.textContent = str;
  return div.innerHTML;
}

// Dastur ishga tushganda bazadan o'qish
document.addEventListener('DOMContentLoaded', renderCards);
