# Создание модели машинного обучения, которая поможет определить регион, где добыча принесёт наибольшую прибыль. Анализ возможной прибыли и рисков техникой Bootstrap

## Введение
Добывающей компании «ГлавРосГосНефть» нужно решить, где бурить новую скважину.

Шаги для выбора локации обычно такие:
В избранном регионе собирают характеристики для скважин: качество нефти и объём её запасов;
Строят модель для предсказания объёма запасов в новых скважинах;
Выбирают скважины с самыми высокими оценками значений;
Определяют регион с максимальной суммарной прибылью отобранных скважин.

Предоставлены пробы нефти в трёх регионах. Характеристики для каждой скважины в регионе уже известны.

## Цель исследования
1. Построить модель для определения региона, где добыча нефти принесёт наибольшую прибыль;
2. Проанализировать возможную прибыль и риски техникой Bootstrap.

## Ход исследования
1. Загрузка и подготовка данных;
2. Обучение и проверка модели для каждого региона;
3. Подготовка к расчёту прибыли;
4. Написание функции для расчёта прибыли по выбранным скважинам и предсказаниям модели;
5. Подсчет рисков и прибыли для каждого региона.

## Общие выводы
В настоящем проекте были выполнены действия по поиску наиболее оптимального с точки зрения прибыльности и ограничения рисков региона для бурения нефтяных скважин. Для этого были пройдены следующие этапы:
1. Предобработка данных <br>
Удалены неявные дубликаты. <br><br>

2. Исследовательский анализ данных <br>
В каждом регионе есть скважины с отсутствием нефти.
По медианному и среднему объемам запасов второй регион уступает остальным.
Скважина, имеющая максимальный объем запасов, во втором регионе имеет меньшее значение обхема, чем аналогичная в регионе №1 и регионе №3.

Распределение целевого признака в регионе geo_1 сильно отличается от нормального и распределений других регионов. Возможно, группы скважин в geo_1 были слишком близко расположены друг к другу. В geo_1 целевой признак сильно проседают объемы в середине распределения, но высоки по границам. Были удалены выбросы, т.к. они влияют на целевую метрику RMSE. <br><br>

3. Корреляционный анализ данных <br>
Наибольшая корреляция признака product наблюдается с признаком f2 во всех регионах, но с разной силой.

Наиболее похожая на линейную взаимосвязь наблюдается у целевого признака и f2 (при этом в geo_1 - четкая линейная взаимосвязь). Взаисосвязь признаков друг с другом отчиается от региона к региону. <br><br>

4. Поготовка данных к моделированию <br>
Выполнена разбивка датасетов на тренировочню и валидационную выборки, масштабирование количественных признаков, кодирование качественных, инициализация и обучение модели линейной регрессии. <br><br>

5. Обучение модели линейной регрессии <br>
В результате обучения модели линейной регрессии и ее применения для трех регионов было установлено, что:
- наибольший запас предсказанного сырья находится в регионе geo_2; <br>
- наименьшая ошибка RMSE - в регионе geo_1. Она очень сильно отличается от RMSE других регионов. Результат очень высокой линейной взаимосвязи f2 и product. <br><br>

6. Расчет прибыли, рисков для каждого региона. <br>
Была рассчитана прибыль (не выручка) с 200 лучших скважин в каждом регионе. Прибыльнее всего регион 0 (geo_0).

С помощью техники Bootstrap определены: средняя прибыль, 95%-й доверительный интервал и риск убытков. Регион 1 имеет вероятность убытков менее 2,5 % (условие задачи). Т.о. можно выбираем его для дальнейшей разработки скважин.

## Что использовано
Python, Numpy, Pandas, Matplotlib, Seaborn, Sklearn.
