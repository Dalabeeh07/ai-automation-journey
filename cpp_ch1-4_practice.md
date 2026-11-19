# C++ Ch1–4 (Malik) — شرح مركّز + أسئلة Output

> **تنبيه صريح:** هاد الملف مبني على كتاب Malik وقواعد C++ العامة، **مش** على شرح عادل نسيم (ما قدرت أفحص الفيديوهات) ولا على السلايدات (ما وصلتني). فإذا السلايدات فيها شي مختلف أو إضافي، السلايدات أولى.
> كل **ناتج** مكتوب هون طلع من تشغيل فعلي بـ `g++ (Ubuntu 13.3.0-6ubuntu2~24.04.1) 13.3.0` (C++17). الأرقام اللي بتعتمد على الجهاز (مثل `sizeof`) منبّه عليها.
> الأسئلة بتفترض إن فوق الكود دايماً: `#include <iostream>` و `<iomanip>` و `<cmath>` و `<string>` و `<cctype>` و `using namespace std;` وإن الكود داخل `main()`.

## خطة الساعتين

| الوقت | شو بتعمل | الأسئلة |
|---|---|---|
| 0:00 – 0:10 | **Ch1**: اقرأ القسم بس (نظري، حفظ تعريفات) | Q1–Q5 (مفاهيم) |
| 0:10 – 0:55 | **Ch2**: الأهم بالامتحان (int/double، precedence، casting، ++/--) | Q6–Q25 |
| 0:55 – 1:15 | **Ch3**: cout/cin، manipulators، الدوال الرياضية | Q26–Q38 |
| 1:15 – 1:40 | **Ch4**: if/switch/logical/assert | Q39–Q53 + أخطاء compile E1–E9 |
| 1:40 – 2:00 | **امتحان تجريبي**: الأسئلة المعلّمة ⭐، بدون ما تطلع على الشرح، وبعدين صحّح من الأجوبة | ⭐ |

**طريقة الشغل:** لكل مثال غطّي الناتج، خمّن، بعدين قارن. اللي غلطت فيه سجّله وارجع له بآخر 5 دقائق.

### طريقة تتبّع الكود (للأسئلة "شو الأوتبوت")
1. اكتب نوع كل متغيّر (`int` ولا `double` ولا `char`...).
2. احسب كل تعبير بالترتيب الصحيح (precedence)، ودير بالك: **int ÷ int = int**.
3. حدّث قيم المتغيرات سطر بسطر (جدول صغير على ورقة المسودة).
4. بالآخر شوف التنسيق: `endl` ولا لا، المسافات، `fixed/setprecision`، وهل بيطبع `1/0` للـ bool.

## ورقة الفخاخ (راجعها بآخر 5 دقائق)

| # | الفخ | مثال |
|---|---|---|
| 1 | `int / int` = `int` (بيقطع الكسر) | `7/2` → `3` |
| 2 | `%` بس للـ int، وإشارة الناتج = إشارة المقسوم | `-7 % 2` → `-1` |
| 3 | التحويل بصير **بعد** الحساب | `double x = 7/2;` → `3` مش `3.5` |
| 4 | مكان الـ cast بفرق | `(double)a/b` ≠ `(double)(a/b)` |
| 5 | تخزين double بـ int = **قطع** مش تقريب | `int x = 3.99;` → `3` |
| 6 | الـ char بالحساب = رقم ASCII | `'A'+1` → `66`، بس `char('A'+1)` → `B` |
| 7 | `x++` بيرجّع القيمة القديمة، `++x` الجديدة | |
| 8 | `cout` الافتراضي: 6 أرقام معنوية وما بيطبع `.0` | `cout << 2.0;` → `2` |
| 9 | `=` مش `==` داخل if | `if (x = 5)` دايماً true |
| 10 | `;` بعد `if (...)` بيخلي الجملة فاضية | |
| 11 | `else` بيرتبط بأقرب `if` (مش بالمسافات!) | dangling else |
| 12 | `10 < x < 12` دايماً true | |
| 13 | `&&` أقوى من `||`؛ وفيه short-circuit | |
| 14 | `switch` بدون `break` = fall-through | |
| 15 | `cin >> x` بعدها `getline` بتاخد سطر فاضي → `cin.ignore()` | |
| 16 | `toupper('a')` بترجع `int` | `cout << toupper('a')` → `65` |
| 17 | أي قيمة ≠ 0 = true (حتى -1 و 0.1) | |
| 18 | `"A" + "B"` غلط (string literals)؛ `'A'`≠`"A"` | |

---
## Ch1 — مقدمة عن الكمبيوتر واللغات (نظري، 10 دقايق)

**ما في كود هون.** حفظ تعريفات. هاي الأشياء اللي بتنسأل عادةً (تأكد من السلايدات للتفاصيل):

**Hardware vs Software**
- **Hardware**: الأجزاء الفيزيائية: **CPU** (فيه ALU للحساب + Control Unit)، **Main memory (RAM)** (مؤقتة، بتروح لما ينطفي الجهاز)، **Secondary storage** (HDD/SSD، دائمة)، أجهزة **Input/Output**.
- **Software**: البرامج. نوعين: **System software** (مثل الـ OS والـ compiler) و**Application software**.

**الوحدات والتمثيل**
- **bit** = 0 أو 1. **byte** = 8 bits. **KB** = 1024 byte، **MB** = 1024 KB، وهكذا.
- الكمبيوتر بيفهم **binary** بس. الحرف بينخزن كرقم حسب **ASCII** (أو Unicode).

```cpp
cout << bitset<8>(13) << endl;
cout << bitset<8>(255) << endl;
cout << int('A') << " " << int('a') << " " << int('0') << " " << int(' ') << endl;
```

الناتج:
```text
00001101
11111111
65 97 48 32
```

يعني `13` = `00001101` (8+4+1). و`'A'`=65، `'a'`=97 (الفرق 32)، `'0'`=48، المسافة=32. الأرقام دي بتنفعك بأسئلة الـ char.

**لغات البرمجة**
| النوع | الفكرة |
|---|---|
| Machine language | 0/1 مباشرة، الكمبيوتر بفهمها بدون ترجمة |
| Assembly | رموز قريبة من الآلة، بتتترجم بـ **assembler** |
| High-level (C++) | قريبة للإنجليزي، بتتترجم بـ **compiler** |

