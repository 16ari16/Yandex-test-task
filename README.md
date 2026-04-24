# Дизайн-система: Достижения (Личный кабинет игрока)

## Описание проекта

Дизайн-система для мобильного приложения Яндекс Игры. Раздел «Достижения» в личном кабинете игрока.

**Версия:** 1.0  
**Платформа:** Mobile (iOS/Android)  
**Viewport:** 375×812 px  
**Стиль:** Классический Яндекс (синий + элементы)

---

## Структура файлов

| Файл | Описание |
|------|----------|
| `design-system.json` | JSON-спецификация токенов, компонентов, экранов |
| `achievements-design.html` | Визуальная спецификация (открыть в браузере) |
| `README.md` | Документация |

---

## Pages

### Page 1: Tokens
Дизайн-токены (Design Tokens) —原子ные значения для всей системы.

**Цвета:**
- `--color-primary` #1A88FF — основной синий
- `--color-success` #28A745 — выполнено
- `--color-warning` #FFD400 — редкое/золотое
- `--color-bg` #F5F5F5 — фон страницы
- `--color-surface` #FFFFFF — карточки
- `--color-text-*` — текстовые цвета

**Отступы (4px grid):**
- `--space-xs` 4px
- `--space-sm` 8px
- `--space-md` 16px
- `--space-lg` 24px
- `--space-xl` 32px

**Типографика:**
- `--text-h1` 24px/700 — заголовок экрана
- `--text-h2` 20px/600 — подзаголовок
- `--text-body` 16px/400 — основной текст
- `--text-caption` 12px/400 — подписи

**Border Radius:**
- `--radius-sm` 8px
- `--radius-md` 12px
- `--radius-lg` 16px
- `--radius-full` 9999px (pill)

---

### Page 2: Components

#### AchievementCard
Карточка достижения. variants: `default`, `completed`, `locked`.

**Состояния:**
- default — стандартная карточка
- completed — зелёная рамка, badge ✓
- locked — opacity 0.5, серый фон иконки

**Элементы:**
- icon: 48×48 px, center
- title: 2 строки max
- game name
- status badge (top-right)
- date (если получено)

#### GameTab
Табы игр. variants: `active`, `inactive`.

- height: 36px
- padding: 16px
- border-radius: full (pill)
- active: синий фон, белый текст
- inactive: прозрачный, серая рамка

#### ProgressRing
Кольцевой индикатор прогресса. variants: `s` (40px), `m` (80px), `l` (160px).

- stroke-width: 4/6/10px
- track: `--color-border`
- progress: `--color-primary`
- label: centered

#### LeaderboardRow
Строка рейтинга.

- height: 56px
- layout: horizontal
- elements: rank, avatar (40×40), name, score

---

### Page 3: Screens (Auto-layout)

#### Screen 1: achievements_list
Главный экран списка достижений.

**Структура:**
1. Header: "Достижения" + иконка поиска
2. GameTabs: горизонтальный скролл табов игр
3. Stats: 2 карточки (получено N/M, процент)
4. Grid: карточки достижений (2 колонки)

**Interactions:**
- tap card → achievement_detail
- tap tab → filter by game

---

#### Screen 2: achievement_detail
Детали одного достижения.

**Структура:**
1. Header: "Достижение" + back
2. Large icon: 120×120 px со свечением (rare)
3. Title + игра (badge)
4. Description
5. Progress bar
6. Date received (если выполнено)

---

#### Screen 3: my_progress
Измерение общего прогресса.

**Структура:**
1. Header: "Мой прогресс"
2. ProgressRing (large): общий процент
3. Stats: общее число / всего
4. List by game: прогресс по каждой игре

---

#### Screen 4: leaderboard
Сравнение с другими игроками.

**Структура:**
1. Header: "Рейтинг"
2. Tabs: "Друзья" / "Все игроки"
3. Search: поиск по нику
4. List: LeaderboardRow × N
5. Your position: sticked bottom, highlighted

---

### Page 4: Content (Mock Data)

**Игры:**
- Яндекс Игры (3 достижения)
- Лучник (5 достижений)
- Находкин (4 достижения)
- Шахматы (2 достижения)

**Пользователи рейтинга:**
- Александр, Ирина, Константин, Настя, Дмитрий, Елена, Сергей, Анна

---

## Interactions

| Action | Trigger | Result |
|--------|---------|--------|
| tap_achievement | tap card | navigate_to → achievement_detail |
| tap_game_tab | tap tab | filter → achievements_list |
| swipe_achievement | swipe card | expand → card_preview |
| tap_leaderboard_row | tap row | navigate_to → user_profile |

---

## Техническая сборка (для разработчиков)

### CSS Variables
```css
:root {
  --color-primary: #1A88FF;
  --color-primary-pressed: #1570DE;
  --color-success: #28A745;
  --color-warning: #FFD400;
  --color-bg: #F5F5F5;
  --color-surface: #FFFFFF;
  --color-text-primary: #212121;
  --color-text-secondary: #6E6E6E;
  --color-text-tertiary: #A6A6A6;
  --color-border: #E3E3E3;

  --space-xs: 4px;
  --space-sm: 8px;
  --space-md: 16px;
  --space-lg: 24px;
  --space-xl: 32px;

  --radius-sm: 8px;
  --radius-md: 12px;
  --radius-lg: 16px;
  --radius-full: 9999px;

  --shadow-sm: 0 1px 2px rgba(0,0,0,0.08);
  --shadow-md: 0 4px 12px rgba(0,0,0,0.1);
  --shadow-glow: 0 0 24px rgba(255,212,0,0.4);
}
```

### Viewport (Safe Area)
- Width: 375px
- Height: 812px
- Safe area top: 44px
- Safe area bottom: 34px

---

## Acceptance Criteria

- [x] Токены вынесены на отдельную страницу
- [x] Компоненты: карточки, табы, прогресс, рейтинг
- [x] 4 экрана с auto-layout
- [x] Моковые данные для контента
- [x] Фильтрация по играм
- [x] Экран "Мой прогресс" с кольцевым индикатором
- [x] Экран "Рейтинг" с лидербордом
- [x] Статус: выполнено / заблокировано
- [x] Дата получения достижения
- [x] Привязка достижений к конкретным играм

---

## Как использовать

1. **Для дизайнера:** открыть `achievements-design.html` в браузере для визуальной референс
2. **Для разработчика:** использовать токены из `design-system.json` или CSS Variables из README

---

*Дизайн-система подготовлена для тестового задания на стажировку по продуктовому дизайну.*