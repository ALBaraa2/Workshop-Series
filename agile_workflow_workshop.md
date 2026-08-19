# Agile & Software Team Workflow: How Software Teams Build Products
### Workshop Material — Bilingual (Arabic / English)

---

# الجزء الأول: بالعربي

## 1. عنوان الورشة
**Agile & Software Team Workflow: How Software Teams Build Products**
(أجايل وسير عمل فريق البرمجيات: كيف بتبني الفرق منتجاتها)

## 2. أهداف التعلّم
بنهاية الورشة، المشارك رح يقدر:
- يفهم Agile ليش وجد، والفرق بينه وبين النموذج التقليدي (Waterfall).
- يفهم أدوار وأحداث Scrum بشكل عملي، مش نظري.
- يتتبّع رحلة المتطلب من Requirement لـ Epic لـ User Story لـ Task قابل للتنفيذ.
- يعرف بالضبط شو بده يعمل "يوم الاثنين الأول" لما ينضم لفريق تطوير حقيقي.
- يتعاون بـ Git بشكل احترافي: branches، commits، Pull Requests، حل التعارضات.
- يعطي ويستقبل Code Review بشكل بنّاء ومهني.
- يتواصل بفعالية بالفريق: يبلّغ عن bug، يشرح blocker، يقدّر مهمة، يعبّر عن رأي مختلف باحترام.

## 3. المتطلبات المسبقة
- أساسيات Git (init, commit, push) — تغطّت بورشة Developer Toolkit.
- فكرة عامة عن SRS وUser Stories — تغطّت بورشة Software Requirements.
- لا حاجة لخبرة سابقة بالعمل ضمن فريق حقيقي.

## 4. الأجندة — 60 دقيقة
| الوقت | المحتوى |
|---|---|
| 0:00–0:05 | مقدمة: Agile مقابل Waterfall + Agile Manifesto |
| 0:05–0:12 | Scrum: الأدوار والأحداث |
| 0:12–0:18 | من Requirement لـ Epic لـ User Story لـ Task |
| 0:18–0:26 | Developer Workflow: يوم الاثنين الأول |
| 0:26–0:34 | Git Collaboration + Pull Requests |
| 0:34–0:40 | Code Review: كيف تعطي وتستقبل feedback |
| 0:40–0:45 | Team Communication: bugs, blockers, estimation |
| 0:45–0:55 | محاكاة فريق كاملة (Team Simulation) |
| 0:55–0:58 | التحدي النهائي |
| 0:58–1:00 | ملخّص + نقاش |

---

## 5. مقدمة: Agile

### شو هو Agile؟
Agile مش أداة ولا framework محدد — هو **طريقة تفكير** بتطوير البرمجيات بشكل تدريجي (Incremental) وتكراري (Iterative)، بدل تسليم المنتج كامل دفعة وحدة بنهاية مشروع طويل.

### ليش وجد Agile؟
بالنموذج التقليدي (Waterfall)، بتجمع كل المتطلبات بالبداية، تصمم، تطور، تختبر، وتسلّم — كل مرحلة بعد ما تخلص التانية. المشكلة: العميل بيشوف المنتج أول مرة بعد شهور، ولو في تغيير بالسوق أو بالفهم — التصحيح مكلف جدًا ومتأخر.

### Waterfall مقابل Agile
| Waterfall | Agile |
|---|---|
| كل المتطلبات تتحدد بالبداية وتُثبّت | المتطلبات ممكن تتطور مع الوقت بناءً على Feedback |
| تسليم واحد بنهاية المشروع (شهور) | تسليمات صغيرة متكررة (كل أسبوعين مثلًا) |
| العميل بيشوف النتيجة متأخر | العميل بيشوف ويجرّب نسخ عاملة بدري وباستمرار |
| تغيير المتطلبات مكلف ومربك | التغيير متوقّع ومُدار كجزء من العملية |

### Agile Manifesto — الفكرة الجوهرية
Agile Manifesto (2001) بيلخّص أولويات فرق التطوير الحديثة:
- الأفراد والتفاعل بينهم أهم من الأدوات والعمليات الجامدة.
- برنامج يشتغل فعليًا أهم من توثيق ضخم ما حد بيقراه.
- التعاون مع العميل أهم من التفاوض على تفاصيل عقد جامدة.
- الاستجابة للتغيير أهم من الالتزام الحرفي بخطة ثابتة.

> ملاحظة: هاد مش يعني "التوثيق والخطة مش مهمين" — يعني الأولوية بالتوازن لصالح المرونة والقيمة الفعلية.

### Iterative & Incremental Development
- **Incremental:** بتبني المنتج بأجزاء صغيرة تشتغل فعليًا (مش نسخة كاملة ناقصة).
- **Iterative:** بترجع على نفس الجزء وتحسّنه بناءً على Feedback حقيقي، بدل ما تحاول توصل "للكمال" من أول مرة.