- **Compiler**: بترجم البرنامج **كله** لـ machine code قبل التشغيل. **Interpreter**: بترجم وبنفّذ **سطر سطر** وقت التشغيل. C++ لغة **compiled**.

**مراحل معالجة برنامج C++** (بالترتيب، سؤال كلاسيكي):
1. **Editor**: بتكتب الـ **source code** (`.cpp`).
2. **Preprocessor**: بنفّذ أوامر `#` مثل `#include`.
3. **Compiler**: بتفحص الـ syntax وبتولّد **object code** (`.o`/`.obj`)، وبتطلّع syntax errors.
4. **Linker**: بيربط الـ object code مع الـ libraries → **executable**.
5. **Loader**: بيحمّل البرنامج للـ memory.
6. **Execution**: الـ CPU بنفّذ التعليمات.

**أنواع الأخطاء**
| الخطأ | متى بينكشف | مثال |
|---|---|---|
| **Syntax error** | وقت الـ compile، والـ compiler بيعطي رسالة | نسيان `;` |
| **Runtime error** | وقت التشغيل، البرنامج بيوقف | القسمة على صفر (int) |
| **Logic error** | البرنامج بيشتغل بس النتيجة غلط، وما في رسالة | كتبت `+` بدل `*` |

**حل المشاكل**: Analysis → Design (algorithm) → Coding → Compile → Execute/Test. **Algorithm** = خطوات محدودة ومرتّبة لحل مشكلة.
**Programming paradigms**: **Structured programming** (تقسّم المشكلة لدوال) مقابل **OOP** (بتبني حول objects؛ أهم مفاهيمها: encapsulation, inheritance, polymorphism).

---
## Ch2 — أساسيات C++ (45 دقيقة)

### 2.1 هيكل البرنامج والـ tokens
```cpp
#include <iostream>        // preprocessor directive
using namespace std;       // عشان نكتب cout بدل std::cout
int main() {               // البرنامج يبدأ من main
    cout << "Hello" << endl;
    return 0;              // 0 = انتهى بنجاح
}
```
- **Comments**: `// سطر واحد` و `/* عدة أسطر */` (الـ compiler بتجاهلها).
- **Tokens** (أصغر وحدات): **special symbols** (`+ - * / ; ,`...)، **reserved words** (`int`, `if`, `return`...)، **identifiers** (أسماء من عندك).
- **قواعد الـ identifier**: حروف وأرقام و `_` بس، **ما يبدأ برقم**، ما يكون reserved word، و**case-sensitive** (`Total` ≠ `total`).

| الاسم | صح؟ | ليش |
|---|---|---|
| `my_var`, `_x`, `total2`, `Sum` | ✅ | |
| `2ndName` | ❌ | يبدأ برقم |
| `first-name` | ❌ | `-` مش مسموح |
| `total#` | ❌ | `#` مش مسموح |
| `int`, `return` | ❌ | reserved words |
| `my var` | ❌ | فيه مسافة |

### 2.2 الأنواع (Data types) — الفرق بين int و double

| النوع | بيخزّن | حجمه الشائع | مثال |
|---|---|---|---|
| `int` | عدد **صحيح** (بدون كسر) | 4 bytes (≈ ±2.1 مليار) | `5`, `-3` |
| `double` | عدد **حقيقي** (فيه كسر) | 8 bytes (≈ 15 رقم معنوي) | `3.14`, `2.0` |
| `float` | عدد حقيقي بدقة أقل | 4 bytes (≈ 7 أرقام معنوية) | `3.14f` |
| `char` | **حرف واحد** (فعلياً رقم ASCII) | 1 byte | `'A'` |
| `bool` | `true`/`false` | 1 byte | |
| `string` | نص (من `<string>`) | | `"Hello"` |

```cpp
cout << sizeof(int) << " " << sizeof(short) << " " << sizeof(long long) << endl;
cout << sizeof(char) << " " << sizeof(bool) << endl;
cout << sizeof(float) << " " << sizeof(double) << endl;
```

الناتج:
```text
4 2 8
1 1
4 8
```

⚠️ الأحجام تعتمد على الجهاز/الـ compiler؛ هاي أرقام هالجهاز (النمط الشائع). `sizeof(char)` دايماً 1.

**الفرق الجوهري int مقابل double:**
- `int` ما بيخزّن كسر أبداً. `int x = 3.99;` بيخزّن **3** (قطع، مش تقريب).
- القسمة `/` على **int و int** بتعطي **int**. إذا واحد منهم على الأقل double → النتيجة double.

```cpp
cout << 7 / 2 << endl;
cout << 7 % 2 << endl;
cout << 7.0 / 2 << endl;
cout << -7 / 2 << endl;
cout << -7 % 2 << endl;
cout << 1 / 3 << endl;
cout << 1 / 3.0 << endl;
cout << 5 % 10 << endl;
```

الناتج:
```text
3
1
3.5
-3
-1
0
0.333333
5
```

لاحظ: `-7/2` = `-3` (بيقطع باتجاه الصفر)، و`-7 % 2` = `-1` (إشارة المقسوم)، و`1/3` = `0`.

```cpp
double x = 7 / 2;
cout << x << endl;
int y = 7.9;
cout << y << endl;
int z = 3.99 + 2.99;
cout << z << endl;
double w = 7 / 2.0;
cout << w << endl;
```

الناتج:
```text
3
7
6
3.5
```

`double x = 7/2;` → أول بتنحسب `7/2` (int) = 3، وبعدين بتتحوّل لـ `3.0`. من أكثر الأخطاء شيوعاً بأسئلة الـ output.

### 2.3 Precedence (أولوية العمليات) و Associativity
الترتيب (من الأقوى): `()` ← `++ --` ← `!` و unary minus (`-x`) ← `* / %` ← `+ -` ← `< <= > >=` ← `== !=` ← `&&` ← `||` ← `?:` ← `=` والـ compound assignment. (الجزء بعد `+ -` بنحتاجه بـ Ch4.)
العمليات اللي بنفس المستوى بتنحسب **من اليسار لليمين** (ما عدا `=` فمن اليمين).

