# 1-oy Yakuniy Imtihoni: C# Asoslari va OOP Negizlari



---

## 1-topshiriq: 
Quyidagi konsol dasturini yozing:

1. Foydalanuvchidan **3 ta talaba**ning ismini va bittadan test balini (double) kiritishni so'rang. (Talabalar soni belgilangan — "nechta talaba" deb so'rash shart emas.)
2. Ma'lumotlarni `Dictionary<string, double>` (ism → ball) ko'rinishida saqlang.
3. Sikl (loop) yordamida har bir talabaning balini va harfli bahosini if-else yoki switch-case orqali chop eting:
   - 90+ → A, 80–89 → B, 70–79 → C, 60–69 → D, 60 dan past → F
4. Ball kiritishni bitta `try-catch` bilan o'rab qo'ying — son bo'lmagan qiymat kiritilsa, dastur qulamasdan xato xabari chiqsin (qayta so'rash shart emas — bitta xabar yetarli).


---

## 2-topshiriq: Kutubxona Katalogi
1. `Book` klassini yarating:
   - `Title`, `Author`, `IsCheckedOut` (bool) uchun auto-property'lar
   - `Title` va `Author`ni talab qiluvchi konstruktor (`IsCheckedOut` boshlang'ich qiymati — false)
   - `CheckOut()` metodi — `IsCheckedOut = true` qilib qo'yadi va xabar chiqaradi; agar kitob allaqachon olingan bo'lsa, **exception (xato) throw qilsin** aniq xabar bilan.
2. `Main` metodida:
   - 3–4 ta kitobdan iborat `List<Book>` yarating.
   - Bitta kitobni Checkout qiling.
   - Xuddi shu kitobni yana olishga urinib ko'ring, buni `try-catch` ichida qilib, exception qanday ushlanishini (catch) ko'rsating.
   - Ro'yxat bo'ylab sikl yuritib, har bir kitobning nomi va holatini (checked-out yoki yo'q) chop eting.

**Qamrab oladi:** klasslar/obyektlar, property'lar, konstruktorlar, metodlar, xatolarni boshqarish.

---

## 3-topshiriq: Shakllar Ierarxiyasi 
1. `Shape` degan **abstract klass** yarating, unda `CalculateArea()` degan abstract metod bo'lsin (double qaytaradi).
2. `Shape`dan meros oluvchi **ikkita klass** yarating (masalan, `Circle` va `Rectangle`), ular `CalculateArea()` metodini o'ziga mos formula bilan override qilsin.
3. `IDescribable` degan **interface** yarating, unda `Describe()` metodi bo'lsin. Buni ikkala shakl klassida ham amalga oshiring — shaklning nomi va yuzasini chop etsin.
4. `Main`da har bir shakldan bittadan bo'lgan `List<Shape>` yarating, sikl orqali har birida `Describe()`ni chaqiring — bu polimorfizmni namoyish etadi.

**Qamrab oladi:** abstract klasslar, meros olish (inheritance), metodlarni override qilish, interfeyslar, polimorfizm.

---

## 4-topshiriq: LINQ yordamida Ombor Hisoboti 
1. `Product` klassini yarating (`Name`, `Category`, `Price`, `Quantity`).
2. `Repository<T>` degan generic klass yarating — ichida `List<T>`, `Add(T item)` metodi va ro'yxatni qaytaruvchi `GetAll()` metodi bo'lsin.
3. Qayerdadir bitta **static metod** qo'shing (masalan, `PriceHelper` degan static klass ichida `ApplyDiscount(double price, double percent)` metodi) — bu shunchaki static ishlatilishini ko'rsatish uchun, boshqa qismlarga ulanishi shart emas.
4. `Repository<Product>`ni kamida 2 ta kategoriyadan iborat 5–6 ta mahsulot bilan to'ldiring.
5. **LINQ** yordamida konsolga chop eting:
   - `Quantity < 5` bo'lgan barcha mahsulotlarni, `Quantity` bo'yicha o'sish tartibida saralab.
   - O'rtacha narxdan qimmat bo'lgan mahsulotlarning nomlarini, bitta zanjirlangan (chained) LINQ ifodasi orqali (masalan, `.Where(...).Select(...)`).

**Qamrab oladi:** static a'zolar, generiklar (generics), LINQ asoslari va zanjirlash (chaining).

---

## Baholash Mezoni (tavsiya etiladi, 100 ballik)

| Mezon | Ball |
|---|---|
| 1-topshiriq – Baholar Kitobi | 20 |
| 2-topshiriq – Kutubxona Katalogi | 25 |
| 3-topshiriq – Shakllar Ierarxiyasi | 25 |
| 4-topshiriq – Ombor/LINQ | 30 |

