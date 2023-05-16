# Стажировка Моторика, спринт 2

16 мая 2023, Г.Бут, Команда 3

Другой спринт стажировки в компании Моторика. Задача спринта - распознать (предсказать) положение каждого пальца на руке по результатам измерения ОМГ датчиков. Новый формат входных данных. Несколько пилотов. Пилот в ходе опыта совершает пронации - вращения запястьем и кистью вокруг локтевой оси. В решении я вернулся к предложенным компаниям НС моделям. Одно из важных ограничений решения - обработка входных данных в реальном времени. Время обработки не должно превышать 33 мСек.

Первоначально я предполагал распознавать пронацию по результатам ОМГ измерений. Однако в дальнейшем я остановился на гипотезе игнорирования пронации. Довольно простая модель обеспечивала хорошее качество распознавания. 

Файл .ipynb реализует следующий алгоритм:
- отбор значимых сенсоров с высоким уровнем сигнала,    
- MinMax скалирование значений сенсоров,     
- выделение диапазона тестовых измерений для контроля переобучения НС модели,     
- нарезка фрагментов входных данных для обучения НС модели,      
- формирование реккурентной НС модели, ее обучение и контроль ее качества,   
- построение statefull реккурентной НС модели для последовательного инференса и контроль ее качества, 
- формирование обработок для последовательного инференса на основе statefull реккурентной НС модели, 
- прокси-моделирование обработок последовательного инференса на фрагменте входных данных и замер производительности. 

Достигнутая производительность - 7.22 мСек на наблюдение, условиям ограничения соответствует. 

Ключевые результаты разработки и отладки НС решения:
- В разработке НС моделей ключевое значение имеют регуляризация и борьба с переобучением.
- Данные для обучения НС модели должны быть подготовлены с учетом планируемой архитектуры реккурентной НС модели.
- Statefull реккурентная модель при последовательном выводе может сохранять в своей памяти результаты предыдущего вывода и не требует внешней дополнительной обвязки. Реккурентную НС модель можно обучить как обычную, а затем полученные веса использовать в statefull модели с внутренней памятью. Требуется контроль правильности трансфера весов.   