# Портфоліо: як опублікувати і підключити CMS

Сайт на Hugo + Decap CMS. Публікується на GitHub Pages автоматично після кожної зміни в гілці `main`.

## 1. Завантажити сайт на GitHub

1. Створіть **публічний** репозиторій з назвою точно `NazarShubeliak.github.io` (без README, порожній).
2. У папці проєкту виконайте:

   ```bash
   git init
   git add .
   git commit -m "Portfolio site"
   git branch -M main
   git remote add origin https://github.com/NazarShubeliak/NazarShubeliak.github.io.git
   git push -u origin main
   ```

3. У репозиторії: **Settings → Pages → Build and deployment → Source: GitHub Actions**.
4. Відкрийте вкладку **Actions**: за 1–2 хвилини збірка завершиться, і сайт відкриється на `https://nazarshubeliak.github.io`.

## 2. Створити OAuth-посередника на Cloudflare (для входу в CMS онлайн)

GitHub Pages не вміє авторизувати вхід у Decap, тому потрібен маленький безкоштовний сервіс на Cloudflare Workers.

1. Зареєструйтеся на [cloudflare.com](https://dash.cloudflare.com/sign-up) (безкоштовно).
2. Відкрийте [github.com/sveltia/sveltia-cms-auth](https://github.com/sveltia/sveltia-cms-auth) і натисніть кнопку **Deploy to Cloudflare Workers**. Він сумісний з Decap CMS.
3. Після деплою скопіюйте адресу worker'а, вона має вигляд `https://sveltia-cms-auth.<ваш-піддомен>.workers.dev`.

## 3. Створити GitHub OAuth App

1. Відкрийте [github.com/settings/applications/new](https://github.com/settings/applications/new).
2. Заповніть:
   - **Application name:** `Portfolio CMS`
   - **Homepage URL:** `https://nazarshubeliak.github.io`
   - **Authorization callback URL:** `https://sveltia-cms-auth.<ваш-піддомен>.workers.dev/callback`
3. Натисніть **Register application**, потім **Generate a new client secret**. Збережіть **Client ID** і **Client Secret**.

## 4. Передати ключі worker'у

У Cloudflare: **Workers & Pages → sveltia-cms-auth → Settings → Variables and Secrets**. Додайте:

| Назва | Значення |
| --- | --- |
| `GITHUB_CLIENT_ID` | Client ID з кроку 3 |
| `GITHUB_CLIENT_SECRET` | Client Secret з кроку 3 (тип **Secret**) |
| `ALLOWED_DOMAINS` | `nazarshubeliak.github.io` |

Збережіть і задеплойте ще раз (Deploy).

## 5. Вписати адресу worker'а в CMS

У файлі `static/admin/config.yml` замініть рядок:

```yaml
base_url: https://sveltia-cms-auth.YOUR-SUBDOMAIN.workers.dev
```

на вашу адресу з кроку 2. Закомітьте і запуште зміну.

## 6. Готово

Відкрийте `https://nazarshubeliak.github.io/admin/`, натисніть **Login with GitHub**. Кожне збереження в CMS створює коміт у репозиторії, а GitHub Actions за 1–2 хвилини оновлює сайт.

---

## Як працювати з CMS

- **Projects** — проєкти. Ліворуч англійська, праворуч українська. Тексти пишуться для кожної мови окремо; тип, порядок, обкладинка, відео й посилання копіюються в обидві мови автоматично. **Стек** і **Скріншоти** заповнюються лише в англійській частині, українська сторінка бере їх звідти.
- **Відео:** довгі ролики завантажуйте на YouTube з доступом «За посиланням» (Unlisted) і вставляйте посилання в поле *YouTube link*. Файл MP4 — лише для коротких кліпів, до ~20 MB.
- **Обкладинка** — горизонтальна картинка від 1600 px завширшки. Поки її немає, картка показує стек проєкту.
- **Порядок у каталозі** — число в полі *Order*: 1 — перший.
- **Pages** — тексти головної сторінки, окремо англійською й українською.
- **Settings → Contacts** — email, Telegram, посилання на Upwork і Freelancehunt. Порожні поля на сайті не показуються.

## Локальна робота (необов'язково)

```bash
hugo server            # сайт на http://localhost:1313
npx decap-server       # в іншому терміналі: CMS на http://localhost:1313/admin/ без входу
```
