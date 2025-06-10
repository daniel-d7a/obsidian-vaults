#video_script/typescript_intro

## Interfaces

- can only represent objects and functions
- intersections and extension 
- interfaces can be extended 
- interfaces can extend multiple interfaces 
- can represent functions as an object's call signature 

## Types

- best candidates are fn types and objects
- are like typescript variables
- Are aliases for other types
- types can extend each other
- types can extend multiple other types

## Types vs interfaces

- interface extends is cached so it is faster
- interfaces with the same name collapse to one (declaration merging)
- usefull for overriding global types like window
- types with the same name cause errors
- both support optionals
- both support 2 function ways
- interface extends is faster than type intersection


## script

النهاردة هنتعرف على ال interfaces و ال types و الفرق ما بينهم 

الاتنين هدفهم متشابه بشكل كبير الا و هو انك تمثل ال complex types الي عندك بمعنى لو عندك type كبير و فيه تفاصيل كتير و حابب تستخدمه اكتر من مرة تقدر تعمل كده باستخدام ال types و ال interfaces 

## ال interfaces 

هنبدأ بال interfaces و هي مشابهه الى حد ما لل interfaces في اللغات ال object oriented زي ال c# و ال java

بكتبها بكلمه interface و بديها اسم و بفتح اقواس و ابتدي اكتب ال types بتاعتي 

مثال ال user

طيب انا كده كتبت ال interface بتاعتي و اقدر استخدمها زي اي typescript type عادي جدا

و اقدر استخدم جواها كل الي اتعلمناه قبل كده زي ال tuples و ال arrays و ال optionals و ال functions 

كمان اقدر اخليها تعمل extend ل interfaces تانية برضو زي اللغات ال object oriented 

يعني ممكن يبقى عندي base interface و interfaces تانية بتزود عليه عن طريق ال extends

و كمان اقدر اعمل extend لاكتر من interface ف وقت واحد 

مثال

و حاجة برضو شبه اللغات ال object oriented هي اني اقدر اخلي class ي implement interface و ده بيفرض عليه انه ي implement ال functions و ال variables الي فيها

الشكل ده بتشوفه ف angular مثلا مع ال life cycle methods كل واحدة فيهم متعرفه ف interface و عشان تستخدمها بت implement ال interface الي انت عاوزها

معلومة مهمة لازم تعرفها ف الاول هي ان ال interface تقدر تمثل ال objects و ال functions بس يعني تستخدمها بس لما تكون عاوز توصف شكل Object او function بس 

انما في حجات تانية زي ال unions و ال mapped types و غيرهم دول بنستخدم معاهم ال types زي ما هنشوف كمان شوية

طيب كل الي فات احنا بنستخدم ال interfaces عشان نمثل ال objects ازاي نخليها تمثل function 

ال interfaces بتمثل ال functions عن طريق معلومة صغيرة في ال js الا و هي ان ال functions عبارة عن object عادي جدا بس عنده call signature 

يعني عنده حاجة يقدر يعملها لما اناديه باستخدام الاقواس 

ف عشان اوصف ده في typescript اقدر اكتبله اقواس و اكتب فيهم ال params لو في و احط قصادهم ال return type بتاعي 

مثال على فنكشن ال add 

و مش بس كده ده كمان ممكن احط properties تانية جمب ال call signature لانها ف الاول و ف الاخر object عادي ف ممكن احط فيه كذا حاجة 

الشكل ده بتشوفه مثلا في ال testing libraries زي jest و vitest هتلاقي عندك ال function بتاعه ال test تقدر تناديها و ف نفس الوقت عليها properties تانية

مثال عليه

## ال types

هي في الحقيقة مسمهاش types اسمها type aliases و alias يعني اسم بديل ف هي مش بتعمل حاجة جديدة هي مجرد اسم بديل ل type موجود عندك 

و بالتالي اقدر امثل بيها اي حاجة سواء object او function او array او tuple او union او mapped type او حتى ادي اسم ل built in type من الي جايين جاهزين في اللغة 

حتى انت ممكن تفكر فيهم انهم زي ال variables بالنسبة لعالم ال types يعني زي ما انت بتعرف variable و تديله قيمة لحاجة موجودة عندك او نتيجة عملية كذلك ال type aliases بنعرفها و نديها type تاني ممكن يكون كبير او معقد عشان نقدر نعيد استخدامه

تعالى نشوف بنستخدمه ازاي

