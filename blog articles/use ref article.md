السلام عليكم ازيكو عاملين ايه ؟ في مقالة النهاردة جايين نتعرف على ال use ref hook بشوية تفصيل. 
  
ال use ref hook هو react hook بيرجع قيمة بتتحفظ ما بين ال renders بس لا اكثر ولا اقل. 
  
زيه بالظبط زي ال use state بل كمان ممكن نقول انه هو اصلا عبارة عن use state مع شوية فروقات صغيرة و زي ما احنا عارفين ال use state بيرجعلي قيمة بتتحفظ ما بين ال renders و setter function عشان اقدر اغير بيها القيمة دي و اعمل rerender لل ui. 
  
انت ممكن تتخيل ال use ref من جوه كأنه بينادي ال use state و بياخد القيمة الي انت بتديهاله يحطها قيمة default عبارة عن object جواه property واحدة فقط اسمها current قيمتها بالقيمة الي انت اديتها لل use ref hook و بعد كده يرجعلك ال value الي رجعت من ال use state من غير ما يديك ال setter function, حاجة زي كده:
```ts 
function useRef(initialValue){
	const [ref] = useState({ current: initialValue })
	return ref
}

// ...

const ref = useRef("eyad") // ref = {current: "eyad"}
```

هنا ممكن يجي ف بالك اكتر من سؤال زي مثلا: -  
- ليه مش بيديني setter function ؟  
- لما ميدينيش setter function هغير القيمة ازاي ؟  
  
ده فرق من فروقات ال ref عن ال state ان ال state بتتغير ب ال setter function عشان تعمل rerender لل UI انما ال ref نقدر نغيره من ال variable عادي و بالتالي مش هيعمل rerender لل component و مش هحتاج setter function  
  
ال refs معمولة عشان احط فيها بيانات انا محتاج احافظ عليها ما بين ال rerenders بس مش محتاجها ف ال ui و بالتالي مش بحتاج اعمل rerender لما اغيرها  
  
- طب لما هو بيحفظ data زي ال use state ليه عملوله hook لوحده طب ما انا استخدم use state بنفسي و خلاص ؟  
  
ده لان حفظ الداتا هو واحد من استخدامات ال refs و ليهم استخدام تاني مهم جدا هو انهم بيخلوك تقدر تتعامل مع ال dom زي ما هنشرح تحت  
  
- ايه استخدامات حاجة زي كده  
-  
ليها استخدامين اساسيين اولهم حفظ ال data بين ال renders بس مش اي data و خلاص كده  
لو ال data دي ليها علاقة بال UI زي مثلا اسم المستخدم او ال todos او اي حاجة متعلقة بال UI لازم تتحفظ ف state  
ده لانها reactive data يعني تفاعليه بتتغير و لما تتغير لازم التغير ينعكس على ال UI  
انما ال ref بيستخدم عشان نحفظ فيه اي data غير متعلقة بال UI زي مثلا ال interval id او ال timeout id  
(شوف سلايد ٢ و ٣ تحت)  
  
و حاجة كمان مهمة جدا ف ال refs انه بيساعدك تتحكم في ال DOM nodes عن طريق ال DOM methods زي query selector او add event listener او غيرهم.  
ده عن طريق انك تعمل ref و تديه لاي DOM node ف ال ref property بتاعتها و react تلقائيا هتخلي ال current بتاع ال ref عبارة عن ال DOM node دي  
(شوف سلايد ٤ تحت)  
  
بس لازم تخلي بالك ان عمليه ربط ال DOM node بال ref بتحصل بعد ال rendering ف يفضل تستخدم ال DOM node جوه event handler زي ال on click مثلا او جوه use effect عشان تضمن ان ال node مش undefined  
  
اخر معلومة نختم بيها ال post ده هي ان ال use ref يعتبر escape hatch يعني موجود عشان نطلع برا سيستم react زي انك تتحكم بال DOM بشكل مباشر او تتعامل مع library مش مكتوبة ل react فلازم قبل ما تستخدم ref تتأكد انك محتاجه الاول و بعدها تستخدمه بحذر مش عمال على بطال لانه غالبا هيؤدي لنتايج عكس ما انت متوقع