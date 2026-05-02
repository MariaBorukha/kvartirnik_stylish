# Architecture — Квартирник у Маши Боруха

## Обзор

Статический многостраничный сайт без фреймворка и сборщика. Каждая страница — отдельный HTML-файл с общим CSS. Хостится на **GitHub Pages** (ветка `main`, корень репозитория).

Живой адрес: https://mariaborukha.github.io/kvartirnik_stylish/

---

## Структура файлов

```
/
├── index.html          # Главная: tagline, фото, история, как прийти
├── events.html         # Следующий квартирник (TBD май 2026)
├── archive.html        # Прошедшие квартирники (список с датами)
├── team.html           # Команда: звук, house band, гости, доноры, орг
├── rules.html          # Правила поведения в офисе
├── finance.html        # Отчёт о расходах и доходах
├── playlist.html       # Плейлист и инструкция, как предложить песню
├── registration.html   # Регистрация (заглушка, ссылка появится позже)
├── directions.html     # Как пройти в БЦ Лотте (заглушка TBD)
├── vacancies.html      # Вакансии квартирника
├── 404.html            # Страница ошибки (используется GitHub Pages)
├── styles.css          # Единственный таблица стилей для всех страниц
├── img/                # Фотографии с квартирников
│   ├── p1.jpg … p5.jpg
│   ├── p6.png, p7.png
└── README.md
```

---

## Дизайн-система (`styles.css`)

**Шрифты** (Google Fonts, все поддерживают кириллицу):
- `Fraunces` — variable serif, display-заголовки (оси: `opsz`, `SOFT`, `wght`)
- `Spectral` — тело текста, подзаголовки
- `JetBrains Mono` — метки, кикеры, навигация, числа

**Палитра:**
| Переменная       | Значение   | Применение                        |
|------------------|------------|-----------------------------------|
| `--bg`           | `#fbfbf9`  | Фон страниц                       |
| `--bg-2`         | `#f3f3ef`  | Подложки карточек, stub билетов   |
| `--ink`          | `#111111`  | Основной текст, кнопки, рамки     |
| `--ink-soft`     | `#555555`  | Второстепенный текст              |
| `--ink-mute`     | `#8a8a85`  | Кикеры, метки, номера             |
| `--rule`         | rgba ink 12% | Разделители                    |

**Ключевые компоненты:**
- `.site-header` — sticky, backdrop-blur, монохромная навигация
- `.ticket` — двухколоночная карточка-билет (события, регистрация)
- `.archive` — grid-список прошедших событий с hover-эффектом
- `.team-list` — auto-fill grid для списков команды
- `.finance-card` — карточки расходов с лейблом, суммой, описанием
- `.song-list` — двухколоночный список песен
- `.rules` — две колонки «Можно / Нельзя»
- `.btn` / `.btn--ghost` — кнопки с тенью при hover
- `.rise` + `.d1–.d4` — CSS-анимация появления (staggered)

---

## Контент

Тексты перенесены из **Notion-экспорта** (`Flatnik_context/`).  
Исключение: страница «Финансы» — данные извлечены из таблиц экспорта и оформлены как карточки.

Исходный Notion-экспорт хранится в `~/Documents/Flatnik_context/`.

---

## Локальные секреты (`.env`)

Файл `.env` лежит в корне папки и содержит переменные окружения для работы с GitHub.  
Он добавлен в `.gitignore` — на GitHub **не попадает**.

```
GITHUB_TOKEN=<personal access token>   # токен для git push через HTTPS
GITHUB_REPO=https://github.com/MariaBorukha/kvartirnik_stylish
GITHUB_PAGES=https://mariaborukha.github.io/kvartirnik_stylish/
```

**Как использовать токен при пуше вручную:**
```bash
source .env
git remote set-url origin https://x-access-token:$GITHUB_TOKEN@github.com/MariaBorukha/kvartirnik_stylish.git
git push
```

**Ротация токена:** если токен скомпрометирован или истёк —
1. Отозвать старый: [github.com/settings/tokens](https://github.com/settings/tokens) → Revoke
2. Создать новый с правами `repo`
3. Заменить значение `GITHUB_TOKEN=` в `.env`

---

## Деплой

Сайт публикуется автоматически через **GitHub Pages** при любом пуше в ветку `main`.

Чтобы обновить сайт:
```bash
cd ~/Documents/Flatnik_context/Flatnik_GitHub_Stylish
# редактируем нужные .html или styles.css
git add .
git commit -m "описание изменений"
git push
```

Через 1–3 минуты изменения появятся на живом сайте.

---

## Репозиторий

GitHub: https://github.com/MariaBorukha/kvartirnik_stylish  
Видимость: **public** (GitHub Pages на free-плане работает только с public-репо)
