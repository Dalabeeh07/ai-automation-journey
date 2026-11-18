# C++ (Malik) — Ch1–Ch4: ملخص + أسئلة تدريب مع حلول

> كل نواتج الكود تحت اتأكدت بتشغيلها (g++ -std=c++17). غطّي الأجوبة وحاول بنفسك قبل ما تقرأها.

---

## 0) أشياء بتنسأل كثير (اقرأها آخر شي)

| الفخ | الصح |
|---|---|
| `7/2` | `3` (قسمة صحيحة) — `7/2.0` = `3.5` |
| `-7/2` , `-7%2` | `-3` , `-1` |
| `y = ++x` / `y = x++` | الأولى: x و y الاثنين الجديد. التانية: y القديم، x يزيد |
| `0 <= num <= 10` | دايماً `true` (لأن `0<=num` بطلع 0 أو 1، وهذا `<= 10`) — الصح: `0 <= num && num <= 10` |
| `if (x = 5)` | مش syntax error، هو logical error: بعيّن x=5 والشرط دايماً true |
| `else` | بنربط مع أقرب `if` ما إله else (حتى لو الـ indentation يوحي غير هيك) |
| `switch` بدون `break` | بكمل ينفذ الـ cases اللي بعده (fall-through) |
| `setprecision(n)` بدون `fixed` | n = عدد الأرقام المعنوية (significant)، مش عدد الخانات بعد الفاصلة |
| `&&` و `||` | short-circuit: بوقف التقييم أول ما تتحدد النتيجة |
| `cin >> int` وإدخال حرف | input failure — الـ stream بصير fail state والإدخالات اللي بعده تنتجاهل |
| `cin >> char` | بتخطى الـ whitespace. `cin.get(ch)` ما بتخطاه |

---

## 1) Chapter 1 — أسئلة مفاهيمية

1. رتّب خطوات معالجة برنامج C++.
   **editor (source .cpp) → preprocessor (`#...`) → compiler (object code) → linker → loader (يحمّله بالـ main memory) → execute.**
2. شو الفرق بين RAM والـ secondary storage؟
   **RAM:** متصل مباشرة بالـ CPU، لازم البرنامج والبيانات يتحملوا فيه قبل التنفيذ، وبنمسح لما ينقطع الكهرباء (volatile). **Secondary:** تخزين دائم (hard disk, flash, CD...).
3. الـ CPU شو بعمل؟ **عمليات حسابية ومنطقية؛ "دماغ" الكمبيوتر؛ أغلى قطعة hardware.**
4. bit و byte؟ **bit = 0 أو 1. byte = 8 bits.**
5. ASCII مقابل Unicode؟ **ASCII = 128 حرف (EBCDIC = 256، من IBM). Unicode = 65536 حرف، حرفين (2 bytes) للحرف الواحد.**
6. الفرق بين assembler و compiler؟ **assembler يترجم assembly → machine. compiler يترجم high-level → machine.**
7. شو الـ algorithm؟ **خطوات متسلسلة لحل مشكلة، تنتهي بوقت محدود (finite).**
8. خطوات الـ Problem Analysis–Coding–Execution cycle؟ **(1) حلل المشكلة وصمم الخوارزمية (2) نفّذ الخوارزمية بكود وتحقق منها (3) maintenance.**
9. الـ compiler بضمن إيش؟ **إن البرنامج بتبع قواعد اللغة (syntax) — مش إنه بعطي النتيجة الصحيحة.**
10. structured vs object-oriented؟ **Structured: تقسيم المشكلة لمشاكل أصغر (top-down / stepwise refinement / modular). OOD: البرنامج مجموعة objects، كل object = data + operations عليها.**
11. مين صمم C++ ومتى؟ **Bjarne Stroustrup، Bell Labs، أوائل الثمانينات؛ تطورت من C. ANSI/ISO standard انقر بـ 1998.**
12. System software مقابل application software؟ **System: يتحكم بالجهاز (مثل OS). Application: مهمة محددة (word processor, spreadsheet, games).**

---

## 2) Chapters 2–4 — شو ناتج هذا الكود؟

(كل سؤال: توقّع الناتج، بعدين شوف الجواب.)

