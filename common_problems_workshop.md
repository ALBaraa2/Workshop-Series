# Common Problems in Software Development: Problems Every Developer Should Know
### Workshop Material — Bilingual (Arabic / English)

---

# الجزء الأول: بالعربي

## 1. عنوان الورشة
**Common Problems in Software Development: Problems Every Developer Should Know**

## 2. أهداف التعلّم
بنهاية الورشة، المشارك رح يقدر:
- يتعرّف على أشهر المشاكل بالـ Backend/Database/API/Security قبل ما توصل للإنتاج.
- يفهم **ليش** بتصير كل مشكلة، مش بس يحفظ حلها.
- يكتشف هاي المشاكل بكوده أو بكود فريقه قبل ما تصير bug حقيقي.
- يطبّق حل عملي لكل مشكلة، وياخد إجراء وقائي يمنعها بالمستقبل.
- يتبع منهجية منظّمة بالـ Debugging بدل التخبيط العشوائي.

## 3. المتطلبات المسبقة
- أساسيات برمجة + قواعد بيانات (SQL أساسي، Foreign Keys، Joins).
- معرفة أساسية بمفهوم API وHTTP.
- خبرة سابقة بكتابة Backend بسيط (Laravel/PHP أو أي framework مشابه).

## 4. الأجندة — 60 دقيقة
| الوقت | المحتوى |
|---|---|
| 0:00–0:05 | مقدمة + العقلية الصحيحة: "لاحظ قبل ما تصلح" |
| 0:05–0:15 | Database & Performance Problems |
| 0:15–0:25 | Backend & Application Logic Problems |
| 0:25–0:32 | API Problems |
| 0:32–0:42 | Security Problems |
| 0:42–0:46 | Development & Team Problems |
| 0:46–0:50 | منهجية Debugging منظّمة |
| 0:50–0:57 | تمارين عملية + التحدي النهائي |
| 0:57–1:00 | ملخّص + نقاش |

## 5. مقدمة (Introduction)
كتير مطورين Junior بيتعلموا "كيف نكتب كود يشتغل" — بس ما حد بيعلمهم "كيف نلاحظ إن الكود بده يصير مشكلة" قبل ما توصل للإنتاج وتصير كارثة (تسريب بيانات، سيرفر واقع، فاتورة استضافة ضخمة بسبب استعلامات بطيئة).

**العقلية المطلوبة بهاي الورشة:**
> "ما تتعلم بس تكتب كود — تعلم تلاحظ إمتى كودك بده يصير مشكلة."

كل مشكلة رح ناخدها بنفس المنهجية:
**شو المشكلة ← ليش بتصير ← كيف تكتشفها ← كيف تصلحها ← كيف تمنعها مستقبلاً.**

## 6. تصنيف المشاكل (Problem Categories)
1. **Database & Performance** — مشاكل بتبطّئ النظام أو تكلّف موارد زيادة.
2. **Backend & Application Logic** — مشاكل بمنطق البرنامج نفسه.
3. **API Problems** — مشاكل بتصميم وتواصل الـ API.
4. **Security** — ثغرات بتعرّض النظام والمستخدمين للخطر.
5. **Development & Team Problems** — مشاكل بعملية التطوير الجماعي نفسها.

---

## 7–8. المشاكل بالتفصيل + أمثلة واقعية

### القسم الأول: Database & Performance

#### 1) N+1 Query Problem
- **شو المشكلة:** بدل استعلام واحد لجلب بيانات مرتبطة، النظام بيسوي استعلام منفصل لكل عنصر — يعني N+1 استعلام بدل استعلام أو اثنين.
- **ليش بتصير:** استخدام Lazy Loading بدون انتباه — كل ما توصل لعلاقة (relationship) جوا loop، بيصير استعلام جديد.
- **مثال واقعي:** صفحة "كل الطلبات مع اسم العميل" — لو عندك 100 طلب، هيك بتصير 101 استعلام بدل استعلامين.
```php
// ❌ Bad — N+1
$orders = Order::all();
foreach ($orders as $order) {
    echo $order->customer->name; // استعلام منفصل لكل order
}
```
```php
// ✅ Good — Eager Loading
$orders = Order::with('customer')->get();
foreach ($orders as $order) {
    echo $order->customer->name; // كل البيانات جاية من استعلامين بس
}
```
- **كيف تكتشفها:** فعّل query log (Laravel Debugbar / Telescope)، أو راقب عدد الاستعلامات بصفحة معينة.
- **كيف تصلحها:** استخدم Eager Loading (`with()`) بدل Lazy Loading جوا loop.
- **كيف تمنعها مستقبلاً:** راجع الاستعلامات بالـ code review، فعّل أدوات مراقبة أداء (query count alerts) بالبيئة التطويرية.
- **لو تجاهلتها:** صفحة بتاخد ثواني بدل ميلي ثانية، وبتنهار كليًا مع نمو البيانات.

#### 2) Missing Indexes & Inefficient / Too Many Queries
- **شو المشكلة:** استعلامات بتفحص كل صفوف الجدول (Full Table Scan) لعدم وجود index، أو استعلامات مكتوبة بشكل غير فعّال، أو استدعاء قاعدة البيانات أكتر من اللازم.
- **ليش بتصير:** نسيان إضافة index على الأعمدة المستخدمة بـ `WHERE`/`JOIN`/`ORDER BY`، أو استعلامات جوا loops بدل batch queries.
- **مثال واقعي:** البحث عن مستخدم بالإيميل بجدول فيه مليون سجل بدون index — كل بحث بياخد ثواني.
```php
// ❌ Bad — بدون index على email + استعلام جوا loop
foreach ($emails as $email) {
    $user = DB::table('users')->where('email', $email)->first();
}
```
```php
// ✅ Good — index + استعلام واحد
// Migration: $table->index('email');
$users = DB::table('users')->whereIn('email', $emails)->get();
```
- **كيف تكتشفها:** `EXPLAIN` على الاستعلام لمعرفة إذا في Full Table Scan، أو مراقبة Slow Query Log.
- **كيف تصلحها:** ضيف index على الأعمدة المستخدمة بالفلترة، واستبدل loops من استعلامات بـ `whereIn`/batch queries.
- **كيف تمنعها مستقبلاً:** راجع خطة الاستعلام (`EXPLAIN`) لأي استعلام جديد بيتعامل مع جدول كبير، وثّق الأعمدة اللي لازم تتفهرس بالـ migration.
- **لو تجاهلتها:** الأداء بيتدهور تدريجيًا مع نمو البيانات، لحد ما ينهار النظام تحت الحمل.

#### 3) Over-fetching & Under-fetching
- **شو المشكلة:** **Over-fetching** = جلب بيانات أكتر بكتير مما محتاج (كل الأعمدة والعلاقات). **Under-fetching** = جلب بيانات ناقصة يخلي الـ frontend يسوي طلبات إضافية.
- **ليش بتصير:** استخدام `select *` بشكل افتراضي، أو تصميم API/query بدون التفكير بشو فعليًا محتاج المستهلك (consumer).
- **مثال واقعي:** صفحة قائمة منتجات بتحتاج بس (اسم، سعر، صورة)، بس الاستعلام بيجيب كل أعمدة الجدول + كل العلاقات.
```php
// ❌ Bad — Over-fetching
$products = Product::with('reviews', 'supplier', 'warehouse')->get();
```
```php
// ✅ Good — بس اللي محتاجينه
$products = Product::select('id', 'name', 'price', 'image')->get();
```
- **كيف تكتشفها:** راقب حجم الـ response وقارنه بشو فعليًا مستخدم بالـ frontend.
- **كيف تصلحها:** استخدم `select()` محددة، وGraphQL أو Resource Transformers لو الحاجة متكررة عبر endpoints مختلفة.
- **كيف تمنعها مستقبلاً:** صمّم كل endpoint حسب حاجة المستهلك الفعلية، مش "خد كل شي احتياطًا".
- **لو تجاهلتها:** استهلاك bandwidth وذاكرة زيادة، واستجابة أبطأ، وطلبات إضافية غير ضرورية للـ under-fetching.