---

## 6. Scrum

Scrum هو الـ Framework الأكتر انتشارًا لتطبيق Agile عمليًا.

### الأدوار (Roles)
- **Product Owner (PO):** بيمثّل صوت العميل/العمل. بيحدد **شو** المطلوب بناؤه وبأي أولوية — مش **كيف** يُبنى تقنيًا. مسؤول عن الـ Product Backlog.
- **Scrum Master:** ميسّر العملية، بيشيل العوائق (Blockers) عن طريق الفريق، بيحمي وقت وتركيز الفريق. **مش "بوس" أو مدير مباشر للمطورين.**
- **Developers:** فريق متعدد المهارات (Backend, Frontend, QA...) مسؤول جماعيًا عن بناء واختبار وتسليم زيادة (Increment) شغّالة من المنتج.

### Product Backlog
قائمة مرتّبة حسب الأولوية بكل شي ممكن يُبنى بالمنتج — features، bug fixes، تحسينات تقنية. بتتغيّر وتترتّب من جديد باستمرار.

### Sprint
فترة زمنية ثابتة (غالبًا أسبوعين) الفريق فيها بيلتزم ببناء زيادة شغّالة من المنتج.

### Sprint Planning
اجتماع ببداية الـ Sprint: الفريق بيختار عناصر من الـ Backlog للـ Sprint هاد، وبيقسّمها لمهام (Tasks) قابلة للتنفيذ.

### Daily Scrum (Standup)
اجتماع قصير جدًا (15 دقيقة)، يوميًا، ثلاث أسئلة بس: شو سويت أمس؟ شو رح أسوي اليوم؟ في عائق (Blocker) واقفني؟ **مش تقرير للمدير — هو تزامن بين الفريق.**

### Sprint Review
بنهاية الـ Sprint: الفريق بيعرض (Demo) الزيادة الشغّالة فعليًا لـ Stakeholders، وبياخد Feedback مباشر.

### Sprint Retrospective
اجتماع داخلي للفريق (بدون stakeholders خارجيين): شو اشتغل منيح؟ شو ما اشتغل؟ شو رح نغيّر بالـ Sprint الجاي؟ هدفه تحسين **العملية**، مش تقييم أشخاص.

---

## 7. من Requirements لـ User Stories لـ Tasks

بورشة SRS اتعلمنا نحوّل فكرة غامضة لمتطلبات واضحة. بـ Agile، هاي المتطلبات بتتحوّل لعمل قابل للتنفيذ بخطوات:

**Requirement → Epic → User Story → Task → Acceptance Criteria**

- **Epic:** مجموعة عمل كبيرة، أكبر من إنها تتخلّص بـ Sprint وحد. مثال: *"Volunteer Task Management"* (من مشروع Volunteer Management System اللي شفناه بورشة SRS).
- **User Story:** جزء أصغر من الـ Epic، بيندمج بـ Sprint وحد. مثال: *"As a volunteer, I want to browse and sign up for tasks near my location."*
- **Task:** تقسيم تقني للـ Story — كل Task بياخده مطوّر محدد. مثال:
  - Task 1: بناء `GET /api/tasks?location=` (Backend).
  - Task 2: بناء واجهة قائمة المهام مع فلتر الموقع (Frontend).
  - Task 3: كتابة اختبارات للـ endpoint (QA/Backend).
- **Acceptance Criteria:** شروط الاكتمال الواضحة (زي ما شفنا بورشة SRS — Given/When/Then).

> **نقطة أساسية:** المطوّر بالغالب ما بيشتغل مباشرة على "Requirement" ضخم — بيشتغل على **Task** واضح ومحدد، جزء من Story، جزء من Epic، جزء من متطلب أكبر.

---

## 8. Developer Workflow: يوم الاثنين الأول

هاد بالضبط شو بيصير لما تنضم لفريق تطوير حقيقي وتاخد أول Task:

