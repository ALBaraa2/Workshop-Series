# From Idea to Requirements: Software Engineering & SRS
### Workshop Material — Bilingual (Arabic / English)

---

# الجزء الأول: بالعربي

## 1. عنوان الورشة
**From Idea to Requirements: Software Engineering & SRS**
(من الفكرة إلى المتطلبات: هندسة البرمجيات ووثيقة SRS)

## 2. أهداف التعلّم
بنهاية الورشة، المشارك رح يقدر:
- يفهم الفرق بين Software Engineering والـ Programming، ومكان مرحلة المتطلبات بالـ SDLC.
- يحوّل طلب عميل غامض لأسئلة توضيحية دقيقة.
- يفرّق بين Functional وNon-Functional Requirements، وBusiness Rules، Constraints، وAssumptions.
- يستخدم تقنيات عملية لجمع المتطلبات (Interviews, Questionnaires, Observation...).
- يكتشف متطلبات غامضة، متعارضة، أو ناقصة قبل ما توصل لمرحلة التطوير.
- يكتب User Stories وUse Cases احترافية بمعايير واضحة.
- يفهم شو هو الـ SRS، ليش مهم، وكيف يبنيه من الصفر.
- يطبّق كل هاد على مشروع واقعي واحد من أول فكرة غامضة لحد SRS كامل.

## 3. المتطلبات المسبقة
- خلفية عامة بتطوير البرمجيات (مش لازم خبرة عملية بمشروع حقيقي).
- فكرة أساسية عن دورة حياة تطوير البرمجيات (SDLC) — رح نراجعها بسرعة.
- لا حاجة لخبرة سابقة بكتابة SRS أو User Stories.

## 4. الأجندة — 60 دقيقة
| الوقت | المحتوى |
|---|---|
| 0:00–0:05 | مقدمة: Software Engineering vs Programming + SDLC |
| 0:05–0:10 | Requirements Engineering: المفاهيم الأساسية |
| 0:10–0:18 | Requirements Gathering — تطبيق على "Volunteer Management System" |
| 0:18–0:26 | Requirements Analysis: غموض، تعارض، Scope، Prioritization |
| 0:26–0:32 | Functional & Non-Functional Requirements + Business Rules |
| 0:32–0:38 | User Stories |
| 0:38–0:44 | Use Cases |
| 0:44–0:52 | SRS: البنية + مثال كامل |
| 0:52–0:57 | تمارين عملية |
| 0:57–1:00 | التحدي النهائي + ملخّص + نقاش |

## 5. مقدمة: Software Engineering

### شو هي Software Engineering؟
Software Engineering هي المنهج المنظّم لبناء برمجيات — من فهم المشكلة، لتصميم الحل، لتطويره، اختباره، وصيانته. **البرمجة (Programming) هي جزء واحد بس من هاد المنهج.**

### Software Engineering vs Programming
| Programming | Software Engineering |
|---|---|
| كتابة كود يحل مشكلة محددة | فهم المشكلة، تخطيط الحل، بناؤه، صيانته بمرور الوقت |
| غالبًا فردي أو نطاق ضيق | يشمل فريق، عملاء، stakeholders متعددين |
| التركيز على "كيف أكتب هاد الجزء؟" | التركيز على "شو المطلوب فعليًا، وليش؟" |

### دورة حياة تطوير البرمجيات (SDLC) — نظرة سريعة
Requirements → Design → Implementation → Testing → Deployment → Maintenance

> **النقطة الأساسية للورشة:** أكتر مرحلة بتتقفز أو تُعمل بشكل سطحي بالمشاريع الصغيرة والجامعية هي **Requirements** — وهي بالضبط المرحلة اللي أخطاؤها بتكلّف أكتر شي لاحقًا.

### ليش التخطيط والمتطلبات مهمين؟
- تعديل خطأ باكتشفته أثناء جمع المتطلبات بياخد دقائق. نفس الخطأ لو اكتشفته بعد التسليم بياخد أسابيع وموارد.
- عميل قال "بدي نظام يدير المتطوعين" — هاد مش متطلب، هاد **فكرة**. شغلنا كمهندسين برمجيات نحوّلها لشي قابل للبناء.

> **العقلية الأساسية لهاي الورشة:**
> **"قبل ما تحل المشكلة، تأكد إنك فاهمها."**

---

## 6. Requirements Engineering

### شو هو الـ Requirement؟
جملة واضحة وقابلة للاختبار بتوصف شي لازم النظام يعمله أو صفة لازم يمتلكها — مش "فكرة عامة"، ومش "حل تقني".

### Stakeholders
أي شخص أو جهة إلها مصلحة أو تأثير بالنظام:
- **العميل/الإدارة:** صاحب القرار، بيموّل المشروع.
- **المستخدمون النهائيون:** (بمشروعنا: المتطوعين، منسّقي المهام).
- **فريق التطوير:** المطورين، المختبرين.
- **أطراف خارجية:** جهات مانحة، شركاء، جهات تنظيمية.

