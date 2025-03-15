Scrapy Spider: DivanNewPars

Описание

Этот Scrapy-паук (divannewpars) предназначен для сбора информации о диванах и креслах с сайта Divan.ru. Он извлекает название, цену и URL-адрес каждого товара на странице категории.

Установка и запуск

Установка Scrapy

Если у вас еще не установлен Scrapy, установите его с помощью pip:

pip install scrapy

Запуск паука

Сохраните код в файле divannewpars.py внутри проекта Scrapy (в папке spiders). Затем запустите команду:

scrapy crawl divannewpars -o output.json

Эта команда создаст файл output.json с собранными данными в формате JSON.

Разбор кода

import scrapy

class DivannewparsSpider(scrapy.Spider):
    name = "divannewpars"
    allowed_domains = ["divan.ru"]
    start_urls = ["https://divan.ru/category/divany-i-kresla"]

    def parse(self, response):
        divans = response.css("div._Ud0k")
        for divan in divans:
            yield {
                'name': divan.css('div.lsooF span::text').get(),
                'price': divan.css('div.pY3d2 span::text').get(),
                'url': divan.css('a').attrib['href']
            }

Разбор структуры

name: идентификатор паука.

allowed_domains: разрешенный домен для парсинга.

start_urls: начальная страница для сбора данных.

parse: основная функция парсинга, которая:

Извлекает блоки товаров (div._Ud0k).

Собирает название, цену и ссылку на товар.

Возвращает данные в виде словаря.

Возможные доработки

Обход нескольких страниц категории (реализация пагинации).

Дополнительные параметры товаров (описание, рейтинг и т. д.).

Запуск через API или интеграция с базой данных.

Заключение

Этот Scrapy-скрипт помогает автоматически собирать данные о товарах на сайте Divan.ru. При необходимости его можно адаптировать под другие категории или сайты.
