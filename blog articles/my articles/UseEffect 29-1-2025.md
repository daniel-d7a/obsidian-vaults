
ف المقال ده هنتكلم عن ال use effect hook من جميع الجوانب هنفهم وظيفته في react
  
لو سألت ١٠ اشخاص مختلفين ايه وظيفة ال use effect hook هيجيلك ١٠ اجابات مختلفة ..
  
الي هيقولك انه بيعمل حاجة لما ال UI يحصله render.
الي هيقولك انه مستخدم عشان تجيب داتا من API.
الي هيقولك انه موجود عشان يراقب قيم معينة ولما تتغير يعمل حاجة.
  
احنا ممكن نجمع الردود دي كلها في اجابة واحدة من جزئين: 

اولا: ال use effect hook هو escape hatch زيه زي use ref بيسمحلنا نتواصل مع حجات برا react جوه ال components بتاعتنا.  
  
حجات زي: -
- ال DOM APIs زي add event listener و ال intersection observer.
- ال APIs الخارجية و اني اجيب منها data باستخدام ال fetch API.
- اي element خارجي مش معمول عشان react زي custom video player او map component او jQuery plugins مثلا.
  
ثانيا: هو كمان بيسمحلنا اننا نعمل synchronization ما بين ال component بتاعنا و السيستم الخارجي ده. بمعنى ان ال لما ال system الخارجي يتغير ال UI يتغير معاه و العكس صحيح.  
  
طب الكلام ده كله بيحصل ازاي ؟  ال use effect hook بيتكون من ايه ؟ طب اقدر استخدمه ازاي ؟  كل دي اسئلة هنجاوب عليها في المقال ده.

## مكونات ال useEffect
  
هو بشكل عام بيتكون من ٣ اجزاء  
- ال Effect. 
- ال Clean up.
- ال Dependencies.

``` ts
// add highlightes to these parts
import {useState, useEffect} from "react"

export default function App({ roomId }){

	const [serverUrl, setServerUrl] = useState("https://localhost:5173")

	// effect
	useEffect(()=>{
		const connection = createConnection(serverUrl, roomId)
		connection.connect()

		// clean up
		return ()=>{
			connection.disconnect()
		}
		
	}, [roomId, serverUrl]) // dependencies

}
```
  
تعالى كده نفصل ف شرحهم على اكتر من مثال: -  

ال effect ده الحاجة الي انت عاوز تعملها و بيتنفذ اول لما ال component يظهر اول مرة او لو ال dependencies اتغيرت بعد اي rerender و ده غالبا بيبقى له تأثير على حاجة او بيستخدم حاجة من برا ال component و ليكن مثلا انك تعمل event listener او تعمل fetch لشوية data او تعمل set timeout.  
  
ال clean up دي بتبقى حاجة عكس ال effect بالظبط و بتشتغل لما ال component يتشال من ال component tree او لو ال dependencies اتغيرت بعد اي rerender بس قبل ما يتم تنفيذ ال effect الجديد و دي موجودة عشان لما ال component يتشال ميسبش وراه اثر بحيث ال effects متدخلش ف بعض ما بين ال rerenders ف لازم ايا كان ال effect يبقى في حاجة بتعكسه او بتلغيه و لو كان حاجة ملهاش تأثير باقي يبقى مش محتاج تعمل clean up (مع العلم انه لو حاجة ملهاش تأثير ف هي غالبا مش effect و مش محتاج تحطها ف use effect)
  
لو كان fetch ممكن تستعمل abort controller
``` ts
useEffect(()=>{
	const abortController = new AbortController();
	async function fetchData(){
		const response = await fetch(url, {
			signal: abortController.signal,
		})
	}
	
	fetchData()
	
	return ()=>{
		abortController.abort()
	}
}, []) 
```

لو كان set timeout او interval ممكن تستعمل clear timeout او clear interval 
``` ts
useEffect(()=>{
	const timer = setTimeout(()=>{
		console.log('1 second later')
	}, 1000)

	return ()=>{
		clearTimeout(timer)
	}
}, []) 
```

لو كان add event listener ممكن تستعمل remove event listener  
``` ts
useEffect(()=>{
	function handleMove(e){
		console.log(`mouse at ${e.clientX}, ${e.clientY}`)
	}
	window.addEventListener("pointermove", handleMove)

	return ()=>{
		window.removeEventListener("pointermove", handleMove)
	}
}, []) 
```  

و كمان على حسب ال effect تقدر تعمل ال cleanup المناسب.





لو انت جاي من ايام ما كانت react بتستخدم ال class component ف ال effect ممكن يعتبر بديل لل componentDidMount و componentDidUpdate و ال cleanup بديل لل componentWillUnmount.
## ال dependency array