#### 4) Unnecessary Data Loading & Pagination Mistakes
- **شو المشكلة:** تحميل كل سجلات جدول دفعة وحدة بدون Pagination، أو Pagination مكتوب بشكل غير فعّال (زي `OFFSET` كبير على جداول ضخمة).
- **ليش بتصير:** نسيان الـ Pagination بالـ MVP، أو عدم توقّع نمو البيانات.
- **مثال واقعي:** `GET /api/users` بترجّع 500,000 مستخدم بطلب وحد.
```php
// ❌ Bad
$users = User::all(); // كل الجدول!
```
```php
// ✅ Good
$users = User::paginate(20);
```
- **كيف تكتشفها:** راقب حجم الـ response وزمن الاستجابة مع نمو البيانات.
- **كيف تصلحها:** استخدم Pagination من أول يوم، وفكّر بـ Cursor Pagination للجداول الضخمة بدل Offset Pagination.
- **كيف تمنعها مستقبلاً:** خلّي Pagination جزء من الـ API design من البداية، مش إضافة لاحقة.
- **لو تجاهلتها:** استهلاك ذاكرة ضخم، تعليق السيرفر، وتجربة مستخدم سيئة.

#### 5) Caching Problems
- **شو المشكلة:** غياب الـ caching بالكامل (كل طلب بيضرب قاعدة البيانات)، أو caching خاطئ (بيانات قديمة/Stale Cache) ما بتنعكس بها التحديثات.
- **ليش بتصير:** إضافة cache بدون استراتيجية invalidation واضحة، أو الاعتماد على قاعدة البيانات لبيانات بتتغيّر نادرًا.
- **مثال واقعي:** صفحة "الأكثر مبيعًا" بتضرب قاعدة البيانات بكل زيارة رغم إن البيانات بتتحدث كل ساعة بس.
```php
// ❌ Bad — بدون cache
$topProducts = Product::orderBy('sales', 'desc')->limit(10)->get();
```
```php
// ✅ Good — مع cache واستراتيجية انتهاء واضحة
$topProducts = Cache::remember('top_products', now()->addHour(), function () {
    return Product::orderBy('sales', 'desc')->limit(10)->get();
});
```
- **كيف تكتشفها:** راقب عدد استعلامات قاعدة البيانات لبيانات مش بتتغيّر بسرعة.
- **كيف تصلحها:** استخدم `Cache::remember` مع مدة انتهاء منطقية، واعمل invalidation عند التحديث الفعلي للبيانات.
- **كيف تمنعها مستقبلاً:** حدّد من البداية أي بيانات "بتتغيّر نادرًا" ومرشحة للـ caching.
- **لو تجاهلتها:** حمل زايد على قاعدة البيانات، أو بيانات قديمة معروضة للمستخدم بدون داعي.

---

### القسم الثاني: Backend & Application Logic

#### 6) Race Conditions & Duplicate Operations
- **شو المشكلة:** عمليتين أو أكتر بيصير عليهم تنفيذ بنفس الوقت على نفس البيانات، فبتصير نتيجة غير متوقعة (زي خصم رصيد مرتين، أو حجز نفس المقعد لشخصين).
- **ليش بتصير:** عدم استخدام Locking أو Transactions عند التعامل مع عمليات حسّاسة بالتزامن (concurrency).
- **مثال واقعي:** مستخدم بيضغط زر "Checkout" مرتين بسرعة، فيصير طلبين بدل واحد.
```php
// ❌ Bad — race condition محتملة
$wallet = Wallet::find($id);
if ($wallet->balance >= $amount) {
    $wallet->balance -= $amount;
    $wallet->save();
}
```
```php
// ✅ Good — Database Transaction + Locking
DB::transaction(function () use ($id, $amount) {
    $wallet = Wallet::lockForUpdate()->find($id);
    if ($wallet->balance >= $amount) {
        $wallet->decrement('balance', $amount);
    }
});
```
- **كيف تكتشفها:** اختبار الحمل (concurrent requests)، أو ملاحظة نتائج غير منطقية بالبيانات (رصيد سالب، طلبات مكررة).
- **كيف تصلحها:** استخدم Database Transactions مع `lockForUpdate()`، أو Idempotency Keys لمنع تكرار العمليات.
- **كيف تمنعها مستقبلاً:** أي عملية بتلمس رصيد/مخزون/حجز لازم تكون جوا Transaction محمية بـ Locking من البداية.
- **لو تجاهلتها:** خسارة مالية مباشرة، بيانات غير متسقة، ثقة مستخدمين مهزوزة.

#### 7) Poor Error Handling & Improper Validation
- **شو المشكلة:** الأخطاء بتتبلع بصمت (silent failure)، أو ما في تحقق كافي من المدخلات قبل معالجتها.
- **ليش بتصير:** استعجال بالتطوير، الاعتماد على "المستخدم رح يدخل بيانات صحيحة".
- **مثال واقعي:** API بياخد `quantity` سالب أو نص بدل رقم، والنظام بيكمّل تنفيذ بدون ما يوقف.
```php
// ❌ Bad
function addToCart($productId, $quantity) {
    Cart::create(['product_id' => $productId, 'quantity' => $quantity]);
}
```
```php
// ✅ Good
function addToCart(AddToCartRequest $request) {
    // Validation جوا Form Request: quantity: required|integer|min:1
    Cart::create($request->validated());
}
```
- **كيف تكتشفها:** راجع الـ logs بحثًا عن استثناءات متجاهلة، اختبر Edge Cases يدويًا.
- **كيف تصلحها:** Validation صارم بمدخل الـ API، وException Handling واضح بيرجّع رسالة مفهومة بدل انهيار صامت.
- **كيف تمنعها مستقبلاً:** لا تثق بأي مدخل خارجي، تحقق دايمًا قبل المعالجة.
- **لو تجاهلتها:** بيانات فاسدة بقاعدة البيانات، أخطاء يصعب تتبّع مصدرها لاحقًا.

#### 8) Infinite Loops & Memory Issues
- **شو المشكلة:** حلقة ما بتوصل لحالة توقف (infinite loop)، أو تحميل بيانات ضخمة كلها بالذاكرة دفعة وحدة.
- **ليش بتصير:** شرط توقف خاطئ أو منسي، أو استخدام `->get()` على جدول ضخم بدل معالجته بدفعات (chunks).
- **مثال واقعي:** معالجة مليون سجل بحلقة `foreach` عادية بتحمّلهم كلهم بالذاكرة فيوقع السيرفر (Out of Memory).
```php
// ❌ Bad
$users = User::all(); // مليون سجل بالذاكرة
foreach ($users as $user) {
    // process...
}
```
```php
// ✅ Good — معالجة بدفعات
User::chunk(500, function ($users) {
    foreach ($users as $user) {
        // process...
    }
});
```
- **كيف تكتشفها:** مراقبة استهلاك الذاكرة (memory_get_usage)، أو ملاحظة تعليق العملية بدون استجابة.
- **كيف تصلحها:** استخدم `chunk()`/`cursor()` للجداول الضخمة، وتأكد من شرط توقف واضح بكل حلقة.
- **كيف تمنعها مستقبلاً:** أي معالجة لبيانات كبيرة لازم تكون بدفعات من البداية، مش تحميل كامل.
- **لو تجاهلتها:** انهيار السيرفر، فاتورة استضافة أعلى بسبب استهلاك موارد غير ضروري.