```cpp
// Q1
int x = 5; int y = ++x; cout << x << " " << y;
// Q2
int x = 5; int y = x++; cout << x << " " << y;
// Q3
cout << 7/2 << " " << 7%2 << " " << 7/2.0 << " " << -7/2 << " " << -7%2;
// Q4
cout << (3 * 7 - 6 + 2 * 5 / 4 + 6);
// Q5
cout << static_cast<int>(7.9) + static_cast<double>(5)/2;
// Q6
cout << 6/4 + 3.9 << " " << 5.4*2 - 13.6 + 18/2;
// Q7
int num = 15; if (0 <= num <= 10) cout << "true"; else cout << "false";
// Q8
int x = 3; if (x = 5) cout << "in, x=" << x;
// Q9
int y = 0, x = 5;
if ((x == 5) || (++y)) cout << "y=" << y;
// Q10
int a = 5, b = 3;
if (a > 3) if (b > 5) cout << "A"; else cout << "B";
cout << "end";
// Q11
int x = 2;
switch (x) { case 1: cout << "one "; case 2: cout << "two "; case 3: cout << "three "; break; default: cout << "def "; }
// Q12   (string a="Hello", b="Hi", c="Air", d="Bill", e="Big")
cout << (a<b) << (c<d) << (e<d) << (a<a) << (string("Hi") < string("Hi!"));
// Q13
cout << ('R'>'T') << (' '<'a') << ('6'<='>') << ('a'>'A');
// Q14
char ch = 'A'; cout << ch+1 << " " << (char)(ch+1) << " " << (int)'0';
// Q15  (include <iomanip>)
cout << "[" << setw(5) << 42 << "]" << "[" << setfill('#') << setw(6) << 42 << "]";
// Q16
cout << fixed << setprecision(2) << 3.14159 << " " << 2.5 << " " << 10.0;
// Q17  (بدون fixed!)
cout << setprecision(3) << 3.14159 << " " << 2.5 << " " << showpoint << 2.5;
// Q18
int x = 10; x *= 2+3; int y = 7; y %= 4; int z = 20; z /= 3; cout << x << " " << y << " " << z;
// Q19
int a = 4, b = 9; int m = (a > b) ? a : b; cout << m;
// Q20
cout << 2+3*5 << " " << (2+3)*5 << " " << 10-4-3 << " " << 20/4/2;
// Q21
double d = 5/2; double e = 5/2.0; int f = 5/2.0; cout << d << " " << e << " " << f;
// Q22
int a = 3; cout << (a>1 && a<5) << (!(a==3)) << (a==3 || a==4) << (!a);
// Q23
string s = "William Jacob"; cout << s.length() << " " << s[0] << " " << s[8];
// Q24
bool t = true, f = false; cout << t << f << (t+t);
// Q25
cout << "Hello\\n" << "A\nB\tC";
```

### الأجوبة

| Q | الناتج | ليش |
|---|---|---|
| 1 | `6 6` | pre-increment: يزيد أول، بعدين يعيّن |
| 2 | `6 5` | post-increment: يعيّن القديم، بعدين يزيد |
| 3 | `3 1 3.5 -3 -1` | قسمة صحيحة تقتطع الجزء العشري |
| 4 | `23` | `((3*7)-6) + ((2*5)/4) + 6` = 15 + 2 + 6 (10/4 = 2) |
| 5 | `9.5` | 7 + 2.5 |
| 6 | `4.9 6.2` | `6/4`=1 فـ 1+3.9؛ والتانية 10.8−13.6+9 |
| 7 | `true` | الفخ تبع `0<=num<=10` |
| 8 | `in, x=5` | `=` مش `==` |
| 9 | `y=0` | `x==5` true فالـ `++y` ما بنفذ (short-circuit) |
| 10 | `Bend` | `else` مع `if (b>5)` الداخلي؛ b>5 false فبطبع B |
| 11 | `two three ` | ما في break بعد case 2 |
| 12 | `11101` | "Hello"<"Hi" (e<i)، "Air"<"Bill"، "Big"<"Bill" (g<l)، a<a=0، الأقصر أصغر |
| 13 | `0111` | ASCII: R=82 < T=84، space=32 < a=97، '6'=54 <= '>'=62، a=97 > A=65 |
| 14 | `66 B 48` | `ch+1` بتصير int |
| 15 | `[   42][####42]` | setw يعبي بالـ fill؛ setfill يضل مفعّل |
| 16 | `3.14 2.50 10.00` | fixed + 2 خانات عشرية |
| 17 | `3.14 2.5 2.50` | بدون fixed: 3 أرقام معنوية؛ showpoint يعرض الأصفار |
| 18 | `50 3 6` | `x *= (2+3)` = 50؛ 7%4=3؛ 20/3=6 |
| 19 | `9` | ternary |
| 20 | `17 25 3 2` | left-to-right: (10−4)−3؛ (20/4)/2 |
| 21 | `2 2.5 2` | `5/2` قسمة صحيحة قبل التحويل لـ double |
| 22 | `1010` | true, false, true, false |
| 23 | `13 W J` | الـ index يبدأ من 0 (`"William Jacob"`: الفراغ index 7) |
| 24 | `102` | true=1، false=0، t+t=2 |
| 25 | `Hello\n` ثم سطر جديد `A` / سطر `B<tab>C` | `\\` تطبع backslash |