1. **استلام User Story** — من أداة إدارة المهام (Jira, Trello, GitHub Projects).
2. **فهم المتطلب** — اقرأ الـ Story والـ Acceptance Criteria كاملين قبل ما تكتب أي سطر كود.
3. **اسأل أسئلة توضيحية** — لو في غموض، اسأل الـ PO أو زميلك **قبل** ما تبلش، مش بعد ما تخلّص وتكتشف إنك فهمت غلط.
4. **استلام/إنشاء Task** — تقسيم تقني واضح إذا لسا ما انعمل.
5. **إنشاء Git Branch** — فرع خاص للـ Task هاد (`feature/task-location-filter`).
6. **التنفيذ (Implement)** — اكتب الكود مع مراعاة مبادئ Clean Code.
7. **الاختبار (Test)** — اختبر محليًا (Postman للـ API، اختبار يدوي للواجهة).
8. **Commit** — commits صغيرة برسائل واضحة.
9. **Push** — ادفع الفرع لـ GitHub.
10. **إنشاء Pull Request** — وصف واضح لشو تغيّر وليش.
11. **Code Review** — زميل بيراجع الكود.
12. **معالجة الملاحظات** — عدّل بناءً على الـ feedback.
13. **Merge** — بعد الموافقة، الفرع بينضم لـ main.
14. **Deploy** — النشر (تلقائي عبر CI/CD أو يدوي).
15. **المراقبة (Monitor)** — تابع الـ logs/الأخطاء بعد النشر — مسؤوليتك ما بتخلص عند الـ merge.

> لاحظ: هاي بالضبط نفس الأدوات اللي اتعلمناها بورشة **Developer Toolkit** (Git, GitHub, Postman) — وهون بيشتغلوا سوا كسلسلة وحدة بسياق فريق حقيقي.

---

## 9. Git & Team Collaboration

### استراتيجية Branching مبسّطة
- **`main`:** دايمًا كود شغّال وجاهز للنشر — ما حد بيدفع له مباشرة.
- **Feature Branches:** فرع منفصل لكل Task/Story (`feature/...`, `fix/...`).

### رسائل Commit جيدة
```bash
# ❌ Bad
git commit -m "fix"
git commit -m "changes"

# ✅ Good
git commit -m "Add location filter to tasks API endpoint"
git commit -m "Fix null pointer error in volunteer signup flow"
```
قاعدة: صيغة أمرية (Imperative)، واضحة، توصف **شو** تغيّر بجملة وحدة.

### ليش ما ندفع مباشرة على main؟
- main لازم يضل شغّال دايمًا — أي مطوّر تاني أو الـ CI/CD بيعتمد عليه.
- الدفع المباشر بيلغي فرصة الـ Code Review قبل ما الكود يوصل للإنتاج.
- بيصعّب تتبّع أي تغيير سبّب مشكلة.

### حل تعارضات الدمج (Merge Conflicts)
- اسحب (`pull --rebase`) من main بشكل متكرر عشان التعارضات تضل صغيرة.
- لو صار تعارض: افهم **ليش** الكودين بيختلفوا (مش بس تختار نسخة عشوائي)، وتواصل مع زميلك لو مو واضح.
- بعد الحل، اختبر الكود من جديد قبل ما تكمل.

---

## 10. Pull Requests

### عناصر PR جيد
- **عنوان واضح** يوصف التغيير.
- **وصف** يشرح: شو تغيّر، ليش، وكيف تختبره.
- **رابط** للـ Task/Story المرتبطة (`Closes #45`).
- **حجم صغير ومركّز** — تغيير واحد منطقي، مش 20 ملف غير مترابطين.
- **Reviewers محددين** — مش "بعت لكل الفريق واللي يشوفه يشوفه".

```markdown
## What
Added a location filter to the tasks list endpoint.

## Why
Volunteers requested seeing only tasks near their area (User Story #12).

## How to test
1. GET /api/tasks?location=Gaza
2. Confirm only tasks in Gaza are returned

Closes #45
```

---

## 11. Code Review

### ليش موجود؟
- اكتشاف أخطاء بدري (قبل الإنتاج).
- نشر معرفة الكود بين الفريق — مش شخص واحد بس عارف كل شي.
- الحفاظ على جودة واتساق الكود.

### شو بيراجع الـ Reviewer؟
الصحة المنطقية، القراءة والوضوح، وجود اختبارات، الحالات الحدّية (Edge Cases)، مخاطر أمنية واضحة.

### شو المفروض المطوّر يتوقّعه؟
Feedback على **الكود**، مش على **شخصه**. ملاحظات بالـ review طبيعية وصحية، مش دليل ضعف.

### كيف تعطي Feedback بنّاء
```
❌ "هاد الكود غلط."
✅ "ممكن هون تصير مشكلة لو الـ array فاضي — شو رأيك نضيف تحقق قبل الحلقة؟"
```
كن محدد، اشرح "ليش"، اقترح بدل ما تأمر، وانوّه على الأجزاء الجيدة كمان مش بس الملاحظات.

### كيف تستقبل Feedback بمهنية
- ما تاخدها شخصي — الهدف تحسين الكود، مش تقييمك.
- اسأل لو الملاحظة مش واضحة، بدل ما تفترض أو تتضايق.
- اشكر المراجع — وقته صرف عشان يحسّن شغلك.