#### 9) Poor Architecture, Tight Coupling & Code Duplication
- **شو المشكلة:** كلاسات مترابطة بشكل زايد (Tight Coupling) بحيث تغيير بسيط بمكان بيكسر أماكن تانية، ومنطق مكرر بأكتر من مكان.
- **ليش بتصير:** كتابة كود سريع بدون تخطيط للهيكلية، الاعتماد المباشر على implementations محددة بدل abstractions.
- **مثال واقعي:** `OrderController` بيستدعي `StripePayment` مباشرة — أي تغيير لبوابة دفع تانية بده يعدّل كل مكان استخدمت فيه.
```php
// ❌ Bad — Tight Coupling
class OrderController {
    public function checkout() {
        $stripe = new StripePayment();
        $stripe->charge(...);
    }
}
```
```php
// ✅ Good — الاعتماد على Interface
class OrderController {
    public function __construct(private PaymentGatewayInterface $gateway) {}
    public function checkout() {
        $this->gateway->charge(...);
    }
}
```
- **كيف تكتشفها:** لاحظ لو تغيير بسيط بصف واحد بيتطلّب تعديل ملفات كتير غير مرتبطة مباشرة.
- **كيف تصلحها:** استخدم Interfaces وDependency Injection، وطبّق DRY لإزالة التكرار.
- **كيف تمنعها مستقبلاً:** فكّر بالـ Dependencies من البداية — "لو غيّرت هاد الجزء، شو غيره رح يتأثر؟"
- **لو تجاهلتها:** أي تغيير بسيط بصير مشروع كامل، وسرعة التطوير بتنخفض بشكل كبير مع الوقت.

---

### القسم الثالث: API Problems

#### 10) Poor API Design, Inconsistent Responses & Incorrect HTTP Status Codes
- **شو المشكلة:** API بترجّع أشكال response مختلفة بين endpoints، أو status codes غلط (زي 200 لعملية فشلت).
- **ليش بتصير:** غياب معايير موحّدة (API standards) بالفريق، كل مطور بيصمم على مزاجه.
- **مثال واقعي:** endpoint واحد بيرجّع الخطأ بـ `{error: "..."}` وendpoint تاني بـ `{message: "..."}` — الـ frontend لازم يتعامل مع كل حالة لحالها.
```php
// ❌ Bad — status code غلط + شكل غير موحّد
return response()->json(['error' => 'Not found'], 200);
```
```php
// ✅ Good — status code صحيح + شكل موحّد
return response()->json([
    'success' => false,
    'message' => 'Resource not found',
], 404);
```
- **كيف تكتشفها:** قارن الـ responses بين endpoints مختلفة، تحقق من الـ status codes مقابل الـ HTTP standard.
- **كيف تصلحها:** بنِ API Resource/Response format موحّد يُستخدم بكل مكان (زي Laravel API Resources).
- **كيف تمنعها مستقبلاً:** وثّق معيار الـ API (شكل النجاح، شكل الخطأ، status codes المستخدمة) من أول يوم بالمشروع.
- **لو تجاهلتها:** frontend هش وصعب الصيانة، وأخطاء صعب تشخيصها لأن status code مضلّل.

#### 11) Missing Pagination & Lack of Rate Limiting
- **شو المشكلة:** endpoints بترجّع كل البيانات بدون تحديد، وما في حد أقصى لعدد الطلبات المسموحة لكل مستخدم/IP.
- **ليش بتصير:** التركيز على "خلّي الـ API يشتغل" بدون تفكير بالاستخدام السيئ أو نمو البيانات.
- **مثال واقعي:** حد بيسوي script بيضرب API-ك آلاف المرات بالثانية فيوقع السيرفر لكل المستخدمين.
```php
// ❌ Bad — بدون rate limiting
Route::get('/api/products', [ProductController::class, 'index']);
```
```php
// ✅ Good — مع rate limiting
Route::middleware('throttle:60,1')->get('/api/products', [ProductController::class, 'index']);
```
- **كيف تكتشفها:** راقب عدد الطلبات لكل IP/مستخدم بفترة زمنية قصيرة.
- **كيف تصلحها:** فعّل Rate Limiting middleware، وطبّق Pagination إلزامي على أي endpoint بيرجّع قوائم.
- **كيف تمنعها مستقبلاً:** خلي Rate Limiting وPagination جزء أساسي من الـ API checklist قبل النشر.
- **لو تجاهلتها:** انهيار الخدمة (DoS)، استغلال الموارد من مستخدمين سيئي النية.

#### 12) Poor Authentication/Authorization Design
- **شو المشكلة:** الخلط بين "مين إنت" (Authentication) و"شو مسموحلك تعمل" (Authorization)، أو endpoints حساسة بدون حماية كافية.
- **ليش بتصير:** الاعتماد على تحقق بسيط بالـ frontend فقط، أو نسيان فحص الصلاحية بجانب السيرفر.
- **مثال واقعي:** `DELETE /api/users/5` بيشتغل لأي مستخدم مسجّل دخول، مش بس الأدمن.
```php
// ❌ Bad — بدون فحص صلاحية
Route::delete('/api/users/{id}', [UserController::class, 'destroy'])->middleware('auth');
```
```php
// ✅ Good — Authorization صريح
Route::delete('/api/users/{id}', [UserController::class, 'destroy'])
    ->middleware(['auth', 'can:delete,App\Models\User']);
```
- **كيف تكتشفها:** اختبر endpoints حساسة بحساب مستخدم عادي (مش أدمن) وشوف هل بينفّذ العملية.
- **كيف تصلحها:** استخدم Policies/Gates بشكل صريح على كل عملية حساسة، لا تثق بفحص الـ frontend لحاله.
- **كيف تمنعها مستقبلاً:** أي endpoint حساس لازم يمر بمراجعة أمنية: "مين بالضبط مسموحله يعمل هاد؟"
- **لو تجاهلتها:** أي مستخدم عادي ممكن يحذف/يعدّل بيانات مش إله، خرق أمني خطير.

---

### القسم الرابع: Security

#### 13) SQL Injection
- **شو المشكلة:** إدخال مستخدم بيندمج مباشرة بجملة SQL، فيقدر المهاجم يغيّر منطق الاستعلام بالكامل.
- **ليش بتصير:** بناء استعلامات SQL بـ string concatenation بدل استخدام Prepared Statements/ORM.
- **مثال واقعي:** إدخال `' OR '1'='1` بحقل الإيميل ممكن يخلي المهاجم يسجّل دخول بدون كلمة سر صحيحة.
```php
// ❌ Bad — عرضة لـ SQL Injection
$email = $_GET['email'];
DB::select("SELECT * FROM users WHERE email = '$email'");
```
```php
// ✅ Good — Parameter Binding
DB::select("SELECT * FROM users WHERE email = ?", [$email]);
// أو أفضل: استخدام Eloquent
User::where('email', $email)->first();
```
- **كيف تكتشفها:** راجع أي مكان بيبني SQL بـ string concatenation، استخدم أدوات فحص أمني (SAST tools).
- **كيف تصلحها:** استخدم ORM (Eloquent) أو Prepared Statements دايمًا — بدون استثناء.
- **كيف تمنعها مستقبلاً:** ممنوع نهائيًا دمج مدخلات المستخدم مباشرة بأي query، اجعلها قاعدة صارمة بالفريق.
- **لو تجاهلتها:** تسريب كامل لقاعدة البيانات، أو حذفها بالكامل — من أخطر الثغرات على الإطلاق.

