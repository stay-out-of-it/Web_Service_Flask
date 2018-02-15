**ІНТРО**

**_Клієнтська частина_**: Складає з себе 2 html сторінки. 
Перша - _base.html_, яка відкривається по дефолту, коли ми вводимо в браузері _http://localhost:5000/register_. На ній користувач вводить свою пошту, та текст який він хоче шукати в нашій бібліотеці і нажимає submit.
Друга - _index.html_, дана сторінка відкривається у випадку вдалого заповнення даних.


**_Серверна частина_**: Пралельно з переходом на сторінку _index.html_ на сервері, до файлу _text.txt_ додається в кінець запис у форматі _JSON_, що зберігає пошту та текст для пошуку.
Далі підключається в роботу файл _search.py_. Там відбувається в нескінченному циклі перебір даних з _text.txt_, якщо файл пустий то програма очікує зазначений термін. Також проводиться повнотекстний пошук в базі даних db та відбувається відправлення листа з результатом на пошту. Перед запуском треба поміняти в файлі _config.py_ значення поля *ADMINS* на локальну пошту та налаштувати локальну пошту. Потім видаляється з файла _text.txt_ опрацьований запис.
 
Самі бази даних я не робив, це з вязано з великою трудоємністю (на мою думку, бо для створення БД, що містила би в своїх значеннях главу,розділ,сторінку процедура довготривала). Тому я вирішив описати структуру та зробити дану програму більше процедурного типу, тобто "БД можна підгрузити і все повинно працювати". Тому опишу лише форму в якій потрібно подавати дані. Взагалі для економії памяті(при великих даних), потрібно зробити деревовидну структуру. і все зведеться до того, що буде привязка тексту лише до сторінки і по ієрархії складаючись буде давати нам повну інформацію. Бо робити бд що буде містити поля: назва книги, розділ, главу, номер сторінки, текст. Містить 5 категорій, що в РАЗИ більше памяті.

**Структура програми**

├── app

│   ├── email.py (модуль для відправки відповіді на пошту)

│   ├── forms.py (реалізується форма для _base.html_, тобто для сторінки з заповненням реєстраційної форми (початкової) )

│   ├── __init__.py (ініціалізуються обєкти)

│   ├── routes.py (реалізується заповнення реєстраційної форми. В результаті отримуємо нові дані в файлі _text.txt_ та при успішній реалізації відкривається _index.html_)

│   └── templates (тут зберігаються два шаблона _base.html_ та _index.html_)

│       ├── base.html (відкривається по дефолту на _http://localhost:5000/register_. Містить 2 поля: пошта(з перевіркою на коректність) та текст(який потрібно шукати). І кнопка для підтвердження запиту)

│       └── index.html (сторінка з написом **Data requested!** для підтвердження запиту на пошук)

├── config.py (дефолтні параметри (константи) )

├── db (тут повинна бути БД)

├── docker-compose.yml (докер для запуску (docker-compose build; docker-compose up))

├── Dockerfile (докер)

├── requirements.txt (файл з необхідними для установки версіями програм, через pip)

├── run.py (файл який запускає все)

├── search.py (пошук в БД даних з text.txt, відправка на пошу листа, виділення використаних даних, якщо файл пустий то програма чекає зазначений час)

└── text.txt (файл в який додаються в чергу зипити)

Окремо всі модулі були перевірені на коректність, але через відсутність БД програма в цілому не перевірялась на коректність. В даному випадку довірюсь принципу "утиной типизации")

Мені здається, ви якраз і хотіли перевірити моє розуміння та бачення проекту в цілому. Сподіваюсь мені вдалося передати моє бачення. Як не дивно, мені не вистачило часу для реалізації всього. Хоча якщо відкинути БД, то більш менш вдалося реалізувати те, що і планувалося.

Не судіть строго, вихідні - це якраз той час, коли хочеться зайнятися програмуванням)

Дякую за терпіння дочитати до кінця!