زي ما بنعرف variable ب const مثلا و نديله اسم و علامة يساوي و قيمة نفس الكلام بنعرف type alias بكلمه type و نديله اسم و علامة يساوي و قيمة و القيمة ممكن تكون اي شئ زي ما قلنا من شوية

مثال ال user و ال add

و زي ال interfaces اقدر ادمج اكتر من type سوا عن طريق ال intersection باستخدام علامة ال & 



لكن خد بالك ان ال interface extends مختلف عن ال type intersection و هنتكلم عنه اكتر ف نهاية الفيديو و فيديوهات جاية ف متنساش اللايك و السبسكرايب عشان ميفوتكش

طيب احنا كده شوفنا ال interfaces و ال types و لاحظنا انهم متشابهين بشكل كبير و بيعملو حجات كتير شبه بعض ف هل في بينهم فرق فعلا و لو في امتى استخدم ايه ؟

## الفروقات

اول فرق تقدر تلاحظه بكل سهوله هو ان ال interface بتمثل ال objects و ال functions بس في حين اني اقدر امثل اي شئ بال types 

في فروقات تانية زي ايه الي بيحصل لما اعمل اتنين بنفس الاسم 

في حالة  ال types هيبقى عندي error زي ال variables بالظبط 


و في حالة ال interfaces هيحصل حاجة اسمها declaration merging الي هو باختصار ان typescript هتدمج الاتنين ف واحد و من غير ما تقولك و من غير ما يحصل اي حاجة 

يعني انت مثلا ممكن تبقى شغال على interface اليوزر مثلا الي انت كاتبها فوق و يجي حد يكتب interface اليوزر تاني تحت بعيد تيجي تبص عاليوزر تلاقيه بقى عنده properties زيادة جم منين من ال declaration merging 

و ده تقدر تعتبره سلاح ذو حدين يعني زي ما ممكن يسبب لك مشاكل لو مخدتش بالك تقدر تستخدمه لصالحك عن طريق انك ت merge properties جديدة ف interfaces موجودة بس متقدرش تعدل عليها زي مثلا window او ال document او ال interfaces بتاعة library انت بتستخدمها زي في express مثلا تقدر تزود حجات عال request و ال response 
في فروقات بتظهر لما تيجي تدمج حاجتين سوا 

يعني مثلا افترض ان عندنا ٢ interfaces فيهم نفس ال property هيحصل ايه لما اخلي واحدة ت extend التانية ؟  طب لو كانو types هيحصل ايه ؟ تعالى نشوف 

هتلاحظ ان ال interface بتديك error عشان هي مش عارفه تتصرف في حين ان ال types بتدمجهملك عادي بس مش زي ما انت متخيل هي كمان بتدمج ال type بتاع ال property و ده ممكن يؤدي ل types غير متوقعه زي هنا جينا ندمج string مع number طلعنا never

و لو انت مش فاهم ده حصل ازاي ف الفيديوهات الجاية هتتكلم بشكل اكبر عن ال unions و ال interfaces و ال unknown و ال never ف خليك متابع عشان تفهم 

اخر فرق ما بينهم و ده مش هتلاحظه غير لو عندك مشروع كبير جدا هو ان ال interface extends اسرع من ال type intersection 

و خد بالك انا مقولتش ال interface اسرع من ال type انا قولت ال extend اسرع من ال intersection ف لو انت مبتستخدمهمش مش هتلاحظ فرق لكن لو بتدمج types كتير ف الكود بتاعك و عندك مشروع كبير هتلاحظ ان ال extends اسرع بحوالي الضعف من ال intersection 

و ده مش كلامي انا ده كلام ميكروسوفت نفسهم و كلام شركات كتير شافت زيادة ف الاداء بعد ما غيرت من ال intersection لل extends

و عشان نختم اقدر اديك فكرة بسيطة جدا عشان تعرف تستخدم مين امتى

استخدم ال interface عشان تمثل ال objects و استخدم ال types لكل شئ اخر

يعني وانت بتنظم مشروعك ولقيت عندك مثلا يوزر وبروداكت وكارت وحاجات ثانيه كثير استخدم لهم interface وبعد كده عايز تعمل types مخصصه اكثر او عايز تعمل يونيunions او عايز تعمل حاجات ثانيه دي تقدر تعملها ب types عادي و ده الي انت هتشوفه لو بصيت في مشاريع كبيرة او بصيت على ال libraries الي انت بتستخدمها.