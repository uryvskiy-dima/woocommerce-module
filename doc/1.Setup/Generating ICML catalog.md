### Генерация ICML

Данная опция позволяет сгенерировать каталог вручную.

Для активации необходимо нажать на кнопку и дождаться сообщения о завершении генерации. Сгенерированный каталог будет доступен по ссылке https://yoursite.com/simla.xml

Чтобы проверить, что команда по генерации каталога отработала успешно, можно перейти по ссылке и сравнить дату генерации каталога с текущей:

![](https://lh3.googleusercontent.com/Z6qwxSjGA9AHjaDi3RgbJyeQRhvXAkXRvtzXmEJzVdMpwQ2Rc4N0FM9YFhMWYTL-dwoxKmSYgPsJU68TfCer_og-BmnUruKJMJlmjIM7suz42OMCJFH3cwPoKfbW66AYzUL3UZTd=s0)

Ссылку на каталог требуется указать в настройках магазина в CRM. Для его загрузки в CRM необходимо активировать опцию “Загрузить каталог из ICML сейчас” и сохранить настройки.
![](https://lh4.googleusercontent.com/oPPNIbm11rgYUbeWIKkyp1XdqC47_N-iTh-jp0C3V5QrRemD-0Gco6pholEP0HKKmkZCpag1n7oiMNvPXiUh5yjSF2DSLtX5_wJPqwQ97XsJDdFdbAPsTYU4LpMdSlPyfs-hviw7=s0)

### Генерация ICML каталога товаров с помощью wp-cron

Данный функционал позволяет генерировать каталог в автоматическом режиме с помощью WP-CRON, в этом случае не потребуется каждый раз при необходимости обновить каталог, заходить в настройки и запускать его загрузку вручную.

Каталог генерируется **раз в 3 часа**.

### Синхронизация остатков и связь товаров

Функционал служит для **идентификации товаров по SKU (xmlID)**. Для активации необходимо поставить галочку.

После активации опции при генерации каталога в нем появится параметр xmlID *(артикул)*.

С версии 4.7.5 после активации/деактивации опции и сохранении настроек, каталог будет сгенерирован автоматически.

**xmlID** - внешний идентификатор товара, элемент не является обязательным. В случае, если интернет-магазин использует выгрузку номенклатуры товаров из складской системы *(1С, МойСклад)*, то значение этого элемента соответствует идентификатору товара в данной системе. Активируется, когда клиенты используют Woocommerce + MC/1C.

### Недавние обновления:

**В версии 4.4.4** добавлен функционал передачи описания товара в каталог. В настройках каталога необходимо выбрать, какое описание передавать краткое или полное. По умолчанию передается полное описание товара.

Поле description(описание) выводится в карточке товара, так же его можно использовать в twig-шаблонах. Например, для вывода в печатных формах.
Пример получения описание торгового предложения:
```twig
{% for availableOrderProduct in order.availableOrderProducts %} {{ availableOrderProduct.getOffer().getDescription() }} {% endfor %}
```

**В версии 4.4.6** добавлен фильтр:

> retailcrm_process_offer - позволяет изменить данные товара, перед записью в ICML каталог.


**Пример использования:**
```php
<?php

add_action('retailcrm_process_offer', 'changeProductInfo', 10, 2);

function changeProductInfo($productData, $wcProduct)
{
    $productData['name'] .= 'Test';

    return $productData;
}
```
