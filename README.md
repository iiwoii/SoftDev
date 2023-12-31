# Основное
Мы работаем с сайтом производителя керамики Agami Ceramics https://agami.moscow/shop/ и извлекаем информацию об их продукции

Код содержит две функции: 
- get_list_of_products
- print_product_details

# Список товаров
Функция `get_list_of_products` получает список товаров на веб-сайте с их ценами. Она принимает два необязательных параметра: `number_of_products` (количество товаров) и `pages_total` (общее количество страниц).

Если не указан параметр `pages_total`, функция вычисляет его на основе `number_of_products`. Предполагается, что на каждой странице находится 15 товаров. Таким образом, функция вычисляет общее количество страниц (`pages_total`) путем деления `number_of_products` на 15 (с округлением вверх) и прибавляет 1.

Затем функция выполняет следующие шаги для каждой страницы:

1. Отправляет GET-запрос на указанный URL-адрес страницы сайта, используя номер страницы.
2. Используя библиотеку BeautifulSoup, функция парсит HTML-контент ответа.
3. Ищет все элементы `div` с классом "prodlist prodlist--shop", которые представляют список товаров.
4. Для каждого товара в списке товаров извлекает наименование (`name`) и цену (`price`) из соответствующих элементов HTML.
5. Выводит наименование и цену товара в формате `"<номер>. <наименование товара>, <цена>"`.
6. Увеличивает счетчик (`cnt`) на 1.
7. Проверяет, достигнуто ли указанное количество товаров (`number_of_products`). Если достигнуто, прекращает выполнение цикла.

После обработки каждой страницы, функция выводит пустую строку для разделения вывода товаров на разных страницах

## Примеры применения
Когда задаем кол-во товаров:
```
    number_of_products = 16
    get_list_of_products(number_of_products)
```
Когда задаем кол-во страниц:
```
    get_list_of_products(pages_total=2)
```

# Информация о товаре
Функция `print_product_details` выводит информацию о товаре на основе его полного названия и номера страницы. Она использует библиотеку `IPython.display` для отображения изображения товара.

Вот как функция работает:

1. Отправляет GET-запрос на указанный URL-адрес страницы сайта, используя номер страницы.
2. Используя библиотеку BeautifulSoup, функция парсит HTML-контент ответа.
3. Ищет элемент, содержащий полное название товара, путем поиска строки с заданным полным названием и перехода к родительскому элементу.
4. Извлекает ссылку на товар из найденного элемента.
5. Отправляет GET-запрос на ссылку товара.
6. Парсит HTML-контент страницы товара.
7. Извлекает информацию о товаре, такую как название (`product_name`), цена (`product_price`), ссылка на изображение (`img_link`), вес (`product_weight`), размер (`product_size`), инструкции по уходу (`product_care`) и состав (`product_compound`).
8. Отправляет GET-запрос на ссылку изображения товара.
9. Отображает изображение товара с помощью функции `display` из библиотеки `IPython.display`.
10. Выводит информацию о товаре, включая название, цену, вес, размер, инструкции по уходу и состав, с использованием функции `print`.

## Примеры применения
Для товаров на первой странице page_number можно не передавать
```
    full_name = "Миска из темного шамота бирюзовая ровный край"
    print_product_details(full_name)
```
Для товаров на других страницах нужен page_number 
```
    full_name = 'Набор из 4 глубоких тарелок "Дюна"'
    print_product_details(full_name, page_number=2)
```
