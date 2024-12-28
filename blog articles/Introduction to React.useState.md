

في المقالة دي هنتكلم عن شوية خصائص في ال use state hook و نفهم ازاي نقدر نستخدمه باحسن شكل ممكن. 

كلنا عارفين انه بيستخدم عشان يحفظ الداتا جوه ال components بتاعتنا عن طريق انه بيرجعلك variable شايل الداتا و setter function عشان تغير بيها الداتا و تعمل rerender لل component بالشكل التالي:

```ts

```
const [counter, setCounter] = useState()
ال setter function ممكن تستخدمها بطريقتين يا اما انك تديها القيمة الجديدة بشكل مباشر زي كده:

setCounter(10)
و دي هنا بتشيل القيمة القديمة من ال state و تحط القيمة الجديدة.

او انك تديها updater function و دي بتكون function بتاخد parameter واحد عبارة عن قيمة ال state القديمة و ال return بتاعها بيكون هو القيمة الجديدة لل state زي كده:

setCounter(c => c + 10)
ف المثال ده عندنا function بتاخد parameter اسمه c عبارة عن قيمة counter الحالية الي احنا حطيناها ب 10 ف المثال الي فات و بترجع c + 10 الي هي هتبقى 20 و دي بتكون قيمة counter الجديدة.

طب كده ايه الفرق ما بين الاتنين ؟ خلينا نشوف مثال: -

اوقات كتير بنحتاج نعدل ال state بناء على قيمة ال state نفسها زي مثلا لو عندك counter و عاوز لما تضغط زرار معين تزوده ب 1 ممكن تستخدم الطريقتين:

setCounter( counter + 1 )
setCounter( c => c + 1 )
ف المثال ده الفرق ما بينهم مش كبير بس الفرق هيبان اكتر لو حاولت مثلا انك تنادي setCounter اكتر من مرة ورا بعض و لنفترض مثلا ان ال counter قيمته 0 و انت عاوز لما يضغط عالزرار تزوده 2 ف هتعمل كده:

setCounter( counter + 1 )
setCounter( counter + 1 )
هتيجي بعدها تشوف ال counter هتلاقيه قيمته ب 1 مش 2 مع انك عملت setCounter مرتين، بس ليه؟

المشكلة هنا ان السطرين الي فوق كلهم بيعملو setCounter بنفس القيمة و ده بيحصل لان قيمة counter مش بتتغير بعد كل سطر عشان كده وقت ما انت كتبت ال setCounter ف الrender ده كانت قيمة counter ب 0 و بالتالي كلهم شايفينها 0.

ده لان react مش بتغير ف ال state اول اما تشوف الsetter function لا هي بتشوف كل حاجة بتعمل setState و تحطها ف queue و بتنفذها بعدين مرة واحدة بالتالي الكلام الي مكتوب فوق بيتم تنفيذه كده:

<<<<<<< HEAD
```ts
setCounter( counter + 1 ) // setCounter( 0 + 1 )
setCounter( counter + 1 ) // setCounter( 0 + 1 )
```
=======
setCounter( 0 + 1 )
setCounter( 0 + 1 )
>>>>>>> origin/main
لانهم معتمدين على قيمة counter الي لسه متعملهاش update و لو عاوز تتأكد ممكن تعمل console.log(counter) بعد ال setCounter هتلاقيه كمان ب 0.

الطريقة الصح هنا انك تستخدم updater function جوه ال setCounter لانها بتاخد اخر قيمة لل state وقت ما تيجي تعمل update للقيمة و rerender لل component مش وقت ما انت تستخدمها ف لما تيجي تعملها اكتر من مرة ورا بعض لما تيجي تتنفذ قيمتها هتتحط صح زي كده:
```ts
// c = 0
setCounter(c => c + 1) // 0 => 0 + 1 = 1
// c = 1
setCounter(c => c + 1) // 1 => 1 + 1 = 2
```
و ف النهاية قيمة ال counter هتكون 2 بعد ما يحصل rerender.

او ممكن تريح نفسك من كل ده و تعمل
```ts
setCounter(counter + 2)
```


بس ساعتها مش هيبقى عندنا مثال 😉

فرق تاني بينهم و كمان ميزة لل updater function انها مش بتعتمد على اي حاجة من برا ال updater function، ف لو انت مثلا بتستخدمها من جوه اي حاجة ليها dependency array زي use Effect مش هتحتاج انك تحط ال state القديمة ك dependency ليها

و دول لينكات فيها كلام اكتر عن الموضوع ده:
Link 1 Link 2
و اخر لينك ده في تاسك انك تعمل ال update queue بنفسك لازم تجربه.