#### 14) XSS (Cross-Site Scripting)
- **شو المشكلة:** عرض مدخل مستخدم بالصفحة بدون تنظيف (sanitize)، فيقدر المهاجم يحقن كود JavaScript ينفّذ بمتصفح ضحايا تانيين.
- **ليش بتصير:** الثقة بمدخلات المستخدم وعرضها كما هي بالـ HTML بدون escaping.
- **مثال واقعي:** حقل تعليقات بيعرض `<script>steal_cookies()</script>` وينفّذ عند أي زائر يشوف التعليق.
```html
<!-- ❌ Bad — عرض مباشر بدون escaping -->
<div>{!! $comment->body !!}</div>
```
```html
<!-- ✅ Good — escaping تلقائي -->
<div>{{ $comment->body }}</div>
```
- **كيف تكتشفها:** جرّب تدخل `<script>alert(1)</script>` بأي حقل نص وشوف هل بينفّذ.
- **كيف تصلحها:** استخدم escaping تلقائي (زي `{{ }}` بـ Blade)، ونظّف أي HTML قبل التخزين لو لازم تسمح بجزء منه.
- **كيف تمنعها مستقبلاً:** ما تستخدم `{!! !!}` أو ما يعادلها إلا لما تكون متأكد 100% إن المحتوى موثوق ومنظّف.
- **لو تجاهلتها:** سرقة جلسات مستخدمين (cookies/tokens)، تنفيذ أفعال باسمهم بدون علمهم.

#### 15) Mass Assignment
- **شو المشكلة:** السماح بتحديث أي عمود بالجدول عبر مدخل المستخدم مباشرة، حتى لو مش مفروض يتعدّل (زي `is_admin`).
- **ليش بتصير:** استخدام `$request->all()` مباشرة بعمليات create/update بدون تحديد الحقول المسموحة.
- **مثال واقعي:** مستخدم بيضيف `is_admin: true` بجسم الطلب وقت التسجيل، فيصير أدمن بدون صلاحية.
```php
// ❌ Bad — Mass Assignment
User::create($request->all());
```
```php
// ✅ Good — تحديد الحقول المسموحة صراحة
User::create($request->only(['name', 'email', 'password']));
// أو عبر $fillable/$guarded بالـ Model
```
- **كيف تكتشفها:** راجع كل استخدام لـ `->all()` بعمليات create/update، تحقق من `$fillable`/`$guarded` بكل Model.
- **كيف تصلحها:** حدّد `$fillable` بوضوح بكل Model، واستخدم `->only()`/`->validated()` بدل `->all()`.
- **كيف تمنعها مستقبلاً:** اجعل تحديد الحقول المسموحة خطوة إلزامية بأي Model جديد.
- **لو تجاهلتها:** تصعيد صلاحيات (Privilege Escalation) — مستخدم عادي يصير أدمن بضغطة زر.

#### 16) Broken Authentication & Broken Authorization
- **شو المشكلة:** ضعف بآلية تسجيل الدخول نفسها (Authentication) — زي tokens ما بتنتهي صلاحيتها، أو ثغرات بفحص الصلاحيات (Authorization) بعد تسجيل الدخول.
- **ليش بتصير:** تنفيذ آلية مصادقة/صلاحيات مخصصة (custom) بدل استخدام حلول مجرّبة (Laravel Sanctum/Passport)، أو نسيان فحص ownership بالبيانات.
- **مثال واقعي:** `GET /api/orders/123` بيرجّع تفاصيل الطلب لأي مستخدم مسجّل دخول، مش بس صاحب الطلب فعليًا (IDOR — Insecure Direct Object Reference).
```php
// ❌ Bad — بدون فحص ownership
public function show($id) {
    return Order::find($id);
}
```
```php
// ✅ Good — تحقق من الملكية
public function show($id) {
    $order = Order::findOrFail($id);
    abort_unless($order->user_id === auth()->id(), 403);
    return $order;
}
```
- **كيف تكتشفها:** جرّب توصل لبيانات مستخدم تاني بتغيير الـ ID بالرابط وإنت مسجّل بحساب مختلف.
- **كيف تصلحها:** استخدم مكتبات مصادقة موثوقة، وأضف فحص ownership/Policy لكل عملية على بيانات خاصة بمستخدم معيّن.
- **كيف تمنعها مستقبلاً:** كل endpoint بيرجّع/يعدّل بيانات لازم يسأل: "هل فعلاً هاد المستخدم إله حق يوصل لهاد المورد بالذات؟"
- **لو تجاهلتها:** أي مستخدم يقدر يشوف أو يعدّل بيانات مستخدمين تانيين — خرق خصوصية وأمان خطير.

#### 17) Exposing Sensitive Information & Poor Handling of Secrets
- **شو المشكلة:** كشف بيانات حساسة بالـ response (كلمات سر، tokens) أو رفع أسرار (API keys, DB credentials) على GitHub.
- **ليش بتصير:** إرجاع الـ Model كامل بدون فلترة، أو نسيان `.env` بـ `.gitignore`.
- **مثال واقعي:** `/api/users/1` بترجّع `password_hash` و`remember_token` مع باقي بيانات المستخدم.
```php
// ❌ Bad — كل شي مكشوف
return User::find($id);
```
```php
// ✅ Good — استخدام API Resource للتحكم بالمُرجَع
return new UserResource(User::find($id)); // بيحدد بالضبط شو يظهر
```
- **كيف تكتشفها:** افحص كل response من endpoints حساسة، وابحث بتاريخ الـ Git commits عن أي secret اتحط بالغلط.
- **كيف تصلحها:** استخدم API Resources/DTOs للتحكم الصريح بشكل الـ response، و`.env` + `.gitignore` للأسرار دايمًا.
- **كيف تمنعها مستقبلاً:** لا ترجّع Model مباشرة أبدًا بـ API عام، راجع `.gitignore` قبل أول commit بأي مشروع.
- **لو تجاهلتها:** سرقة هوية، اختراق حسابات، وصول غير مصرّح لقاعدة البيانات أو خدمات خارجية.

---

### القسم الخامس: Development & Team Problems

#### 18) Merge Conflicts & Poor Git Practices
- **شو المشكلة:** تعارضات دمج متكررة وصعبة الحل، غالبًا بسبب عادات Git سيئة.
- **ليش بتصير:** فروع (branches) طويلة العمر بدون مزامنة مع main، commits ضخمة، أكتر من شخص بيعدّل نفس الملف بنفس الوقت بدون تنسيق.
- **مثال واقعي:** فرع feature ضل مفتوح أسبوعين بدون sync مع main، ولما جا يدمج صار عنده عشرات التعارضات.
- **كيف تكتشفها:** لاحظ تكرار التعارضات الكبيرة وقت الـ merge كمؤشر على مشكلة بسير العمل.
- **كيف تصلحها:** `git pull --rebase` بشكل دوري من main، فروع قصيرة العمر، تواصل بالفريق قبل تعديل ملفات مشتركة كبيرة.
- **كيف تمنعها مستقبلاً:** commits صغيرة ومتكررة، دمج/rebase يومي مع main، تقسيم العمل بحيث ملفات متداخلة أقل ما يمكن.
- **لو تجاهلتها:** وقت ضايع بحل تعارضات، وخطر دمج خاطئ بيكسر كود شغّال.

#### 19) Lack of Code Review
- **شو المشكلة:** كود بيوصل للإنتاج بدون ما حد تاني يراجعه.
- **ليش بتصير:** ضغط الوقت، أو فريق صغير "كلنا بنعرف بعض ما محتاجين review".
- **كيف تكتشفها:** راجع سجل الـ PRs — كم منها اتدمج بدون أي approval أو تعليق حقيقي.
- **كيف تصلحها:** فعّل قاعدة إلزامية: PR ما بينضم إلا بـ approval واحد على الأقل.
- **كيف تمنعها مستقبلاً:** اجعل الـ Code Review جزء أساسي من workflow الفريق، مش خطوة اختيارية.
- **لو تجاهلتها:** أخطاء وثغرات وممارسات سيئة بتتراكم بدون ما حد يلاحظها، وانتشار "معرفة الكود" بين شخص واحد بس.