### Functional Requirements
شو **يعمل** النظام. مثال: "النظام لازم يسمح للمتطوع يسجّل بمهمة."

### Non-Functional Requirements
**كيف** النظام بيعمل (جودة، أداء، أمان). مثال: "النظام لازم يدعم 1000 مستخدم متزامن."

### Business Rules
قواعد عمل مستقلة عن النظام، موجودة أصلًا بواقع المؤسسة. مثال: "المتطوع ما بقدر يسجّل بمهمتين بنفس الوقت."

### Constraints
قيود مفروضة على المشروع (ميزانية، وقت، تقنية معيّنة لازم تُستخدم).

### Assumptions
أشياء نفترضها صحيحة بدون تأكيد كامل (زي: "المتطوعين عندهم إنترنت وهواتف ذكية").

### Dependencies
اعتماديات على أنظمة/خدمات خارجية (زي: خدمة SMS للتنبيهات).

---

## 7. Requirements Gathering

### تقنيات عملية لجمع المتطلبات
| التقنية | متى تُستخدم |
|---|---|
| **Interviews** | فهم عميق من stakeholder محدد (المدير، صاحب القرار) |
| **Questionnaires** | جمع آراء من عدد كبير (زي المتطوعين أنفسهم) |
| **Observation** | مراقبة العملية الحالية (يدوية) قبل الأتمتة |
| **Workshops** | جمع كل الـ stakeholders سوا لحل تعارضات بسرعة |
| **Document Analysis** | مراجعة ملفات Excel/نماذج ورقية مستخدمة حاليًا |
| **Prototyping** | نموذج أولي بسيط يوضّح فكرة قبل البناء الكامل |
| **Stakeholder Discussions** | نقاش مستمر أثناء المشروع، مش مرة وحدة بالبداية |

### تطبيق عملي: مشروع Volunteer Management System

> **جملة العميل الأولى (غامضة):**
> *"بدي نظام يدير المتطوعين والمهام ومواقع العمل."*

هاي مش متطلب — هاي فكرة عامة جدًا. شغلنا الآن نسأل أسئلة صح:

**أسئلة توضيحية (Interview مع العميل):**
- مين بالضبط بيحدد/ينشئ المهام؟ الإدارة بس، ولا أي منسّق؟
- المتطوع بيختار المهمة بنفسه، ولا بتنعيّنله؟
- في موافقة مطلوبة على تسجيل المتطوع بمهمة، ولا تلقائي؟
- بدنا نتابع ساعات التطوع لكل شخص؟ ليش (تقارير؟ شهادات؟)
- في أكتر من موقع عمل بنفس الوقت؟
- بدها تطبيق موبايل ولا بس موقع ويب؟
- في تنبيهات مطلوبة (SMS/Email) قبل المهمة؟
- شو بيصير لو متطوع لغى تسجيله بآخر لحظة؟

**من المقابلة مع المنسّق + استبيان قصير للمتطوعين + مراجعة جدول Excel الحالي، طلعنا بالتالي:**
- في احتياج فعلي لموافقة الإدارة على التسجيل (لأسباب أمان بمواقع معينة).
- المتطوعين بدهم يشوفوا المهام قريبة من مكان سكنهم.
- التقارير مطلوبة فعلًا — الجهة المانحة بتطلب عدد ساعات التطوع سنويًا.
- ما في حاجة فعلية لتطبيق موبايل بالمرحلة الأولى — موقع ويب متجاوب كافي.

---

## 8. Requirements Analysis

### متطلبات غامضة (Ambiguous)
> "النظام لازم يكون سريع." ← غامض. ما بيعرف المطوّر شو "سريع" يعني.
**تحويلها لمتطلب قابل للاختبار:** "صفحة قائمة المهام لازم تحمّل خلال أقل من 2 ثانية."

### متطلبات متعارضة (Conflicting)
> المنسّق طلب "موافقة إدارية على كل تسجيل" — بنفس الوقت طلب "تسجيل سريع وسهل للمتطوع".
**الحل:** نقاش بـ Workshop مع الطرفين، وطلعنا بحل وسط: الموافقة مطلوبة بس للمهام بمواقع معينة (حساسة)، والباقي تسجيل فوري.

### متطلبات ناقصة (Missing)
محدش ذكر شو بيصير لو متطوع لغى تسجيله بآخر لحظة، أو شو بيصير لو المهمة اكتمل عدد المتطوعين المطلوب. هاي أسئلة **لازم تُسأل بدري**، مش تُكتشف بعد التسليم.