```cpp
cout << 2 + 3 * 4 << endl;
cout << (2 + 3) * 4 << endl;
cout << 10 - 4 - 3 << endl;
cout << 2 * 3 % 4 << endl;
cout << 10 / 3 * 3 << endl;
cout << 10 % 3 * 2 << endl;
cout << 2 + 10 / 4 << endl;
cout << 2 + 10 / 4.0 << endl;
cout << 100 / 10 / 5 << endl;
cout << 5 + 3 % 2 * 4 << endl;
```

الناتج:
```text
14
20
3
2
9
2
4
4.5
2
9
```

تتبّع واحد: `10 / 3 * 3` → `(10/3)*3` = `3*3` = **9** (مش 10!). و`5 + 3%2*4` = `5 + ((3%2)*4)` = `5 + 4` = 9.

### 2.4 Type conversion و Casting
- **Implicit (تلقائي)**: بالتعبير المختلط، الأضيق بيتحوّل للأوسع (`int` → `double`). و`char` بيتحوّل لـ `int` بالحساب.
- **Explicit (cast)**: `(double)x` أو `static_cast<double>(x)`. الـ cast بيطبّق على **اللي بعده مباشرة** (قبل القسمة).

```cpp
int a = 5, b = 2;
cout << a / b << endl;
cout << (double)a / b << endl;
cout << (double)(a / b) << endl;
cout << static_cast<double>(a) / b << endl;
cout << static_cast<int>(3.99) << endl;
cout << static_cast<int>(-3.99) << endl;
cout << static_cast<int>(3.5 + 0.5) << endl;
cout << int('A') << endl;
cout << char(66) << endl;
cout << 'A' + 1 << endl;
cout << char('A' + 1) << endl;
cout << 5 / 2 * 2.0 << endl;
cout << 5 / 2.0 * 2 << endl;
```

الناتج:
```text
2
2.5
2
2.5
3
-3
4
65
B
66
B
4
5
```

**النقاط:**
- `(double)a / b` → الـ cast على `a` أول، فالقسمة double → `2.5`.
- `(double)(a / b)` → القسمة int أول = 2، بعدين تتحول → `2`.
- `'A' + 1` → int = `66`؛ بس `char('A'+1)` → `B`.
- `5/2*2.0` → `(5/2)*2.0` = `2*2.0` = **4**؛ بس `5/2.0*2` = **5**. الترتيب بفرق!

### 2.5 الـ char: حرف ولا رقم؟

```cpp
cout << 'a' << endl;
cout << "a" << endl;
cout << 'a' + 1 << endl;
cout << (char)('a' + 1) << endl;
cout << '5' - '0' << endl;
cout << 5 << '5' << "5" << endl;
cout << (5 > 3) << endl;
cout << true << false << endl;
cout << boolalpha << (5 > 3) << endl;
```

الناتج:
```text
a
a
98
b
5
555
1
10
true
```

`'5' - '0'` = `53 - 48` = **5** (الحيلة المعروفة لتحويل رقم-حرف لرقم). والـ bool بينطبع `1`/`0` إلا إذا استخدمت `boolalpha`. و`'a'` (single quote) حرف، `"a"` (double quote) string.

### 2.6 ++ و -- و compound assignment
- `x++` (**postfix**): استخدم القيمة الحالية، بعدين زِد. `++x` (**prefix**): زِد، بعدين استخدم.
- `x op= y` تعني `x = x op (y)`، **كل اللي على اليمين بين قوسين**: `c *= 2 + 1` ≡ `c = c * (2 + 1)`.

```cpp
int x = 5;
int y = x++;
cout << x << " " << y << endl;
int a = 5;
int b = ++a;
cout << a << " " << b << endl;
int c = 10;
c += 5;  cout << c << endl;
c -= 3;  cout << c << endl;
c *= 2 + 1; cout << c << endl;
c /= 4;  cout << c << endl;
c %= 5;  cout << c << endl;
```

الناتج:
```text
6 5
6 6
15
12
36
9
4
```

⚠️ لا تكتب بالامتحان تعبير بيستخدم نفس المتغير مرتين مع `++` (مثل `a++ + ++a`)، سلوكه غير محدد (undefined). لو جاك سؤال، غالباً المتغيرات مختلفة.

### 2.7 Variables, constants, assignment, strings
- **Declaration**: `int a, b = 5;` ← **`a` بدون قيمة** (garbage)، بس `b` initialized.
- **const**: ما بتتغيّر بعد التعريف، ولازم تعطيها قيمة وقت التعريف: `const double PI = 3.14159;`
- **Chained assignment**: `a = b = c = 5;` (من اليمين).
- **Swap** بدون ما تخسر قيمة: بدنا متغير مؤقت `temp`.
- **string**: `+` للدمج، `.length()`/`.size()`، `.at(i)`/`[i]` (يبدأ من 0)، `.substr(pos, len)`، `.find(s)`.

```cpp
const double PI = 3.14159;
double r = 2;
cout << PI * r * r << endl;
int a, b, c;
a = b = c = 5;
cout << a << b << c << endl;
int p = 3, q = 8, temp;
temp = p; p = q; q = temp;
cout << p << " " << q << endl;
```

الناتج:
```text
12.5664
555
8 3
```

```cpp
string s = "Hello";
string t = " World";
string u = s + t;
cout << u << endl;
cout << u.length() << " " << u.size() << endl;
cout << u.at(0) << u[4] << endl;
cout << u.substr(6, 3) << endl;
cout << u.find("World") << endl;
cout << (u.find("xyz") == string::npos) << endl;
string a = "apple", b = "banana";
cout << (a < b) << endl;
```

الناتج:
```text
Hello World
11 11
Ho
Wor
6
1
1
```

`substr(6, 3)` = ابدأ من index 6 وخد 3 أحرف. مقارنة الـ strings بتتم حرف حرف (ترتيب القاموس حسب ASCII).

**أخطاء compile مشهورة بالـ strings/الثوابت:** `string s = "A" + "B";` ❌ (مش مسموح جمع literals)، وتغيير `const` ❌. (الأخطاء المتحقق منها بقسم "أخطاء compile" بالأسئلة).

---
## Ch3 — Input/Output (20 دقيقة)

