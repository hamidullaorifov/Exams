# Amaliy imtihon: Ma'lumotlar bazasi va EF Core

**Davomiyligi:** 90 daqiqa
**Umumiy ball:** 100

**Umumiy shartlar:** Barcha topshiriqlar bitta mavzu (onlayn kutubxona tizimi) atrofida qurilgan. PostgreSQL va C# (.NET, EF Core) dan foydalaning. Natijalar (SQL skriptlari va loyiha fayllari) topshirilishi shart.

---

## 1-topshiriq: Relyatsion baza va SQL (35 ball)

Kutubxona tizimi uchun PostgreSQL da `LibraryDb` nomli ma'lumotlar bazasini yarating.

### A) Jadvallarni yaratish (10 ball)

Quyidagi jadvallarni mos ma'lumot turlari va cheklovlar (constraints) bilan yarating:

- **authors**: `id` (PRIMARY KEY, avtomatik oshuvchi), `full_name` (bo'sh bo'lmasligi shart), `birth_year`
- **books**: `id` (PRIMARY KEY), `title` (bo'sh bo'lmasligi shart), `author_id` (FOREIGN KEY, authors jadvaliga), `price` (0 dan katta bo'lishi shart, CHECK), `published_year`, `isbn` (takrorlanmas, UNIQUE)

### B) Ma'lumot kiritish va o'zgartirish (10 ball)

1. `authors` jadvaliga kamida 3 ta muallif, `books` jadvaliga kamida 6 ta kitob qo'shing (INSERT).
2. Narxi 50 000 so'mdan past bo'lgan barcha kitoblar narxini 10% ga oshiring (UPDATE).
3. Nashr yili 1990 dan oldingi kitoblardan birini o'chiring (DELETE).

### C) So'rovlar (15 ball)

Quyidagi so'rovlarni yozing:

1. Barcha kitoblarning nomi va muallifining to'liq ismini chiqaring (INNER JOIN).
2. Barcha mualliflarni, hatto kitobi yo'qlarini ham, ularning kitoblari bilan chiqaring (LEFT JOIN).
3. Har bir muallifning kitoblari sonini va o'rtacha narxini toping (`COUNT`, `AVG`, `GROUP BY`). Faqat 2 tadan ortiq kitobi bor mualliflar chiqsin (`HAVING`).
4. `books` jadvalidagi `title` ustuniga indeks yarating va `EXPLAIN ANALYZE` yordamida nom bo'yicha qidiruv so'rovining bajarilish rejasini ko'rsating. Indeks nima uchun kerakligini 1-2 gapda izohlang.

---

## 2-topshiriq: Normalizatsiya (25 ball)

Quyida kutubxonaning normallashtirilmagan jadvali berilgan:

| order_id | member_name | member_phone | book_titles | book_authors | order_date |
|----------|-------------|--------------|-------------|--------------|------------|
| 1 | Aziz Karimov | 901234567 | Otkan kunlar, Mehrobdan chayon | Abdulla Qodiriy, Abdulla Qodiriy | 2026-09-01 |
| 2 | Dilnoza Aliyeva | 935556677 | Sariq devni minib | Xudoyberdi Toxtaboyev | 2026-09-03 |
| 3 | Aziz Karimov | 901234567 | Sariq devni minib | Xudoyberdi Toxtaboyev | 2026-09-05 |

**Vazifalar:**

1. **(5 ball)** Jadval nima uchun 1NF ni buzayotganini tushuntiring.
2. **(5 ball)** Jadvaldagi takrorlanish (redundancy) va anomaliyalarni (yangilash, o'chirish, qo'shish) misollar bilan ko'rsating.
3. **(10 ball)** Jadvalni 3NF gacha normallashtiring: yangi jadvallar tuzilmasini (ustunlar, PRIMARY KEY va FOREIGN KEY lar bilan) yozing va har bir bosqichda (1NF, 2NF, 3NF) nima o'zgarganini qisqacha izohlang.
4. **(5 ball)** Normallashtirilgan jadvallar uchun ERD (Entity-Relationship Diagram) chizing yoki matn ko'rinishida munosabatlarni (one-to-many, many-to-many) ko'rsating.

---

## 3-topshiriq: EF Core (40 ball)

Yangi .NET Console yoki Web API loyihasi yarating va EF Core (Npgsql provayderi bilan) dan foydalaning.

### A) Modellar va DbContext (10 ball)

Quyidagi entity klasslarini yarating:

- **Author**: `Id`, `FullName`, `BirthYear`, `Books` (navigatsion xossa)
- **Book**: `Id`, `Title`, `Price`, `PublishedYear`, `AuthorId`, `Author`, `Categories`
- **Category**: `Id`, `Name`, `Books`
- **Member**: `Id`, `FullName`, `Phone`, `Loans`
- **Loan**: `Id`, `MemberId`, `BookId`, `LoanDate`, `ReturnDate` (nullable)

`LibraryContext : DbContext` klassini yarating, `DbSet` larni e'lon qiling va ulanish satrini (connection string) sozlang.

### B) Munosabatlar (10 ball)

Fluent API yoki Data Annotations yordamida quyidagilarni sozlang:

1. **One-to-many**: bitta `Author` ko'p `Book` ga ega bo'lishi.
2. **Many-to-many**: `Book` va `Category` o'rtasida (EF Core 5+ ning avtomatik bog'lovchi jadvali yordamida).
3. `Book.Title` uchun maksimal uzunlik (200) va majburiylik (`IsRequired`), `Book.Price` uchun aniqlik (`HasPrecision(10, 2)`).

### C) Migratsiyalar (10 ball)

1. `InitialCreate` nomli migratsiya yarating.
2. Migratsiyani bazaga qo'llang (`dotnet ef database update`).
3. Keyin `Book` ga `Isbn` (string, unique indeks) maydonini qo'shing va `AddIsbnToBook` nomli ikkinchi migratsiya yarating va qo'llang.
4. Ishlatilgan barcha `dotnet ef` buyruqlarini hisobotda ko'rsating.

### D) Seeding (10 ball)

`OnModelCreating` ichida `HasData` yordamida boshlang'ich ma'lumotlarni kiriting:

- Kamida 3 ta muallif
- Kamida 4 ta kategoriya
- Kamida 6 ta kitob (har xil mualliflarga biriktirilgan)

Migratsiya yarating, qo'llang va ma'lumotlar bazada paydo bo'lganini SQL so'rovi (`SELECT`) yoki EF Core so'rovi bilan tasdiqlang.

---

## Baholash mezonlari

| Mezon | Ball |
|-------|------|
| 1-topshiriq: SQL | 35 |
| 2-topshiriq: Normalizatsiya | 25 |
| 3-topshiriq: EF Core | 40 |
| **Jami** | **100** |

**Baholash shkalasi:**

- 86-100: A'lo (5)
- 71-85: Yaxshi (4)
- 56-70: Qoniqarli (3)
- 0-55: Qoniqarsiz (2)

**Topshirish:** SQL skriptlar (`.sql`), normalizatsiya javobi (`.md` yoki `.docx`), EF Core loyihasi (Migrations papkasi bilan) arxivlangan holda yuboriladi.