ال dependency array ده بيبقى array من القيم الي ال effect بيعتمد عليها بحيث ان لو حاجة منهم اتغيرت انا بحتاج اعمل re-run لل effect عشان يبقى in sync مع ال data الي اتغيرت دي.
  
كل rerender بنقارن القيم الي موجودة ف ال dependency array بالقيم الي كانت موجودة ف ال render الي فات و لو لقينا واحد فيهم عالاقل مختلف هيشغل ال cleanup بتاع ال effect الي فات و بعدها يشغل ال effect تاني بالقيم الجديدة.

و عشان نبسط الموضوع اكتر ده ترتيب تشغيل اجزاء ال useEffect hook:

``` ts
// add a mermaid graph for these steps
```

1. ال component بيظهر لاول مرة (mount)
2. ال effect بيشتغل لاول مرة
3. بيحصل rerender
4. لو في dependency array بنقارن ال dependencies من ال render القديم مع القيم الموجودة حاليا
5. لو في اختلاف في ال dependencies بنشغل ال cleanup function (لو موجودة) بالقيم القديمة
6. بنشغل ال effect بالقيم الجديدة
7. ال component بيتشال (unmount)
8. بنشغل ال cleanup function (لو موجودة) باخر قيم موجودة معانا

ايه القيم الي ممكن تكون ف ال dependency array ؟ اي قيمة reactive يعني ممكن تتغير ما بين ال rerenders زي ال props او ال state مثلا و كمان اي variable بياخد قيمته من props او state و اي function مكتوبة جوه ال component سواء بتستخدم قيم من ال state او ال props او لا (بس دي فيها اعتبارات هنتكلم فيها كمان شوية) ولو انت بتستخدم linter زي eslint مثلا هتلاقيه بيقولك لو ال dependency array ناقصه حاجة.
``` ts
// add highlightes to these parts
import {useState, useEffect} from "react"

// props are reactive
export default function App({ roomId }){

	// state is reactive
	const [serverUrl, setServerUrl] = useState("https://localhost:5173")
	
	useEffect(()=>{
		const connection = createConnection(serverUrl, roomId)
		connection.connect()
		return ()=>{
			connection.disconnect()
		}
		
	}, [roomId, serverUrl]) // dependencies
}
```

```ts
// add highlightes to these parts
import {useState, useEffect} from "react"

export default function App(){
	const [firstName, setFirstName] = useState("eyad")
	const [lastName, setLastName] = useState("alsherif")

	// name is reactive
	const name = firstName + " " lastName
	
	useEffect(()=>{
		console.log(name)
	}, [name]) // dependencies
}
```

و ال dependency array ممكن يبقى فاضي و ده معناه ان ال effect بتاعك مش معتمد على قيم خارجية يبقى كده ال effect هيحصل مرة واحدة بس اول لما ال component يحصله mount و ال cleanup هيحصل مرة واحدة بس لما ال component يحصله unmount.

```ts
// add highlightes to these parts
import {useState, useEffect} from "react"

export default function App({ url }){
	const [data, setData] = useState(null)

	// effect only runs once
	useEffect(()=>{
	
		async function fetchData(){
			const response = await fetch(url)
			const jsonData = await response.json()
			setData(jsonData);
		}
		
		fetchData()
	}, []) // no dependencies
}
```
  
و ال dependency array ده optional اصلا يعني ممكن تشيله و متحطهوش من اساسه و ده معناه انك عاوز ال use effect hook بتاعك يشتغل بعد كل rerender و ده استخدامه قليل عشان ممكن يأثر عال performance بتاع الويبسايت