### أخطاء شائعة بالـ Code Review
- التركيز بس على تفاصيل شكلية (تنسيق) وتجاهل مشاكل حقيقية.
- موافقة (Approve) بدون قراءة فعلية للكود.
- وصف PR فاضي أو غير واضح بيصعّب المراجعة من الأساس.

---

## 12. Team Communication

### كيف تسأل سؤال تقني جيد
```
❌ "الكود مش شغال، ساعدوني."
✅ "بحاول أعمل GET request لـ /api/tasks وبرجعلي 500 error.
    جربت X وY. هاد الـ error message: [...]. أي أفكار؟"
```
اعطِ سياق كافي: شو حاولت، شو النتيجة، شو رسالة الخطأ بالضبط.

### كيف تكتب تقرير Bug جيد
- **خطوات إعادة الإنتاج (Steps to Reproduce)** واضحة ومرقّمة.
- **النتيجة المتوقعة مقابل الفعلية.**
- **البيئة** (متصفح، نظام تشغيل، بيئة تطوير/إنتاج).
- **Screenshot أو log** لو ممكن.

### كيف تشرح Blocker
قول إنك متوقّف **بأول يوم توقّفت فيه**، مش بعد يومين صمت. بالـ Daily Standup: "متوقّف على X، محتاج مساعدة من Y."

### تقدير المهام (Estimation)
تقدير نسبي (Story Points: 1, 2, 3, 5, 8) بدل ساعات دقيقة — لأن التقدير الدقيق صعب، والمقارنة النسبية بين المهام أسهل وأدق بالممارسة.

### التواصل والتوثيق
- حدّث حالة مهمتك بأداة الفريق يوميًا، ما تستنى حد يسألك.
- وثّق "ليش" القرار اتخذ (بـ PR description أو تعليق)، مش بس "شو" اتعمل.
- الخلاف بالرأي التقني طبيعي وصحي — ناقش الفكرة، مش الشخص.
- **المسؤولية (Ownership):** مسؤوليتك عن الكود ما بتخلص عند الـ merge — تابعه لحد ما يستقر بالإنتاج.

---

## 13. محاكاة فريق كاملة (Practical Team Simulation)

### تعليمات للمدرّب
قسّم المشاركين لمجموعات من 5: **Product Owner, Scrum Master, Backend Developer, Frontend Developer, QA.**

**المشروع:** ميزة "Task Sign-Up" من مشروع **Volunteer Management System** (نفس المشروع من ورشة SRS).

**خطوات المحاكاة (وقت مقترح لكل خطوة):**

| # | الخطوة | الوقت | المطلوب |
|---|---|---|---|
| 1 | Backlog Creation | 3 د | الـ PO يكتب 3 عناصر Backlog للميزة، مرتّبة بالأولوية |
| 2 | كتابة User Stories | 3 د | الفريق يحوّل عنصرين لـ User Stories بصيغة قياسية |
| 3 | Sprint Planning | 3 د | اختيار Story واحدة لـ"sprint" المحاكاة، تقسيمها لـ Tasks، تقدير بسيط |
| 4 | Task Assignment | 1 د | Backend Dev ياخد task الـ API، Frontend ياخد task الواجهة، QA يحضّر حالات اختبار |
| 5 | Development Workflow | 3 د | كل مطوّر يكتب (على ورقة/لوح) اسم الفرع + وصف مختصر لشو "نفّذه" |
| 6 | Pull Request | 2 د | كتابة وصف PR كامل حسب القالب |
| 7 | Code Review | 2 د | زميل تاني (أو QA) يراجع الوصف/الكود المفترض ويعطي ملاحظة بنّاءة وحدة على الأقل |
| 8 | Bug Report | 2 د | المدرّب يعطي bug مخفي، QA يكتب تقرير bug صحيح |
| 9 | Sprint Review | 2 د | الفريق "يعرض" الميزة للـ PO (30 ثانية تقديم) |
| 10 | Retrospective | 2 د | كل عضو يقول شي واحد "اشتغل منيح" وشي واحد "لازم يتحسّن" |

**ملاحظات للمدرّب:** كون جاهز تلعب دور "العميل" لو فريق سأل سؤال توضيحي أثناء كتابة الـ Stories. شجّع الفرق يلتزموا بالوقت المحدد لكل خطوة لمحاكاة ضغط الـ Sprint الحقيقي.

---

## 14. تمارين عملية إضافية (Exercises)