#### 20) Debugging Without a Systematic Approach & Fixing Symptoms Instead of Root Causes
- **شو المشكلة:** محاولة إصلاح "الأعراض" (زي إضافة `if` استثنائي لحالة معينة) بدل فهم السبب الجذري للمشكلة.
- **ليش بتصير:** ضغط الوقت، أو عدم اتباع منهجية واضحة بالـ debugging (رح نشرحها بالقسم الجاي).
- **مثال واقعي:** خطأ بيصير لمستخدم معيّن، فبيتصلّح بإضافة شرط خاص لهاد المستخدم بدل ما يُفهم ليش صار الخطأ أصلاً.
- **كيف تكتشفها:** لاحظ لو نفس نوع الـ bug بيرجع يظهر بأشكال مختلفة بأماكن مختلفة — علامة إن السبب الجذري ما انحل.
- **كيف تصلحها:** اسأل "ليش" عدة مرات لحد توصل للسبب الحقيقي (5 Whys)، مش بس تغطي العرض الظاهر.
- **كيف تمنعها مستقبلاً:** اتبع منهجية Debugging منظّمة دايمًا (القسم الجاي).
- **لو تجاهلتها:** نفس المشكلة بترجع بأشكال مختلفة، والكود بيمتلئ بـ "رقعات" مؤقتة متراكمة.

---

## 10. منهجية Debugging منظّمة
1. **Reproduce** — أعد إنتاج المشكلة بخطوات واضحة وثابتة.
2. **Isolate** — قلّص نطاق المشكلة (أي جزء بالضبط مسؤول؟).
3. **Check Logs & Data** — راجع الـ logs، الـ query log، وقيم المتغيرات الفعلية وقت المشكلة.
4. **Form a Hypothesis** — احتمال واضح لسبب المشكلة.
5. **Test the Hypothesis** — تحقق منه بشكل مباشر (breakpoint, log مؤقت, اختبار معزول).
6. **Fix the Root Cause** — عالج السبب الحقيقي مش العرض.
7. **Verify** — تأكد إن المشكلة انحلت فعليًا وما ظهرت مشاكل جديدة.
8. **Document** — وثّق السبب والحل لو مشكلة ممكن تتكرر أو تفيد الفريق.

## 9. تمارين عملية (Hands-on Exercises)

**تمرين 1 (N+1):** عندكم كود بيعرض قائمة تدوينات مع اسم الكاتب، وبياخد وقت طويل بالتحميل. لاقوا المشكلة، فسّروا السبب الجذري، واقترحوا حل.

**تمرين 2 (Security):** فحصوا هاد الكود ولاقوا الثغرة:
```php
$id = $_GET['id'];
DB::select("SELECT * FROM orders WHERE id = $id");
```

**تمرين 3 (Race Condition):** نظام حجز مقاعد بيسمح لشخصين يحجزوا نفس المقعد بنفس الثانية. اشرحوا السبب واقترحوا حل بالكود.

**تمرين 4 (API Design):** راجعوا هاد الـ response واقترحوا تحسينات:
```json
{"error": "no", "data": null}
// HTTP Status: 200
```

## 11. التحدي النهائي (Final Challenge)
عطوا المشاركين Controller كامل (endpoint لإدارة طلبات) فيه مشاكل مخفية متعددة بنفس الوقت: N+1 query، بدون validation، Mass Assignment، بدون فحص authorization، وstatus code غلط. المطلوب: يلاقوا كل مشكلة (من غير ما تنقال بالاسم)، يفسّروا السبب الجذري لكل وحدة، ويعيدوا كتابة الـ Controller بشكل صحيح وآمن وفعّال.

## 12. أفضل الممارسات (ملخّص عام)
- لا تثق بأي مدخل من المستخدم — تحقق دايمًا.
- افحص أي كود بيتعامل مع تزامن (concurrency) أو أموال/مخزون بعناية خاصة.
- استخدم أدوات مراقبة (query log, error tracking) من بداية المشروع، مش بعد ما تصير مشكلة.
- الأمان والأداء مو "إضافة أخيرة" — لازم يكونوا جزء من كل قرار تصميم.

## 13. الملخّص (Summary)
معظم المشاكل الكبيرة بالإنتاج مش نتيجة "قلة معرفة تقنية" — هي نتيجة عدم ملاحظة إشارات واضحة كانت موجودة من البداية: استعلام بطيء اتجاهل، مدخل ما اتفحص، صلاحية ما اتحقق منها. المطوّر المحترف مش بس بيكتب كود يشتغل، هو بيلاحظ هاي الإشارات قبل ما تتحول لمشكلة حقيقية.

## 14. أسئلة للنقاش
- شو أكبر مشكلة من هاي المشاكل صادفتوها (أو سمعتوا عنها) بمشروع حقيقي؟
- ليش بالرأيكم مشاكل الأمان بالذات بتتأجل كتير بالمشاريع الصغيرة؟ شو الحل؟
- كيف ممكن يصير Code Review فعّال أكتر باكتشاف هاي المشاكل بدري؟

## 15. مصادر إضافية
- OWASP Top 10 — owasp.org
- Laravel Documentation — Eloquent Performance, Security
- "Use The Index, Luke" — use-the-index-luke.com (فهم الـ database indexing)
- Laravel Telescope / Debugbar لمراقبة الاستعلامات

---
---

# Part 2 — English

## 1. Workshop Title
**Common Problems in Software Development: Problems Every Developer Should Know**

## 2. Learning Objectives
By the end of this workshop, participants will be able to:
- Recognize the most common Backend/Database/API/Security problems before they reach production.
- Understand **why** each problem happens, not just memorize its fix.
- Detect these problems in their own or their team's code before they become real bugs.
- Apply a practical fix for each problem, and take a preventive action to avoid it in the future.
- Follow a systematic debugging methodology instead of random trial and error.

## 3. Prerequisites
- Basic programming + database knowledge (basic SQL, foreign keys, joins).
- Basic understanding of APIs and HTTP.
- Prior experience building a simple backend (Laravel/PHP or a similar framework).

## 4. Agenda — 60 Minutes
| Time | Content |
|---|---|
| 0:00–0:05 | Intro + the right mindset: "Notice before you fix" |
| 0:05–0:15 | Database & Performance Problems |
| 0:15–0:25 | Backend & Application Logic Problems |
| 0:25–0:32 | API Problems |
| 0:32–0:42 | Security Problems |
| 0:42–0:46 | Development & Team Problems |
| 0:46–0:50 | Systematic Debugging Methodology |
| 0:50–0:57 | Practical exercises + Final Challenge |
| 0:57–1:00 | Summary + Discussion |

## 5. Introduction
Many junior developers learn "how to write code that works" — but no one teaches them "how to notice code that's about to become a problem" before it reaches production and becomes a disaster (a data leak, a downed server, a huge hosting bill from slow queries).

**The mindset for this workshop:**
> "Don't just learn to write code. Learn to recognize when your code is going wrong."

We'll approach every problem with the same method:
**What it is ← Why it happens ← How to detect it ← How to fix it ← How to prevent it.**

## 6. Problem Categories
1. **Database & Performance** — problems that slow down the system or waste resources.
2. **Backend & Application Logic** — problems in the program's own logic.
3. **API Problems** — problems in how the API is designed and communicates.
4. **Security** — vulnerabilities that put the system and users at risk.
5. **Development & Team Problems** — problems in the development process itself.