### Scope (نطاق المشروع)
لازم نحدد بوضوح شو **داخل** النطاق وشو **خارجه**:
- ✅ داخل النطاق: تسجيل مهام، تسجيل متطوعين، تتبّع ساعات، تقارير أساسية.
- ❌ خارج النطاق (بالمرحلة الأولى): نظام تبرعات مالية، تطبيق موبايل، دردشة مباشرة بين المتطوعين.

> **Scope Creep:** لما ميزات جديدة تنضاف تدريجيًا بدون موافقة رسمية ("بما إنك هون، ضيف كمان...") — لازم يُدار عبر Change Requests رسمية، مش يُقبل تلقائيًا.

### Prioritization — طريقة MoSCoW
| الأولوية | مثال بمشروعنا |
|---|---|
| **Must have** | تسجيل مهمة، تسجيل متطوع بمهمة |
| **Should have** | تنبيهات بالإيميل |
| **Could have** | فلترة المهام حسب الموقع الجغرافي |
| **Won't have (الآن)** | تطبيق موبايل، نظام تبرعات |

### Feasibility (الجدوى)
هل التكلفة/الوقت/التقنية المتاحة كافية لتنفيذ المتطلب؟ مثال: تكامل SMS ممكن يكون مكلف — لازم نتأكد من الميزانية قبل ما نلتزم بيه كـ "Must have".

### Acceptance Criteria (معايير القبول)
شروط واضحة تحدد "متى نعتبر هاد المتطلب مكتمل وصحيح". مثال لمتطلب التسجيل بمهمة:
- المتطوع ما بقدر يسجّل بمهمة اكتمل عدد المتطوعين فيها.
- المتطوع بيستلم رسالة تأكيد فورية بعد التسجيل.
- لو المهمة بتحتاج موافقة، حالة التسجيل تكون "قيد المراجعة" لحد يوافق المسؤول.

---

## 9. User Stories

### شو هو الـ User Story؟
وصف قصير للميزة من منظور المستخدم، بيركّز على **القيمة** مش التفاصيل التقنية.

### الصيغة القياسية
> **As a** [role], **I want** [feature], **so that** [benefit/value].

### أمثلة من مشروعنا
```
As a volunteer,
I want to see a list of available tasks near my location,
so that I can choose tasks that are convenient for me.
```
```
As a coordinator,
I want to approve or reject volunteer sign-ups for sensitive tasks,
so that I can ensure only vetted volunteers work at those locations.
```

### Acceptance Criteria بصيغة Given/When/Then
```
Given a volunteer is logged in
When they select a task that requires approval and click "Sign up"
Then the sign-up status should be "Pending Approval"
And the coordinator should receive a notification
```

### User Story جيدة مقابل ضعيفة
| ❌ ضعيفة | ✅ جيدة |
|---|---|
| "بدي صفحة مهام." | "As a volunteer, I want to filter tasks by location, so that I only see relevant tasks." |
| غامضة، بدون قيمة واضحة، صعب تُختبر | واضحة، فيها قيمة محددة، وقابلة لكتابة acceptance criteria عليها |

**معيار INVEST السريع:** الـ User Story الجيدة تكون: Independent (مستقلة)، Negotiable (قابلة للنقاش)، Valuable (فيها قيمة واضحة)، Estimable (ممكن نقدّر جهدها)، Small (صغيرة بما يكفي)، Testable (قابلة للاختبار).

---

## 10. Use Cases

### العناصر الأساسية
- **Actor:** مين بيتفاعل مع النظام (المتطوع، المنسّق).
- **Preconditions:** شو لازم يكون صحيح قبل ما يبلش الـ use case.
- **Main Flow:** الخطوات الطبيعية للنجاح.
- **Alternative Flow:** شو بيصير بحالات استثنائية.
- **Postconditions:** حالة النظام بعد انتهاء الـ use case بنجاح.

### مثال كامل: "Volunteer Signs Up for a Task"
| العنصر | التفاصيل |
|---|---|
| **Actor** | Volunteer |
| **Preconditions** | المتطوع مسجّل دخول، المهمة متاحة وما اكتمل عدد المتطوعين فيها |
| **Main Flow** | 1. المتطوع بيتصفح قائمة المهام المتاحة.<br>2. بيختار مهمة.<br>3. بيضغط "Sign up".<br>4. النظام بيتحقق من توفر مكان بالمهمة.<br>5. النظام بيسجّل المتطوع ويرسل تأكيد. |
| **Alternative Flow** | لو المهمة اكتمل عدد المتطوعين → النظام بيعرض خيار الانضمام لقائمة الانتظار (Waitlist). |
| **Postconditions** | المتطوع مسجّل رسميًا بالمهمة، وحالة تسجيله محدّثة بالنظام. |

---

## 11. SRS — Software Requirements Specification

### شو هو الـ SRS؟
وثيقة رسمية توثّق **كل** متطلبات النظام (Functional وNon-Functional) بشكل واضح ومنظّم ومتفق عليه بين العميل وفريق التطوير.

