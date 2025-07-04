# Texnik topshiriq 

- Versiya 1.0 — 4 iyul 2025 (Asia/Tashkent)


## 1. Loyiha nomi

**HeadHunter Vacancy Collector** — hh.uz (HeadHunter) saytidagi vakantliklarni real vaqt rejimida yig‘ish, tozalash va ma’lumotlar bazasiga joylashtirish uchun ETL tizimi.

## 2. Maqsad

- **Asosiy maqsad:** vakantlik ma’lumotlarini toza, dublikatsiyasiz va normalizatsiya qilingan shaklda saqlash.
- **Qo‘shimcha:** kelgusida vizualizatsiya (Power BI) jarayonini yengillashtirish uchun standart dataset tayyorlash.

## 3. Tavsiya etiladigan rxitektura

```
┌──────────┐       ┌────────────┐
│   API    │       │  Scraper   │
└──────────┘       └────────────┘
      │               │
      └──────┬────────┘
             ▼
     ┌────────────────┐
     │ VacancyLoader  │
     └────────────────┘
             │
             ▼
     ┌────────────────┐
     │   DB (RDBMS)   │
     └────────────────┘
```

**Nega API + Scraping?** API tezkor, biroq har doim barcha elonlarni bermaydi HTML sahifani parslab, API’dan kelmagan elonlar olinadi, shu orqaliy to‘liq qamrovga erishiladi.

## 4. Texnik cheklovlar

| Talab              | Izoh                                                                                               |
| ------------------ | -------------------------------------------------------------------------------------------------- |
| Dasturlash tili    | Python (versiya erkin tanlanadi)                                                            |
| Kutubxonalar       | `aiohttp` / `requests`, `beautifulsoup4` / `selenium`|
| Ma’lumotlar bazasi | MySQL **yoki** PostgreSQL (MySQL tavsiya)                                                          |
| Docker             | **Talab qilinmaydi**                                                                                  |
| Testlar            | **Talab qilinmaydi**                                                                               |

## 5. Ma’lumotlar talablari

### 5.1. Majburiy ustunlar (kamida)

| Ustun nomi   | Nima saqlanadi?                                                         |
|--------------|-------------------------------------------------------------------------|
| **category** | Ish e'lonining umumiy yo‘nalishi yoki sohasi (masalan, Marketing, Data Science)   |
| **position** | Kompaniya ichidagi lavozim (Data Analyst, Backend Engineer va h.k.)     |
| **title**    | E'lon sahifasida ko‘rinadigan to‘liq sarlavha                            |
| **h_id**     | HeadHunter platformasidagi unikal e'lon identifikatori                  |
| **publish_date** | E'lon HH’da birinchi marta chop etilgan sana (YYYY-MM-DD)          |
| **company**  | Ish beruvchi nomi (kompaniya yoki brend)                                |
| **skills**   | Talab qilinadigan ko‘nikmalar ro‘yxati                                 |
| **country**  | Ish joyi joylashgan mamlakat                                            |
| **location** | Mamlakat ichidagi shahar yoki hudud                                     |
| **min_salary** | Ko‘rsatilgan minimal oylik (mahalliy valyutada)                      |
| **max_salary** | Ko‘rsatilgan maksimal oylik (mahalliy valyutada)                     |

- Sana `YYYY-MM-DD` formatida.
- `skills` — alohida jadavalda saqlanadi.

### 5.2. Normalizatsiya

Ma’lumotlar jadvallarga bo‘lingan holatda saqlanishi kerag, Misol:

- `vacancies`  — asosiy jadval (FK: `company_id`, `location_id` …)
- `companies`  — kompaniya ma’lumotlari
- `locations`  — mamlakat/shahar
- `skills` va `vacancy_skill` — M\:N bog‘lanish.
- Bu misol uchun kursatildi, ma'lumotlar strukturasi uzingiz tomoningizdan tuziladi.

## 6. Dublikatlarni oldini olish

- **Asosiy kalit:** `h_id` (HH tizimidagi unikal identifikator).
- Ushbu kalit buyicha dublikatlik tekshirilishi va dublikat ma’lumotlar saqlanishing oldi olinishi kerag.

## 7. Konfiguratsiya

`.env` namunasi:

```
DB_HOST=127.0.0.1
DB_PORT=3306
DB_USER=hh_user
DB_PASSWORD=strongPass
DB_NAME=headhunter
HH_API_BASE=https://api.hh.ru
```


## 8. Baholash mezonlari

| Vazn     | Kriteriy                                                |
| -------- | ------------------------------------------------------- |
| **50 %** | Saqlangan ma’lumot sifatining tozaligi va optimalligi   |
| **30 %** | Yigʻish va yozish jarayonining tezligi                  |
| **20 %** | Hujjatlar (README, diagramma) va kodni o‘qish qulayligi |

## 9. README.md’da nimalar bo‘lishi shart

1. Loyiha tavsifi.
2. Arxitektura sxemasi.
3. Ishga tushirish bo‘yicha ko‘rsatma (virtual env, `pip install -r requirements.txt`).
4. `.env` namunasi.
5. Lisenzya.

## 10. Manbalar

| Nomi                  | URL                                                                                                              |
| --------------------- | ---------------------------------------------------------------------------------------------------------------- |
| HeadHunter API docs   | [https://dev.hh.ru/](https://dev.hh.ru/)                                                                         |
| BeautifulSoup4 docs   | [https://www.crummy.com/software/BeautifulSoup/bs4/doc/](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) |
| Selenium docs         | [https://www.selenium.dev/documentation/](https://www.selenium.dev/documentation/)                               |
| aiohttp docs          | [https://docs.aiohttp.org/en/stable/](https://docs.aiohttp.org/en/stable/)                                       |
| requests docs         | [https://requests.readthedocs.io/](https://requests.readthedocs.io/)                                             |
| Eraser (diagram tool) | [https://www.eraser.io](https://www.eraser.io)                                                                   |

---

**Deadline:** Imtihon kuni.