---

## 7–8. Detailed Problems + Real-World Examples

### Section 1: Database & Performance

#### 1) N+1 Query Problem
- **What it is:** Instead of one query to fetch related data, the system runs a separate query for every item — N+1 queries instead of one or two.
- **Why it happens:** Using lazy loading without care — every time you touch a relationship inside a loop, a new query fires.
- **Real-world example:** An "all orders with customer name" page — with 100 orders, this becomes 101 queries instead of two.
```php
// ❌ Bad — N+1
$orders = Order::all();
foreach ($orders as $order) {
    echo $order->customer->name; // a separate query per order
}
```
```php
// ✅ Good — Eager Loading
$orders = Order::with('customer')->get();
foreach ($orders as $order) {
    echo $order->customer->name; // all data from just two queries
}
```
- **How to detect it:** Enable query logging (Laravel Debugbar / Telescope), or monitor query counts on a given page.
- **How to fix it:** Use eager loading (`with()`) instead of lazy loading inside a loop.
- **How to prevent it:** Review query patterns in code review, enable query-count monitoring in development.
- **If ignored:** A page that should take milliseconds takes seconds, and it collapses entirely as data grows.

#### 2) Missing Indexes & Inefficient / Too Many Queries
- **What it is:** Queries that scan the entire table (full table scan) due to missing indexes, poorly written queries, or hitting the database more than necessary.
- **Why it happens:** Forgetting to index columns used in `WHERE`/`JOIN`/`ORDER BY`, or querying inside loops instead of using batch queries.
- **Real-world example:** Searching for a user by email in a table with a million rows and no index — every search takes seconds.
```php
// ❌ Bad — no index on email + query inside a loop
foreach ($emails as $email) {
    $user = DB::table('users')->where('email', $email)->first();
}
```
```php
// ✅ Good — index + one query
// Migration: $table->index('email');
$users = DB::table('users')->whereIn('email', $emails)->get();
```
- **How to detect it:** Run `EXPLAIN` on the query to check for a full table scan, or watch the slow query log.
- **How to fix it:** Add indexes on filtered columns, and replace query-in-loop patterns with `whereIn`/batch queries.
- **How to prevent it:** Review the query plan (`EXPLAIN`) for any new query touching a large table, document which columns need indexing in the migration.
- **If ignored:** Performance degrades gradually as data grows, until the system collapses under load.

#### 3) Over-fetching & Under-fetching
- **What it is:** **Over-fetching** = fetching far more data than needed (all columns and relations). **Under-fetching** = fetching too little data, forcing the frontend to make extra requests.
- **Why it happens:** Defaulting to `select *`, or designing the API/query without considering what the consumer actually needs.
- **Real-world example:** A product listing page needs only (name, price, image), but the query fetches every column plus every relation.
```php
// ❌ Bad — Over-fetching
$products = Product::with('reviews', 'supplier', 'warehouse')->get();
```
```php
// ✅ Good — only what's needed
$products = Product::select('id', 'name', 'price', 'image')->get();
```
- **How to detect it:** Compare response size against what the frontend actually uses.
- **How to fix it:** Use explicit `select()`, or GraphQL / resource transformers when this pattern repeats across endpoints.
- **How to prevent it:** Design every endpoint around the consumer's actual needs, not "grab everything just in case."
- **If ignored:** Wasted bandwidth and memory, slower responses, and unnecessary extra requests for the under-fetching case.

#### 4) Unnecessary Data Loading & Pagination Mistakes
- **What it is:** Loading an entire table's records at once with no pagination, or pagination implemented inefficiently (e.g. large `OFFSET` on huge tables).
- **Why it happens:** Skipping pagination in the MVP, or not anticipating data growth.
- **Real-world example:** `GET /api/users` returning 500,000 users in a single request.
```php
// ❌ Bad
$users = User::all(); // the whole table!
```
```php
// ✅ Good
$users = User::paginate(20);
```
- **How to detect it:** Monitor response size and response time as data grows.
- **How to fix it:** Use pagination from day one, and consider cursor pagination over offset pagination for very large tables.
- **How to prevent it:** Make pagination part of the API design from the start, not an afterthought.
- **If ignored:** Massive memory consumption, server hangs, and a poor user experience.

#### 5) Caching Problems
- **What it is:** Either no caching at all (every request hits the database), or caching done wrong — stale data that doesn't reflect updates.
- **Why it happens:** Adding a cache without a clear invalidation strategy, or relying on the database for data that rarely changes.
- **Real-world example:** A "top-selling products" page hits the database on every visit, even though the data only updates hourly.
```php
// ❌ Bad — no cache
$topProducts = Product::orderBy('sales', 'desc')->limit(10)->get();
```
```php
// ✅ Good — cached with a clear expiration
$topProducts = Cache::remember('top_products', now()->addHour(), function () {
    return Product::orderBy('sales', 'desc')->limit(10)->get();
});
```
- **How to detect it:** Watch for repeated database queries for data that doesn't change quickly.
- **How to fix it:** Use `Cache::remember` with a sensible expiration, and invalidate the cache when the underlying data actually changes.
- **How to prevent it:** Identify from the start which data "rarely changes" and is a good caching candidate.
- **If ignored:** Unnecessary database load, or stale data shown to users for no reason.

---

### Section 2: Backend & Application Logic

#### 6) Race Conditions & Duplicate Operations
- **What it is:** Two or more operations execute at the same time on the same data, producing an unexpected result (e.g. a balance deducted twice, or the same seat booked by two people).
- **Why it happens:** Not using locking or transactions for concurrency-sensitive operations.
- **Real-world example:** A user double-clicks "Checkout" quickly, creating two orders instead of one.
```php
// ❌ Bad — potential race condition
$wallet = Wallet::find($id);
if ($wallet->balance >= $amount) {
    $wallet->balance -= $amount;
    $wallet->save();
}
```
```php
// ✅ Good — Database Transaction + Locking
DB::transaction(function () use ($id, $amount) {
    $wallet = Wallet::lockForUpdate()->find($id);
    if ($wallet->balance >= $amount) {
        $wallet->decrement('balance', $amount);
    }
});
```
- **How to detect it:** Load testing (concurrent requests), or noticing illogical data results (negative balances, duplicate orders).
- **How to fix it:** Use database transactions with `lockForUpdate()`, or idempotency keys to prevent duplicate operations.
- **How to prevent it:** Any operation touching balance/inventory/booking must be wrapped in a transaction protected by locking from the start.
- **If ignored:** Direct financial loss, inconsistent data, and eroded user trust.

#### 7) Poor Error Handling & Improper Validation
- **What it is:** Errors fail silently, or input isn't sufficiently validated before being processed.
- **Why it happens:** Rushed development, assuming "the user will enter correct data."
- **Real-world example:** An API accepts a negative `quantity` or a string instead of a number, and the system keeps processing anyway.
```php
// ❌ Bad
function addToCart($productId, $quantity) {
    Cart::create(['product_id' => $productId, 'quantity' => $quantity]);
}
```
```php
// ✅ Good
function addToCart(AddToCartRequest $request) {
    // Validated inside a Form Request: quantity: required|integer|min:1
    Cart::create($request->validated());
}
```
- **How to detect it:** Review logs for silently swallowed exceptions, manually test edge cases.
- **How to fix it:** Strict input validation, and clear exception handling that returns an understandable message instead of a silent crash.
- **How to prevent it:** Never trust any external input — always validate before processing.
- **If ignored:** Corrupted data in the database, errors that are hard to trace back to their source later.