1. **حوّلوا** هاد المتطلب لـ User Story: *"النظام لازم يسمح للمنسّق يرفض تسجيل متطوع."*
2. **قسّموا** User Story لـ 3 Tasks تقنية واضحة.
3. **قدّروا** هاي المهام نسبيًا (Story Points): إضافة زر بسيط / بناء نظام تنبيهات كامل / تعديل نص بالواجهة.
4. **قارنوا** رسالتي commit وحددوا الأفضل: `"update"` مقابل `"Fix crash when volunteer profile has no phone number"`.
5. **راجعوا** وصف PR فاضي (`"fixed stuff"`) واقترحوا نسخة محسّنة.
6. **تعارض دمج:** زميلين عدّلوا نفس السطر بملف الإعدادات بنفس الوقت — كيف تتعاملوا؟
7. **Blocker:** إنت متوقّف على API لسا ما جهز من فريق تاني — اكتبوا كيف تشرحوها بالـ Daily Standup.
8. **اكتبوا bug report كامل** لوصف غامض: "الصفحة مش شغالة."
9. **Retro مصغّرة بالثنائي:** كل واحد يشارك شي واحد "نبدأ نعمله" وشي واحد "نوقف نعمله" لـ sprint وهمي.

## 15. الأخطاء الشائعة
- الدفع المباشر على main بدون PR أو review.
- Pull Requests ضخمة بتشمل تغييرات غير مترابطة.
- الصمت على Blocker لحد ما يصير متأخر جدًا.
- أخذ ملاحظات الـ Code Review بشكل شخصي.
- Standup بيتحوّل لتقرير للمدير بدل تزامن بين الفريق.
- تخطي الـ Retrospective أو تحويلها لجلسة لوم بدل تحسين.

## 16. أفضل الممارسات
- Sprints وPRs صغيرة أسهل بكتير من كبيرة.
- تواصل بدري وبشكل متكرر — الصمت أخطر من "سؤال غبي".
- وثّق "ليش" بالإضافة لـ"شو".
- الملكية (Ownership) بتمتد بعد الـ merge لحد الاستقرار بالإنتاج.
- التقدير النسبي (Story Points) أفضل من محاولة تخمين ساعات دقيقة.

## 17. التحدي النهائي (Final Challenge)
بنفس مجموعات المحاكاة: عطوهم ميزة جديدة صغيرة ("إضافة خانة بحث لقائمة المهام"). خلال 20 دقيقة، لازم يمروا بالسلسلة كاملة بشكل مضغوط: User Story → Tasks → تقدير → "تطوير" → PR → Review → اكتشاف bug → إصلاح → Sprint Review → Retro — وبعدين يعرضوا الرحلة كاملة أمام باقي المشاركين خلال دقيقة وحدة.

## 18. الملخّص (Summary)
Agile وScrum مش مصطلحات نظرية تُحفظ — هما إطار عملي بيحدد كيف بيشتغل فريق تطوير حقيقي يوميًا: من متطلب غامض، لـ Story واضحة، لـ Task محدد، لكود مُراجَع ومنشور ومراقَب. لما تنضم لفريقك الأول، السؤال مش "شو هو Scrum؟" — السؤال "شو Task-ي اليوم، ومين بحتاج أتواصل معه، وشو الخطوة الجاية؟"

## 19. أسئلة للنقاش
- شو الفرق العملي بين Scrum Master و"مدير مباشر"؟
- ليش ممكن فريق يتجاهل الـ Retrospective؟ شو بيخسر لو سوى هيك؟
- كيف كنت بتتعامل مع زميل ياخد ملاحظات الـ Code Review بشكل شخصي؟
- هل Agile مناسب دايمًا؟ في حالات النموذج التقليدي (Waterfall) بيكون أفضل؟

## 20. مصادر إضافية
- Scrum Guide الرسمي — scrumguides.org
- Agile Manifesto — agilemanifesto.org
- Conventional Commits — conventionalcommits.org
- GitHub Flow — docs.github.com

---
---

# Part 2 — English

## 1. Workshop Title
**Agile & Software Team Workflow: How Software Teams Build Products**

## 2. Learning Objectives
By the end of this workshop, participants will be able to:
- Understand why Agile exists and how it differs from the traditional Waterfall model.
- Understand Scrum roles and events in practical, not just theoretical, terms.
- Trace the journey of a requirement from Requirement to Epic to User Story to an actionable Task.
- Know exactly what to do on their "first Monday" joining a real development team.
- Collaborate professionally using Git: branches, commits, Pull Requests, resolving conflicts.
- Give and receive Code Review feedback constructively and professionally.
- Communicate effectively within a team: report a bug, explain a blocker, estimate work, and disagree respectfully.

## 3. Prerequisites
- Basic Git (init, commit, push) — covered in the Developer Toolkit workshop.
- General understanding of SRS and User Stories — covered in the Software Requirements workshop.
- No prior experience working on a real team is required.