### 3.1 cout و escape sequences
| Escape | المعنى |
|---|---|
| `\n` | سطر جديد |
| `\t` | tab |
| `\\` | backslash |
| `\"` | علامة اقتباس |
| `\'` | apostrophe |

- `endl` = سطر جديد **+ flush** للـ buffer. `'\n'` = سطر جديد فقط. بالنتيجة الظاهرة هم نفس الشي.

```cpp
cout << "Hello\nWorld" << endl;
cout << "A\tB\tC" << endl;
cout << "She said \"Hi\"" << endl;
cout << "Path: C:\\temp" << endl;
cout << "abc" << '\n' << "def" << endl;
```

الناتج:
```text
Hello
World
A	B	C
She said "Hi"
Path: C:\temp
abc
def
```

### 3.2 الطباعة الافتراضية للأرقام (فخ كبير)
بدون manipulators: `cout` بيطبع **6 أرقام معنوية** (significant) كحد أقصى، وبيحذف الأصفار الزايدة، وممكن يتحول لصيغة علمية (`e+06`).

```cpp
cout << 100000.0 << endl;
cout << 1234567.0 << endl;
cout << 0.00001234 << endl;
cout << 2.50 << endl;
cout << 2.0 << endl;
cout << 10 / 4.0 << endl;
cout << 1.0 / 3 << endl;
```

الناتج:
```text
100000
1.23457e+06
1.234e-05
2.5
2
2.5
0.333333
```

### 3.3 Manipulators (من `<iomanip>`)
- `fixed` + `setprecision(n)` → **n رقم بعد الفاصلة**. بدون `fixed`، `setprecision(n)` → **n رقم معنوي** (مجموع).
- `setw(n)` → عرض الحقل n للعنصر **التالي بس**، والمحاذاة يمين افتراضياً (`left`/`right`). ما بقصّ إذا الرقم أطول.
- `setfill(c)` → الحرف اللي بيعبّي الفراغ. `showpoint` → بيطبع الفاصلة والأصفار حتى للأعداد الكاملة.

```cpp
double pi = 3.14159265;
cout << fixed << setprecision(2) << pi << endl;
cout << setw(8) << 42 << "|" << endl;
cout << left << setw(8) << 42 << "|" << endl;
cout << right << setfill('*') << setw(8) << 42 << endl;
cout << setw(3) << 12345 << endl;
cout << 7 << setw(5) << 8 << endl;
```

الناتج:
```text
3.14
      42|
42      |
******42
12345
7****8
```

`fixed` و`setprecision` بيضلوا فعّالين لحد ما تغيّرهم. بس `setw` بيأثر على العنصر التالي فقط. والأصفار اللي بعد الفاصلة بتنطبع مع `fixed` (`2.000`).

```cpp
cout << 5.0 << endl;
cout << showpoint << 5.0 << endl;
cout << setprecision(3) << 3.14159 << " " << 1234.5678 << " " << 0.5 << endl;
cout << fixed << setprecision(3) << 3.14159 << " " << 2.0 << " " << 10 << endl;
```

الناتج:
```text
5
5.00000
3.14 1.23e+03 0.500
3.142 2.000 10
```

`setprecision(3)` بدون `fixed` = 3 أرقام معنوية، فـ `1234.5678` → `1.23e+03`. ولاحظ `0.500` بالسطر التالت: لأن `showpoint` من السطر اللي قبله لسا فعّال (بيبقى فعّال مثل `fixed`). والـ int (مثل `10`) ما بتتأثر بـ `fixed` ولا `setprecision`.

### 3.4 cin
- `cin >> x` بيقرأ ويتجاهل المسافات/الأسطر قبل القيمة، وبيوقف عند أول whitespace.
- قراءة `string` بـ `>>` بتاخد **كلمة وحدة** بس. لقراءة سطر كامل: `getline(cin, s)`.
- قراءة `int` من `3.7`: بياخد `3` وبيخلي `.7` بالـ buffer.
- لو القراءة فشلت (حرف بدل رقم): الـ stream بيدخل بحالة **fail** والمتغير بياخد `0` (من C++11).

المدخل (input): `3⏎4⏎`

```cpp
int a, b;
cin >> a >> b;
cout << a + b << endl;
```

الناتج:
```text
7
```

المدخل (input): `h   i⏎`

```cpp
char a, b;
cin >> a >> b;
cout << a << b << endl;
```

الناتج:
```text
hi
```

`cin >>` مع الـ char بتتجاهل المسافات.

المدخل (input): `3.7 5⏎`

```cpp
int a, b;
cin >> a >> b;
cout << a << " " << b << endl;
```

الناتج:
```text
3 0
```

`a` بياخد `3` ويبقى `.7 5` بالـ buffer. بعدين `b` بيحاول يقرأ int من `.7` وهاد مش int صحيح، فالقراءة بتفشل (fail state) و`b = 0`. الـ `5` ما انقرأت أصلاً.

المدخل (input): `Ali Ahmad⏎`

```cpp
string name;
cin >> name;
cout << name << endl;
```

الناتج:
```text
Ali
```

`cin >> string` بوقف عند أول مسافة.

**فخ `cin >>` ثم `getline`:**

المدخل (input): `25⏎Ali Ahmad⏎`

```cpp
int age; string name;
cin >> age;
getline(cin, name);
cout << "[" << name << "]" << endl;
```

الناتج:
```text
[]
```

`getline` قرأت بقية السطر بعد `25` (فاضي) → الاسم ضاع.

المدخل (input): `25⏎Ali Ahmad⏎`

```cpp
int age; string name;
cin >> age;
cin.ignore(100, '\n');
getline(cin, name);
cout << "[" << name << "]" << endl;
```

الناتج:
```text
[Ali Ahmad]
```

الحل: `cin.ignore()` قبل `getline` عشان يتخلص من الـ `\n` اللي ضل.

### 3.5 الدوال الجاهزة (predefined functions)
- **`<cmath>`**: `pow(x,y)`, `sqrt(x)`, `floor(x)` (للأسفل)، `ceil(x)` (للأعلى)، `fabs(x)` / `abs(x)`. دوال `pow/sqrt/floor/ceil/fabs` بترجّع **double** (فـ `pow(2,3)` بتنطبع `8` مش `8.0`، لأن `cout` بيحذف `.0`)؛ و`abs` على int بترجّع int.
- **`<cctype>`**: `toupper(c)`, `tolower(c)`, `isdigit(c)`, `isalpha(c)`, `isupper`, `islower`, `isspace`. ⚠️ `toupper`/`tolower` بترجع **int**!