```ts
// add highlightes to these parts
import {useReducer, useEffect, useRef} from "react"

export default function App({ url }){
	const rerenderCount = useRef(0)
	// this forces the component to rerender
	const rerender = useReducer(x => x+1, 0)[1]

	// effect runs on every rerender
	useEffect(()=>{
		rerenderCount.current += 1;
	}) // no dependency array

	return <button onClick={rerender}>rerendered {rerenderCount.current} times </button>
}
```

 اهم معلومة لازم تعرفها هنا ان ال use effect hook لما يجي يقارن ال dependencies القديمة بالجديدة بيستخدم [Object.is](http://object.is/) يعني لازم القيمة تكون نفسها و ال reference كمان يكون نفسه و لو لقى واحدة فيهم عالاقل مختلفة بيشغل ال cleanup القديمة و يشغل ال effect تاني.
 
 ده مش مهم لو كانت ال dependencies بتاعتنا primitives زي ال strings او ال numbers بس هتعمل معانا مشاكل لو كانت reference types زي ال functions و ال objects و ال arrays عشان لما تيجي تكتب function او object جوه ال component هتلاقيه بيحصله creation بعد كل rerender و بالتالي ال reference بتاعه هيتغير و بالنسبة لل use effect هيبقى قيمة مختلفة عن الي فاتت و ال effect بتاعك هيشتغل مع ان مفيش حاجة اتغيرت.

```ts
import {useReducer, useEffect} from "react"

export default function App(){

	// this object is recreated on every rerender
	// and its reference is not stable
	const user = { name:"eyad", age:23 }

	// effect runs on every rerender
	// even if user doesn't change
	useEffect(()=>{
		console.log(user)
	}, [user]) 
	
}
```
  
لكن لا تقلق فالحل بسيط، الحل انك متعتمدش على حاجة ال reference بتاعها بيتغير بعد كل rerender او انك تحاول تخلي ال reference بتاعها يتغير لما هي تتغير فعلا او لو هي قيمه ثابته يبقى تثبت ال reference انه ميتغيرش. طب تعمل حاجة زي دي ازاي ؟  

### حلول مشاكل الاعتماد على ال reference types في ال dependency array
  
1. لو بتعتمد على حاجة ثابته يبقى اكتبها برا ال component بتاعك كده ال reference بتاعها هيفضل ثابت على طول
```ts

import {useReducer, useEffect, useRef} from "react"

// this objects doesn't change.
// and its reference is stable
const user = {name:"eyad", age:23}

export default function App(){

	// user is not a dependency 
	useEffect(()=>{
		console.log(user)
	}, []) 
	
}
```
  
لو بتعتمد على حاجة بتحتاج قيم من ال component عندك اكتر من حل: - 
  
2. ممكن تكتبها جوا ال useEffect كده هو مش هيعتبرها dependency اصلا بس كده مش هتقدر تشوفها برا ال effect.

```ts

import {useReducer, useEffect, useRef} from "react"

// this objects doesn't change.
// and its reference is stable
const user = {name:"eyad", age:23}

export default function App(){

	// user is not a dependency 
	useEffect(()=>{
		console.log(user)
	}, []) 
	
}
```
  
لو محتاج تشوفها برا ال effect عندك حل تاني انك تحطها جوا state او useMemo لو هي object او array او تحطها جوا useCallback لو هي function بحيث ان ال reference بتاعهم يبقى ثابت معظم الوقت و يتغير بس لو الحاجة فعلا محتاجة تتغير.  
  
  
ده كده الحل لو ال dependencies بتاعه ال useEffect كلها موجودة جوه ال component طب لو كانت بتجيلك من ال props تعمل ايه ؟  
  
هنعرف البوست الجاي ان شاء الله.  
  
و كده ال effects بتاعتك بتشتغل لما القيم الي هي معتمده عليهم بس تتغير  
  
بس بعد كل ده ممكن برضو تلاقي ال effect بتاعك بيشتغل مع انك عامل كل الخطوات الي فوق دي طب ايه السبب ؟  
  
### مشكلة الاعتماد على dependencies من خارج ال component  
  
المشكلة دي بتحصل ف حالة ان ال component بيستقبل props نوعها object او function او array و ال props دي مكتوبة بشكل يخليها تتغير بعد كل rerender زي مثلا انها تبقى مكتوبة inline على ال component نفسه.
  
و من اكتر الامثلة شيوعا على حاجة زي كده لما بكون عامل button component مثلا و بديله onClick handler (صورة ٢)  
معظمنا بيكتب ال onClick بشكل inline و ده ف معظم الحالات بيكون عادي الا لو في effect معتمد عليها ساعتها هتخلي ال effect ده يشتغل اكتر من مرة  
  
ف الحالة دي بيحصل اكتر من حاجة  
- لما ال parent يحصله rerender ال inline props او اي variable جواه بتتعمل من اول و جديد و ف حالة لو كانت object او function ال reference بتاعها بيتغير و ده بيخلي ال child component يحصله rerender حتى لو قيم ال props بتاعته متغيرتش  
- كل مرة ال component يعمل rerender ال props بتاعته بتتغير و ده بيخلي ال effects المعتمدة على ال props تشتغل تاني مع ان قيمها متغيرتش برضو  
  
طب ازاي نحل المشكلة دي ؟  
نفس الحل الي اتكلمنا عنه البوست الي فات هنعمله هنا ف ال parent component  
هنشوف ايه ال props الي بتكون arrays او objects او functions و نحطها ف use memo او use callback او نطلعها برا ال parent component عشان متتأثرش بال rerenders ال ف حالة ان قيمتها اتغيرت فعلا  
ولو مش فاكر الطريقة هتلاقي لينك البوست الي فات ف اول كومنت

لا تنسو الدعاء لاخواننا في فلسطين و السودان  
السلام عليكم ازيكو عاملين ايه النهاردة جايين نكمل كلام عن ال useEffect hook و هنتكلم عن حاجة مهمة جدا  
  
 انت ممكن متحتاجش useEffect 

  
ال useEffect هي طريقة اني اعمل حاجة (effect) اول لما ال component بتاعي يظهر ف الصفحة (mount) او يتشال منها (unmount) او يحصله تحديث (rerender) ، و كمان هو طريقة اني اعمل side effects بدون ما يكون في event بيشغلها زي ضغطة ماوس او كيبورد مثلا.  
  
و كمان نقدر نقول ان ال useEffect هي زي مخرج طوارئ من نظام React. بتسمحلك "تخرج برا" React و تعمل حاجة بعيدا عن تحكم react زي تعامل مع ال network ، ال DOM، او المتصفح.  
ف في حالة ان مفيش نظام خارجي انت ف الغالب مش محتاج تستخدم useEffect و تقدر تحل مشكلتك بطريقة ابسط زي ما هنشوف ف الامثلة الي معانا.  
  
  
١- تحديث الـ State بناءً على State أو Props:  
  
ممكن تكون بتستخدم useEffect لتحديث الـ state بناءً على state أو props تانية. في الحالة دي، ممكن تعمل التحديث بتاعك مباشرة من غير useEffect او من غير state جديدة.  
  
حاجة زي انك تجمع اكتر من state ف variable واحد او انك تحسب داتا من state موجودة عندك كل ده تقدر تعمله مباشرة من غير useEffect او state جديدة  
  
٢- اعادة قيمة ال state لقيمة default في حالة تغير ال props:  
  
ف اوقات كتير بيكون عندك component جواه state و قيمة ال state بتتحسب بناء على prop ، ف بتكون عاوز لما ال prop يتغير قيمة ال state ترجع ب null او بقيمة default عندك ف بتلجأ لل useEffect  
مشكلة ال effect هنا ان ال component هيتعمله render مرتين ، مرة بال state القديمة بعدين ال effect يشتغل و يعمل rerender عشان يظهر بال state الجديدة  
  
مع ان ليها حل تاني و هو ان ال component الي قيمته مرتبطه ب props اديله key بنفس قيمة ال props دي  
  
لان بالنسبة ل react طالما ال key بتاع ال component اتغير ف ده معناه ان ال component اتغير و لازم اعمله mount من الاول تاني و ارجع اي state جواه لقيمتها الافتراضية.  
  
و هنتكلم بالتفصيل عن ال keys ف بوست قادم باذن الله.  
  
طريقة ال key كويسة لو انا عاوز اعمل reset لل state الي عندي كلها ، لكن مش هتنفع لو انا عاوز اغير ف state معينة و اسيب الباقي.  
  
في حل تاني هو اني احتفظ بالقيمة الي انا عاوز اعرف انها اتغيرت و كل مرة اشوف هل هي اتغيرت ولا لا و لو اتغيرت اقدر اعمل ال state updates الي انا عاوزها من غير use Effect و من غير ما اخلي ال component بتاعي يحصله render مرتين.  
  
لو الطريقة دي جديدة عليك متقلقش انت مش لوحدك ، و حتى ف ال docs بيحذرك من استخدامها كتير ، مع انها احسن من ال useEffect بس بتخلي ال debugging اصعب.  
ف يفضل انك تشوف طريقة تانية انك تحفظ بيها ال state بتاعتك زي مثلا انك تحتفظ بال id بتاع ال selected item بحيث تحسبه كل مرة تتغير ال items ب حسبة بسيطة من غير اي state زيادة.  
  
٣- التعامل مع ال user events:  
  
زي ما ذكرنا في البداية ، ال useEffect الغرض منها انها تشتغل لما ال component بتاعي يظهر ف الصفحة (mount) او يتشال منها (unmount) او يحصله تحديث (rerender) ، الجملة الي فاتت دي مفيها كلمة event لان ال useEffect مش الغرض منها التعامل مع ال events زي ال click و ال keyDown و غيرهم.  
  
ف لو انا عندي كود بيشتغل لما event يحصل يبقى مكانه مع ال event handler مش ف useEffect.  
  
ف مثلا لو تبص على الصورة من ٥ ل ٧ هتلاقي عندي فيهم useEffect صح لأن الغرض منها انها تشتغل لما ال component يظهر انما ال useEffect الغلط غلط لانها بتشتغل ردا على event من ال user.  
  
  
٤- سلاسل ال effects:  
لما تيجي تستخدم ال useEffect لازم تفكر ف كل useEffect عندك انه مستقل بذاته ، يعني مينفعش يبقى عندك اكتر من useEffect معتمدين على بعض لان كده هتكون بتعمل rerenders كتير ملهاش لازمة و بتوزع logic مرتبط ببعضه على اجزاء بعيده عن بعضها.  
  
ف المثال الي معانا هنا احنا بنحاول نعمل لعبة كروت بسيطة بس ال logic بتاعها متوزع على اكتر من useEffect ف لو شغلت الكود هتلاحظ انه بيعمل حاجى زي كده:  
setCard > render > setGoldCardCount > render > setRound > setIsGameOver > render  
  
هتلاقي ٣ renders موجودين بلا هدف في حين ان لو كان ال logic كله ف useEffect واحد زي الصورة الي بعدها هتلاقي عندك render واحد فقط.  
  
وغير كده لما اجمع ال logic المرتبط ببعضه ف مكان واحد ده بيخلي الكود اوضح و بيسهل الاضافة و التعديل عليه.  
  
و ف نفس الوقت متحطش كل حاجة جوا effect واحد ، لو عندك حجات مختلفة و كل حاجة ليها dependencies مختلفة يفضل انك تقسمهم على اكتر من useEffect واحد.  
  
ف المثال الي عندنا انا عاوز اعمل log visit كل مرة user جديد يدخل room جديدة بغض النظر هو بيستعمل اي serverUrl ، بس برضو لما الserverUrl او ال roomId يتغير بحتاج اعمل connection جديد .  
لو حطيت ال logic كله ف useEffect هتلاقي ان log visit بتشتغل لما ال serverUrl مع ان الداتا المرتبطة بيها متغيرتش بس لازم ال effect كله يشتغل ، ف هنا حل افضل اننا نفصلهم عن بعض.  
  
  
  
٥- التواصل من ال child لل parent:  
ف react المفروض التعامل و حركة الداتا ف معظم الاوقات بتكون من فوق من عند ال parent ل تحت عند ال child ، لكن ف بعض الاوقات بيبقى عندك state ف ال child ال parent مهتم بيها و محتاج يعرف لما تتغير ، زي مثلا انك تكون بتعمل data fetching ف ال child و محتاج الداتا ف ال parent.  
  
احد الطرق انك تعمل كده انك تبعت لل child بتاعك function ينفذها لما القيمة تتغير ، بس هتعرف ازاي ان القيمة اتغيرت ؟ عن طريق انك تعمل useEffect و تحط القيمة الي انت عاوزها ف ال dependency array عشان لما تتغير تشغل ال function الي جاية من ال parent.  
  
بس ده بيوقعك ف نفس مشكلة رقم ٢ انك بتحتاج تعمل render مرتين ، مرة عشان تعمل update لل child و مرة لل parent ، ف حلها هيكون انك بتشوف ال قيمة بتاعة ال child بتتغير فين (ف اي event مثلا) و تحط معاها ال function الي بتغير قيمة ال parent عشان تغيرهم الاتنين مرة واحدة.  
  
بس برضو ده عكس المتعارف عليه و الاحسن ان الداتا تمشي من ال parent لل child ف هنا هيبقى عندك حلين افضل من الي فات ده  
- ممكن ترفع ال state لل parent و تديها لل child ك props.  
- ممكن تستخدم pattern زي ال render props لو انت محتاج الداتا دي عشان ال render بس و مش عاوز تطلعها برا ال child.  
  
و لينا كلام عن ال patterns في react باذن الله.  
  
اخيرا و ليس اخرا  
٦- ال data fetching:  
  
ممكن تكون مستغرب ، اوومتعود انك بت fetch الداتا بتاعتك على طول ف ال useEffect ، هو ينفع لكنه مش افضل حل لان الطريقة دي مش بتتعامل مع حجات كتير زي ال loading state, error state, race condition و حجات غيرهم كتير لدرجة ان ال documentation بتاع react ذات نفسه بيرشحلك انك تستخدم فريمورك زي nextjs او data fetching library زي react query عشان تقدر ت fetch الداتا بشكل اسهل و افضل.  
  
هسيبلك تحت ف الكومنتات لينك مقال بيتكلم عن ليه احنا محتاجين react query بدل ما نستخدم ال useEffect و باذن الله هنتكلم عن react query بصفتها احد افضل الحلول لمشكلة ال data fetching في react في سلسلة بوستات زي دي قريبا ان شاء الله.