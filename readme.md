## -1. To-do лист

- [x] Диагностирование диабета
- [x] Диагностирование меланомы
- [x] Соединить все в единый сервис
- [ ] Диагностироавние сердечно-сосудистых заболеваний
- [ ] Диагностирование COVID-19
- [ ] Диабет: feature importance

## 0. О проекте и репозитории
Данный проект выполнен в рамках домашнего задания Летней Школы МТС.Тета, направление "Машинное обучение" командой **paranormal**:
* Алиферов Валентин;
* Кочкин Павел;
* Мельникова Маргарита;
* Чехоева Анастасия;
* Шакиров Ренат.

## 1. Выбор проекта

Проект посвящен проблеме раннего диагностирования сахарного диабета.

Важность проекта обусловлена тем, что сахарный диабет – **хроническое и полностью неизлечимое заболевание.**
* Каждые 10 секунд в мире становится на 2 больных сахарным диабетом больше. Каждые 10 секунд 1 человек умирает от связанного с диабетом заболевания.
* Пациенты **могут и не подозревать** о существовании у них сахарного диабета, и в таких случаях диабет выявляется либо при профилактических осмотрах, либо при обследовании другого заболевания, когда уже не будет возможности недопустить его развития или осложнений. 
* Диабет опасен осложнениями. 8 самых грозных из них – инфаркт, инсульт, слепота, заболевания почек, гангрена нижних конечностей (с последующей ампутацией), осложнения беременности и риск здоровья будущего ребёнка, эректильная дисфункция, инфекционные заболевания.
* По статистике, диабет может отнять 10 лет жизни человека.

**Ситуация в мире:**
* На текущий момент именно диабет является тем хроническим заболеванием, **распространенность которого растет в мире.** И если вероятность смерти в возрасте от 30 до 70 лет по причине неинфекционных заболеваний, принадлежащих к одной из четырех основных групп (сердечно-сосудистые, онкологические, хронические заболевания органов дыхания или диабет), снизилась во всем мире на 18% за 2000-2016 гг., то заболеваемость именно от диабета увеличилась на 5% за 2000-2016гг.  
* За период с 1980 по 2014 г. количество людей, страдающих диабетом, выросло со 108 миллионов до 422 миллионов. **Но реальное число заболевших еще выше**, т. к. часто диабет протекает в стертой форме и своевременно не диагностируется, соответственно больные не получают необходимого лечения, что может приводить к инвалидизации больных без должного лечения.

**Ситуация в России:**
* В России предположительная распространенность сахарного диабета составляет 5,7%, а численность больных - 9 миллионов человек.
* По прогнозам, к 2025 году количество больных сахарным диабетом увеличится вдвое, а к 2030 году, по расчетам Международной федерации диабета, с этим диагнозом будет 500 миллионов человек

**Описание проекта**
* Мы предлагаем сервис по раннему диагностированию сахарного диабета для растущей сети клиник M, расположенных в городе-миллионнике N.
* Разработана модель раннего диагностирования сахарного диабета с использованием реальных данных 512 пациентов, опубликованных на http://archive.ics.uci.edu/ml/datasets/Early+stage+diabetes+risk+prediction+dataset.#
* Также модель выполняет и просветительскую функцию - информирование населения о проблеме диабета в целом и о тех симптомах, которые возникают при диабете, в частности.

**Источники:**
* https://www.who.int/ru/news-room/fact-sheets/detail/diabetes
* http://68.rospotrebnadzor.ru/content/545/21700/
* https://minzdrav.gov.ru/news/2019/11/14/12812-vsemirnyy-den-borby-s-diabetom


## 2. Бизнес и математическая постановки задачи

### Бизнес постановка задачи:

Мы - активно развивающаяся сеть клиник M, расположенных в городе-миллионнике N.

14 ноября 2021 года будет проходить Всемирный день борьбы с диабетом (далее – День). Для повышения узнаваемости бренда сети клиник M и привлечения большего числа клиентов, мы предлагаем приурочить ко Дню запуск телеграмм-бота/сайта с тестом для ранней диагностики повышенного риска сахарного диабета для сети клиник M.

