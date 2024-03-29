# analysis of 240 profiles in mamba
#### Зачем эта работа? 
<br> Была цель - сформировать портреты пользователей и наметить идеи для развития рекомендательных систем. 
<br> <b> В итоге: </b> сформированы кластеры пользователей, а также выявлены паттерны в профилях в зависимости от пола, возраста, диапазона возраста потенциального партнера. Чтобы строить рекомендации, было бы круто иметь обобщенные и анонимные переписки, чтобы смотреть, например, по каким параметрам люди не просто мэтчаться, а идут на свидания или же долго переписываются. 


 🤓 Спарсила 240К анкет на mamba.ru, парсила только то, что видно всем, а точнее: 
- возраст
- вес
- образование
- о себе
- с кем живу
- дети
- цель на сайте
- пол
- в каком поле заинтересован
- язык
- возраст партнера

<br> Сделала так, чтобы мужчин и женщин было одинаково (сначала мужчин было намного больше, пришлось парсить еще только женщин, иначе результаты статистических тестов были какие-то скошенные). 

<img width="116" alt="genders_count" src="https://user-images.githubusercontent.com/84775580/199487357-b60e9c62-e89a-49ef-a014-e27e59ca6c19.png">

Посмотрела на графики возрастов и убрала "выбросы", хвосты, оставив только 18-45 лет включительно. Без выбросов вполне похоже на нормальное распределение. 
![ages_men](https://user-images.githubusercontent.com/84775580/199490138-4bc71d03-850b-498f-a6d9-8b298121129d.png)

![ages_women](https://user-images.githubusercontent.com/84775580/199490158-c24379f0-5362-4c0e-89c4-30ee047c509e.png)

👌🏻 Добавила дополнительные столбцы:
- диапазон возраста партнера (есть и такие, но их мало, кто искал в диапазоне до 60 лет)
- начальные возраст партнера
- упростила (сгруппировала) разнообразие целей на 6 групп: флирт, отношения, семья, друзья, неуверенные (очень много целей, от 5), не указали цель. 
- столбец процента, иначе, сколько процентов от общего числа мужчин или женщин составляет один мужчина или одна женщина соответственно. 

Постепенно в ходе анализа заметила, что работал закон больших чисел - поэтому каким-то базовым статистикам можно доверять смело. А точнее - по возрасту, весу, росту. 
<br> <b> Получилась некоторая демографическая сводка. </b>
<br> Возраст - 31 
<br> Вес - 70
<br> Рост - 172

<img width="313" alt="basic statistics" src="https://user-images.githubusercontent.com/84775580/199488242-1c1e3f78-2888-4c6c-a604-87eb3d87cdaa.png">

Посмотрела, чтобы удостовериться, есть ли корреляция в возрастах между теми, кто ищет, и теми, кого ищут. Закономерно, корреляция практически прямая: более старшие ищут более старших. 

<img width="193" alt="searxhfor" src="https://user-images.githubusercontent.com/84775580/199489919-d0a04959-6748-4fe1-8541-e22da40d3dfa.png">

### Анализ целей. 
Распределение целей на графике вполне соответствует генеральной совокупности, проверила с помощью хи-квадрата. 

![newplot](https://user-images.githubusercontent.com/84775580/199490573-f1c2421a-1cb5-4c89-baa1-e908392ce354.png)

Отличаются ли цели на сайте по возрастам у мужчин и женщин?

![aim_age_gender_dist](https://user-images.githubusercontent.com/84775580/199491056-10d24f38-8e06-414d-be3e-321b9c3e0b30.png)


Средние возраста по целям:
* флиртовать, встречаться: м 31, ж 29
* быть в отношениях: м 31, ж 32
* дружить: м, ж ~ 30
* хочу все подряд: м 32, ж 31
* не указали цель: м 31, ж 30
* семья: м, ж ~ 34,5

📣 Очевидный вывод - средний возраст колеблется от 29 до 32 с маленькими различиями. Самый большой разрыв в 2 года в цели флирт: мужчины хотят в 31, а женщины - в 29.

В целом, в около 30 все хотят "гулять" и люди ищут партнера (романтического, сексуального, дружеского), к семье приходят к 35, и мало кто сидит на сайте с целью семьи (всего ~0,9%) ❤

п.с. Данные проверены на t-test, в возрастах нет выбросов (возраст от 18 до 45 лет), но, в целом, данных настолько много, что начинает действовать закон больших чисел - и, в теории, уже можно (было бы достаточно) использовать центральную предельную теорему.

<br> <b> При этом неуверенные </b> (группа, кто писал кучу всего, unsure) хотят, похоже, повстречаться, подружить, пообщаться. 
<img width="155" alt="usure" src="https://user-images.githubusercontent.com/84775580/199491679-6e384e14-6d89-4375-b9a9-04f293350c9c.png">

❓ А есть ли разница по целям между теми, кто пишет о себе, и теми, кто не пишет? 
В графике верхний столбец (над чертой) - это мужчины. 
![newplot (1)](https://user-images.githubusercontent.com/84775580/199492076-83f0ba6b-2033-46b8-b9cb-d06dc38a2146.png)

Интересно, или даже закономерно, что люди, <b> которые пишут кучу целей, пишут и более пространственные описания </b>. Наверное, поясняют, что хотят. Ну и более дружелюбиные тоже, вероятно, чтобы пояснить, что они только дружить хотят. 
<br> И интересно, что повстречаться-отношения пишут 50 на 50 о себе. 
<br> А еще мужчины чаще пишут о себе в целях флирт и когда много целей. 

#### Поглядела на базовые статистики гомосексуалистов.

<img width="573" alt="geys" src="https://user-images.githubusercontent.com/84775580/199492654-136f1ae3-1437-4cab-9eef-03967e969070.png">

Похоже, они в целом помоложе, чем в группе с остальными (на 2 года средние и медианы меньше в возрасте) 
<br> Как следствие, ищут партнеров помоложе (на 1 год в медиане и среднем).
<br> И, похоже, меньше весят тоже на 7-8 кг в среднем и в медиане.
<br> И меньше ростом на 2 см в среднем и в медиане.
<b>Но, конечно, сравнивать общую выборку и выборку гомосексуалистов статистически невозможно, только если добирать бутстрепом больше значений у гомосексуалистов</b>

### Массив анализа по двум группам: кто указал 4 в диапазоне возраста партнера, и кто нет

Процент людей, у которых диапазон возраста того, кого ищут, равен 4: 64.2. 
💥 Мне показалось это интересным, потому что я предположила, что 4 - это стандартный диапазон и, возможно, люди которые выбирают стандартный диапазон, меньше заинтересованы в использовании сайта, т.е. они могут быть менее активными. 

<b> Отличаются ли группы тех, у кого диапазон возраста партнера 4 и все остальные? </b>
По базовым статистикам разницы почти нет. 
* НО у НЕ4 больше стандартное отклонение в возрасте - у них больший диапазон, похоже. И больше ст.отклонение в начальном возрасте партнера. 
* НО очень интересно, что люди НЕ4, <b> намного лучше заполяют профиль </b>, в их группе меньший процент нулевых значений.

<b> Какие различия есть у группе ДА4 и НЕТ4 по уровню образования? </b>
Цифры на графике проверены по хи-квдрату. 
Различия есть: похоже, в группе ДА4 больше людей с высшим образованием. 

![edu](https://user-images.githubusercontent.com/84775580/199495578-73eabee2-ebd9-4dd0-adc1-9f7d659205bc.png)

<b> Есть ли различия в возрасте у группы ДА4 и НЕТ4? </b>
Они явно есть. Кажется, что распределения по возрастам похожи, но отличие в том, что у НЕ4 очень много значений до 20, а у ДА4 - около 22 и 32 лет небольшие пики. Это интересно, потомму что НЕ4 отличаются более высоким уровнем образования... Дело в том, что 75% людей до 20 лет в группе НЕ4 образование просто не указывают. А после 20 лет в группе НЕ4 не указывают 45%.

![ages](https://user-images.githubusercontent.com/84775580/199496103-2d1671b7-3336-4485-b9e1-bc6dc4e5d431.png)

<b> Есть ли разница в цели на сайте у групп ДА4 и НЕ4? </b>
есть. Те, кто НЕ4 не уверены в своих целях (33%), при этом у другой группы 55% вообще не указывают цель, но и очень мало (6%) указывают больше трех целей. Количество людей, ищущих отношения или флирт одинаковое в двух группах. У НЕ4 в три раза больше семьянинов и в 4 раза больше дружелюбных.

![newplot (2)](https://user-images.githubusercontent.com/84775580/199496658-0a4c409f-0ed4-41fd-bb94-fb61198cc570.png)

#### Выводы по ДА4 и НЕТ4.
Субъективно по цифрам, НЕ4 лучше заполняют профиль, более образованные, возможно, они нацелены более серьезно, т.е. действительно хотят использовать сайт, чтобы удовлетворить свою цель, а не избавиться от скуки 🖤

### Какие есть закономерности в группах по детям, месту жительства, городу, курению? 

<img width="159" alt="cities" src="https://user-images.githubusercontent.com/84775580/199497549-0575d91a-7ac9-4625-9e95-bfc5cf7700e5.png">

#### О детях написали конкретно 25% людей. Какой у них возраст? Откуда они? Кто хочет детей?
* интересно, что мужчины больше хотят детей, чем женщины; мужчины чуть ли не в 4 раза больше женщин живут порознь со своими детьми, а женщины чуть ли не в 8 раза больше живут со своими детьми. Ну и логично: дети обычно остаются с мамой. 
* дети есть пишут, начиная, в среднем, от 35 лет (закономерно тоже)
<img width="283" alt="children" src="https://user-images.githubusercontent.com/84775580/199497783-44131ee1-390c-4b8c-8edc-f380af2eac8d.png">

#### Кто с кем живет и чего хочет? 
* в группе Живу с родителями отношений хотят поровну, мужчины больше хотят флирта-встречи и в большей степени не знают, чего хотят. 
* в группе Отдельная квартира женщины больше хотят отношений, мужчина больше хотят флирта, одинаково хотят семью.

<img width="220" alt="live" src="https://user-images.githubusercontent.com/84775580/199498034-e82312b3-72b6-4d73-ab62-814a9f3dcb8f.png">

### Алгоритм классификации K-means
Я оставила признаки (фичи): о себе, возраст, пол, образование, дети, с кем живет, цель. Присвоила значениям этих фичей числовые классификаторы. 
"Методом локтя" выбрала, что у меня будет 4 кластера. 

<img width="313" alt="angle" src="https://user-images.githubusercontent.com/84775580/199498661-1be384bd-b872-4628-a811-084e753ef167.png">

И даже получила некоторые закономерности 💣

#### Кластер 0 
Похоже, там много людей, которые ничего о себе не указали, кроме пола, которые живут с родителями и указали 4 года в диапазоне возраста партнера. 
#### Кластер 1
Отличительная черта - у них нет детей (самая многочисленная группа по 4-ем кластерам). Также в эту группу, похоже, вошли все, кто сам не знает, чего хочет от сайта, и кто хочет дружить. Больше всего людей среди других кластеров там о себе что-то написали. Разные уровни образования.
#### Кластер 2
Очень похожий на другие кластер, очень отличительно, что живут с родителями и при этом больше остальных кластеров хотят в равных долях флиртовать и отношений. У них нет детей. 
#### Кластер 3
Очень средний кластер, похож на кластер 1, возможно, их следовало в одну группу.

![newplot (3)](https://user-images.githubusercontent.com/84775580/199498828-01c910e8-e1ea-44fa-9599-cfbf3840e19a.png)

## Результаты анализа секций "О себе"

### О чем пишут женщины? 
<br> <br> Женщины, в среднем, пишут на два-три слова больше о описании в анкете. Пишут о том, что и каких любят, также часто «ищу мужчину», «мужчина, который». То есть описывают себя и своего партнера. Часто пишут слова «общение», «отношения».
<br> <br> <b> Женщины любят, согласно описаниям</b>: путешествовать, гулять, готовить, природу, читать, танцевать и петь. 
<br> <br> В партнере очень ценят юмор, активность, доброту, часто ищут «хорошего», а ближе к середине в списке характеристик будущего избранника начинают появляться слова: «щедрый», «заботливый», «сильный», «порядочный», «самодостаточный», «русский». Приближаясь к концу списка популярных эпитетов, встречаем «высокий».
<br><br> <b>О себе женщины пишут</b>, в порядке убывания популярности (в м.р.) : 'добрый', 'красивый', 'общительный', 'весёлый', 'хороший', 'милый', 'позитивный', 'умный', 'интересный', 'семейный', 'адекватный', 'нежный', 'скромный', 'спокойный', 'активный', 'творческий', 'заботливый', 'открытый', 'романтичный', 'верный', 'искренний'.
<br> <br> Нечасто пишут о счастье: хотят сделать кого-то счастливым или самой быть счастливой. Или же ищут уже счастливого человека. В целом, пишут о том, кого хотят и зачем,  а также о своих интересах. 
### О чем пишут мужчины? 
<br> <br> Забавно, что у мужчин в топ-50 самых встречаемых слов встречаются разные формы слова «работать» или «работа», а у женщин – нет. Также у мужчин часто встречается слово «женат», а вот у девушек «замужем» - нет. Часто пишут слова «общение», «отношения».
<br> <br> <b>О себе мужчины пишут</b>, в порядке убывания популярности 'добрый', 'хороший', 'общительный',  'адекватный', 'активный', 'спокойный', 'весёлый', 'позитивный', 'высокий', 'скромный', 'честный', 'заботливый' , 'красивый', 'интересный', 'русский', 'верный', 'спортивный', 'отзывчивый', 'воспитанный', 'нежный', 'порядочный', 'умный',  'открытый', 'внимательный', 'работящий',  'сильный', 'ласковый'. 
<br> <br> <b>В партнере очень ценят… А не очень понятно, что! </b> Потому что в описаниях будто два варианта: либо прямое «я хочу только секс без обязательств», либо какая-то философская фраза, либо «если вы за феррари – мимо, я ищу любимую». Поэтому встречаем эпитеты: «единственная»,  «любимая», «милая», «адекватная», «умная» и только ближе к концу – «симпатичная», «сексуальная», «верная», и в самом конце – «веселая», «общительная», «творческая». 
<br><br>  Интересно, что мужчины не употребляют особо глаголов, связанных с хобби. В основном, это глаголы действия: «поговорить», «смотреть», «узнать», «сходить», «пообщаться», «создать» (вероятно, в контексте «создать семью»), «поддержать», «сказать». Из глаголов-хобби: готовить, путешествовать, гулять, играть, читать.
### И мужчины, и женщины 
пишут о сексе, детях (вероятно, в контексте есть или нет детей), душе (вероятно, в контексте «родственной души»), семье, музыке, спорте, юморе (очевидно, все ищут партнера с чувством юмора). 
### В целом 
Порядка 900 упоминаний (лидер) словосочетания (или похожего) «серьезные отношения». Порядка 1300 описаний, где есть слово «отношения». Много словосочетаний, связанных с чувством юмора, общением, спортом, вероятно, пишут, что хотят «общаться, смеяться, оздоровляться». 
Много упоминаний того, что «пара ищет третьего партнера». Также ищут «новые знакомства». Много упоминаний слов «жизнь», «человек», «хороший(ая)», «добрый(ая)», «друг» (здесь, очевидно, в контексте, что кто-то ищет друзей в прямом смысле или партнера и душевного друга). 

### В ЦЕЛОМ, СУБЪЕКТИВНО
Складывается впечатление, что женщины более точны в своих описаниях и себя, и партнера, а мужчины, наверное, больше пишут про свои цели (секс, романтика, жена) или же философствуют. Также приятно удивило, что будто много людей настроены на поиск именно романтического, семейного партнера. Те, кто пишет характеристики желаемого партнера, определенно хотят «доброго», «хорошего», «с чувством юмора», и мужчины, и женщины. Женщины пишут описания побольше, чем мужчины. 