```cpp
cout << pow(2, 3) << endl;
cout << pow(2, 0.5) << endl;
cout << sqrt(16) << endl;
cout << floor(3.9) << " " << ceil(3.1) << endl;
cout << floor(-3.1) << " " << ceil(-3.9) << endl;
cout << abs(-5) << " " << fabs(-5.5) << endl;
cout << pow(2, 3) / 3 << endl;
cout << (int)pow(10, 2) << endl;
cout << toupper('a') << endl;
cout << (char)toupper('a') << endl;
char c = toupper('a');
cout << c << endl;
```

الناتج:
```text
8
1.41421
4
3 4
-4 -3
5 5.5
2.66667
100
65
A
A
```

`floor(-3.1)` = `-4` و`ceil(-3.9)` = `-3`. و`cout << toupper('a')` بيطبع **65** لأنها int؛ بس لو خزّنتها في `char` أو عملت cast بتطلع `A`.

### 3.6 File I/O (باختصار)
`#include <fstream>`: `ofstream out("f.txt");` للكتابة، `ifstream in("f.txt");` للقراءة. بنستخدم `<<` و `>>` نفسهم، وبنسكّر بـ `.close()`.

```cpp
ofstream out("data.txt");
out << 10 << " " << 20 << endl;
out.close();
ifstream in("data.txt");
int a, b;
in >> a >> b;
cout << a + b << endl;
in.close();
```

الناتج:
```text
30
```

---
## Ch4 — جمل الاختيار (25 دقيقة)

### 4.1 Relational و Logical operators
- **Relational**: `==  !=  <  <=  >  >=` والنتيجة `true`(1) أو `false`(0).
- **Logical**: `!` (not) ← `&&` (and) ← `||` (or) (من الأقوى).
- أي قيمة **≠ 0 = true**، والـ `0` = false.

| `a` | `b` | `a && b` | `a \|\| b` | `!a` |
|---|---|---|---|---|
| T | T | T | T | F |
| T | F | F | T | F |
| F | T | F | T | T |
| F | F | F | F | T |

```cpp
cout << (true || false && false) << endl;
cout << ((true || false) && false) << endl;
cout << (!true || true) << endl;
cout << (!(true || true)) << endl;
int x = 5;
cout << (x > 3 && x < 10) << endl;
cout << (x < 3 || x > 10) << endl;
cout << (!x) << endl;
cout << (!0) << endl;
cout << (5 && 0) << (5 || 0) << endl;
cout << (5 > 3 > 2) << endl;
cout << (5 + 2 > 6 && 3 * 2 == 6) << endl;
```

الناتج:
```text
1
0
1
0
1
0
0
1
01
0
1
```

`true || false && false` → `&&` أول: `true || (false&&false)` = `true`. و`5 > 3 > 2` → `(5>3)>2` → `1>2` → `0`. وآخر سطر: الحسابات أول (`7 > 6` و`6 == 6`) وبعدين `&&` → `1`.

### 4.2 الأخطاء الكلاسيكية بالـ if

```cpp
int x = 3;
if (x = 5)
    cout << "A" << endl;
else
    cout << "B" << endl;
cout << x << endl;
```

الناتج:
```text
A
5
```

`x = 5` **assignment** مش مقارنة: بتخزّن 5 في x وقيمة التعبير 5 (≠0) → true. و`x` صار 5. المفروض `x == 5`.

```cpp
int x = 3;
if (x > 10);
    cout << "inside" << endl;
cout << "done" << endl;
```

الناتج:
```text
inside
done
```

الـ `;` بعد `if (...)` أنهت الجملة (جملة فاضية)، والـ `cout` بعدها دايماً بتتنفذ.

```cpp
if (5) cout << "a";
if (-1) cout << "b";
if (0) cout << "c";
if (0.1) cout << "d";
if ('0') cout << "e";
cout << endl;
```

الناتج:
```text
abde
```

`'0'` الحرف قيمته 48 (≠0) → true. أي شي غير الصفر true.

```cpp
int x = 5;
if (10 < x < 12) cout << "yes"; else cout << "no";
cout << endl;
```

الناتج:
```text
yes
```

الشرط الرياضي `10 < x < 12` ما بشتغل: `(10<5)` = 0، بعدين `0 < 12` = true. الصح: `x > 10 && x < 12`.

### 4.3 if / else if / else و dangling else
- بالـ chain (`if ... else if ... else`) **أول شرط صحيح بس** بتتنفذ جملته وبتتخطى الباقي. فالترتيب مهم!
- لو بدك أكتر من جملة: `{ }` (compound statement).
- **else بيرتبط بأقرب if** بغض النظر عن المسافات.

```cpp
int score = 85;
if (score >= 50) cout << "pass" << endl;
else if (score >= 80) cout << "good" << endl;
else cout << "fail" << endl;
```

الناتج:
```text
pass
```

`85 >= 50` صح أول شي، فبتطبع `pass` وما بتوصل لـ `good`. الشرط الأضيق لازم يجي أول.

```cpp
int x = 5, y = 3;
if (x > 3)
    if (y > 5)
        cout << "A" << endl;
else
    cout << "B" << endl;
cout << "end" << endl;
```

الناتج:
```text
B
end
```

رغم إن `else` مكتوب تحت `if (x > 3)`، هو بيتبع `if (y > 5)` (الأقرب). `y > 5` خاطئ → بتنفذ `B`.

**المعامل الشرطي `?:`**: `شرط ? قيمة_لو_صح : قيمة_لو_خطأ`

```cpp
int a = 7, b = 3;
int m = (a > b) ? a : b;
cout << m << endl;
cout << (a % 2 == 0 ? "even" : "odd") << endl;
```

الناتج:
```text
7
odd
```

### 4.4 Short-circuit evaluation
- `A && B`: لو `A` خطأ → `B` **ما بتنحسب**. `A || B`: لو `A` صح → `B` **ما بتنحسب**.
- مفيد لتجنب القسمة على صفر: `if (x != 0 && y / x > 1)`.

