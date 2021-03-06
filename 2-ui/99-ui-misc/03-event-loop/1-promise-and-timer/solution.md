1. Создание промиса
2. Конец скрипта
3. Обработка промиса
4. Таймаут

Давайте разберем что здесь происходит.

Изначально в стеке выполнения находится сам скрипт, поэтому сначала выполняется только он.

В первой строке появляется `setTimeout`, который ставит переданный колбэк в очередь макрозадач (macrotask queue) на выполнение.

После этого в переменную `p` запишется промис. Стоит отметить, что создание промиса в данном случае происходит синхронно. Это значит, что код из переданного колбэка выполнится прямо сейчас. 
В результате в консоль выведется `'Создание промиса'`.

Далее мы уведомляем потребителя `then`, что хотели бы выполнить переданную функцию после успешного выполнения промиса. Так как промис уже имеет состояние `fulfilled` (мы вызвали `resolve()` при его создании), колбэк из `then` будет немедленно передан в очередь микрозадач (microtask queue) на выполнение.

В конце выполнения скрипта выведется `'Конец скрипта'`.

Скрипт является макрозадачей. Как мы уже знаем, после завершения каждой задачи опустошается очередь микрозадач. В ней находится только ранее переданный в `then` колбэк. В результате его выполнения в консоль выведется `'Обработка промиса'`.

Так как очередь микрозадач опустела, можно продолжить выполнять код из очереди макрозадач. Там сейчас находится только колбэк, который мы передавали `setTimeout`. После его выполнения выведется `'Таймаут'`.