### ليش نحتاجه؟
- مرجع واحد متفق عليه — بيقلل سوء الفهم بين العميل والفريق.
- أساس لتقدير الوقت والتكلفة.
- أساس لكتابة اختبارات القبول (Acceptance Testing).
- حماية قانونية/تعاقدية — "هاد بالضبط اللي اتفقنا عليه."

### مين بيستخدمه؟
العميل (للموافقة)، مدير المشروع (للتخطيط)، المطورين (للتنفيذ)، فريق الاختبار (لكتابة test cases).

### بنية عملية للـ SRS
1. **Introduction** — الغرض، النطاق، التعريفات، المراجع.
2. **Overall Description** — لمحة عامة عن المنتج، المستخدمين، القيود العامة.
3. **Functional Requirements** — مرقّمة وواضحة (FR1, FR2...).
4. **Non-Functional Requirements** — مرقّمة (NFR1, NFR2...).
5. **Use Cases / User Stories** — تفصيل السيناريوهات الأساسية.
6. **Business Rules & Constraints**.
7. **Assumptions & Dependencies**.
8. **Appendices** — مسرد مصطلحات، مخططات إضافية.

### خصائص SRS جيد
- **Correct** — يعكس فعليًا شو العميل يريد.
- **Unambiguous** — كل جملة إلها تفسير واحد بس.
- **Complete** — ما في متطلبات ناقصة.
- **Consistent** — ما في تعارض بين المتطلبات.
- **Verifiable** — كل متطلب ممكن تُختبر إنه تحقق.
- **Modifiable** — سهل التحديث بدون فوضى.
- **Traceable** — كل متطلب ممكن تربطه بمصدره (طلب عميل، user story، إلخ).

---

## 12. مثال SRS كامل (مختصر) — Volunteer Management System

**1. Introduction**
الغرض: بناء نظام ويب لإدارة تسجيل المتطوعين بمهام تطوعية بمواقع مختلفة، وتتبّع ساعات التطوع لأغراض التقارير.

**2. Stakeholders:** إدارة المنظمة، منسّقي المهام، المتطوعون، الجهات المانحة (تستلم تقارير).

**3. Functional Requirements**
- FR1: النظام لازم يسمح للأدمن بإنشاء مهمة تطوعية (عنوان، وصف، موقع، تاريخ، عدد المتطوعين المطلوب).
- FR2: النظام لازم يسمح للمتطوع بإنشاء حساب وملف شخصي.
- FR3: النظام لازم يسمح للمتطوع بتصفح المهام المتاحة والتسجيل بمهمة.
- FR4: النظام لازم يطلب موافقة المنسّق على التسجيل بالمهام المصنّفة كـ"حساسة".
- FR5: النظام لازم يتتبّع ساعات التطوع لكل متطوع تلقائيًا.
- FR6: النظام لازم يولّد تقرير سنوي بساعات التطوع لكل شخص/مهمة.

**4. Non-Functional Requirements**
- NFR1 (Performance): صفحة قائمة المهام لازم تحمّل خلال أقل من 2 ثانية.
- NFR2 (Availability): النظام متاح 99% من الوقت.
- NFR3 (Usability): متطوع بلا خبرة تقنية يقدر يسجّل بمهمة خلال أقل من 3 نقرات.
- NFR4 (Security): بيانات المتطوعين الشخصية مشفّرة بقاعدة البيانات.
- NFR5 (Localization): الواجهة تدعم العربي والإنجليزي.

**5. Business Rules**
- BR1: المتطوع ما بقدر يسجّل بمهمتين بيتعارض وقتهم.
- BR2: المهمة ما بتقبل تسجيلات أكتر من الحد الأقصى المحدد لها.

**6. Constraints:** الميزانية والوقت المتاح (تسليم خلال 3 أشهر)، فريق تطوير من شخصين.

**7. Assumptions:** المتطوعون عندهم إنترنت وهواتف ذكية/حواسيب. البيانات الحالية موجودة بملف Excel هيتم استيراده.

**8. Out of Scope (Phase 1):** تطبيق موبايل، نظام تبرعات مالية.

---

## 13. تمارين عملية (Hands-on Exercises)

**السيناريو الجديد:** عميل قال: *"بدي تطبيق لمطعمي يدير طلبات الأونلاين."*

1. **حددوا المعلومات الناقصة:** شو الأسئلة اللي لازم تسألوها العميل قبل ما تبلشوا؟
2. **حوّلوا الجملة لـ 3 Functional Requirements و2 Non-Functional Requirements.**
3. **صنّفوا هاي القائمة** (Functional أو Non-Functional): "النظام لازم يرسل إشعار عند تأكيد الطلب" / "النظام لازم يدعم 500 طلب متزامن" / "النظام لازم يعرض قائمة الطعام بالعربي والإنجليزي".
4. **اكتبوا User Story واحدة** لميزة "متابعة حالة الطلب" مع Acceptance Criteria.
5. **ابنوا Use Case كامل** لـ "العميل يقدّم طلب أونلاين" (Actor, Preconditions, Main Flow, Alternative Flow, Postconditions).
6. **حددوا مثال على Scope Creep** ممكن يصير بهاد المشروع.

