# PRD: Islamic Lifestyle & Finance Super-App (MVP as Telegram Mini App)

## 1) Product Vision & Business Goal

### Vision
Создать премиальный исламский daily-use продукт, где религиозная ценность (намаз, Коран, привычки) становится trust-слоем для высококонверсионных финансовых сценариев (ИЖС-рассрочка, халяльные инвестиции, туризм).

### North Star
**Qualified Halal Leads per MAU (QHL/MAU)** — доля активных пользователей, которые оставили валидный лид в одном из коммерческих направлений.

### Business outcomes (12 мес.)
- K-factor Telegram-цикла: >1.1.
- Конверсия MAU -> лид ИЖС: 6–10%.
- Конверсия MAU -> инвестиционный лид: 4–8%.
- 90-day retention: >25% за счет ежедневных религиозных и командных механик.
- Доля пользователей, прошедших AI-консультацию -> коммерческий CTA: >35%.

---

## 2) ICP & JTBD

### ICP (приоритет)
1. **Семейные 25–45** (Татарстан/ПФО): интерес к дому (ИЖС), рассрочке, стабильным условиям.
2. **Осознанные инвесторы 22–40**: золото/серебро/платина, регулярные накопления, соответствие шариату.
3. **Практикующие пользователи 18–35**: ежедневные религиозные практики + мотивация через комьюнити.

### Core JTBD
- «Хочу жить по исламу и принимать финансовые решения без сомнений в халяльности».
- «Хочу быстро понять, потяну ли ИЖС при фиксированных условиях (8 лет, 40% ПВ, Татарстан)».
- «Хочу, чтобы приложение не просто считало, а давало конкретные выгодные предложения».

---

## 3) Killer Features (монетизация + удержание)

## 3.1 AI Deen & Finance Assistant

### Ценность
Единая точка входа для вопросов по фикху и исламским финансам, с мягким переводом в продуктовый оффер.

### Core capabilities
- RAG-поиск по 3 корпусам знаний:
  1) исламское право (источники, фетвы, FAQ);
  2) финансовые правила (риба, гаррар, мудараба и т.д.);
  3) внутренние офферы (ИЖС, туры, инвестиции).
- Режимы ответа:
  - **Deen Mode**: строго религиозное разъяснение.
  - **Finance Mode**: практическая финансовая трактовка.
  - **Action Mode**: шаги «что делать дальше» + CTA.
- Обязательный дисклеймер: не является персональной фетвой/инвестсоветом.

### Lead-gen логика в диалоге
1. User intent detection (намерение): «дом», «инвестиции», «закят», «долг», «халяльность сделки».
2. Qualification questions (до 3 коротких): бюджет, регион, срок, первоначальный взнос.
3. Smart bridge: ассистент показывает полезный расчет -> кнопка «Получить персональные условия».
4. Lead capture (1 экран): имя, телефон, Telegram handle, согласие на обработку данных.
5. CRM handoff + статус воронки в профиле.

### LLM Architecture (Qwen 2.5 / Llama-3.2 ready)
- Orchestrator (server): роутинг запроса -> модель.
- Model gateway:
  - default: open model (Qwen2.5-Instruct / Llama-3.2-Instruct);
  - fallback: managed API при пиковых нагрузках.
- Vector DB (pgvector в PostgreSQL): эмбеддинги источников + офферы.
- Guardrails:
  - prompt policies (без крайних трактовок);
  - citation-first ответы;
  - блок токсичных/небезопасных финансовых советов.
- Observability: лог качества ответов, CTR CTA, conversion to lead.

---

## 3.2 Halal Finance Core (monetization engine)

### A) Закят + ROI по драгметаллам

#### Функции
- Калькулятор закята:
  - активы (кэш, золото, серебро, инвестиции, дебиторка);
  - обязательства;
  - автоматический nisab check;
  - расчет 2.5% при достижении порога.
- ROI калькулятор металлов:
  - цена входа/выхода, спред, комиссии, горизонт, волатильность;
  - сценарии: conservative/base/aggressive;
  - «чистая доходность после издержек».

#### Монетизация
- CTA после результата:
  - «Сформировать халяльный инвестиционный план»;
  - «Подключить консультацию менеджера»;
  - «Открыть подборку продуктов (золото/серебро/платина)».
- Revenue model: CPA/CPL от партнеров, premium-консалтинг, embedded marketplace.

### B) ИЖС-рассрочка агрегатор (условия fixed)

#### Жесткие входные условия (MVP)
- Регион: Татарстан.
- Срок: 8 лет.
- Первоначальный взнос: 40%.

#### UX-флоу высокой конверсии
1. **Pre-check экран (30 сек)**
   - «Стоимость дома», «Доступный ПВ», «Доход семьи».
   - Индикатор вероятности одобрения (low/medium/high).
