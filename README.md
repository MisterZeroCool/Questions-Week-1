# Questions
### 1.Какие компоненты андроид системы вы знаете?
Основные компоненты андроид системы которые должны быть зарегестрированы в файле AndroidManifest:
+Activity
+Servicy
+BroadcastReceivers
+ContentProviders


### 2.Какой из этих компонентов не обязательно регистрировать в файлу AndroidManifest и почему?
В системе Android необязательным компонентом для регистрации в манифесте является Service. В отличии от Activity и BroadcastReceivers, Servicy могут быть запущены и работать в фоновом режиме без непосредственного взаимодействия с пользователем. 


### 3.Что такое Activity?
Это компонент приложения, который представляет собой экран, с которым пользователи могут взаимодействовать для выполнения каких-либо действий, например набрать номер телефона, сделать фото, отправить письмо или просмотреть карту. Каждой Activity присваивается окно для прорисовки соответствующего пользовательского интерфейса.


### 4.Опишите жизненный цикл Activity
Жизненный цикл представляет собой последовательность методов, которые вызываются в определенной последовательности во время создания/уничтожения/приостановки Activity.

<h3 align="center"><strong>Activity Lifecucler</strong></h3>
<p align="center">
  <img src="https://www.sysbunny.com/blog/wp-content/uploads/2021/04/Android-Activity-Lifecycle-768x917.jpg" alt="Preview"">
</p>

+ <b>onCreate()</b>
Необходимо обязательно реализовать, поскольку система вызывает его при создании Activity. Важно именно здесь вызвать метод <b>setContentView()</b> для определения пользовательского интерфейса. Вызывается первым, во время создания Activity. Вызывается один раз, после чего наше Activity переходит в состояние <b>Created</b>. В данном методе мы инициализируем интерфейс нашего Activity, а также выполняем некоторую базовую логику, которая необходима нам для корректной работы Activity, например, создаём список с какими-либо данными. Также, в качестве аргумента метода <b>onCreate()</b> нам передаётся объект <b>Bundle</b>, который содержит в себе информацию, которая была предварительно сохранена, во время пересоздания <b>Activity</b>.

+ <b>onStart()</b>
Переводит нашу Activity в состояние <b>Started</b>, после чего Activity становится видно для пользователя. Метод может использоваться для какой-либо логики, которая взаимодействует с UI.

+ <b>onResume()</b>
Наше Activity переходит на передний план приложения (foreground) изменяя своё состояние на Resumed. После вызова данного метода, пользователь может взаимодействовать с Activity. В данном состоянии Activity остается до тех пор, пока не потеряет фокус, это может произойти, например, при переходе на другую Activity, либо при входящем телефонном звонке.

+ <b>onPause()</b>
Наше Activity теряет фокус, больше не видно для пользователя и выходит из состояния foreground. При этом Activity не уничтожается и продолжает существовать. В этом методе, например, мы можем приостановить логику связанную с GPS навигацией, чтобы минимизировать расход <b>батареи<b/>.

+ <b>onStop()</b>
Состояние <b>Activity</b> изменяется на Stopped. Вызывается, когда Activity не видно пользователю, например, при переходе на другой экран или при сворачивании приложения, а также при подготовке к полному уничтожению нашей <b>Activity</b>. системой.

+ <b>onDestroy()</b>
Метод вызывается непосредственно перед уничтожением нашей <b>Activity</b>, например, после вызова метода <b>finish()</b>, или переходе на предыдущую <b>Activity</b>, путём нажатия кнопки “назад”.
Если активность завершается, <b>onDestroy()</b> – это последний метод жизненного цикла, который вызывает <b>Activity</b>. Если <b>onDestroy()</b> вызывается в результате изменения конфигурации, система немедленно создает новый экземпляр активности вызывает <b>onCreate()</b> в новом экземпляре и новой конфигурации.
Метод <b>onDestroy()</b> должен освобождать все ресурсы нашей Activity.


### 5.Что происходит при перевороте экрана Activity? Какие методы вызываются? Как сохранить данные при перевороте?
При повороте экрана система уничтожает и полностью пересоздаёт экземпляр <b>Activity</b>. 

Вызываются коллбэки   <b> onPause(), onStop(), onSaveInstanceState(), onDestroy() – onCreate(), onStart(), onRestoreInstanceState(), onResume()</b>.




Для того, что сохранить какие-либо пользовательские данные и затем восстановить их в нашей <b>Activity</b>, используются следующие методы:

+ <b>onSaveInstanceState()</b>
Данный метод вызывается перед тем, как <b>Activity</b> будет уничтожена. Параметром метода является Bundle, в который мы будем складывать необходимые для сохранения данные. Рекомендуется сохранять данным способом информацию, объём которой не превышает 1 мегабайт, в случае превышения лимита мы получим ошибку <b>TransactionTooLargeException</b>.
+ <b>onRestoreInstanceState()</b>
Вызывается после метода <b>onStart()</b>. В данный метод мы получим наш <b>Bundle</b>, в котором была сохранена информация.

Стоит заметить, что Bundle с сохранёнными данными мы также получаем в методе <b>onCreate()</b>, но данную ситуацию нужно отдельно обрабатывать, чтобы не получить <b>NullPointerException</b>.