## 4. Agenda — 60 Minutes
| Time | Content |
|---|---|
| 0:00–0:05 | Intro: Agile vs Waterfall + the Agile Manifesto |
| 0:05–0:12 | Scrum: roles and events |
| 0:12–0:18 | From Requirement to Epic to User Story to Task |
| 0:18–0:26 | Developer Workflow: your first Monday |
| 0:26–0:34 | Git Collaboration + Pull Requests |
| 0:34–0:40 | Code Review: giving and receiving feedback |
| 0:40–0:45 | Team Communication: bugs, blockers, estimation |
| 0:45–0:55 | Full Team Simulation |
| 0:55–0:58 | Final Challenge |
| 0:58–1:00 | Summary + Discussion |

---

## 5. Introduction: Agile

### What is Agile?
Agile isn't a specific tool or framework — it's a **way of thinking** about software development that is incremental and iterative, rather than delivering the whole product at once at the end of a long project.

### Why Does Agile Exist?
In the traditional model (Waterfall), you gather all requirements upfront, then design, build, test, and deliver — each phase only after the previous one finishes. The problem: the client first sees the product months later, and if the market or understanding shifted, correcting course is expensive and comes far too late.

### Waterfall vs Agile
| Waterfall | Agile |
|---|---|
| All requirements defined upfront and locked in | Requirements can evolve over time based on feedback |
| One delivery at the end of the project (months) | Small, repeated deliveries (e.g., every two weeks) |
| The client sees the result late | The client sees and tries working versions early and continuously |
| Changing requirements is costly and disruptive | Change is expected and managed as part of the process |

### The Agile Manifesto — Core Idea
The Agile Manifesto (2001) summarizes the priorities of modern development teams:
- Individuals and their interactions matter more than rigid tools and processes.
- Working software matters more than extensive documentation no one reads.
- Collaborating with the client matters more than negotiating rigid contract details.
- Responding to change matters more than strictly following a fixed plan.

> Note: this doesn't mean "documentation and planning don't matter" — it means the priority tilts toward flexibility and actual delivered value.

### Iterative & Incremental Development
- **Incremental:** you build the product in small, genuinely working pieces (not one incomplete whole).
- **Iterative:** you return to the same piece and improve it based on real feedback, instead of trying to reach "perfect" on the first attempt.

---

## 6. Scrum

Scrum is the most widely used framework for putting Agile into practice.

### Roles
- **Product Owner (PO):** represents the voice of the customer/business. Defines **what** needs to be built and in what order of priority — not **how** it's built technically. Owns the Product Backlog.
- **Scrum Master:** facilitates the process, removes blockers on the team's behalf, protects the team's focus and time. **Not a "boss" or a direct manager of the developers.**
- **Developers:** a cross-functional team (backend, frontend, QA...) collectively responsible for building, testing, and delivering a working increment of the product.

### Product Backlog
A prioritized list of everything that could be built in the product — features, bug fixes, technical improvements. It's continuously reordered and refined.

### Sprint
A fixed time period (commonly two weeks) during which the team commits to delivering a working increment of the product.

### Sprint Planning
A meeting at the start of the sprint: the team selects items from the backlog for this sprint and breaks them into actionable tasks.

### Daily Scrum (Standup)
A very short (15-minute) daily meeting, three questions only: what did I do yesterday? what will I do today? is anything blocking me? **It's not a status report to a manager — it's team synchronization.**

### Sprint Review
At the end of the sprint: the team demos the actual working increment to stakeholders and gets direct feedback.

### Sprint Retrospective
An internal team meeting (no external stakeholders): what went well? what didn't? what will we change next sprint? Its goal is improving the **process**, not evaluating people.

---

## 7. From Requirements to User Stories to Tasks

In the SRS workshop, we learned to turn a vague idea into clear requirements. In Agile, those requirements become actionable work through a chain:

**Requirement → Epic → User Story → Task → Acceptance Criteria**

- **Epic:** a large body of work, too big to finish in a single sprint. Example: *"Volunteer Task Management"* (from the Volunteer Management System project we saw in the SRS workshop).
- **User Story:** a smaller slice of the Epic, that fits inside one sprint. Example: *"As a volunteer, I want to browse and sign up for tasks near my location."*
- **Task:** a technical breakdown of the Story — each task is picked up by a specific developer. Example:
  - Task 1: build `GET /api/tasks?location=` (backend).
  - Task 2: build the task-list UI with a location filter (frontend).
  - Task 3: write tests for the endpoint (QA/backend).
- **Acceptance Criteria:** clear completion conditions (as seen in the SRS workshop — Given/When/Then).

> **Key point:** a developer usually doesn't work directly on a giant "Requirement" — they work on a clear, specific **Task**, which is part of a Story, which is part of an Epic, which is part of a larger requirement.

---

## 8. Developer Workflow: Your First Monday

This is exactly what happens when you join a real development team and pick up your first task:

1. **Receive a User Story** — from a task-tracking tool (Jira, Trello, GitHub Projects).
2. **Understand the requirement** — read the full Story and Acceptance Criteria before writing a single line of code.
3. **Ask clarifying questions** — if anything's unclear, ask the PO or a teammate **before** starting, not after finishing and discovering you misunderstood.
4. **Receive/create a Task** — a clear technical breakdown, if not already done.
5. **Create a Git branch** — a dedicated branch for this task (`feature/task-location-filter`).
6. **Implement** — write the code following Clean Code principles.
7. **Test** — test locally (Postman for the API, manual testing for the UI).
8. **Commit** — small commits with clear messages.
9. **Push** — push the branch to GitHub.
10. **Create a Pull Request** — a clear description of what changed and why.
11. **Code Review** — a teammate reviews the code.
12. **Address feedback** — revise based on the review comments.
13. **Merge** — once approved, the branch merges into main.
14. **Deploy** — release (automatic via CI/CD or manual).
15. **Monitor** — watch logs/errors after deployment — your responsibility doesn't end at merge.

> Notice: these are exactly the same tools we covered in the **Developer Toolkit** workshop (Git, GitHub, Postman) — now working together as one chain, in the context of a real team.

---

## 9. Git & Team Collaboration

### A Simplified Branching Strategy
- **`main`:** always working, always deployable code — no one pushes to it directly.
- **Feature branches:** a separate branch per task/story (`feature/...`, `fix/...`).

### Good Commit Messages
```bash
# ❌ Bad
git commit -m "fix"
git commit -m "changes"

# ✅ Good
git commit -m "Add location filter to tasks API endpoint"
git commit -m "Fix null pointer error in volunteer signup flow"
```
Rule: imperative mood, clear, describes **what** changed in one sentence.

### Why Not Push Directly to Main?
- Main must always stay working — other developers and CI/CD depend on it.
- Pushing directly skips code review before the code reaches production.
- It makes it much harder to trace which change caused a problem.