## 14. التحدي النهائي (Final Challenge)
بمجموعات: عطوهم جملة غامضة تانية — *"بدنا نظام لإدارة استعارة الكتب بمكتبة الجامعة."* المطلوب: بناء **Mini-SRS** كامل خلال 15 دقيقة يتضمّن: Stakeholders، 5 Functional Requirements، 3 Non-Functional Requirements، 2 User Stories مع Acceptance Criteria، Use Case واحد كامل، Business Rules، وتحديد صريح لـ Scope (داخل/خارج النطاق).

## 15. الأخطاء الشائعة
- كتابة **حل تقني** بدل **متطلب** (مثال خاطئ: "النظام لازم يستخدم MySQL" — هاد قرار تقني مش متطلب عمل، إلا لو كان constraint حقيقي من العميل).
- استخدام كلمات غامضة بدون تكميم: "سريع"، "سهل الاستخدام"، "آمن" — بدون تعريف قابل للقياس.
- جمع المتطلبات من stakeholder واحد بس وتجاهل الباقي.
- الخلط بين Functional وNon-Functional Requirements.
- عدم توثيق الافتراضات (Assumptions) — وبعدين اكتشاف إنها غلط بعد التطوير.
- قبول أي طلب إضافة ميزة أثناء التطوير بدون تقييم أثره على الـ Scope (Scope Creep).

## 16. أفضل الممارسات
- استخدم صيغة "شرطية" واضحة بكل متطلب: "The system shall..." — لغة رسمية قابلة للاختبار.
- طبّق MoSCoW لترتيب الأولويات من أول يوم.
- تحقق (Validate) من كل متطلب مع الـ stakeholder المعني قبل ما تعتبره نهائي.
- اكتب Acceptance Criteria لكل متطلب مهم — هاد اللي بيحدد "متى خلصنا فعليًا".
- خلّي كل متطلب قابل للتتبّع (Traceable) لمصدره.

## 17. الملخّص (Summary)
تحويل فكرة غامضة لمتطلبات واضحة مش خطوة إدارية روتينية — هو جوهر شغل المهندس البرمجي قبل ما يكتب سطر كود وحد. من فهم الـ Stakeholders، لجمع المتطلبات بتقنيات صح، لتحليلها واكتشاف الغموض والتعارض والنقص، لتوثيقها بـ User Stories وUse Cases وSRS واضح — كل هاي الخطوات هدفها واحد: **تأكد إنك فاهم المشكلة صح قبل ما تبلش تحلها.**

## 18. أسئلة للنقاش
- شو المخاطر الحقيقية لو فريق قفز مباشرة للتطوير بدون SRS واضح؟
- كيف كنتوا بتتعاملوا لو اثنين stakeholders أعطوكم متطلبات متعارضة تمامًا؟
- متى ممكن يكون جمع المتطلبات المفصّل زيادة عن اللزوم (Over-analysis) لمشروع صغير؟

## 19. مصادر إضافية
- ISO/IEC/IEEE 29148 — Requirements Engineering Standard
- *User Stories Applied* — Mike Cohn
- IEEE 830 — SRS Structure (مرجع تاريخي معروف)
- Business Analysis Body of Knowledge (BABOK)

---
---

# Part 2 — English

## 1. Workshop Title
**From Idea to Requirements: Software Engineering & SRS**

## 2. Learning Objectives
By the end of this workshop, participants will be able to:
- Understand the difference between Software Engineering and Programming, and where requirements fit in the SDLC.
- Turn a vague client request into precise clarifying questions.
- Distinguish Functional from Non-Functional Requirements, Business Rules, Constraints, and Assumptions.
- Use practical techniques to gather requirements (interviews, questionnaires, observation...).
- Spot ambiguous, conflicting, or missing requirements before development starts.
- Write professional User Stories and Use Cases with clear criteria.
- Understand what an SRS is, why it matters, and how to build one from scratch.
- Apply all of this to a single realistic project, from a vague idea to a complete SRS.

## 3. Prerequisites
- General background in software development (no need for real-project experience).
- Basic idea of the Software Development Lifecycle (SDLC) — we'll review it briefly.
- No prior experience writing an SRS or User Stories is required.

