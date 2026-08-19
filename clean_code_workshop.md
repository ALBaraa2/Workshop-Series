# Clean Code: Writing Maintainable and Professional Software
### Workshop Material — Bilingual (Arabic / English)

---

# الجزء الأول: بالعربي

## 1. عنوان الورشة
**Clean Code: Writing Maintainable and Professional Software**
(كتابة كود احترافي قابل للصيانة)

## 2. أهداف التعلّم
بنهاية الورشة، المشارك رح يقدر:
- يميّز بين كود "شغّال" وكود "نظيف" — وليش الفرق مهم بفريق حقيقي.
- يكتب أسماء متغيرات/دوال/كلاسات واضحة بدون حاجة لتعليقات إضافية.
- يطبّق SRP, DRY, KISS, YAGNI بشكل عملي بمشاريعه.
- يكتشف Code Smells شائعة (Long functions, Deep nesting, Magic numbers...) بأي كود يشوفه.
- يعرف يعيد هيكلة (Refactor) كود سيء لكود نظيف خطوة بخطوة.
- يفهم مبادئ SOLID الأساسية بدون تعقيد زايد.
- يكتب كود سهل المراجعة (Review-friendly) ومناسب للعمل الجماعي.

## 3. المتطلبات المسبقة
- أساسيات برمجة (متغيرات، شروط، حلقات، دوال، كلاسات).
- معرفة أساسية بـ PHP أو أي لغة OOP مشابهة — الأمثلة بـ PHP/Laravel بس المفاهيم عامة.
- خبرة سابقة بكتابة كود لمشروع صغير على الأقل (تكليف جامعي، مشروع شخصي...).

## 4. الأجندة — 60 دقيقة
| الوقت | المحتوى |
|---|---|
| 0:00–0:05 | مقدمة: شو هو Clean Code وليش مهم |
| 0:05–0:12 | Readability + Naming + Magic Numbers |
| 0:12–0:20 | Functions + SRP + Long Functions + Deep Nesting |
| 0:20–0:26 | DRY, KISS, YAGNI |
| 0:26–0:30 | Comments: متى تساعد ومتى تضر |
| 0:30–0:36 | Error Handling + Input Validation |
| 0:36–0:42 | Separation of Concerns + Large Classes + Duplication |
| 0:42–0:46 | Code Smells + Refactoring Techniques |
| 0:46–0:52 | SOLID مبسّط للـ Juniors |
| 0:52–0:55 | Clean Code بالفرق + كود سهل الـ Review |
| 0:55–1:00 | تمرين ختامي + ملخّص + نقاش |

## 5. مقدمة (Introduction)

### شو هو Clean Code؟
كود بيقرأه أي مطوّر تاني (أو إنت بعد 6 شهور) ويفهمه بسرعة، بدون ما يحتاج يشغّله بالـ debugger أو يسأل صاحبه "شو قصدك هون؟".

### ليش مهم؟
- **95% من وقت المطوّر بيروح بقراءة كود موجود، مش كتابة كود جديد.** كود غير مفهوم = وقت ضايع لكل الفريق.
- كود سيء بيصير أبطأ وأخطر تعدّل عليه مع الوقت — أي تغيير بسيط بيصير مخاطرة.
- بالشغل الحقيقي، الكود بيعيش لسنين وبيمر عليه عشرات المطورين — مش زي مشروع جامعي بينخلص وينسى.

> **القاعدة الذهبية:** "Any fool can write code that a computer can understand. Good programmers write code that humans can understand." — Martin Fowler

## 6. مبادئ Clean Code (نظرة عامة)
كود نظيف لازم يكون:
- **Readable** — مفهوم من أول قراءة.
- **Maintainable** — سهل التعديل بدون خوف من كسر شي.
- **Testable** — ممكن تكتبله اختبارات بسهولة.
- **Reusable** — أجزاء منه ممكن تستخدمها بمكان تاني بدون نسخ ولصق.
- **Consistent** — نفس الأسلوب بكل المشروع، مش كل ملف بطريقة.

## 7–8. المفاهيم التفصيلية + أمثلة Bad vs Good

### أ) Readability + Meaningful Naming + Magic Numbers

**المشكلة:** أسماء مبهمة وأرقام "سحرية" بدون معنى بتخلي القارئ يخمّن قصدك.