### Resolving Merge Conflicts
- Pull (`pull --rebase`) from main frequently so conflicts stay small.
- When a conflict happens: understand **why** the two versions differ (don't just pick one at random), and talk to your teammate if it's unclear.
- After resolving, re-test the code before continuing.

---

## 10. Pull Requests

### Elements of a Good PR
- **A clear title** describing the change.
- **A description** explaining: what changed, why, and how to test it.
- **A link** to the related task/story (`Closes #45`).
- **A small, focused scope** — one logical change, not 20 unrelated files.
- **Specific reviewers** — not "sent to everyone, whoever gets to it."

```markdown
## What
Added a location filter to the tasks list endpoint.

## Why
Volunteers requested seeing only tasks near their area (User Story #12).

## How to test
1. GET /api/tasks?location=Gaza
2. Confirm only tasks in Gaza are returned

Closes #45
```

---

## 11. Code Review

### Why Does It Exist?
- Catching mistakes early (before production).
- Spreading code knowledge across the team — not one person knowing everything.
- Maintaining code quality and consistency.

### What Should a Reviewer Check?
Logical correctness, readability and clarity, presence of tests, edge cases, obvious security risks.

### What Should a Developer Expect?
Feedback on the **code**, not on them **personally**. Review comments are normal and healthy, not a sign of weakness.

### How to Give Constructive Feedback
```
❌ "This code is wrong."
✅ "This could break if the array is empty — what do you think about
    adding a check before the loop?"
```
Be specific, explain "why," suggest instead of command, and acknowledge the good parts too, not only the issues.

### How to Receive Feedback Professionally
- Don't take it personally — the goal is improving the code, not judging you.
- Ask if a comment is unclear instead of assuming or getting frustrated.
- Thank the reviewer — their time went toward improving your work.

### Common Code Review Mistakes
- Focusing only on cosmetic formatting and missing real issues.
- Approving without actually reading the code.
- An empty or unclear PR description that makes review harder from the start.

---

## 12. Team Communication

### How to Ask a Good Technical Question
```
❌ "The code doesn't work, help."
✅ "I'm trying to GET /api/tasks and getting a 500 error.
    I tried X and Y. Here's the error message: [...]. Any ideas?"
```
Give enough context: what you tried, what happened, the exact error message.

### How to Write a Good Bug Report
- **Clear, numbered steps to reproduce.**
- **Expected result vs. actual result.**
- **Environment** (browser, OS, dev/production environment).
- **A screenshot or log**, if possible.

### How to Explain a Blocker
Say you're stuck **on the first day you're stuck**, not after two days of silence. In the daily standup: "I'm blocked on X, I need help from Y."

### Estimating Work
Relative estimation (story points: 1, 2, 3, 5, 8) instead of exact hours — because precise estimation is hard, while relative comparison between tasks is easier and more accurate in practice.

### Communication and Documentation
- Update your task status in the team's tool daily — don't wait to be asked.
- Document "why" a decision was made (in a PR description or comment), not just "what" was done.
- Disagreeing on a technical opinion is normal and healthy — debate the idea, not the person.
- **Ownership:** your responsibility for the code doesn't end at merge — follow it until it's stable in production.

---

## 13. Practical Team Simulation

### Instructions for the Trainer
Split participants into groups of 5: **Product Owner, Scrum Master, Backend Developer, Frontend Developer, QA.**

**Project:** the "Task Sign-Up" feature from the **Volunteer Management System** (the same project from the SRS workshop).

**Simulation steps (suggested time per step):**

| # | Step | Time | Task |
|---|---|---|---|
| 1 | Backlog Creation | 3 min | The PO writes 3 backlog items for the feature, ranked by priority |
| 2 | Writing User Stories | 3 min | The team turns two items into User Stories in the standard format |
| 3 | Sprint Planning | 3 min | Select one story for the mock "sprint," break it into tasks, do rough estimation |
| 4 | Task Assignment | 1 min | Backend Dev takes the API task, Frontend takes the UI task, QA prepares test cases |
| 5 | Development Workflow | 3 min | Each developer writes (on paper/board) a branch name + a short description of what they "implemented" |
| 6 | Pull Request | 2 min | Write a full PR description using the template |
| 7 | Code Review | 2 min | Another teammate (or QA) reviews the description/assumed code and gives at least one constructive comment |
| 8 | Bug Report | 2 min | The trainer introduces a hidden bug; QA writes a proper bug report |
| 9 | Sprint Review | 2 min | The team "demos" the feature to the PO (a 30-second pitch) |
| 10 | Retrospective | 2 min | Each member shares one thing that "went well" and one thing "to improve" |

**Notes for the trainer:** be ready to play the role of "the client" if a team asks a clarifying question while writing stories. Encourage teams to stick to the time box for each step to simulate real sprint pressure.

---

## 14. Additional Exercises

1. **Convert** this requirement into a User Story: *"The system shall allow a coordinator to reject a volunteer's sign-up."*
2. **Break** a User Story into 3 clear technical tasks.
3. **Estimate** these tasks relatively (story points): adding a simple button / building a full notification system / editing text on a screen.
4. **Compare** two commit messages and pick the better one: `"update"` vs. `"Fix crash when volunteer profile has no phone number"`.
5. **Review** an empty PR description (`"fixed stuff"`) and propose an improved version.
6. **Merge conflict:** two teammates edited the same line in a config file at the same time — how do you handle it?
7. **Blocker:** you're stuck waiting on an API another team hasn't finished — write how you'd explain it in the daily standup.
8. **Write a full bug report** for a vague description: "the page isn't working."
9. **Mini retro in pairs:** each person shares one thing to "start doing" and one thing to "stop doing" for a fictional sprint.

## 15. Common Mistakes
- Pushing directly to main without a PR or review.
- Huge Pull Requests bundling unrelated changes.
- Staying silent about a blocker until it's far too late.
- Taking Code Review comments personally.
- Standups turning into a status report to a manager instead of team sync.
- Skipping the retrospective or turning it into a blame session instead of an improvement session.

## 16. Best Practices
- Small sprints and small PRs are far easier to manage than large ones.
- Communicate early and often — silence is riskier than a "dumb question."
- Document "why," not just "what."
- Ownership extends past merge, until the code is stable in production.
- Relative estimation (story points) beats guessing exact hours.

## 17. Final Challenge
With the same simulation groups: give them a new small feature ("add a search box to the task list"). Within 20 minutes, they must go through the full chain in compressed form: User Story → Tasks → estimation → "development" → PR → review → a discovered bug → fix → Sprint Review → Retro — then present the whole journey to the rest of the room in one minute.

## 18. Summary
Agile and Scrum aren't theoretical terms to memorize — they're a practical framework describing how a real development team works day to day: from a vague requirement, to a clear story, to a specific task, to reviewed, deployed, and monitored code. When you join your first team, the question isn't "what is Scrum?" — it's "what's my task today, who do I need to talk to, and what's the next step?"

## 19. Discussion Questions
- What's the practical difference between a Scrum Master and a "direct manager"?
- Why might a team skip the retrospective? What do they lose by doing that?
- How would you handle a teammate who takes code review feedback personally?
- Is Agile always the right approach? Are there cases where the traditional (Waterfall) model fits better?

## 20. Additional Resources
- The official Scrum Guide — scrumguides.org
- The Agile Manifesto — agilemanifesto.org
- Conventional Commits — conventionalcommits.org
- GitHub Flow — docs.github.com
