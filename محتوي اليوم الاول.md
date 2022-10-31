# محتوى اليوم الأول

محتوى الملف:
-  نظرة على Express
- دوال express()
- دوال Application
- الخصائصRequest
- دوال Response

# Express

يعتبر Express من أشهر web frameworks الخاصة في Node والتي تساعدنا على تطوير مواقع الويب و APIs.
 كما أنه يزودنا بالعديد من الخصائص مثل التعامل مع Requests المستقبلة بمختلف أنواعهاGET, POST… إلخ ومختلف المسارات أو الروابط (routers) وتحديد رد أو Response مناسب لها سواء كان الرد بعرض صفحة View أو غيرها مثل الرد من خلال إرسال البيانات بصيغة Json، أيضًا نستطيع استخدام Express لاضافة middleware في أي نقطة خلال التعامل مع Request.
 
 
لإنشاء express والذي يسمح لبرنامجك الاتصال بالسيرفر واستقبال requests نقوم بإستدعاء دالة ()express
 
    const express = require('express')
    const app = express()
     
 ## شرح مهمة الدالة ([express.json([options
يكمن دور الدالة عند استخدامها بالسّماح باستقبال ومعالجة البيانات القادمة من عملية request من نوع البيانات json، فسوف تقوم بإرجاع middleware التي تقوم بمعالجة نوع البيانات json فقط. 
     
     
     
## دالة ([express.Router([options

وظيفة هذه الدالة هي إنشاء كائن جديد من نوع Router.

     const router = express.Router([options])
مابين أقواس الدالة [option] يحدد سلوك الدالة، في الجدول التالي وصف لكل  option والسلوك الذي يحدده.


     
| سلوك الخاصية             | الخاصية            |               
| ---------------- | -------------------- | 
| تفعل حساسية حالة الأحرف من حيث كونها capital أو small.              | caseSensitive           | 
| في حال وجود نفس اسم المتغير في  req.body لكائنين يتم استخدام هذه الخاصية لاختيار احدهما              | mergeParams           |
  
##  دالة ([…app.delete(path, callback [, callback 
عند النقر على “حذف” في جزء معين من البرنامج يتم توجيه طلب الحذف هذا على دالة ()delete حيث ان path هي منطقة من البرنامج المراد تطبيق عملية الحذف عليها ، يتليها callback وهي الدالة التي ستطبق عملية الحذف.


### مثال:

     app.delete('/', function (req, res) {
         res.send('DELETE request to homepage')
        })


##  دالة (app.get(path, callback function
تستخدم هذة الداله لارسال طلب الى السيرفر  لجلب اي نوع بيانات سواء كانت ملفات او بيانات من نوع json وما الى ذلك والقيام باي عمليات على هذة البيانات داخل دالة callback . وتتكون الدالة من جزئين:

### ١-  الجزء الاول: وهو لتحديد الباث ويمكن ان تكتب كنص عادي او تكتب باستخدام regular expression او نص يجمع الطريقتان مثال : 

       
     app.get('/ab?cd', function (req, res) {
        res.send('ab?cd')
       })
          
هذا الباث سيطابق فقط  abcd او acd  


### ٢- الجزء الثاني : هي دالة callback  ويمكن ان تكون داخلها اي عمليه تريد اجرائها للطلب request  

###  مثال على ذلك 


        app.get('/', function (req, res) {
           res.send('GET request to homepage')
           })
           
  كما في المثال الموضح اعلاه عندما يقوم المستخدم بالطلب باستخدام الباث root ستقوم دالة callback بارجاع رسالة “GET request to homepage” 




## دالة app.post(path, callback [, callback ...])

تستخدم هذة الداله لادخال بيانات إلى السيرفر وللقيام بأي عمليات على هذة البيانات يكون داخل دالة callback .
تتكون الدالة من جزئين:



### ١-  الجزء الاول: وهو لتحديد path ويمكن كتابته على شكل نص أو باستخدام regular expression أو نص يجمع الطريقتان.
 

###  مثال على ذلك 


         app.post(/\/abc|\/xyz/, function (req, res, next) {
            next();
           });
هذاالباث سيطابق فقط`/abc` أو `/xyz`



### ٢- الجزء الثاني : هي دالة callback  ويمكن أن تكون داخلها أي عمليات تريد اجراءها.


        app.post('/', function (req, res) {
         res.send('POST request to homepage')
          })
كما في المثال الموضح أعلاه عندما يقوم المستخدم باستخدام الباث root ستقوم دالة callback بارجاع رسالة


       POST request to homepage


## دالة ([…app.put(path, callback [, callback
 وهي تستخدم غالباً للتحديث، لأنها توجه request إلى مسار path محدد مع callback functions خاصة به. 
وتستخدم بالشكل الموضح في المثال التالي :


        app.put('/', function (req, res) {
           res.send('PUT request to homepage')
           })


## دور الدالة ()app.listen
سوف نفهم دورها من خلال اسمها listen أي معناها السماع، ويقصد بذلك انها سوف تقوم بسماع اي عملية اتصال تربط  بين host و port او  path لكي يتم تنفيذ عمليات الخادم.


-  يمكن استخدامها وإعطائها path محدد مثال :


        const express = require('express')
        const app = express()
        app.listen('/tmp/sock')

ويمكن جعلها تستمع لعملية اتصال محدده بين host و port لكي يتم الربط بينهم وتنفيذ عمليات request و response بإعطائها رقم port محدد. 

- مثال:


       const express = require('express')
       const app = express()
       app.listen(3000)