---

## 3) أسئلة قصيرة (input / syntax)

1. `int a, b; cin >> a >> b;` والمدخل `4   5` (3 فراغات). **a=4, b=5** — `>>` بتخطى الـ whitespace.
2. `int a; cin >> a;` والمدخل `A`. **input failure → a=0 (C++11+) والـ stream بصير fail state؛ أي cin بعده ينتجاهل.**
3. `char c; cin >> c;` والمدخل `   Z`. **c = 'Z'.** لو استخدمت `cin.get(c)` بيصير c = ' ' (أول فراغ).
4. أيها identifier صحيح؟ `2nd`، `_total`، `payRate`، `my-var`، `int`، `Total`
   **`_total`, `payRate`, `Total`.** (`2nd` يبدأ برقم، `my-var` فيه `-`، `int` keyword). و`Total` ≠ `total` (case sensitive).
5. شو الخطأ؟
   ```cpp
   int x;
   int y
   double z;
   y = w + x;
   ```
   **السطر 2: ناقص `;`. السطر 4: `w` ما اتعرّف.** (لو الأول بسبب syntax، التاني بسبب undeclared).
6. أي header بحتاجها؟ `cout`: `<iostream>` + `using namespace std;` — `string`: `<string>` — `setw/setprecision/setfill`: `<iomanip>` — `pow/sqrt`: `<cmath>` — `assert`: `<cassert>`.
7. شو الفرق بين `endl` و `'\n'`؟ **كلاهم سطر جديد؛ endl كمان manipulator (flush).**
8. `const double PI = 3.14159;` — هل بصير `PI = 3;` بعدها؟ **لا: named constant ما بتتغير.**
9. أيّ manipulators بتحتاج `<iomanip>`؟ **اللي إلها parameter: setw, setprecision, setfill.** أما endl, fixed, showpoint, left, right, flush فـ `<iostream>`.
10. كيف بطفي `assert`؟ **`#define NDEBUG` قبل `#include <cassert>`.**

---

## 4) اكتب الكود (حلّها بدون ما تشوف)

**أ)** برنامج بقرأ علامة (0–100) وبطبع A (≥90)، B (≥80)، C (≥70)، D (≥60)، وإلا F.

```cpp
#include <iostream>
using namespace std;
int main() {
    int score;
    cout << "Enter score: ";
    cin >> score;
    if (score >= 90)      cout << "A";
    else if (score >= 80) cout << "B";
    else if (score >= 70) cout << "C";
    else if (score >= 60) cout << "D";
    else                  cout << "F";
    cout << endl;
    return 0;
}
```

**ب)** يقرأ طول بالـ feet والـ inches ويحوله لـ cm (1 inch = 2.54 cm، 1 foot = 12 inches).

```cpp
#include <iostream>
using namespace std;
int main() {
    const double CM_PER_INCH = 2.54;
    const int INCHES_PER_FOOT = 12;
    int feet, inches;
    cout << "Enter feet and inches: ";
    cin >> feet >> inches;
    int totalInches = feet * INCHES_PER_FOOT + inches;
    double cm = totalInches * CM_PER_INCH;
    cout << "Total inches = " << totalInches << endl
         << "Centimeters  = " << cm << endl;
    return 0;
}
```
(جربها: `15 7` → 187 و 474.98).

**ج)** يقرأ رمز يوم (1–3) ويطبع الاسم باستخدام `switch`، وغير هيك "Invalid".

```cpp
switch (day) {
    case 1:  cout << "Sat"; break;
    case 2:  cout << "Sun"; break;
    case 3:  cout << "Mon"; break;
    default: cout << "Invalid";
}
```

**د)** اكتب جملة if/else وحدة بالـ ternary: أكبر من عددين.
`int m = (a > b) ? a : b;`

**هـ)** طبّق قاعدة الـ Cable Billing (Ch4) على الورق: residential = 4.50 + 20.50 + 7.50 × عدد الـ premium channels. لو عدد القنوات 3 → **47.50**.
Business: 15.00 + 75.00 + (connections−10)×5.00 (لو connections > 10) + 50.00 × premium channels.

---

## 5) خطة آخر ساعة
1. الجدول بالقسم 0 (5 دقايق).
2. أعد حل Q7, Q8, Q10, Q11, Q12, Q17 بدون ما تشوف الأجوبة — هاي أكثر الفخاخ.
3. اكتب برنامج ب) من الصفر على ورقة.
4. نام.