По итогам ввода анонимных данных пациентом, возможны **следующие сценарии**:
* **риск выше среднего**, мы предложим
пройти “Диабет check-up” в клинике по скидкой 60% (уровень глюкозы, Генетическая предрасположенность к сахарному диабету 2 типа и консультация эндокринолога);
* **риск ниже среднего**, мы предложим:
сдать кровь на уровень глюкозы в крови бесплатно при условии платной консультации у диетолога, чтобы обсудить оптимальный рацион питания для профилактики диабета и сохранения здоровья в дальнейшем.

**Бизнес-цель:**
* повысить узнаваемость бренда сети клиник М.;
* привлечь не менее 200 пациентов в сеть клиник М.

Для измерения результата промо мы введем специальный код скидки и по итогам мы снимем отчетность и посчитаем количество чеков с примененной скидкой с уникальным id клиента сети Клиник.

Затраты на организацию рекламы чат-бота/сайта и оплату сервиса берет на себя PR отдел в рамках проекта повышения узнаваемости бренда сети клиник М. 

### Математическая постановка задачи:
1. Требуется решить задачу бинарной классификации.
    * Необходимо прогнозировать одну из меток: 
        * человек, проходящий тестирование, имеет высокий риск к заболеванию;
        * человек, проходящий тестирование, имеет низкий риск к заболеванию.
    * Горизонта прогнозирования нет. Вероятностная модель не требуется.  

2. Функционал качества бинарной классификации:
    * Оптимизируем F1:
        * Поскольку мы решаем задачу, связанную с медициной, то важной метрикой является полнота (recall). 
        * Значение recall будет максимальным и равно 1, если построим константную модель. Решение константной модели нам не подходит, т.к. завышенное значение FP может негативно сказаться на репутации клиники.
    * Руководствуясь этой логикой, мы делаем вывод, что нужно учитывать и precision (точность).
    * Таким образом, получается, что F1 отлично подходит в качестве метрики для решения поставленной задачи.


## 3. Выбор набора данных
Обезличенные данные 512 пациентов (и провалидированные лечащими врачами), опубликованные на http://archive.ics.uci.edu/ml/datasets/Early+stage+diabetes+risk+prediction+dataset.#

## 4. Валидация данных и оценка потенциала
* Перечисленные в исходных данных признаки (полиурия, полидипсия, внезапная потеря веса, слабость, поышенный аппетит, ожирание, зуд и т.п.) являются симптомами сахарного диабета.  Стоит отметить, что чем выше стадия сахарного диабета, тем заметнее проявление симптомов. 

* Указан признак полиурия, но помимо этого возможно также ночное недержание. Можно добавить и такие признаки, как онемение и покалывание в руках и ногах, повышеная потливость, быстрая утомляемость, нехватка энергии, сильная усталость и сухость во рту из-за чувства жажды.

* На представленных данных можно построить модель. В будущем в данные можно будет добавить указанные выше симптомы, а также расширить географию сбора данных.

* Признаки не противоречат друг другу, данные соответствуют гипотезе.

* Диабет, особенно 2-го типа, наиболее распространен среди мужчин, чем среди женщин. https://www.news-medical.net/health/Diabetes-in-Men-versus-Women.aspx

* Целевой класс сильно коррелирует с переменными полиурия и полидипсия.  https://www.jdrf.org/t1d-resources/about/symptoms/frequent-urination/

* Также целевой класс коррелирует с внезапной потерей веса. https://www.medicinenet.com/is_weight_loss_caused_by_diabetes_dangerous/ask.htm

* [Модель](diabetes/model.ipynb)

## 5. Оценка экономического эффекта

[Оценка экономического эффекта](diabetes/effect.ipynb)

## 6. Разработка и валидация ML модели

[Разработка и валидация ML модели](diabetes/validation.ipynb)

## 7. Веб-сервис

http://paranormal.mcalias.com:8501

### Диагностирование диабета
![Alt Text](pics/diabetes.gif)

### Диагностирование меланомы
![Alt Text](pics/melanoma.gif)

## 8. Телеграм боты

### Диагностирование диабета
https://t.me/paranormal_diabetes_bot
![Alt Text](pics/diabetes_bot.png)

### Диагностирование меланомы
https://t.me/paranormal_melanoma_bot
![Alt Text](pics/melanoma_bot.png)