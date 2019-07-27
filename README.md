### Note
*Для работы скрипта требуется Ruby 2.4+*

# Задание №1
В файле `task-1.rb` находится ruby-программа, которая выполняет обработку данных из файла.

В файл встроен тест, который показывает, как программа должна работать.

С помощью этой программы нужно обработать файл данных `data_large.txt`.

**Проблема в том, что это происходит слишком долго, дождаться пока никому не удавалось.**


## Задача
- Оптимизировать эту программу, выстроив процесс согласно "общему фреймворку оптимизации" из первой лекции;
- Профилировать программу с помощью инструментов, с которыми мы познакомились в первой лекции;
- Добиться того, чтобы программа корректно обработала файл `data_large.txt` за `30 секунд`;
- Написать кейс-стади о вашей оптимизации по шаблону `case-study-template.md`.

## Сдача задания
Для сдачи задания нужно форкнуть этот проект, сделать `PR` в него и прислать ссылку для проверки.

В `PR`
- должны быть внесены оптимизации в `task-1.rb`;
- должен быть файл `case-study.md` с описанием проделанной оптимизации;


# Комментарии

## Какую пользу нужно получить от этого задания
Задание моделирует такую ситуацию: вы получили неффективную систему, в которой код и производительность оставляет желать лучшего. При этом актуальной проблемой является именно производительность.
Вам нужно оптимизировать эту систему.

С какими искушениями вы сталкиваететь:
- вы “с ходу” замечаете какие-то непроизводительные идиомы, и у вас возникает соблазн их сразу исправить;

Эти искушения типичны и часто возникают в моделируемой ситуации.

Их риски:
- перед рефакторингом “очевидных” косяков не написать тестов и незаметно внести регрессию;
- потратить время на рефакторинг, хотя время было только на оптимизацию;
- исправить все очевидные на глаз проблемы производительности, не получить заметного результата, решить что наверное просто Ruby слишком медленный для этой задачи

## Советы
- Найдите объём данных, на которых программа отрабатывает достаточно быстро - это позволит вам выстроить фидбек-луп; если улучшите метрику для части данных, то улучшите и для полного объёма данных;
- Попробуйте прикинуть ассимтотику роста времени работы в зависимости от объёма входных данных (попробуйте объём x, 2x, 4x, 8x)
- Оцените, как долго программа будет обрабатывать полный обём данных
- Оцените, сколько времени занимает работа GC (попробовав отключить его на небольшом объёме данных)

## Что можно делать
- рефакторить код
- рефакторить/дописывать тесты
- разбивать скрипт на несколько файлов

## Что нужно делать
- исследовать предложенную вам на рассмотрение систему
- построить фидбек-луп, который позволит вам быстро тестировать гипотезы и измерять их эффект
- применить инструменты профилирования CPU, чтобы найти главные точки роста
- выписывать в case-study несколько пунктов: каким профилировщиком вы нашли точку роста, как её оптимизировали, какой получили прирост метрики;

## Что не нужно делать
- переписывать с нуля
- забивать на выстраивание фидбек-лупа
- вносить оптимизации по наитию, без профилировщика и без оценки эффективности

## Основная польза задания
Главная польза этого задания - попрактиковаться в применении грамотного подхода к оптимизации, почуствовать этот процесс:
- как взяли незнакомую систему и исследовали её
- как выстроили фидбек луп
- как с помощью профилировщиков нашли что именно даст вам наибольший эффект (главную точку роста)
- как быстро протестировали гипотезу, получили измеримый результат и зафиксировали его
- как в итоге написали небольшой отчёт об успешных шагах этого процесса
инструментов профилирования `CPU` и разъяснений, сделанных на 2й лекции.

## Checklist
- Построить и проанализировать отчёт `ruby-prof` в режиме `Flat`;
- Построить и проанализировать отчёт `ruby-prof` в режиме `Graph`;
- Построить и проанализировать отчёт `ruby-prof` в режиме `CallStack`;
- Построить и проанализировать отчёт `ruby-prof` в режиме `CallTree` c визуализацией в `QCachegrind`;
- Профилировать работающий процесс `rbspy`;
- Построить и проанализировать отчёт `flamegraph` с помощью `rbspy`;
- Добавить в программу `ProgressBar`;
- Постараться довести асимптотику до линейной и проверить это тестом;
- Написать простой тест на время работы: когда вы придёте к оптимизированному решению, замерьте, сколько оно будет работать на тестовом объёме данных; и напишите тест на то, что это время не превышается (чтобы не было ложных срабатываний, задайте время с небольшим запасом);

### Главное
Нужно потренироваться методично работать по схеме с фидбек-лупом:
- построили отчёт каким-то из профилировщиков
- осознали его
- поняли, какая самая большая точка роста
- внесли минимальные изменения, чтобы использовать только эту точку роста
- перестроили отчёт, убедились, что проблема решена
- вычислили метрику - оценили, как изменение повлияло на метрику
- записали полученные результаты
- закоммитились
- перешли к следующей итерации