## مفهوم ()app.use
هذا المفهوم يقصد فيه تحديد دوال Middleware لمسار معين وتنفذ هذه الدوال عندما يتطابق المسار الذي تم استدعائه مع المسار الموجود بدالة app.use .
الشكل العام للدالة هو ([..app.use([path,] callback [, callback .

ويقصد بـ path هو المسار الذي يتم عمل طلب (request) عليه وبشكل افتراضي إذا لم تحدد مسار سيكون المسار '/' ويسمى غالبًا root path
أما الجزء الآخر من الدالة وهو callback يمكن أن يكون دالة او مجموعة دوال او مصفوفة او خليط بينهم.
وكما ذكرنا أن المسار الافتراضي هو '/'  فسيتم تنفيذ جميع الدوال التي بداخل app.use ولم يتم تحديد مسار لها عند كل request لتطبيقك ، كما بالمثال التالي سيتم تنفيذ هذه الدالة عند كل طلب (request) في تطبيقك :


        app.use(function (req, res, next) {
          console.log('Time: %d', Date.now())
           next() 
         })
         
دوال الـ Middleware تنفذ بشكل متتابع فالترتيب فيها مهم ويمكن أن يتم كتابة عدة دوال في جزء callback وتنفيذها واحدة تلو الأخرى لكن يشترط أن يكون بالدوال next وتعني الإكمال للدالة التي تليها وعند آخر دالة لا يتم كتابة next وإنما تعطى النتيجة النهائية للرد كما بالمثال التالي:

             
       function printTime (req, res, next) {
        console.log('Time: %d', Date.now())
         next()
       }
       function welcomeMassage(req, res, next) {
       res.send('Welcome to Express')
       }
       app.use(printTime , welcomeMassage);
       
في البداية يتم تنفيذ دالة printTime وطباعة الوقت في console في كل مرة يتم عمل طلب في تطبيقك ثم يتم الذهاب للدالة التي تليها وهي دالة welcomeMassage يتم الرد هنا فيها وإظهار الجملة في المتصفح فعند كل طلب على تطبيقك سيتم تنفيذ هذه الدالتين.

- دوال معالجة الأخطاء 
يتم تعريف دوال middleware لمعالجة الأخطاء بنفس طريقة تعريف دوال middleware الإعتيادية لكن تحتوي هنا على أربع parameters وهم `(err, req, res, next)` كما بالمثال التالي: 


       app.use(function (err, req, res, next) {
          console.error(err.stack)
        res.status(500).send('Something broke!')
         })
         
## Request

### مقدمة في مفهوم req.params
-َ params هي اختصار لكلمة parameters وهي property خاصة بrequsts والتي من خلالها يمكننا الحصول على القيم المرسلة في الرابط ، لنوضح ذلك بمثال: نفترض لدينا قائمة بالطلاب الجامعيين ولعرض معلومات الطالب نحتاج لمعرفة رقمه الجامعي وللوصول له نستخدم params كما موضح أدناه :


محتوى ملف `app.js`:


     let students =[{id:1,name:'Ahmed',age:22,gpa:4.03}, {id:2,name:'Salem',age:21,gpa:3.83}, {id:3,name:'Khaled',age:23,gpa:4.52}, {id:4,name:'Ali',age:22,gpa:2.98}, {id:5,name:'Nasser',age:21,gpa:3.74}] 
     app.get ('/students/:id', function(req,res){ 
     let studentId = req.params.id
     console.log(studentId)
     if(0<studentId<students.length){
     student=students[studentId-1]
     res.locals.student=student
    res.render( 'show', student)}
    else
    res.render( 'errorMessage')})
    
    
    
 ##  ملاحظة: 
 إذا كنت تريد إرسال قيمة فالرابط فيجيب عليك وضع نقطتان رأسيتان قبل اسم الخاصية كما في المثال أعلاه تم وضع نقطتان رأسيتان قبل id في الرابط  'students/:id/'  في حين الإرسال تستبدل id:  برقم الطالب الجامعي  'students/3/'  كما موضح أدناه.
    
     http://localhost:3000/students/3
    
    
    
## خاصية req.body

قبل الدخول في تفاصيل العملية، لنقم أولاً بتجزئتها وفهمها، فالجزء الأول req هو إختصار request أي الطلب.
والجزء الثاني body أي المحتوى. نستنتج من ذلك أن req.body تعني المحتوى لهذا لطلب.

هذه العملية تمكننا من الوصول الى محتوى الطلب وتحديد المتغير أو القيمة المرسلة مع الطلب وإستخدامها.
مثال، في حالة قام أحد المستخدمين بإرسال طلب للوصول الى مع لوماته الشخصية، ستقوم العملية بإرسال 
المعرف id لهذا المستخدم كجزء من محتواها. وعند وصول الطلب سيتم التحقق من المستخدم من ثم إرسال
البيانات الخاصة به لعرضها.


- مثال إستخدام req.body للوصول الى id المستخدم : 


       const app = require('express')()

       app.use(bodyParser.json()) 
       app.use(bodyParser.urlencoded({ extended: true })) 

       app.post('/userInfo', function (req, res) {
       let userID = req.body.id;// we accesed user's id by using req.body
         })
         
         
        
 ## مقدمة في مفهوم ()res.send:

يتم إرسال رد عن طريق استدعاء دالة ()res.send تتكون هذه الدالة من جزء واحد فقط وهو body يمثل الرد الذي سيتم ارساله وقد يكون الرد أيًا مما يلي: 


- Buffer.
-  String.
- Object.
-  Array.

##  عمليه res.json
 
 وهي عمليه متعلقه بإرسال رد من نوع json عن طريق استدعاء داله res.json ، وتقبل json انواع بيانات محدده وهي 

- string 
- number 
- boolean
- array
- objects
- null

## المرجع 
https://expressjs.com/en/4x/api.html#express
