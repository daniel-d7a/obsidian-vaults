---
title: ايه هو ال useSyncExternalStore و ازاي هو مستخدم حوالينا
pub_date: ""
date_started: 14/03/2025
intro: واحد من ال hooks الي الكلام عنها قليل مع انه من اهم ال hooks الي مخليه react تكون reactive من الاساس تعالى نتعرف عليه و نشوف بيشتغل ازاي
published: false
---

#status/in_progress #react/hooks #my_articles

هنتكلم عن ايه

- ايه هو ده
- بيتكون من ايه
- ايه استخدامه
	- عشان اربط رياكت بحاجة برا رياكت
		- حجات زي ال global state
		- ال window events
		- ال network events
	- عشان ال over returning hooks 
		- زي اني بربط مع ال scroll مثلا و مش عاوز كل مرة اعمل rerender
	- عشان اعمل نظام selector
- كنا بنعمل الحجات دي قبل كده ازاي
- عن طريق state و effect و نخلي ال hook يعمل force rerender
- امثلة عمليه عليه زي مثلا في zustand و redux 


هنتكلم النهاردة عن ال useSyncExternalStore hook و ده hook جديد نسبيا ظهر مع react 18 عشان يدعم ال concurrent features الجديدة بتاعتها

فكرة ال hook جايه من اسمه هو انه بيسمحلنا اننا نعمل sync ما بين react و اي external store و تحديدا عشان اقدر ا subscribe على تغييرات خارجية و اخلي ال components بتاعتي تقدر تتعامل معاها

بيتكون من ايه 

بيتكون من حاجتين اساسيين الي هما ال subscribe fn و دي العقد الي ما بينك و بين ال external store الي بتقوله فيه امتى يحصل rerender لل components عندك و ده بيتم على حسب ال subscription الي بتتعامل معاه.

و دي شبيهة شوية بال effect fn بتاعة use effect من حيث انك بتعمل ال subscription و بترجع clean up function 

الحاجة التانية هي ال get snapshot fn و دي بنستخدمها لما يحصل rerender عشان نجيب اخر قيمة من ال external store

في حجات زيادة زي ال get server snapshot و وده لان ال hook ده يقدر يشتغل عل ال server ف دي بنستخدمها لما يكون في فرق ما بين الطريقة الي اقدر اجيب بيها البيانات من ال external store على ال client و ال server و لو مديتهالوش تلقائيا بيستخدم get snapshot على ال client و ال server 


و في package من react اسمها use sync external store with selector بتديك نفس ال hook بالاضافة ل اضافتين زيادة هما ال selector عشان تقدر تختار اجزاء معينة بس من ال state و equality fn عشان تحدد بنفسك لو ال state القديمة زي الجديدة (و بالتالي ميحصلش rerender ) او لا


امتى بستخدمه ؟

في امثلة كتير على مصادر بيانات خارجية انا ممكن ابقى حابب ا subscribe عليها زي مثلا ال window فيها حجات كتير زي مثلا
- ال online status من ال navigator 
- ال scroll position 
- ال intervals
- ال local storage 
- و عامة اي حاجة ليها event انا احب ا subscribe عليها


و في مصادر تانية غير ال window كذلك زي اني اكون بتعامل مع global state management solution مش مخصص ل react زي redux (مش react redux) او اني حتى اكون بعمل ال state management solution بتاعي 


امثلة بالكود

لو بصيت كده هتلاحظ ان حجات كتير من دي ممكن ال use effect يعملها و كنا بالفعل بنعملها بيه لكن ال hook ده افضل من ال use effect في جزئية ال subscriptions لاكتر من سبب

اولا انه بيشتغل اثناء ال render مش بعده زي ال useEffect ف ده بيخليه يضمن ان كل ال components الي بتستخدمه عندها نفس الداتا في حين لو استخدمنا ال use effect مع مصدر بيانات بيتغير بسرعة ممكن يحصل ما يعرف ب ال tearing الي معناه اني عندي اكتر من نسخة من نفس ال component لكن في ما بينهم اختلاف ف البيانات 

المشكلة دي ظهرت مع react 18 مع ال concurrent apis الجديدة زي start transition عشان دي بتسمح ل react انها توقف ال render و تكمله بعدين ف ممكن تؤدي لحدوث ال tearing 

و تقدر تجرب ده بنفسك من هنا code pen 

كمان use sync external store بيدعم ال ssr و ال hydration لانه من ال hooks القليلة الي ممكن تشتغل على السيرفر على عكس ال use effect الي مش بيشتغل غير على ال client

و كمان هو ف الاخر معمول عشان يتعامل مع ال subscriptions ف بيديك api سهل لو حاولت تقلده باستخدام use effect هتكتب كود اكتر و هتاخد اداء اقل


مثال








مقال تاني 

ازاي استخدم use sync external store عشان اتعامل مع ال over returning values

تكمله للمقال الاخير الي اتكلمنا فيه عن ال useSyncExternalStore هنشوف ازاي نستخدمه عشان نعمل selector hook بيرجعلنا ال data الي احنا محتاجينها بس 


الفايدة من ده انك تقلل ال rerenders الغير مطلوبة ف بالتالي تزود الاداء.

و ده بيتم عن طريق انك لما تعمل subscribe على external store تزود function بتختار بيها الجزئ الي انت مهتم بيه و بالتالي ميحصلش rerender غير لو الجزء ده اتغير

احد استخدامات ده لو انت بتعمل state management solution بحيث تتابع التغييرات على جزء معين من ال state 

و لو بصيت على ال state management solutions المعروفين زي react redux و zustand هتلاقيهم بيعملو كده فعلا

و كمان لو بتتابع event بيتغير بسرعة زي ال scroll position تقدر تتحكم ف سرعته زي انك تتابعه كل ١٠٠ بيكسل بدلا من كل بيكسل

## References

- [[My articles]]
- [helper article 1](https://thisweekinreact.com/articles/useSyncExternalStore-the-underrated-react-api)
- [helper article 2](https://blog.saeloun.com/2021/12/30/react-18-usesyncexternalstore-api/)
- [helper article 3](https://jser.dev/2023-08-02-usesyncexternalstore/)
- [react docs](https://react.dev/reference/react/useSyncExternalStore)
