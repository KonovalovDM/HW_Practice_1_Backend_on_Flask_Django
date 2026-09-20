## HW_Practice_1_Backend_on_Flask_Django
Practice_1_Backend_on_Flask_Django

Практическая работа №1: бэкенд-разработка на Python и Flask

### Задача 1. Работа с запросами формата JSON

В этой задаче вы создадите простой сервер на Flask, который будет принимать JSON-запросы, обрабатывать данные и возвращать JSON-ответ.  Это поможет вам освоить обработку данных в формате JSON, работу с библиотекой Flask и отправку AJAX-запросов с помощью fetch.  Обработка ошибок на сервере покажет вам, как важно писать надежный код, обрабатывающий потенциальные проблемы.

1. Убедитесь, что у вас установлен Python.  Затем установите Flask с помощью команды `pip install flask` в вашей консоли или терминале.

2. Создайте файл main.py и скопируйте в него предоставленный код. Запустите сервер командой `flask --app main run` в консоли, находясь в директории с файлом main.py.

3. Откройте консоль разработчика на главной странице сервера. Для этого нужно:

    открыть браузер на странице http://127.0.0.1:5000/
    открыть консоль разработчика
        Для Chrome
        Для Firefox

Примечание: аналогичным образом можно установить Django.

4. Отправить запрос на http://127.0.0.1:5000/api/v1/json/order методом fetch, содержащий структуру:

const orderData = {
    client: "Jon Smith",
    products: [
        { name: "product A", price: 20 },
        { name: "product B", price: 40 },
        { name: "product B", price: 40 }
    ],
    voucher: {
        discount: "20%"
    }
};

fetch('http://127.0.0.1:5000/api/v1/json/order', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify(orderData)
})
.then(response => response.json())
.then(data => console.log('Ответ:', data))
.catch(error => console.error('Ошибка:', error));


5. Проверьте ответ сервера в консоли. Ответ должен выглядеть так:

const orderData = {
    client: "Jon Smith",
    products: [
        { name: "product A", price: 20 },
        { name: "product B", price: 40 },…
Promise { <state>: "pending" }

Ответ: 
Object { client: "Jon Smith", total: 80, products: (2) […] }


### Задача 2. Работа с запросами формата XML

Эта задача аналогична первой, но теперь нужно работать с XML вместо JSON. Это даст возможность сравнить два формата и понять, как Flask обрабатывает разные типы данных.

Выполните пункты 1-3 из задачи 1.

4. Отправьте запрос на сервер http://127.0.0.1:5000/api/v1/xml/order, содержащий структуры задачи 1.

fetch('http://127.0.0.1:5000/api/v1/xml/order', {
    method: 'POST',
    headers: { 'Content-Type': 'application/xml' },
    body: `<order client="Jon Smith">
        <product name="product A" price="20"/>
        <product name="product B" price="40"/>
        <product name="product B" price="40"/>
        <discount>20%</discount>
    </order>`
})
.then(async (response) => {
    const text = await response.text();
    console.log('HTTP статус:', response.status);
    console.log('Тело ответа:', text);
    return text;
})
.catch(err => console.error('Ошибка:', err));

5. Проверьте ответ сервера. Ответ должен быть в корректном XML-формате и выглядеть примерно так:

fetch('http://127.0.0.1:5000/api/v1/xml/order', {
    method: 'POST',
    headers: { 'Content-Type': 'application/xml' },
    body: `<order client="Jon Smith">
        <product name="product A" price="20"/>…
Promise { <state>: "pending" }

HTTP статус: 200 debugger eval code:13:13
Тело ответа: <order total="80" products="product B,product A" client="Jon Smith" />  debugger eval code:14:13
