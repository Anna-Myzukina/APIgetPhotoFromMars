### Получаем фотографии NASA с Марса с помощью [aiohttp](https://uazmi.tech/news/post/g4y1JyvwZ0eHnTUUVQ3m1o)

#### Создание aiohttp приложения:

* Начнём с простого — установим и запустим aiohttp. 
Для начала создадим виртуальное окружение. 

        Я советую использовать Python 3.5, в котором появился новый синтаксис async def и await. 
        Если вы хотите развивать это приложение в дальнейшем, чтобы лучше понимать асинхронное программирование, 
        то можете ставить сразу Python 3.6. 

* Наконец, установим aiohttp:

        pip install aiohttp
* Добавим файл в проект (назовём его nasa.py) с кодом:

        from aiohttp import web


        async def get_mars_photo(request):
        return web.Response(text='A photo of Mars')


        app = web.Application()
        app.router.add_get('/', get_mars_photo, name='mars_photo')

#### Если вы ещё не работали с aiohttp, то поясню несколько моментов:

* корутина get_mars_photo — обработчик запросов; 
принимает HTTP запрос в качестве аргумента и подготавливает содержимое для HTTP ответа (ну или бросает исключение)

* app — высокоуровневый сервер; 
он поддерживает роутинг, middleware и сигналы (в примере будет показан только роутинг)

* app.router.add_get — регистрирует обработчик HTTP метода GET по пути '/'
Примечание: обработчиком запросов может также быть и обычная функция, а не только корутина.
Но чтобы понять всю мощь asyncio, большинство функций будут определены как async def.

#### Запуск приложения
Для запуска приложения добавьте строчку в конец файла:

        web.run_app(app, host='127.0.0.1', port=8080)
И запустите его как обычный python скрипт:

        python nasa.py
Однако, есть способ получше. Среди множества сторонних библиотек я нашёл aiohttp-devtools.
Она предоставляет замечательную команду runserver, которая запускает ваше приложение, а также поддерживает live reloading.

        pip install aiohttp-devtools
        adev runserver -p 8080 nasa.py

Теперь по адресу localhost:8080 вы должны увидеть текст «A photo of Mars».