```php
// ❌ Bad
function calc($p, $d) {
    if ($d > 100) {
        return $p - ($p * 0.15);
    }
    return $p - ($p * 0.05);
}
```
**شو المشكلة؟** `$p` و`$d` مالهم معنى، `0.15` و`0.05` و`100` أرقام سحرية محدش بيعرف قصدها بدون ما يقرأ المنطق كامل.

```php
// ✅ Good
const BULK_ORDER_THRESHOLD = 100;
const BULK_DISCOUNT_RATE = 0.15;
const STANDARD_DISCOUNT_RATE = 0.05;

function calculateDiscountedPrice(float $price, int $quantity): float
{
    $discountRate = $quantity > BULK_ORDER_THRESHOLD
        ? BULK_DISCOUNT_RATE
        : STANDARD_DISCOUNT_RATE;

    return $price - ($price * $discountRate);
}
```
**ليش أفضل؟** الاسم `calculateDiscountedPrice` بيشرح نفسه، والـ constants بتشرح قصد كل رقم — ما بتحتاج تعليق تشرح فيه الكود.

**قواعد سريعة للتسمية:**
- الدوال: فعل واضح (`getUser`, `calculateTotal`, `isValid`).
- المتغيرات Boolean: `is/has/can` (`isActive`, `hasPermission`).
- تجنّب اختصارات مبهمة (`$d`, `$tmp`, `$data2`).

---

### ب) Functions, SRP, Long Functions, Deep Nesting

**المشكلة:** دالة وحدة بتعمل أشياء كتير (تحقق + منطق عمل + حفظ بقاعدة البيانات) وفيها تعشيش (nesting) عميق.

```php
// ❌ Bad
function registerUser($request) {
    if ($request->email) {
        if (strlen($request->password) >= 8) {
            if (!User::where('email', $request->email)->exists()) {
                $user = new User();
                $user->email = $request->email;
                $user->password = bcrypt($request->password);
                $user->save();
                Mail::to($user->email)->send(new WelcomeEmail($user));
                return response()->json(['success' => true]);
            } else {
                return response()->json(['error' => 'Email exists'], 400);
            }
        } else {
            return response()->json(['error' => 'Weak password'], 400);
        }
    } else {
        return response()->json(['error' => 'Email required'], 400);
    }
}
```
**شو المشكلة؟** الدالة بتعمل validation + business logic + persistence + email كلها سوا، وفيها 3 مستويات تعشيش (nesting) صعب تتابعها، ومسؤولة عن أكتر من شي وحد (بتخالف SRP).

```php
// ✅ Good — Guard Clauses + Single Responsibility
function registerUser(RegisterRequest $request)
{
    $this->ensureEmailIsUnique($request->email);

    $user = $this->userService->create($request->validated());
    $this->notificationService->sendWelcomeEmail($user);

    return response()->json(['success' => true]);
}

function ensureEmailIsUnique(string $email): void
{
    if (User::where('email', $email)->exists()) {
        throw new EmailAlreadyExistsException();
    }
}
```
**ليش أفضل؟**
- **Guard Clauses** بدل تعشيش: نطلع بدري لو في مشكلة، فما في حاجة لـ `else` متداخلة.
- Validation انتقل لـ `RegisterRequest` (مسؤولية منفصلة).
- كل دالة إلها مسؤولية وحدة واضحة — هاد جوهر **Single Responsibility Principle (SRP)**: كل دالة/كلاس لازم يكون إله سبب واحد بس يتغيّر لأجله.

**قاعدة عملية:** لو دالتك محتاجة "و" لتشرحها ("بتتحقق وبتحفظ وبترسل إيميل") — هاي إشارة إنها لازم تنقسم.

---

### ج) DRY, KISS, YAGNI