## 4. Agenda — 60 Minutes
| Time | Content |
|---|---|
| 0:00–0:05 | Intro: Software Engineering vs Programming + SDLC |
| 0:05–0:10 | Requirements Engineering: core concepts |
| 0:10–0:18 | Requirements Gathering — applied to "Volunteer Management System" |
| 0:18–0:26 | Requirements Analysis: ambiguity, conflict, scope, prioritization |
| 0:26–0:32 | Functional & Non-Functional Requirements + Business Rules |
| 0:32–0:38 | User Stories |
| 0:38–0:44 | Use Cases |
| 0:44–0:52 | SRS: structure + full example |
| 0:52–0:57 | Hands-on exercises |
| 0:57–1:00 | Final challenge + Summary + Discussion |

## 5. Introduction: Software Engineering

### What is Software Engineering?
Software Engineering is the disciplined approach to building software — from understanding the problem, to designing a solution, building it, testing it, and maintaining it. **Programming is only one part of this discipline.**

### Software Engineering vs Programming
| Programming | Software Engineering |
|---|---|
| Writing code that solves a specific problem | Understanding the problem, planning the solution, building it, maintaining it over time |
| Often individual or narrow scope | Involves a team, clients, multiple stakeholders |
| Focuses on "how do I write this part?" | Focuses on "what's actually needed, and why?" |

### Software Development Lifecycle (SDLC) — Quick Overview
Requirements → Design → Implementation → Testing → Deployment → Maintenance

> **The core point of this workshop:** the phase most often skipped or done superficially in small and academic projects is **Requirements** — and it's exactly the phase whose mistakes cost the most later.

### Why Do Planning and Requirements Matter?
- Fixing a mistake you catch during requirements gathering takes minutes. The same mistake caught after delivery takes weeks and resources.
- A client saying "I want a system to manage volunteers" isn't a requirement — it's an **idea**. Our job as software engineers is to turn it into something buildable.

> **The core mindset for this workshop:**
> **"Before solving the problem, make sure you understand the problem."**

---

## 6. Requirements Engineering

### What is a Requirement?
A clear, testable statement describing something the system must do, or a quality it must have — not a "general idea," and not a "technical solution."

### Stakeholders
Anyone with an interest in or influence over the system:
- **Client/Management:** decision-maker, funds the project.
- **End users:** (in our project: volunteers, task coordinators).
- **Development team:** developers, testers.
- **External parties:** donors, partners, regulatory bodies.

### Functional Requirements
What the system **does**. Example: "The system shall allow a volunteer to sign up for a task."

### Non-Functional Requirements
**How** the system performs (quality, performance, security). Example: "The system shall support 1,000 concurrent users."

### Business Rules
Rules independent of the system, already existing in the organization's reality. Example: "A volunteer cannot sign up for two tasks at the same time."

### Constraints
Restrictions imposed on the project (budget, time, a mandated technology).

### Assumptions
Things we take as true without full confirmation (e.g., "volunteers have internet access and smartphones").

### Dependencies
Reliance on external systems/services (e.g., an SMS service for notifications).

---

## 7. Requirements Gathering

### Practical Techniques
| Technique | When to Use |
|---|---|
| **Interviews** | Deep understanding from a specific stakeholder (manager, decision-maker) |
| **Questionnaires** | Collecting opinions from a large group (e.g., the volunteers themselves) |
| **Observation** | Watching the current (manual) process before automating it |
| **Workshops** | Bringing all stakeholders together to resolve conflicts quickly |
| **Document Analysis** | Reviewing existing Excel sheets/paper forms currently in use |
| **Prototyping** | A simple mockup to clarify an idea before full development |
| **Stakeholder Discussions** | Ongoing conversation throughout the project, not a one-time event |

### Practical Application: Volunteer Management System

> **The client's first (vague) statement:**
> *"I want a system to manage volunteers, tasks, and work locations."*

This isn't a requirement — it's a very general idea. Our job now is to ask the right questions:

**Clarifying questions (interview with the client):**
- Who exactly creates/defines tasks? Only management, or any coordinator?
- Does the volunteer choose the task, or is it assigned to them?
- Is approval required for a volunteer to sign up for a task, or is it automatic?
- Do we need to track volunteer hours per person? Why (reports? certificates?)
- Are there multiple work locations at once?
- Does this need a mobile app, or is a website enough?
- Are notifications (SMS/Email) needed before a task?
- What happens if a volunteer cancels their sign-up at the last minute?

**From the interview with the coordinator + a short volunteer survey + reviewing the current Excel sheet, we learned:**
- Management approval for sign-ups is genuinely needed (safety reasons at certain locations).
- Volunteers want to see tasks near their home location.
- Reports are genuinely required — the donor organization asks for annual volunteer hours.
- There's no real need for a mobile app in phase one — a responsive website is enough.

---

## 8. Requirements Analysis

### Ambiguous Requirements
> "The system should be fast." ← Ambiguous. The developer has no idea what "fast" means.
**Turning it into a testable requirement:** "The task list page shall load in under 2 seconds."