2. **Scenario builder**
   - Ползунок стоимости проекта + автоподсказка минимального ПВ (40%).
   - Показ ежемесячной нагрузки и общей переплаты в 3 сценариях.
3. **Offer wall (с ранжированием)**
   - Карточки партнеров: monthly payment, требования, скорость сделки.
   - Бейджи: «быстрое одобрение», «минимальный пакет документов».
4. **Trust layer**
   - Объяснение шариатской структуры договора простым языком.
5. **Lead lock-in**
   - «Зафиксировать лучшие условия на 48 часов» (FOMO).
   - Однокнопочный лид: Telegram + телефон (prefill).
6. **Post-lead nurture**
   - Чек-лист «Что подготовить к сделке» + WhatsApp/Telegram менеджер.

#### Конверсионные паттерны
- One-screen math first, документы потом.
- Сравнение «наличный расчет vs рассрочка» с выгодой по срокам/скидкам.
- Social proof (кейсы семей в Татарстане, динамика цен ИЖС).
- Таймер оффера и follow-up в боте.

---

## 3.3 Commercial Gamification (реальная выгода)

### Совместные трекеры привычек
- Привычки: намаз, Коран, утренний зикр, финансовая дисциплина (еженедельный учет).
- Форматы: личный, семейный, группа друзей.

### Reward economy
- 7-day streak: скидка на халяль-тур (например, -3%).
- 30-day streak: апгрейд условий в инвестиционном продукте (снижение комиссии).
- 90-day streak: бонус при сделке по недвижимости (например, бесплатная юрпроверка/скидка на доп.услуги).

### Анти-абьюз
- Награда активируется только при подтвержденных действиях (временные окна + peer verification для групп).
- Лимиты по частоте выдачи купонов.
- Risk-engine на аномальное поведение.

---

## 4) MVP Strategy in Telegram Mini App (virality-first)

### Почему TMA для старта
- Низкий CAC: мгновенный вход через Telegram auth.
- Встроенная виральность: шеринг прогресса/калькуляторов прямо в чатах.
- Быстрые циклы экспериментов (бот + mini app + deep links).

### Feature set для K-factor > 1
1. **Shareable calculators**: «мой план ИЖС», «мой zakat snapshot» (без приватных сумм).
2. **Group streak challenges**: семейные/дружеские челленджи с реальными бонусами.
3. **Invite unlock**: доп.скидка или premium-функция за 3 приглашения.
4. **Referral leaderboard**: ежемесячные призы от партнеров.

### TMA architecture
- Telegram Bot: entry, notifications, lead nurture.
- Mini App (Next.js): основной UX.
- Backend API: auth/session, calculators, offers, AI orchestration.
- CRM connector: передача лидов в amoCRM/Bitrix24/Salesforce.
- Event pipeline: product analytics + attribution.

### Воронка «бот -> mini app -> full app»
1. Bot acquisition (контент, партнерские каналы, лид-магниты).
2. Deep link в Mini App на конкретный сценарий (ИЖС/закят/ассистент).
3. Capture контактов + привычка daily check-in.
4. Trigger перехода в standalone app:
   - push-like напоминания,
   - офлайн-доступ,
   - расширенная персонализация,
   - «лучшие условия только в полном приложении».
5. Seamless migration: login via Telegram + device linking.

---

## 5) UI/UX Information Architecture

### Sitemap (чистое разделение Daily vs Money)
- **Home**
  - Сегодня: намаз, задача дня, 1 релевантный финсовет.
- **Deen**
  - Намаз (время, уведомления)
  - Коран (чтение, прогресс, закладки)
  - Кибла
  - Зикр/дуа
- **Finance**
  - Закят калькулятор
  - ROI металлы
  - ИЖС-рассрочка (Татарстан)
  - Офферы/маркетплейс
- **Assistant**
  - AI чат + быстрые сценарии
- **Community**
  - Трекеры привычек
  - Челленджи
  - Рефералы
- **Profile**
  - Стрики и награды
  - Мои лиды/статусы
  - Настройки и согласия

### UX principle
- Daily религиозное ядро = верх навигации и «спокойный режим».
- Финансы = отдельный контур с language of trust и прозрачной математикой.
- Связка между контурами через contextual cards, а не агрессивные попапы.

### Онбординг (3 минуты, фокус на ценность денег + деена)
1. **Экран 1: Миссия** — «Живите по исламу, управляйте деньгами осознанно».
2. **Экран 2: Daily utility** — намаз/Коран/привычки.
3. **Экран 3: Financial outcomes** — «Проверьте ИЖС за 60 сек, рассчитайте закят и ROI».
4. **Экран 4: Social proof** — кейсы, реальные результаты.
5. **Экран 5: Permission setup** — гео (намаз), уведомления, согласия.
6. **Экран 6: Quick win** — стартовый мини-калькулятор + первый CTA.

---

## 6) Technical Stack & Infra