```cpp
int a = 0, b = 0;
if (a == 0 || ++b > 0) cout << "T ";
cout << a << " " << b << endl;
int c = 0, d = 0;
if (c != 0 && ++d > 0) cout << "T "; else cout << "F ";
cout << c << " " << d << endl;
int e = 1, f = 0;
if (e == 1 && ++f > 0) cout << "T ";
cout << e << " " << f << endl;
```

الناتج:
```text
T 0 0
F 0 0
T 1 1
```

بالمثال الأول `++b` ما اتنفذت لأن `a == 0` صح وخلاص (`||`). بالثاني `++d` ما اتنفذت لأن `c != 0` خطأ (`&&`). بالثالث الاثنين اتنفذوا.

### 4.5 switch
- التعبير لازم يكون **integral** (int, char, bool, enum)، **مش double ولا string**.
- قيم الـ `case` لازم تكون **constants** (حرفية أو const)، مش متغيرات.
- بدون `break` يكمل ينفذ الـ `case` اللي بعده (**fall-through**). الـ `default` اختياري.

```cpp
int n = 2;
switch (n) {
    case 1: cout << "one ";
    case 2: cout << "two ";
    case 3: cout << "three ";
    default: cout << "other ";
}
cout << endl;
char g = 'B';
switch (g) {
    case 'A': cout << "Excellent"; break;
    case 'B':
    case 'C': cout << "Good"; break;
    default: cout << "Unknown";
}
cout << endl;
```

الناتج:
```text
two three other 
Good
```

الأول بدون break: دخل `case 2` وكمل لحد نهاية الـ switch. التاني: `'B'` و`'C'` بيشتركوا بنفس الجملة (grouping).

### 4.6 assert (من `<cassert>`)
`assert(شرط);` — لو الشرط **خطأ** البرنامج بوقف فوراً ويطبع رسالة (لـ stderr)، ولو صح ما بصير شي. بيتعطّل لو عرّفت `NDEBUG`. بنستخدمه للتحقق من الافتراضات أثناء التطوير، مش لمعالجة مدخلات المستخدم.

```cpp
#include <iostream>
#include <cassert>
using namespace std;
int main() {
    int x = -1;
    assert(x > 0);
    cout << "after" << endl;
    return 0;
}
```

الناتج (البرنامج وقف بإشارة abort، يعني إنهاء غير طبيعي):
```text
a.out: main.cpp:6: int main(): Assertion `x > 0' failed.
```

لاحظ إن `"after"` ما انطبعت. شكل الرسالة بيختلف حسب الـ compiler (Visual Studio بيعرض نافذة). المهم: **البرنامج بوقف عند `assert` الفاشلة**.

---
## الأسئلة (جرّب قبل ما تطلع على الأجوبة)
⭐ = أسئلة الامتحان التجريبي (آخر 20 دقيقة).

### أسئلة Ch1

**Q1** — ايش الفرق بين compiler و interpreter؟

**Q2** — رتّب مراحل تشغيل برنامج C++: linker, compiler, loader, preprocessor, editor.

**Q3** — شو الفرق بين syntax error و logic error؟ أيهم بيكتشفه الـ compiler؟

**Q4** — كم bit في الـ byte؟ وشو الرقم binary للعدد 13 في 8 bits؟

**Q5** — الـ RAM مؤقتة ولا دائمة؟ والـ hard disk؟

### أسئلة Ch2

**Q6 ⭐** — شو الناتج؟

```cpp
int a = 17, b = 5;
cout << a / b << " " << a % b << " " << (double)a / b << endl;
```

**Q7 ⭐** — شو الناتج؟

```cpp
double r = 9 / 2 + 9 / 2.0;
cout << r << endl;
```

**Q8** — شو الناتج؟

```cpp
int x = 10;
x += 3 * 2;
x -= 4;
x %= 5;
cout << x << endl;
```

**Q9 ⭐** — شو الناتج؟

```cpp
int a = 3, b = 4;
int c = a++ * 2 + --b;
cout << a << " " << b << " " << c << endl;
```

**Q10** — شو الناتج؟

```cpp
char c = 'D';
cout << c + 1 << " " << (char)(c + 1) << " " << char(c - 3) << endl;
```

**Q11 ⭐** — شو الناتج؟

```cpp
int x = 7;
double y = x / 2;
double z = x / 2.0;
int w = z;
cout << y << " " << z << " " << w << endl;
```

**Q12** — شو الناتج؟

```cpp
cout << 10 + 5 / 2 * 3 - 1 << endl;
```

**Q13** — شو الناتج؟

```cpp
cout << 7 / 2.0 + 7 / 2 << endl;
```

**Q14** — شو الناتج؟

```cpp
cout << (int)(2.7 + 2.7) << " " << (int)2.7 + (int)2.7 << endl;
```

**Q15 ⭐** — شو الناتج؟

```cpp
cout << "x" << 1 + 2 << "y" << '3' + 1 << endl;
```

**Q16** — شو الناتج؟

```cpp
int a = 8, b = 3;
cout << a / b * b + a % b << endl;
```

**Q17** — شو الناتج؟

```cpp
int n = 5;
int m = n++ + 10;
int k = ++n * 2;
cout << n << " " << m << " " << k << endl;
```

**Q18** — شو الناتج؟

```cpp
double d = 5;
int i = 2;
cout << d / i << " " << 5 / i << " " << (5 + 0.0) / i << endl;
```

**Q19** — شو الناتج؟

```cpp
int x = 20, y = 6;
x = x / y;
y = y % 4;
x *= y + 1;
cout << x << " " << y << endl;
```

**Q20** — ايش الفرق بين `int` و `double`؟ وايش بيطلع `double x = 5 / 2;`؟

**Q21** — ايش الفرق بين `float` و `double`؟

**Q22** — ايش الفرق بين `'A'` و `"A"`؟

**Q23** — ايش الفرق بين `x++` و `++x`؟ لو `x = 5` وعملنا `y = x++` شو قيمة x و y؟

**Q24** — هل هالأسماء صالحة كـ identifiers؟ `2ndName`, `my_var`, `first-name`, `Total`, `int`, `_count`

**Q25** — ايش الفرق بين `=` و `==`؟

### أسئلة Ch3

**Q26 ⭐** — شو الناتج؟

```cpp
cout << fixed << setprecision(3) << 3.14159 << " " << 2.0 << " " << 10 << endl;
```

**Q27 ⭐** — شو الناتج؟

```cpp
cout << setprecision(3) << 3.14159 << " " << 1234.5678 << " " << 0.5 << endl;
```

**Q28** — شو الناتج؟

```cpp
cout << "[" << setw(6) << "ab" << "]" << "[" << left << setw(6) << "ab" << "]" << endl;
```

**Q29** — شو الناتج؟

المدخل (input): `5 abc⏎`

```cpp
int a, b;
cin >> a >> b;
cout << a << " " << b << endl;
```

**Q30** — شو الناتج؟

المدخل (input): `A B⏎`

```cpp
char c1, c2;
cin >> c1 >> c2;
cout << c1 + c2 << endl;
```

**Q31** — شو الناتج؟

```cpp
cout << sqrt(pow(3, 2) + pow(4, 2)) << " " << pow(2, 10) << " " << ceil(4.01) << " " << floor(-0.5) << endl;
```

**Q32 ⭐** — شو الناتج؟

```cpp
cout << toupper('b') << " " << (char)toupper('b') << endl;
```

**Q33** — شو الناتج؟

```cpp
cout << "Line1\nLine2\tTabbed\\" << endl << "End" << endl;
```

**Q34** — شو الناتج؟

```cpp
double price = 12.5;
int qty = 3;
cout << fixed << setprecision(2);
cout << "Total: " << price * qty << endl;
cout << qty / 2 << " " << qty / 2.0 << endl;
```

**Q35** — شو الناتج؟

المدخل (input): `42 hello world⏎`

```cpp
int x; string s;
cin >> x;
getline(cin, s);
cout << x << "|" << s << "|" << endl;
```

**Q36** — ايش الفرق بين `endl` و `'\n'`؟

**Q37** — ايش الفرق بين `cin >> name` و `getline(cin, name)`؟

**Q38** — ايش الفرق بين `fixed << setprecision(2)` و `setprecision(2)` لحاله؟

### أسئلة Ch4

**Q39** — شو الناتج؟

```cpp
int x = 4;
if (x > 2 && x < 6) cout << "A";
if (x > 2 || x < 0) cout << "B";
if (!(x == 4)) cout << "C";
else cout << "D";
cout << endl;
```

**Q40 ⭐** — شو الناتج؟

```cpp
int x = 2, y = 9;
if (x > 5)
    if (y > 5)
        cout << "A";
    else
        cout << "B";