### Conflicting Requirements
> The coordinator asked for "management approval on every sign-up" — while also asking for "quick, easy sign-up for volunteers."
**Resolution:** a workshop discussion with both sides landed on a compromise: approval is only required for tasks at sensitive locations; everything else is instant sign-up.

### Missing Requirements
No one mentioned what happens if a volunteer cancels at the last minute, or what happens once a task reaches its volunteer capacity. These are questions that **must be asked early**, not discovered after delivery.

### Scope
We must clearly define what's **in** scope and what's **out**:
- ✅ In scope: task creation, volunteer registration, hour tracking, basic reports.
- ❌ Out of scope (phase one): a financial donation system, a mobile app, direct chat between volunteers.

> **Scope Creep:** when new features get added gradually without formal approval ("since you're at it, also add...") — this must be managed via formal change requests, not accepted automatically.

### Prioritization — the MoSCoW Method
| Priority | Example in Our Project |
|---|---|
| **Must have** | Creating a task, signing up for a task |
| **Should have** | Email notifications |
| **Could have** | Filtering tasks by location |
| **Won't have (for now)** | Mobile app, donation system |

### Feasibility
Is the available cost/time/technology enough to implement the requirement? Example: SMS integration might be costly — we need to confirm the budget before committing to it as a "Must have."

### Acceptance Criteria
Clear conditions defining "when is this requirement considered complete and correct." Example for the task sign-up requirement:
- A volunteer cannot sign up for a task that has reached its volunteer capacity.
- The volunteer receives an immediate confirmation message after signing up.
- If the task requires approval, the sign-up status is "Pending Approval" until a coordinator approves it.

---

## 9. User Stories

### What is a User Story?
A short description of a feature from the user's perspective, focused on **value**, not technical detail.

### Standard Format
> **As a** [role], **I want** [feature], **so that** [benefit/value].

### Examples From Our Project
```
As a volunteer,
I want to see a list of available tasks near my location,
so that I can choose tasks that are convenient for me.
```
```
As a coordinator,
I want to approve or reject volunteer sign-ups for sensitive tasks,
so that I can ensure only vetted volunteers work at those locations.
```

### Acceptance Criteria in Given/When/Then
```
Given a volunteer is logged in
When they select a task that requires approval and click "Sign up"
Then the sign-up status should be "Pending Approval"
And the coordinator should receive a notification
```

### Good vs Bad User Stories
| ❌ Bad | ✅ Good |
|---|---|
| "I want a tasks page." | "As a volunteer, I want to filter tasks by location, so that I only see relevant tasks." |
| Vague, no clear value, hard to test | Clear, has defined value, and testable acceptance criteria can be written for it |

**Quick INVEST criteria:** a good User Story is: Independent, Negotiable, Valuable, Estimable, Small, and Testable.

---

## 10. Use Cases

### Core Elements
- **Actor:** who interacts with the system (the volunteer, the coordinator).
- **Preconditions:** what must be true before the use case begins.
- **Main Flow:** the normal successful steps.
- **Alternative Flow:** what happens in exceptional cases.
- **Postconditions:** the system's state after the use case completes successfully.

### Full Example: "Volunteer Signs Up for a Task"
| Element | Details |
|---|---|
| **Actor** | Volunteer |
| **Preconditions** | The volunteer is logged in; the task is available and not at capacity |
| **Main Flow** | 1. The volunteer browses the list of available tasks.<br>2. They select a task.<br>3. They click "Sign up."<br>4. The system checks task availability.<br>5. The system registers the volunteer and sends a confirmation. |
| **Alternative Flow** | If the task is at capacity → the system offers the option to join a waitlist. |
| **Postconditions** | The volunteer is officially registered for the task, and their sign-up status is updated in the system. |

---

## 11. SRS — Software Requirements Specification

### What is an SRS?
A formal document that captures **all** system requirements (functional and non-functional) in a clear, organized, and mutually agreed form between the client and development team.

### Why Do We Need It?
- One shared reference — reduces misunderstanding between client and team.
- The basis for estimating time and cost.
- The basis for writing acceptance tests.
- Legal/contractual protection — "this is exactly what we agreed on."

### Who Uses It?
The client (for approval), the project manager (for planning), developers (for implementation), the QA team (for writing test cases).

### A Practical SRS Structure
1. **Introduction** — purpose, scope, definitions, references.
2. **Overall Description** — a general overview of the product, users, general constraints.
3. **Functional Requirements** — numbered and clear (FR1, FR2...).
4. **Non-Functional Requirements** — numbered (NFR1, NFR2...).
5. **Use Cases / User Stories** — detailing key scenarios.
6. **Business Rules & Constraints**.
7. **Assumptions & Dependencies**.
8. **Appendices** — glossary of terms, additional diagrams.