#### 8) Infinite Loops & Memory Issues
- **What it is:** A loop that never reaches a stopping condition, or loading massive data entirely into memory at once.
- **Why it happens:** A wrong or forgotten stop condition, or using `->get()` on a huge table instead of processing it in chunks.
- **Real-world example:** Processing a million records with a plain `foreach` loop loads them all into memory and crashes the server (out of memory).
```php
// ❌ Bad
$users = User::all(); // a million records in memory
foreach ($users as $user) {
    // process...
}
```
```php
// ✅ Good — process in chunks
User::chunk(500, function ($users) {
    foreach ($users as $user) {
        // process...
    }
});
```
- **How to detect it:** Monitor memory usage (`memory_get_usage`), or notice a process hanging with no response.
- **How to fix it:** Use `chunk()`/`cursor()` for large tables, and make sure every loop has a clear stopping condition.
- **How to prevent it:** Any processing of large datasets should be chunked from the start, never fully loaded.
- **If ignored:** Server crashes, higher hosting bills from unnecessary resource consumption.

#### 9) Poor Architecture, Tight Coupling & Code Duplication
- **What it is:** Classes overly dependent on each other (tight coupling) so a small change in one place breaks others, plus logic duplicated in multiple places.
- **Why it happens:** Writing code quickly without planning the architecture, depending directly on concrete implementations instead of abstractions.
- **Real-world example:** `OrderController` calls `StripePayment` directly — switching to another payment gateway means editing every place it's used.
```php
// ❌ Bad — Tight Coupling
class OrderController {
    public function checkout() {
        $stripe = new StripePayment();
        $stripe->charge(...);
    }
}
```
```php
// ✅ Good — depend on an interface
class OrderController {
    public function __construct(private PaymentGatewayInterface $gateway) {}
    public function checkout() {
        $this->gateway->charge(...);
    }
}
```
- **How to detect it:** Notice when a small one-line change requires editing many seemingly unrelated files.
- **How to fix it:** Use interfaces and dependency injection, and apply DRY to remove duplication.
- **How to prevent it:** Think about dependencies from the start — "if I change this, what else will it affect?"
- **If ignored:** Any small change turns into a large project, and development speed drops sharply over time.

---

### Section 3: API Problems

#### 10) Poor API Design, Inconsistent Responses & Incorrect HTTP Status Codes
- **What it is:** An API returning different response shapes across endpoints, or wrong status codes (e.g. 200 for a failed operation).
- **Why it happens:** No shared API standards across the team — every developer designs it their own way.
- **Real-world example:** One endpoint returns errors as `{error: "..."}` and another as `{message: "..."}` — the frontend has to handle each case separately.
```php
// ❌ Bad — wrong status code + inconsistent shape
return response()->json(['error' => 'Not found'], 200);
```
```php
// ✅ Good — correct status code + consistent shape
return response()->json([
    'success' => false,
    'message' => 'Resource not found',
], 404);
```
- **How to detect it:** Compare responses across different endpoints, check status codes against the HTTP standard.
- **How to fix it:** Build one shared API response format used everywhere (e.g. Laravel API Resources).
- **How to prevent it:** Document the API standard (success shape, error shape, status codes used) from day one of the project.
- **If ignored:** A fragile, hard-to-maintain frontend, and errors that are hard to diagnose because the status code is misleading.

#### 11) Missing Pagination & Lack of Rate Limiting
- **What it is:** Endpoints returning unbounded data, and no cap on how many requests a user/IP can make.
- **Why it happens:** Focusing on "make the API work" without considering misuse or data growth.
- **Real-world example:** Someone scripts thousands of requests per second against your API, taking the server down for everyone.
```php
// ❌ Bad — no rate limiting
Route::get('/api/products', [ProductController::class, 'index']);
```
```php
// ✅ Good — with rate limiting
Route::middleware('throttle:60,1')->get('/api/products', [ProductController::class, 'index']);
```
- **How to detect it:** Monitor request counts per IP/user within short time windows.
- **How to fix it:** Enable rate-limiting middleware, and enforce pagination on every list-returning endpoint.
- **How to prevent it:** Make rate limiting and pagination part of the standard API checklist before launch.
- **If ignored:** Service outages (DoS), resource abuse by bad actors.

#### 12) Poor Authentication/Authorization Design
- **What it is:** Confusing "who you are" (authentication) with "what you're allowed to do" (authorization), or sensitive endpoints without adequate protection.
- **Why it happens:** Relying on frontend-only checks, or forgetting to verify authorization server-side.
- **Real-world example:** `DELETE /api/users/5` works for any logged-in user, not just an admin.
```php
// ❌ Bad — no authorization check
Route::delete('/api/users/{id}', [UserController::class, 'destroy'])->middleware('auth');
```
```php
// ✅ Good — explicit authorization
Route::delete('/api/users/{id}', [UserController::class, 'destroy'])
    ->middleware(['auth', 'can:delete,App\Models\User']);
```
- **How to detect it:** Test sensitive endpoints with a regular (non-admin) account and see if the action succeeds.
- **How to fix it:** Use explicit policies/gates on every sensitive operation — never trust frontend checks alone.
- **How to prevent it:** Every sensitive endpoint should go through the question: "exactly who is allowed to do this?"
- **If ignored:** Any regular user could delete or modify data that isn't theirs — a serious security breach.

---

### Section 4: Security

#### 13) SQL Injection
- **What it is:** User input gets concatenated directly into a SQL statement, letting an attacker alter the query's logic entirely.
- **Why it happens:** Building SQL queries via string concatenation instead of prepared statements/ORM.
- **Real-world example:** Entering `' OR '1'='1` into an email field can let an attacker log in without a valid password.
```php
// ❌ Bad — vulnerable to SQL Injection
$email = $_GET['email'];
DB::select("SELECT * FROM users WHERE email = '$email'");
```
```php
// ✅ Good — Parameter Binding
DB::select("SELECT * FROM users WHERE email = ?", [$email]);
// or better: use Eloquent
User::where('email', $email)->first();
```
- **How to detect it:** Review any place building SQL via string concatenation; use static analysis (SAST) tools.
- **How to fix it:** Always use an ORM (Eloquent) or prepared statements — no exceptions.
- **How to prevent it:** Never concatenate user input directly into a query — make this a hard rule for the whole team.
- **If ignored:** Full database leak or deletion — one of the most dangerous vulnerabilities that exists.

#### 14) XSS (Cross-Site Scripting)
- **What it is:** User input is rendered on the page without sanitizing, letting an attacker inject JavaScript that runs in other victims' browsers.
- **Why it happens:** Trusting user input and rendering it raw into HTML without escaping.
- **Real-world example:** A comment field displays `<script>steal_cookies()</script>`, which runs for every visitor who views the comment.
```html
<!-- ❌ Bad — rendered raw without escaping -->
<div>{!! $comment->body !!}</div>
```
```html
<!-- ✅ Good — automatic escaping -->
<div>{{ $comment->body }}</div>
```
- **How to detect it:** Try entering `<script>alert(1)</script>` into any text field and see if it executes.
- **How to fix it:** Use automatic escaping (like `{{ }}` in Blade), and sanitize any HTML before storage if partial HTML must be allowed.
- **How to prevent it:** Never use `{!! !!}` or its equivalent unless you're 100% certain the content is trusted and sanitized.
- **If ignored:** Stolen user sessions (cookies/tokens), actions performed on users' behalf without their knowledge.

