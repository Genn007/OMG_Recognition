# Стажировка Моторика, спринт 3

15 июня 2023, Г.Бут Команда 3

Третий спринт стажировки в компании Моторика. Задача спринта - распознать (предсказать) положение каждого пальца на руке по результатам измерения ОМГ датчиков. Один пилот и несколько монтажей.

Файл Sprint3_ENCModel_102-10.ipynb реализует следующий алгоритм:
- Удаление незначащих сигналов ОМГ датчиков и масштабирование.
- Подача исходного таргета с задержкой в форме первой производной с последующим масштабированием на этапе stateless обучения.
- 32 GRU + Dense + Dense 
- Производная предсказания в петле ОС при Stateful Inference 
- 8.5 мСек на измерение. 