### Characteristics of a Good SRS
- **Correct** — genuinely reflects what the client wants.
- **Unambiguous** — every statement has exactly one interpretation.
- **Complete** — no missing requirements.
- **Consistent** — no contradictions between requirements.
- **Verifiable** — every requirement can be tested to confirm it's met.
- **Modifiable** — easy to update without creating chaos.
- **Traceable** — every requirement can be traced to its source (a client request, a user story, etc.).

---

## 12. Complete (Condensed) SRS Example — Volunteer Management System

**1. Introduction**
Purpose: build a web-based system to manage volunteer sign-ups for tasks at various locations, and track volunteer hours for reporting purposes.

**2. Stakeholders:** organization management, task coordinators, volunteers, donor organizations (receive reports).

**3. Functional Requirements**
- FR1: The system shall allow an admin to create a volunteer task (title, description, location, date, number of volunteers needed).
- FR2: The system shall allow a volunteer to create an account and profile.
- FR3: The system shall allow a volunteer to browse available tasks and sign up.
- FR4: The system shall require coordinator approval for sign-ups on tasks flagged as "sensitive."
- FR5: The system shall automatically track each volunteer's hours.
- FR6: The system shall generate an annual report of volunteer hours per person/task.

**4. Non-Functional Requirements**
- NFR1 (Performance): the task list page shall load in under 2 seconds.
- NFR2 (Availability): the system shall be available 99% of the time.
- NFR3 (Usability): a non-technical volunteer can sign up for a task in under 3 clicks.
- NFR4 (Security): volunteers' personal data shall be encrypted in the database.
- NFR5 (Localization): the interface shall support Arabic and English.

**5. Business Rules**
- BR1: A volunteer cannot sign up for two tasks that overlap in time.
- BR2: A task cannot accept sign-ups beyond its defined capacity.

**6. Constraints:** available budget and time (3-month delivery), a two-person development team.

**7. Assumptions:** volunteers have internet access and a smartphone/computer. Existing data lives in an Excel file that will be imported.

**8. Out of Scope (Phase 1):** mobile app, financial donation system.

---

## 13. Hands-on Exercises

**New scenario:** a client says: *"I want an app for my restaurant to manage online orders."*

1. **Identify missing information:** what questions must you ask the client before starting?
2. **Turn the statement into 3 Functional Requirements and 2 Non-Functional Requirements.**
3. **Classify this list** (Functional or Non-Functional): "The system shall send a notification when an order is confirmed" / "The system shall support 500 concurrent orders" / "The system shall display the menu in Arabic and English."
4. **Write one User Story** for an "order status tracking" feature, with Acceptance Criteria.
5. **Build a complete Use Case** for "Customer places an online order" (Actor, Preconditions, Main Flow, Alternative Flow, Postconditions).
6. **Identify one example of potential Scope Creep** for this project.

## 14. Final Challenge
In groups: give them another vague statement — *"We need a system to manage book borrowing at the university library."* The task: build a complete **Mini-SRS** within 15 minutes, including: Stakeholders, 5 Functional Requirements, 3 Non-Functional Requirements, 2 User Stories with Acceptance Criteria, one complete Use Case, Business Rules, and an explicit definition of Scope (in/out).

## 15. Common Mistakes
- Writing a **technical solution** instead of a **requirement** (bad example: "The system shall use MySQL" — that's a technical decision, not a business requirement, unless it's a genuine client-imposed constraint).
- Using vague, unquantified words: "fast," "user-friendly," "secure" — without a measurable definition.
- Gathering requirements from only one stakeholder and ignoring the rest.
- Confusing Functional with Non-Functional Requirements.
- Not documenting Assumptions — then discovering they were wrong after development.
- Accepting any feature-addition request mid-development without evaluating its impact on scope (Scope Creep).

## 16. Best Practices
- Use clear "shall" language for every requirement — formal, testable wording.
- Apply MoSCoW to prioritize from day one.
- Validate every requirement with the relevant stakeholder before considering it final.
- Write Acceptance Criteria for every important requirement — that's what defines "actually done."
- Keep every requirement traceable to its source.

## 17. Summary
Turning a vague idea into clear requirements isn't a routine administrative step — it's the core of a software engineer's job before writing a single line of code. From understanding stakeholders, to gathering requirements with the right techniques, to analyzing them for ambiguity, conflict, and gaps, to documenting them as User Stories, Use Cases, and a clear SRS — every one of these steps serves one goal: **make sure you understand the problem correctly before you start solving it.**

## 18. Discussion Questions
- What are the real risks of a team jumping straight into development without a clear SRS?
- How would you handle two stakeholders giving you completely conflicting requirements?
- When can detailed requirements gathering become overkill (over-analysis) for a small project?

## 19. Additional Resources
- ISO/IEC/IEEE 29148 — Requirements Engineering Standard
- *User Stories Applied* — Mike Cohn
- IEEE 830 — SRS Structure (a well-known historical reference)
- Business Analysis Body of Knowledge (BABOK)