#### 15) Mass Assignment
- **What it is:** Allowing any table column to be updated directly from user input, even columns that should never be user-editable (like `is_admin`).
- **Why it happens:** Using `$request->all()` directly in create/update operations without restricting fields.
- **Real-world example:** A user adds `is_admin: true` to the registration request body and becomes an admin without authorization.
```php
// ❌ Bad — Mass Assignment
User::create($request->all());
```
```php
// ✅ Good — explicitly whitelist fields
User::create($request->only(['name', 'email', 'password']));
// or via $fillable/$guarded on the Model
```
- **How to detect it:** Review every use of `->all()` in create/update operations, check `$fillable`/`$guarded` on every model.
- **How to fix it:** Define `$fillable` clearly on every model, and use `->only()`/`->validated()` instead of `->all()`.
- **How to prevent it:** Make defining allowed fields a mandatory step for every new model.
- **If ignored:** Privilege escalation — a regular user becomes an admin with a single crafted request.

#### 16) Broken Authentication & Broken Authorization
- **What it is:** Weakness in the login mechanism itself (authentication) — e.g. tokens that never expire — or gaps in checking permissions after login (authorization).
- **Why it happens:** Building custom auth/authorization instead of using proven solutions (Laravel Sanctum/Passport), or forgetting to check data ownership.
- **Real-world example:** `GET /api/orders/123` returns order details to any logged-in user, not just the actual owner (IDOR — Insecure Direct Object Reference).
```php
// ❌ Bad — no ownership check
public function show($id) {
    return Order::find($id);
}
```
```php
// ✅ Good — ownership verified
public function show($id) {
    $order = Order::findOrFail($id);
    abort_unless($order->user_id === auth()->id(), 403);
    return $order;
}
```
- **How to detect it:** Try to access another user's data by changing an ID in the URL while logged in as a different account.
- **How to fix it:** Use trusted authentication libraries, and add ownership/policy checks to every operation on user-specific data.
- **How to prevent it:** Every endpoint returning or modifying data should ask: "does this specific user actually have the right to access this resource?"
- **If ignored:** Any user can view or modify other users' data — a serious privacy and security breach.

#### 17) Exposing Sensitive Information & Poor Handling of Secrets
- **What it is:** Sensitive data leaking in a response (password hashes, tokens) or secrets (API keys, DB credentials) getting pushed to GitHub.
- **Why it happens:** Returning a full model with no filtering, or forgetting `.env` in `.gitignore`.
- **Real-world example:** `/api/users/1` returns `password_hash` and `remember_token` alongside the rest of the user's data.
```php
// ❌ Bad — everything exposed
return User::find($id);
```
```php
// ✅ Good — control the output explicitly with an API Resource
return new UserResource(User::find($id)); // defines exactly what's exposed
```
- **How to detect it:** Inspect every response from sensitive endpoints, and search Git history for accidentally committed secrets.
- **How to fix it:** Use API Resources/DTOs to explicitly control response shape, and always keep secrets in `.env` + `.gitignore`.
- **How to prevent it:** Never return a raw model directly from a public API; check `.gitignore` before the first commit of any project.
- **If ignored:** Identity theft, account compromise, unauthorized access to the database or external services.

---

### Section 5: Development & Team Problems

#### 18) Merge Conflicts & Poor Git Practices
- **What it is:** Frequent, hard-to-resolve merge conflicts, usually caused by bad Git habits.
- **Why it happens:** Long-lived branches out of sync with main, huge commits, multiple people editing the same file at once without coordination.
- **Real-world example:** A feature branch stays open for two weeks without syncing with main, and when it's finally merged it has dozens of conflicts.
- **How to detect it:** Notice recurring large conflicts at merge time as a sign of a workflow problem.
- **How to fix it:** Regularly `git pull --rebase` from main, keep branches short-lived, coordinate before editing large shared files.
- **How to prevent it:** Small, frequent commits, daily merge/rebase with main, splitting work to minimize overlapping files.
- **If ignored:** Wasted time resolving conflicts, and the risk of a bad merge breaking working code.

#### 19) Lack of Code Review
- **What it is:** Code reaching production without anyone else reviewing it.
- **Why it happens:** Time pressure, or a small team assuming "we all know the code, we don't need review."
- **How to detect it:** Check the PR history — how many merged without any real approval or comment.
- **How to fix it:** Enforce a rule: no PR merges without at least one approval.
- **How to prevent it:** Make code review a core part of the team's workflow, not an optional step.
- **If ignored:** Bugs, vulnerabilities, and bad practices accumulate unnoticed, and code knowledge stays siloed in one person.

#### 20) Debugging Without a Systematic Approach & Fixing Symptoms Instead of Root Causes
- **What it is:** Trying to fix the "symptom" (like adding a special-case `if`) instead of understanding the root cause.
- **Why it happens:** Time pressure, or not following a clear debugging methodology (covered next).
- **Real-world example:** A bug affects one specific user, so it gets "fixed" by adding a special condition just for them, instead of understanding why it happened at all.
- **How to detect it:** Notice the same type of bug resurfacing in different forms and places — a sign the root cause was never resolved.
- **How to fix it:** Ask "why" repeatedly until you reach the real cause (5 Whys), not just patch the visible symptom.
- **How to prevent it:** Always follow a systematic debugging methodology (next section).
- **If ignored:** The same problem keeps returning in different shapes, and the codebase fills up with accumulated temporary patches.

---

## 10. Systematic Debugging Methodology
1. **Reproduce** — recreate the problem with clear, consistent steps.
2. **Isolate** — narrow down exactly which part is responsible.
3. **Check Logs & Data** — review logs, query logs, and actual variable values at the time of the issue.
4. **Form a Hypothesis** — a clear guess about the cause.
5. **Test the Hypothesis** — verify it directly (breakpoint, temporary log, isolated test).
6. **Fix the Root Cause** — address the real cause, not the symptom.
7. **Verify** — confirm the issue is actually resolved and no new issues appeared.
8. **Document** — record the cause and fix if the issue could recur or would help the team.

## 9. Hands-on Exercises

**Exercise 1 (N+1):** You have code that displays a list of posts with author names, and it's slow to load. Find the problem, explain the root cause, and propose a fix.

**Exercise 2 (Security):** Inspect this code and find the vulnerability:
```php
$id = $_GET['id'];
DB::select("SELECT * FROM orders WHERE id = $id");
```

**Exercise 3 (Race Condition):** A seat-booking system lets two people book the same seat at the same second. Explain the cause and propose a code-level fix.

**Exercise 4 (API Design):** Review this response and propose improvements:
```json
{"error": "no", "data": null}
// HTTP Status: 200
```

## 11. Final Challenge
Give participants a complete controller (an order-management endpoint) with multiple hidden problems at once: an N+1 query, no validation, mass assignment, no authorization check, and a wrong status code. The task: find every problem (without being told what they are), explain the root cause of each, and rewrite the controller correctly, securely, and efficiently.

## 12. Best Practices
- Never trust any user input — always validate.
- Give special scrutiny to any code dealing with concurrency or money/inventory.
- Use monitoring tools (query logs, error tracking) from the start of a project, not after a problem occurs.
- Security and performance aren't "add later" — they must be part of every design decision.

## 13. Summary
Most major production problems aren't caused by "lack of technical knowledge" — they're caused by missing clear warning signs that were there from the start: an ignored slow query, an unchecked input, an unverified permission. A professional developer doesn't just write code that works — they notice these signals before they turn into a real problem.

## 14. Discussion Questions
- What's the biggest problem from this list you've personally encountered (or heard about) in a real project?
- Why do you think security issues specifically get postponed so often in small projects? What's the fix?
- How can code review become more effective at catching these problems early?

## 15. Additional Resources
- OWASP Top 10 — owasp.org
- Laravel Documentation — Eloquent Performance, Security
- "Use The Index, Luke" — use-the-index-luke.com (understanding database indexing)
- Laravel Telescope / Debugbar for query monitoring