### Frontend (TMA)
- Next.js (App Router) + React + TypeScript.
- UI: Tailwind + shadcn/ui (быстрый production-ready дизайн).
- Telegram SDK: @telegram-apps/sdk.
- State/data: TanStack Query + Zustand.

### Backend
- Next.js API routes или отдельный Node.js (NestJS/Fastify) при росте нагрузки.
- Auth: Telegram initData validation + JWT session.
- Async jobs: BullMQ + Redis (уведомления, scoring, AI queue).

### Deploy (Beget-friendly + scalable)
- MVP: Dockerized Next.js + Postgres/Supabase.
- Reverse proxy: Nginx.
- Scale path:
  - выделить AI orchestration в отдельный сервис,
  - вынести очереди и воркеры,
  - CDN для статики,
  - read-replica для аналитики.

### Prayer/Quran APIs
- Время намаза:
  - Aladhan API (быстрый старт),
  - fallback: MuslimSalat/локальные таблицы для критичных регионов.
- Коран:
  - Quran.com API / AlQuran Cloud (текст + аудио + переводы).
- Обязательно: локальный кеш расписаний и graceful fallback offline.

---

## 7) Data Model (Supabase/PostgreSQL)

### Core tables
- `users` (id, telegram_id, region, language, created_at)
- `user_profiles` (family_status, income_range, goals_json)
- `daily_habits_logs` (user_id, habit_type, date, status, proof_type)
- `streaks` (user_id, current_streak, max_streak, last_checkin)
- `rewards_wallet` (user_id, reward_type, value, expires_at, redeemed_at)
- `zakat_calculations` (user_id, payload_json, nisab_met, result_amount)
- `metal_roi_calculations` (user_id, metal_type, input_json, roi_result)
- `ijc_requests` (user_id, region, house_budget, down_payment, income, score, status)
- `partner_offers` (offer_id, partner_id, product_type, terms_json, active)
- `leads` (user_id, source_module, payload_json, crm_status, assigned_to)
- `ai_chats` (chat_id, user_id, mode, created_at)
- `ai_messages` (chat_id, role, content, citations_json, intent_label)
- `events` (user_id, event_name, props_json, ts)

### Minimal indices
- `users(telegram_id)` unique.
- `daily_habits_logs(user_id, date)`.
- `leads(source_module, crm_status, created_at)`.
- `ijc_requests(region, status, created_at)`.
- `events(event_name, ts)`.

### Privacy & compliance
- Явные consent-флаги для персональных данных и маркетинга.
- Шифрование чувствительных полей (телефон).
- Data retention policy + user data deletion flow.

---

## 8) Product Analytics & Growth

### Event taxonomy (must-have)
- `onboarding_completed`
- `assistant_cta_clicked`
- `zakat_calc_completed`
- `roi_calc_completed`
- `ijc_precheck_completed`
- `ijc_offer_viewed`
- `lead_submitted`
- `referral_sent`
- `referral_converted`
- `streak_7/30/90_unlocked`

### KPI tree
- Acquisition: CAC, invite rate, K-factor.
- Activation: TTFV (time-to-first-value) < 5 min.
- Monetization: lead conversion rate per module, ARPU by partner vertical.
- Retention: D1/D7/D30, streak adherence, WAU/MAU.

### Эксперименты (первые 90 дней)
- A/B pre-check wording для ИЖС (религиозный trust vs финансовая выгода).
- A/B lead-form (1-step vs 2-step).
- Incentive tests (скидка тур vs бонус недвижимости).
- AI CTA placement (inline vs end-of-chat card).

---

## 9) Roadmap (phased)

### Phase 0 (0–6 недель): MVP TMA
- Намаз/Коран базово.
- Закят + ROI калькуляторы.
- ИЖС pre-check + lead form.
- Базовый AI ассистент (RAG lite).
- Telegram реферальная механика.

### Phase 1 (2–4 мес.)
- Offer wall с партнерским API.
- Групповые трекеры + rewards wallet.
- CRM automation и сквозная аналитика.

### Phase 2 (4–8 мес.)
- Standalone app (RN).
- Advanced personalization (next-best-offer engine).
- FinScore и динамическая сегментация.

---

## 10) Risks & Mitigations

- **Риск шариатской некорректности** -> advisory board + citation mode + юридические дисклеймеры.
- **Низкое доверие к финансовым офферам** -> прозрачные формулы, партнерская верификация, кейсы.
- **Слабая конверсия лидов** -> сокращение формы, callback <5 минут, SLA для менеджеров.
- **Сложность UI** -> жесткое разделение Deen vs Finance, progressive disclosure.

---

## 11) Definition of Success (MVP exit criteria)
- >= 5 000 MAU в Telegram Mini App.
- >= 7% MAU оставляют хотя бы 1 лид.
- >= 25% D30 у сегмента с трекерами.
- >= 1.1 K-factor у реферальной петли.
- >= 30% AI-сессий завершаются полезным CTA-кликом.