- **DRY (Don't Repeat Yourself):** أي منطق مكرر بمكانين، لو غيّرت بمكان لازم تتذكر تغيّر بالتاني — مصدر أخطاء مضمون.
```php
// ❌ نفس منطق التحقق من الإيميل مكرر بـ 3 أماكن
if (!preg_match('/^[^\s@]+@[^\s@]+\.[^\s@]+$/', $email)) { ... }
```
```php
// ✅ دالة/Rule وحدة تُستخدم بكل مكان
function isValidEmail(string $email): bool {
    return (bool) preg_match('/^[^\s@]+@[^\s@]+\.[^\s@]+$/', $email);
}
```

- **KISS (Keep It Simple, Stupid):** الحل الأبسط اللي بيحل المشكلة هو الأفضل — لا تبني نظام معقد لمشكلة بسيطة.
```php
// ❌ Over-engineered لحساب ضريبة ثابتة
class TaxCalculatorFactory {
    public function make(string $strategy): TaxStrategyInterface { ... }
}
```
```php
// ✅ لو الضريبة ثابتة فعليًا، بساطة أفضل
function calculateTax(float $amount): float {
    return $amount * 0.16;
}
```

- **YAGNI (You Aren't Gonna Need It):** لا تبني ميزة أو تعقيد "لأنك ممكن تحتاجها بالمستقبل" — ابنيها لما فعلاً تحتاجها.
> مثال: ما تبني نظام Plugin كامل لمشروع صغير "احتياطًا" لو حد طلب ميزة زيادة بعد سنة — هاد وقت وتعقيد مهدور غالبًا.

---

### د) Comments: متى تساعد ومتى تضر

```php
// ❌ تعليق بيشرح كود سيء بدل ما يصلحه
// check if user is active and has permission and not banned
if ($u->s == 1 && $u->p == 3 && $u->b == 0) { ... }
```
```php
// ✅ كود يشرح نفسه، بدون حاجة لتعليق
if ($user->isActive() && $user->hasAdminPermission() && !$user->isBanned()) { ... }
```
**القاعدة:** التعليق الجيد بيشرح **"ليش"** (قرار، سبب، ملاحظة أمنية)، مش **"شو"** — لأن الكود نفسه لازم يوضّح الـ"شو". تعليق بيشرح كود مبهم هو إشارة إن الكود بحاجة إعادة كتابة، مش تعليق.

---

### هـ) Error Handling + Input Validation

```php
// ❌ Bad — فشل صامت، ما في تحقق
function getUser($id) {
    $user = User::find($id);
    return $user->name; // بينهار لو $user null
}
```
```php
// ✅ Good
function getUser(int $id): User
{
    $user = User::find($id);

    if (!$user) {
        throw new UserNotFoundException("User with id {$id} not found");
    }

    return $user;
}
```
**ليش أفضل؟** الخطأ واضح ومحدد، وبينكشف بمكانه مباشرة بدل ما "ينهار" الكود بمكان بعيد عن السبب الحقيقي.

**Input Validation في Laravel:** استخدم Form Requests بدل تحقق يدوي متكرر بكل Controller:
```php
class RegisterRequest extends FormRequest {
    public function rules(): array {
        return [
            'email' => 'required|email|unique:users',
            'password' => 'required|min:8',
        ];
    }
}
```

---

### و) Separation of Concerns + Large Classes + Code Duplication

**المشكلة:** Controller "بدين" (Fat Controller) بيعمل كل شي — استعلامات قاعدة بيانات، منطق عمل، تنسيق response.

```php
// ❌ Bad — كل شي بالـ Controller
class OrderController {
    public function store(Request $request) {
        $order = new Order();
        $order->user_id = auth()->id();
        $order->total = $request->items->sum('price');
        if ($order->total > 500) { $order->total *= 0.9; }
        $order->save();
        Mail::to(auth()->user())->send(new OrderConfirmation($order));
        return response()->json($order);
    }
}
```
```php
// ✅ Good — كل مسؤولية بمكانها
class OrderController {
    public function __construct(private OrderService $orderService) {}

    public function store(StoreOrderRequest $request) {
        $order = $this->orderService->createOrder(auth()->user(), $request->validated());
        return response()->json($order);
    }
}

class OrderService {
    public function createOrder(User $user, array $data): Order {
        $order = Order::create([...]);
        $this->applyDiscountIfEligible($order);
        $this->notifyCustomer($order);
        return $order;
    }
}
```
**ليش أفضل؟** الـ Controller بس بيستقبل الـ request ويرجّع response — كل منطق العمل بالـ Service. هاد **Separation of Concerns**: كل جزء من النظام مسؤول عن طبقة وحدة (HTTP, Business Logic, Data).

**Large Classes** غالبًا نتيجة تجميع مسؤوليات كتير بكلاس وحد — الحل نفس الفكرة: فصل حسب المسؤولية (Service, Repository, Policy...).

---

## Code Smells شائعة (ملخّص سريع)
| الرائحة (Smell) | العلامة | الحل |
|---|---|---|
| Long Function | دالة أطول من شاشة واحدة | Extract Function |
| Deep Nesting | أكتر من 2-3 مستويات if/for | Guard Clauses |
| Large Class | كلاس بيعمل أشياء كتير غير مترابطة | Extract Class / SRP |
| Duplicated Code | نفس المنطق بأكتر من مكان | Extract Function / DRY |
| Magic Numbers | أرقام بدون معنى بالكود | Named Constants |
| Long Parameter List | دالة بـ 5+ parameters | استخدم Object/DTO |

## Refactoring Techniques (تقنيات إعادة الهيكلة)
- **Extract Function:** فصل جزء من دالة كبيرة لدالة إلها اسم واضح.
- **Rename Variable/Function:** تحسين الاسم بدون تغيير المنطق.
- **Replace Magic Number with Constant:** استبدال الأرقام السحرية بـ constants واضحة.
- **Guard Clauses:** الخروج المبكر بدل تعشيش عميق.
- **Extract Class:** فصل مسؤوليات كلاس ضخم لكلاسات أصغر.

## SOLID مبسّط للـ Junior Developers
> ملاحظة: ما رح ندخل بتفاصيل نظرية معقدة — بس المعنى العملي لكل حرف.

- **S — Single Responsibility:** كل كلاس/دالة إله سبب واحد بس يتغيّر لأجله (شفناه فوق بمثال `OrderService`).
- **O — Open/Closed:** الكود المفروض يكون قابل للتوسعة بدون ما تعدّل بالكود الموجود. مثال: بدل `if ($type == 'credit') ... elseif ($type == 'paypal') ...` اللي لازم تعدّله كل ما تضيف طريقة دفع، استخدم interface (`PaymentMethod`) وكل طريقة دفع كلاس منفصل بينفّذه.
- **L — Liskov Substitution:** أي كلاس فرعي (subclass) لازم يقدر يحل مكان الكلاس الأساسي بدون ما يكسر البرنامج. (مثال بسيط: لو `Duck extends Bird` وكل الطيور المفروض تطير — لكن الـ Duck ما بتطير، هاد كسر لـ LSP.)
- **I — Interface Segregation:** لا تجبر كلاس يطبّق methods مالها علاقة فيه. أفضل كذا interfaces صغيرة بدل وحدة ضخمة.
- **D — Dependency Inversion:** الكلاسات لازم تعتمد على abstractions (interfaces) مش على implementations محددة مباشرة — بيسهّل التبديل والاختبار (مثال: `OrderService` بياخد `PaymentGatewayInterface` مش `StripeGateway` مباشرة).

## Clean Code بالفرق + كود سهل الـ Review
- التزم بنفس الـ coding style بكل الفريق (استخدم PSR-12 أو أي standard متفق عليه، وأتمتة عبر linter/formatter).
- PR صغيرة ومركّزة على شي واحد أسهل بكتير تتراجع من PR ضخمة فيها 20 تغيير.
- اسم الدالة/المتغير لازم يفهمه أي حد بالفريق، مش بس إنت.
- اكتب كود كأنك بتشرحه لمطوّر جديد بالفريق.

## 10. تمارين عملية (Hands-on Exercises)

**تمرين 1:** حددوا المشاكل بهاد الكود وأعيدوا هيكلته:
```php
function proc($arr) {
    $r = [];
    foreach ($arr as $i) {
        if ($i['s'] == 1) {
            if ($i['p'] > 0) {
                $r[] = $i['p'] * 1.16;
            }
        }
    }
    return $r;
}
```
*(المطلوب: تسمية واضحة، إزالة nesting، إزالة magic number)*

**تمرين 2:** فنّدوا الـ Code Smells بهاد الكلاس وقترحوا حل (SRP):
```php
class UserController {
    public function register($request) {
        // validation + save user + send email + log activity + generate report
    }
}
```

**تمرين 3:** لاقوا التكرار (DRY) بهاد الكود واقترحوا حل:
```php
// دالتين مختلفتين بنفس منطق التحقق من صلاحية الكوبون منسوخ بينهم
```

## 11. التحدي النهائي (Final Challenge)
عطوا المشاركين دالة/كلاس طويل (50+ سطر) فيه: تسمية سيئة، nesting عميق، magic numbers، تكرار كود، ما في error handling، وكل المسؤوليات بمكان وحد. المطلوب: إعادة هيكلته كامل بتطبيق كل المبادئ اللي اتعلموها (SRP, DRY, KISS, Guard Clauses, Constants, Error Handling) وتقديم نسخة نظيفة + شرح كل تعديل ليش صار.

## 12. الأخطاء الشائعة
- اعتقاد إن Clean Code معناه "كود أقصر" — أحيانًا كود نظيف أطول شوي بس أوضح.
- Refactoring كل الكود دفعة وحدة بدل تدريجيًا.
- تطبيق SOLID بشكل حرفي زايد على مشروع بسيط (Over-engineering).
- الاعتماد على تعليقات بدل تحسين الكود نفسه.

## 13. أفضل الممارسات
- اسأل نفسك دايمًا: "لو قرا هاد الكود حد تاني بعد 6 شهور، رح يفهمه بسرعة؟"
- Refactor بخطوات صغيرة، واختبر بعد كل خطوة.
- التزم بمبدأ واحد بكل مرة (مش لازم تطبّق كل SOLID بمرة وحدة على كل شي).

## 14. الملخّص
Clean Code مش مجموعة قواعد صارمة، هو طريقة تفكير: اكتب كود بيحكي قصته لحاله. من التسمية الواضحة، للدوال الصغيرة ذات المسؤولية الوحدة، لتجنب التكرار والتعقيد الزايد، لحد فصل المسؤوليات — كل هاي المبادئ هدفها شي واحد: كود يقدر أي حد (بما فيهم إنت بالمستقبل) يفهمه ويعدّله بثقة.

## 15. أسئلة للنقاش
- شوفوا دالة كتبتوها بمشروع قديم إلكم — شو أول 3 أشياء كنتوا تغيروها اليوم؟
- متى ممكن يكون "التعقيد" مبرر ومش code smell؟
- هل SOLID دايمًا لازم تُطبّق، ولا في حالات بتكون Over-engineering؟

## 16. مصادر إضافية
- كتاب *Clean Code* — Robert C. Martin
- كتاب *Refactoring* — Martin Fowler
- refactoring.guru — شرح مصوّر لـ Code Smells و Refactoring Techniques
- PHP-FIG PSR-12 Coding Standard

---
---

# Part 2 — English

## 1. Workshop Title
**Clean Code: Writing Maintainable and Professional Software**

## 2. Learning Objectives
By the end of this workshop, participants will be able to:
- Distinguish between code that "just works" and code that is truly clean — and why that difference matters on a real team.
- Write variable/function/class names clear enough to need no extra comments.
- Practically apply SRP, DRY, KISS, and YAGNI in their own projects.
- Spot common code smells (long functions, deep nesting, magic numbers...) in any codebase.
- Refactor bad code into clean code step by step.
- Understand the core SOLID principles without unnecessary complexity.
- Write review-friendly code suited for team collaboration.

## 3. Prerequisites
- Basic programming knowledge (variables, conditionals, loops, functions, classes).
- Basic familiarity with PHP or a similar OOP language — examples use PHP/Laravel, but concepts are language-agnostic.
- Prior experience writing code for at least one small project (university assignment, personal project...).

## 4. Agenda — 60 Minutes
| Time | Content |
|---|---|
| 0:00–0:05 | Intro: What is Clean Code and why it matters |
| 0:05–0:12 | Readability + Naming + Magic Numbers |
| 0:12–0:20 | Functions + SRP + Long Functions + Deep Nesting |
| 0:20–0:26 | DRY, KISS, YAGNI |
| 0:26–0:30 | Comments: when they help, when they hurt |
| 0:30–0:36 | Error Handling + Input Validation |
| 0:36–0:42 | Separation of Concerns + Large Classes + Duplication |
| 0:42–0:46 | Code Smells + Refactoring Techniques |
| 0:46–0:52 | SOLID, simplified for Juniors |
| 0:52–0:55 | Clean Code in Teams + Review-friendly code |
| 0:55–1:00 | Final exercise + Summary + Discussion |

## 5. Introduction

### What is Clean Code?
Code that another developer (or you, six months from now) can read and understand quickly, without needing to run it in a debugger or ask the author "what did you mean here?"

### Why does it matter?
- **Developers spend far more time reading code than writing new code.** Unclear code wastes the whole team's time.
- Bad code gets slower and riskier to change over time — every small edit becomes a gamble.
- In real work, code lives for years and passes through dozens of developers — unlike a university project you finish and forget.

> **Golden rule:** "Any fool can write code that a computer can understand. Good programmers write code that humans can understand." — Martin Fowler

## 6. Clean Code Principles (Overview)
Clean code should be:
- **Readable** — understood on first read.
- **Maintainable** — easy to change without fear of breaking something.
- **Testable** — easy to write tests for.
- **Reusable** — parts of it can be reused elsewhere without copy-paste.
- **Consistent** — same style across the whole project, not different per file.

## 7–8. Detailed Concepts + Bad vs Good Examples

### A) Readability + Meaningful Naming + Magic Numbers

**The problem:** Unclear names and "magic" numbers with no meaning force the reader to guess your intent.

```php
// ❌ Bad
function calc($p, $d) {
    if ($d > 100) {
        return $p - ($p * 0.15);
    }
    return $p - ($p * 0.05);
}
```
**What's wrong?** `$p` and `$d` are meaningless, and `0.15`, `0.05`, `100` are magic numbers no one can decode without reading the full logic.

```php
// ✅ Good
const BULK_ORDER_THRESHOLD = 100;
const BULK_DISCOUNT_RATE = 0.15;
const STANDARD_DISCOUNT_RATE = 0.05;

function calculateDiscountedPrice(float $price, int $quantity): float
{
    $discountRate = $quantity > BULK_ORDER_THRESHOLD
        ? BULK_DISCOUNT_RATE
        : STANDARD_DISCOUNT_RATE;

    return $price - ($price * $discountRate);
}
```
**Why is it better?** `calculateDiscountedPrice` explains itself, and the constants explain the intent of every number — no comment needed to explain the code.

**Quick naming rules:**
- Functions: clear verbs (`getUser`, `calculateTotal`, `isValid`).
- Boolean variables: `is/has/can` (`isActive`, `hasPermission`).
- Avoid unclear abbreviations (`$d`, `$tmp`, `$data2`).

---

### B) Functions, SRP, Long Functions, Deep Nesting

**The problem:** One function doing too much (validation + business logic + persistence) with deep nesting.

```php
// ❌ Bad
function registerUser($request) {
    if ($request->email) {
        if (strlen($request->password) >= 8) {
            if (!User::where('email', $request->email)->exists()) {
                $user = new User();
                $user->email = $request->email;
                $user->password = bcrypt($request->password);
                $user->save();
                Mail::to($user->email)->send(new WelcomeEmail($user));
                return response()->json(['success' => true]);
            } else {
                return response()->json(['error' => 'Email exists'], 400);
            }
        } else {
            return response()->json(['error' => 'Weak password'], 400);
        }
    } else {
        return response()->json(['error' => 'Email required'], 400);
    }
}
```
**What's wrong?** The function handles validation, business logic, persistence, and email all at once, with 3 levels of nesting that are hard to follow, and it's responsible for more than one thing (violates SRP).

```php
// ✅ Good — Guard Clauses + Single Responsibility
function registerUser(RegisterRequest $request)
{
    $this->ensureEmailIsUnique($request->email);

    $user = $this->userService->create($request->validated());
    $this->notificationService->sendWelcomeEmail($user);

    return response()->json(['success' => true]);
}

function ensureEmailIsUnique(string $email): void
{
    if (User::where('email', $email)->exists()) {
        throw new EmailAlreadyExistsException();
    }
}
```
**Why is it better?**
- **Guard clauses** replace nesting: return early when something's wrong, so no nested `else` chains.
- Validation moved to `RegisterRequest` (a separate responsibility).
- Each function has one clear responsibility — the core of the **Single Responsibility Principle (SRP)**: a class/function should have one reason to change.

**Practical rule:** if you need "and" to describe your function ("it validates and saves and sends an email") — that's a sign it should be split.

---

### C) DRY, KISS, YAGNI

- **DRY (Don't Repeat Yourself):** duplicated logic in two places means you must remember to update both — a guaranteed source of bugs.
```php
// ❌ The same email-validation logic repeated in 3 places
if (!preg_match('/^[^\s@]+@[^\s@]+\.[^\s@]+$/', $email)) { ... }
```
```php
// ✅ One function/rule used everywhere
function isValidEmail(string $email): bool {
    return (bool) preg_match('/^[^\s@]+@[^\s@]+\.[^\s@]+$/', $email);
}
```

- **KISS (Keep It Simple, Stupid):** the simplest solution that solves the problem is the best one — don't build a complex system for a simple problem.
```php
// ❌ Over-engineered for a fixed tax rate
class TaxCalculatorFactory {
    public function make(string $strategy): TaxStrategyInterface { ... }
}
```
```php
// ✅ If the tax rate is actually fixed, simplicity wins
function calculateTax(float $amount): float {
    return $amount * 0.16;
}
```

- **YAGNI (You Aren't Gonna Need It):** don't build a feature or add complexity "just in case you need it later" — build it when you actually need it.
> Example: don't build a full plugin system for a small project "just in case" someone asks for one extra feature next year — that's usually wasted time and complexity.

---

### D) Comments: When They Help and When They Hurt

```php
// ❌ A comment explaining bad code instead of fixing it
// check if user is active and has permission and not banned
if ($u->s == 1 && $u->p == 3 && $u->b == 0) { ... }
```
```php
// ✅ Self-explanatory code, no comment needed
if ($user->isActive() && $user->hasAdminPermission() && !$user->isBanned()) { ... }
```
**The rule:** a good comment explains **"why"** (a decision, a reason, a security note), not **"what"** — the code itself should already make the "what" clear. A comment explaining unclear code is a sign the code needs rewriting, not a comment.

---

### E) Error Handling + Input Validation

```php
// ❌ Bad — silent failure, no validation
function getUser($id) {
    $user = User::find($id);
    return $user->name; // crashes if $user is null
}
```
```php
// ✅ Good
function getUser(int $id): User
{
    $user = User::find($id);

    if (!$user) {
        throw new UserNotFoundException("User with id {$id} not found");
    }

    return $user;
}
```
**Why is it better?** The error is explicit and specific, and it surfaces exactly where it happened, instead of crashing somewhere far from the real cause.

**Input validation in Laravel:** use Form Requests instead of repeated manual checks in every controller:
```php
class RegisterRequest extends FormRequest {
    public function rules(): array {
        return [
            'email' => 'required|email|unique:users',
            'password' => 'required|min:8',
        ];
    }
}
```

---

### F) Separation of Concerns + Large Classes + Code Duplication

**The problem:** a "fat controller" doing everything — database queries, business logic, and response formatting.

```php
// ❌ Bad — everything in the controller
class OrderController {
    public function store(Request $request) {
        $order = new Order();
        $order->user_id = auth()->id();
        $order->total = $request->items->sum('price');
        if ($order->total > 500) { $order->total *= 0.9; }
        $order->save();
        Mail::to(auth()->user())->send(new OrderConfirmation($order));
        return response()->json($order);
    }
}
```
```php
// ✅ Good — each responsibility in its place
class OrderController {
    public function __construct(private OrderService $orderService) {}

    public function store(StoreOrderRequest $request) {
        $order = $this->orderService->createOrder(auth()->user(), $request->validated());
        return response()->json($order);
    }
}

class OrderService {
    public function createOrder(User $user, array $data): Order {
        $order = Order::create([...]);
        $this->applyDiscountIfEligible($order);
        $this->notifyCustomer($order);
        return $order;
    }
}
```
**Why is it better?** The controller only receives the request and returns a response — all business logic lives in the service. This is **Separation of Concerns**: each part of the system owns one layer (HTTP, business logic, data).

**Large classes** are usually the result of piling too many responsibilities into one class — the fix is the same idea: split by responsibility (Service, Repository, Policy...).

---

## Common Code Smells (Quick Summary)
| Smell | Sign | Fix |
|---|---|---|
| Long Function | Longer than one screen | Extract Function |
| Deep Nesting | More than 2–3 levels of if/for | Guard Clauses |
| Large Class | A class doing many unrelated things | Extract Class / SRP |
| Duplicated Code | Same logic in multiple places | Extract Function / DRY |
| Magic Numbers | Meaningless numbers in code | Named Constants |
| Long Parameter List | 5+ function parameters | Use an Object/DTO |

## Refactoring Techniques
- **Extract Function:** pull part of a large function into a well-named function.
- **Rename Variable/Function:** improve the name without changing behavior.
- **Replace Magic Number with Constant:** swap magic numbers for clear named constants.
- **Guard Clauses:** early returns instead of deep nesting.
- **Extract Class:** split a bloated class into smaller, focused ones.

## SOLID, Simplified for Junior Developers
> Note: we won't go into heavy theory — just the practical meaning of each letter.

- **S — Single Responsibility:** a class/function should have exactly one reason to change (shown above in the `OrderService` example).
- **O — Open/Closed:** code should be extendable without modifying existing code. Example: instead of `if ($type == 'credit') ... elseif ($type == 'paypal') ...` that you must edit every time you add a payment method, use an interface (`PaymentMethod`) with a separate class per method.
- **L — Liskov Substitution:** a subclass must be usable wherever its parent class is expected without breaking the program. (Simple example: if `Duck extends Bird` and all birds are expected to fly, but `Duck` can't fly — that breaks LSP.)
- **I — Interface Segregation:** don't force a class to implement methods it doesn't need. Prefer several small interfaces over one bloated one.
- **D — Dependency Inversion:** classes should depend on abstractions (interfaces), not concrete implementations directly — this makes swapping and testing much easier (e.g., `OrderService` depends on `PaymentGatewayInterface`, not `StripeGateway` directly).

## Clean Code in Team Environments + Review-Friendly Code
- Stick to one coding style across the team (PSR-12 or any agreed standard, enforced via linter/formatter).
- Small, focused PRs are far easier to review than a single 20-file PR.
- Function/variable names should be understandable to anyone on the team, not just you.
- Write code as if you're explaining it to a new team member.

## 10. Hands-on Exercises

**Exercise 1:** Identify the problems in this code and refactor it:
```php
function proc($arr) {
    $r = [];
    foreach ($arr as $i) {
        if ($i['s'] == 1) {
            if ($i['p'] > 0) {
                $r[] = $i['p'] * 1.16;
            }
        }
    }
    return $r;
}
```
*(Expected: clear naming, remove nesting, remove the magic number)*

**Exercise 2:** Identify the code smells in this class and propose a fix (SRP):
```php
class UserController {
    public function register($request) {
        // validation + save user + send email + log activity + generate report
    }
}
```

**Exercise 3:** Find the duplication (DRY) in this code and propose a fix:
```php
// Two different functions with the same coupon-validation logic copy-pasted between them
```

## 11. Final Challenge
Give participants a long function/class (50+ lines) containing: poor naming, deep nesting, magic numbers, duplicated code, no error handling, and every responsibility mixed into one place. The task: fully refactor it applying everything learned (SRP, DRY, KISS, Guard Clauses, Constants, Error Handling) and present a clean version with an explanation of why each change was made.

## 12. Common Mistakes
- Assuming Clean Code means "shorter code" — sometimes clean code is slightly longer but far clearer.
- Refactoring the entire codebase at once instead of incrementally.
- Over-applying SOLID literally on a simple project (over-engineering).
- Relying on comments instead of improving the code itself.

## 13. Best Practices
- Always ask: "If someone reads this code in 6 months, will they understand it quickly?"
- Refactor in small steps, and test after each step.
- Apply one principle at a time (you don't need to apply all of SOLID to everything at once).

## 14. Summary
Clean Code isn't a rigid rulebook — it's a way of thinking: write code that tells its own story. From clear naming, to small single-responsibility functions, to avoiding duplication and unnecessary complexity, to separating concerns — every principle serves one goal: code that anyone (including future-you) can understand and change with confidence.

## 15. Discussion Questions
- Look at a function you wrote in an old project — what are the first 3 things you'd change today?
- When can "complexity" actually be justified and not a code smell?
- Should SOLID always be applied, or are there cases where it becomes over-engineering?

## 16. Additional Resources
- *Clean Code* — Robert C. Martin
- *Refactoring* — Martin Fowler
- refactoring.guru — visual guide to code smells and refactoring techniques
- PHP-FIG PSR-12 Coding Standard