cout << "C" << endl;
```

**Q41 ⭐** — شو الناتج؟

```cpp
int n = 3;
switch (n) {
    case 1: cout << "A";
    case 3: cout << "B";
    case 4: cout << "C"; break;
    case 5: cout << "D";
    default: cout << "E";
}
cout << endl;
```

**Q42** — شو الناتج؟

```cpp
int x = 0, y = 5;
if (x != 0 && y / x > 1) cout << "yes"; else cout << "no";
cout << endl;
```

**Q43** — شو الناتج؟

```cpp
cout << (3 > 2) + (2 > 1) << endl;
```

**Q44** — شو الناتج؟

```cpp
int x = 5;
cout << (x > 3 ? x * 2 : x / 2) << endl;
```

**Q45 ⭐** — شو الناتج؟

```cpp
int a = 5, b = 0;
if (a > 3 || ++b) cout << "T"; else cout << "F";
cout << b << endl;
```

**Q46** — شو الناتج؟

```cpp
int x = 7;
if (x % 2 == 0)
    cout << "even";
else if (x > 5)
    cout << "big odd";
else
    cout << "small odd";
cout << endl;
```

**Q47** — شو الناتج؟

```cpp
int x = 10;
if (x = 0) cout << "zero"; else cout << "nonzero";
cout << " " << x << endl;
```

**Q48** — شو الناتج؟

```cpp
int score = 72;
char g;
switch (score / 10) {
    case 10:
    case 9: g = 'A'; break;
    case 8: g = 'B'; break;
    case 7: g = 'C'; break;
    default: g = 'F';
}
cout << g << endl;
```

**Q49** — شو الناتج؟

```cpp
bool a = true, b = false;
cout << (a && !b) << (a || b) << (!a && b) << (!(a && b)) << endl;
```

**Q50 ⭐** — شو الناتج؟

```cpp
int x = 3;
if (x == 3) cout << "one ";
if (x > 1) cout << "two ";
else cout << "three ";
cout << "four" << endl;
```

**Q51** — ايش الفرق بين `if (a) ... else if (b) ...` وبين `if (a) ...; if (b) ...;`؟

**Q52** — ليش `switch (3.5)` أو `switch (name)` (string) غلط؟ وايش لازم يكون الـ case؟

**Q53** — ايش الفرق بين `&&` و `||`؟ ايش يعني short-circuit؟

### أخطاء compile — هل الكود صحيح؟ (كل واحد منها تحققت إنه **مش** بيعدّي)

**E1** — كود يحتوي مشكلة، شو هي؟

```cpp
int 2x = 5;
```

**E2** — كود يحتوي مشكلة، شو هي؟

```cpp
int x = 5
cout << x;
```

**E3** — كود يحتوي مشكلة، شو هي؟

```cpp
const int N = 5;
N = 6;
```

**E4** — كود يحتوي مشكلة، شو هي؟

```cpp
string s = "A" + "B";
```

**E5** — كود يحتوي مشكلة، شو هي؟

```cpp
switch (3.5) {
    case 1: break;
}
```

**E6** — كود يحتوي مشكلة، شو هي؟

```cpp
int k = 2;
switch (1) {
    case k: break;
}
```

**E7** — كود يحتوي مشكلة، شو هي؟

```cpp
int x = 5;
int x = 6;
```

**E8** — كود يحتوي مشكلة، شو هي؟

```cpp
y = 10;
```

**E9** — كود يحتوي مشكلة، شو هي؟

```cpp
int a = 5;
if (a > 3) {
    cout << a;
```

---
## الأجوبة

**Q1**: الـ compiler بترجم البرنامج كله لـ machine code قبل التشغيل؛ الـ interpreter بترجم وبنفّذ سطر سطر أثناء التشغيل. C++ compiled.

**Q2**: editor → preprocessor → compiler → linker → loader → execution.

**Q3**: الـ syntax error مخالفة لقواعد اللغة والـ compiler بيكتشفه ويرفض يكمل. الـ logic error البرنامج بيشتغل بس بيعطي نتيجة غلط، والـ compiler ما بيكتشفه.

**Q4**: 8 bits. 13 = `00001101` (تحققت منها بـ bitset أعلاه).

**Q5**: RAM (main memory) مؤقتة، بتنمسح لما ينطفي الجهاز. الـ hard disk/SSD (secondary storage) دائمة.

**Q6**: `3 2 3.4`

**Q7**: `8.5`

**Q8**: `2`

**Q9**: `4 3 9`

**Q10**: `69 E A`

**Q11**: `3 3.5 3`

**Q12**: `15`

**Q13**: `6.5`

**Q14**: `5 4`

**Q15**: `x3y52`

**Q16**: `8`

**Q17**: `7 15 14`

**Q18**: `2.5 2 2.5`

**Q19**: `9 2`

**Q20**: `int` بيخزّن أعداد صحيحة بدون كسر؛ `double` بيخزّن أعداد حقيقية بدقة ~15 رقم. `5/2` قسمة int = 2، وبعدين تتحول لـ double فالـ x = `2` (بتنطبع `2`، مش `2.5`). الصح لـ 2.5 هو `5 / 2.0`.

**Q21**: كلاهما أعداد حقيقية؛ `double` أدق (≈15 رقم معنوي، 8 bytes) و`float` أقل دقة (≈7 أرقام، 4 bytes). الأحجام الدقيقة بتعتمد على الجهاز.

**Q22**: `'A'` هو **char** (حرف واحد، قيمته 65). `"A"` هو **string literal** (نص، فيه حرف `A` وعلامة نهاية). مش نفس النوع.

**Q23**: `x++` (postfix): بيرجّع القيمة القديمة بعدين بيزيد. `++x` (prefix): بيزيد بعدين بيرجّع الجديدة. بعد `y = x++`: `y = 5`، `x = 6`.

**Q24**: `2ndName` ❌ (يبدأ برقم)، `my_var` ✅، `first-name` ❌ (`-` مش مسموح)، `Total` ✅، `int` ❌ (reserved word)، `_count` ✅.

**Q25**: `=` **assignment** (بتخزّن قيمة بمتغير). `==` **مقارنة** (بتفحص التساوي وبترجّع true/false).

**Q26**: `3.142 2.000 10`

**Q27**: `3.14 1.23e+03 0.5`

**Q28**: `[    ab][ab    ]`

**Q29**: `5 0`

**Q30**: `131`

**Q31**: `5 1024 5 -1`

**Q32**: `66 B`

**Q33**: `Line1  ⏎  Line2 ⇥ Tabbed\  ⏎  End`

**Q34**: `Total: 37.50  ⏎  1 1.50`

**Q35**: `42| hello world|`

**Q36**: كلاهما سطر جديد. `endl` كمان بيعمل **flush** للـ buffer؛ `'\n'` سطر جديد فقط. بالمخرجات المرئية ما في فرق.

**Q37**: `cin >>` بتقرأ لحد أول whitespace (كلمة وحدة)؛ `getline` بتقرأ السطر كامل بالمسافات. و`getline` بعد `cin >>` بتحتاج `cin.ignore()`.

**Q38**: مع `fixed`: رقمين **بعد الفاصلة**. بدون `fixed`: رقمين **معنويين بالمجموع** (وممكن يطلع بصيغة علمية).

**Q39**: `ABD`

**Q40**: `C`

**Q41**: `BC`

**Q42**: `no`

**Q43**: `2`

**Q44**: `10`

**Q45**: `T0`

**Q46**: `big odd`

**Q47**: `nonzero 0`

**Q48**: `C`

**Q49**: `1101`

**Q50**: `one two four`

**Q51**: بالـ else-if: لو الأولى صحت، الثانية **ما بتنفحص**. بالـ ifs المنفصلة: كل شرط بيتفحص لحاله وممكن ينفذوا الاثنين (شوف Q50).

**Q52**: الـ switch بتقبل بس أنواع integral (int, char, bool, enum) — مش double ولا string. والـ case لازم تكون constant، مش متغيّر.

**Q53**: `&&` صح لما الاثنين صح؛ `||` صح لما واحد على الأقل صح. Short-circuit: في `A && B` لو A خطأ ما بتنحسب B، وفي `A || B` لو A صح ما بتنحسب B.

**أخطاء compile** (رسائل g++ مختصرة؛ الصياغة بتختلف حسب الـ compiler):

- **E1**: اسم يبدأ برقم — `error: expected unqualified-id before numeric constant`

- **E2**: نسيان `;` — `error: expected ‘,’ or ‘;’ before ‘cout’`

- **E3**: تعديل const — `error: assignment of read-only variable ‘N’`

- **E4**: جمع string literals — `error: invalid operands of types ‘const char [2]’ and ‘const char [2]’ to binary ‘operator+’`

- **E5**: switch على double — `error: switch quantity not an integer`

- **E6**: case مش constant — `error: the value of ‘k’ is not usable in a constant expression`

- **E7**: تعريف نفس المتغير مرتين بنفس الـ scope — `error: redeclaration of ‘int x’`

- **E8**: استخدام متغير غير معرّف — `error: ‘y’ was not declared in this scope`

- **E9**: قوس { ما انسكّر — `error: expected ‘}’ at end of input`

---
## ملاحظات على الأجوبة اللي بتغلّط عادةً
- **أسئلة `x++`/`++x`**: ارسم جدول للمتغيرات وحدّثه سطر بسطر.
- **أسئلة القسمة**: اكتب نوع كل طرف جنب العملية (`int/int` ولا `int/double`).
- **أسئلة `setprecision`**: اسأل نفسك: فيه `fixed`؟ (بعد الفاصلة) ولا لأ؟ (أرقام معنوية).
- **أسئلة dangling else**: تجاهل المسافات، اربط الـ else بأقرب if.
- **أسئلة switch**: دور على `break`.
- ما بتضمن إن هالأسئلة نفس أسئلة دكتورك. الهدف تدريب على **أنماط** الأسئلة.
