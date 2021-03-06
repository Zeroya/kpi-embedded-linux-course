=================================================
**Лабораторна робота №0 Робота з потоками**
=================================================


**Завдання:**
~~~~~~~~~~~~~
Написати програму в якій:

* Створити глобальну змінну, ініціалізувану в 0;
* Створити функцію потоку,яка N разів додає до цієї змінної К;
* Запустити два потоки з цією функцією;
* Дочекатись завершення потоків використовуючи ``pthread_join()`` ;
* Вивести в ``stdout`` очікуване та фактичне значення глобальної змінної (2*N*K=1000);
* Створити лістинги ``asm`` для двох рівнів оптимізації: ``-O0``, ``-O2``;  
* Створити ``Makefile``. 

**Хід роботи:**
---------------
На Linux найбільш поширеною бібліотекою для роботи з багатопотоковим кодом є ``POSIX Threads (pthreads)``. Для запуску потоку застосовується функція ``pthread_create``. Найчастіше, завершення потоку потрібно дочекатися, щоб переконатися що вся потрібна робота була виконана. При виході з ``main()`` всі активні потоки знищуються. Якщо один зі створених ``pthread_create`` потоків в цей момент виконується, то його робота буде перервана. Тому ми контролюємо завершення кожного потоку. 
У даній програмі один потік у нас в main, а другий, створений ``pthread_create`` і виконується паралельно з першим, саме його завершення контролює ``pthread_join``.   

*MakeFile*
    Make - утиліта призначена для автоматизації перетворення файлів з однієї форми в іншу. Правила перетворення задаються в скрипті з ім'ям ``Makefile``, який повинен знаходитися в корені робочої директорії проекту. Сам скрипт складається з набору правил, які в свою чергу описуються:
    
    *1) цілями (то, що дане правило робить);
    *2) реквізитами (то, що необхідно для виконання правила і отримання цілей);
    *3) командами (які виконують дані перетворення).

*Рівні оптимізації*
    -O0: Цей рівень оптимізації повністю і є рівнем за замовчуванням, якщо ніякого рівня з префіксом -O не вказано в змінних CFLAGS. Це скорочує час компіляції і може поліпшити дані для налагодження, але деякі програми не будуть працювати належним чином без оптимізації. Ця опція не рекомендується, за винятком використання в цілях налагодження.

    -O1: Це найбільш простий рівень оптимізації. Компілятор спробує згенерувати швидкий, що займає менше обсягу код, без затрачивания найбільшого часу компіляції. Він досить простий, але повинен завжди виконувати свою роботу.

    -O2: Рекомендований рівень оптимізації, до тих пір поки не знадобиться щось особливе. -O2 активує кілька додаткових прапорів на додачу до прапорів, активованих -O1. З параметром -O2, компілятор спробує збільшити продуктивність коду без порушення розміру, і без затрати великої кількості часу компіляції.

*Прапорці GCC*
-Wall
    Дає можливість вивести усі попередження про конструкції, які деякі користувачі вважають сумнівними, і яких легко уникнути (або змінити, щоб запобігти попередженню), навіть у поєднанні з макросами. Це також включає деякі попередження для окремої мови, описані в C ++ Dialect Options та Objective-C та Objective-C ++ Dialect Options.

-Wextra
    Вмикає деякі додаткові прапорці попередження, які не вмикає -Wall.

-Wpedantic
    Видавати всі попередження, які вимагають суворі ISO C та ISO C ++; відхилити всі програми, що використовують заборонені розширення, та деякі інші програми, які не відповідають ISO C та ISO C ++.

-Werror
    Зробити усі попередження помилковими.

Висновки
--------

Завдяки цій лабораторній роботі я навчився використовувати інструменти, які є дуже корисними для програмування, а саме: ``linter clang`` та ``Makefile``. Linter допоміг зробити код коректним, відповідно до стилю, без вад чи порушень стилю. Makefile допомагає дуже просто та швидко отримати програму, завдяки правилам які описані в ньому. Програму було перевірено по черзі рівнями оптимізації ``-O0`` та ``-O2``. За asm-файлами, які були відповідно згенеровані можна спостерігати відмінності у лістингах. По результатах очікуваних та фактичних значень можна сказати наступне: вони завжди збігалися, лише раз я отримав результат 995, замість 1000. Це через те, що в момент сумування вклинювався потік і порушувався результат. 
