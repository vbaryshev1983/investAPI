#Сервис предоставления справочной информации о ценных бумагах

##Получение параметров ценных бумаг

Получение справочной информации об инструментах, торгуемых на бирже, является первоочередной задачей,
которая стоит перед разработчиком торгового робота. Для реализации этой потребности в TINKOFF INVEST API 
существует набор unary-методов. 

Обратите внимание, что методы разделены по типам инструментов (акции, облигации, фонды и т.д.). Например,
для получения списка облигаций используется метод [getInstruments/bonds](/investAPI/instruments#bonds), а для получения 
информации по конкретной облигации метод [getInstruments/bondBy](/investAPI/instruments#bondby). 

Методы получения информации по конкретному инструменту позволяют использовать в качестве идентификатора
figi, isin или связку тикер плюс класс-код. Подробнее об особенностях идентификации инструментов можно почитать
по ссылке: [Идентификация инструментов](/investAPI/faq_identification/)

##Получение расписания торгов 

Для определения времени запуска или остановки торгового робота разработчику требуется также учитывать 
расписание торгов на той или иной торговой площадке ([Подробнее о режимах торгов](/investAPI/markets/)).
Такая информация предоставляется методом [getTradingSchedules](/investAPI/instruments#tradingschedules). 
Данный метод позволяет получить информацию как по конкретной бирже, так и по всему списку доступных в 
TINKOFF INVEST API торговых площадок. Обратите внимание, что расписание торгов может меняться в связи с 
какими-либо внешними обстоятельствами — специалисты Тинькофф стараются максимально оперативно реагировать 
на такие изменения. Поэтому разумнее не ориентироваться на расписание, запрошенное по длительному периоду, 
а запрашивать режимы торгов на более короткие интервалы, например, на текущий день.

Метод [getTradingSchedules](/investAPI/instruments#tradingschedules) позволяет получать расписание торгов
на период не длиннее одной недели с текущего дня (запрос раписания в прошлом недоступен).

Так же важно понимать, что в процессе работы торговой площадки могут случаться моменты приостановки торгов
по той или иной ценной бумаге (например, в следствии резко возросшей волатильности). Поэтому для определения
доступности в данный момент торгов по конкретному инструменту лучше использовать параметр *trading_status*,
который возвращается в рамках подписки на получение статуса инструмента [сервиса котировок](/investAPI/head-marketdata/).

##Получение расписания выплаты купонов по облигациям

Облигация — это долговая ценная бумага, почти как долговая расписка. Выпуская облигации, компания 
или государство берет деньги в долг и затем возвращает их с процентами([Подробнее про облигации](https://help.tinkoff.ru/invest-to/invest-to-bonds/)).

Операции по регулярным выплатам процентов по облигации называются купонами. Для получения графика таких
выплат используется метод [getAccruedInterests](/investAPI/instruments#getaccruedinterests). Метод позволяет получить график выплаты купонов
для запрошенного периода времени.

##Получения размера гарантийного обеспечения по фьючерсу

Фьючерс — это договор между покупателем и продавцом о поставке базового актива в будущем или о выплате 
одной из сторон другой стороне разницы между стоимостью контракта и стоимостью базового актива в 
будущем ([Срочный рынок](https://help.tinkoff.ru/forts/)).

Для операций с фьючерсами брокером "замораживается" определённый размер гарантийного обеспечения на счёте
пользователя. Для получения информации о размере этого обеспечения используется метод [getFuturesMargin](/investAPI/instruments#getfuturesmargin).
Обратите внимание, что размер гарантийного обеспечения может отличаться для операций покупки и продажи
фьючерса.

##Получение и изменение списка избранных инструментов

Используя метод [GetFavorites](/investAPI/instruments#getfavorites) можно получить список избранных инструментов клиента.
Данный метод может использоваться разработчиками для получения списка инструментов, которые робот добавил в избранное используя метод [EditFavorites](/investAPI/instruments#editfavorites).

Для добавления или удаления инструментов из списка избранных можно использовать [EditFavorites](/investAPI/instruments#editfavorites).
Данный метод позволяет разработчикам автоматизировать выделение наиболее интересных инструментов путем редактирования списка избранных инструментов.

Так же все инструменты добавленные в избранное будут отображаться в списке избранных в мобильном приложении Инвестиции и на сайте [Тинькофф Инвестиции](https://www.tinkoff.ru/invest/favorites/).

###Определение биржи на которой исполняются расчеты по инструменту

Для определения биржи на которой исполняются расчеты по финансовому инструменту в TINKOFF INVEST API добавлен параметр [real_exchange](/investAPI/instruments/#realexchange).

Список методов возвращающих в ответе биржу на которой исполняются расчеты:

* [GetInstrumentBy](/investAPI/instruments/#getinstrumentby) - Метод получения основной информации об инструменте.
* [GetBondBy](/investAPI/instruments/#bondby) - Метод получения облигации по её идентификатору.
* [GetBonds](/investAPI/instruments/#bonds) - Метод получения списка облигаций.
* [GetShareBy](/investAPI/instruments/#shareby) - Метод получения акции по её идентификатору.
* [GetShares](/investAPI/instruments/#shares) - Метод получения списка акций.
* [GetEtfBy](/investAPI/instruments/#etfby) - Метод получения инвестиционного фонда по его идентификатору.
* [GetEtfs](/investAPI/instruments/#etfs) - Метод получения списка инвестиционных фондов.
* [GetFutureBy](/investAPI/instruments/#futureby) - Метод получения фьючерса по его идентификатору.
* [GetFutures](/investAPI/instruments/#futures) - Метод получения списка фьючерсов.
* [GetCurrencyBy](/investAPI/instruments/#currencyby) - Метод получения валюты по её идентификатору.
* [GetCurrencies](/investAPI/instruments/#currencies) - Метод получения списка валют.

###Поиск инструментов

Для поиска инструментов в TINKOFF INVEST API предусмотрено большое количество методов. 
Для поиска по идентификаторам вы можете воспользоваться следующими методами в зависимости от типа искомого инструмента:
* [GetInstrumentBy](/investAPI/instruments/#getinstrumentby) - Метод получения основной информации об инструменте.
* [GetBondBy](/investAPI/instruments/#bondby) - Метод получения облигации по её идентификатору.
* [GetBonds](/investAPI/instruments/#bonds) - Метод получения списка облигаций.
* [GetShareBy](/investAPI/instruments/#shareby) - Метод получения акции по её идентификатору.
* [GetShares](/investAPI/instruments/#shares) - Метод получения списка акций.
* [GetEtfBy](/investAPI/instruments/#etfby) - Метод получения инвестиционного фонда по его идентификатору.
* [GetEtfs](/investAPI/instruments/#etfs) - Метод получения списка инвестиционных фондов.
* [GetFutureBy](/investAPI/instruments/#futureby) - Метод получения фьючерса по его идентификатору.
* [GetFutures](/investAPI/instruments/#futures) - Метод получения списка фьючерсов.
* [GetCurrencyBy](/investAPI/instruments/#currencyby) - Метод получения валюты по её идентификатору.
* [GetCurrencies](/investAPI/instruments/#currencies) - Метод получения списка валют.

Так же разработан метод поиска инструмента по различным параметрам - [FindInstrument](/investAPI/instruments/#findinstrument). 
Данный метод выполняет **регистронезависимый** поиск по вхождению строки query согласно следующему приоритету:

* position_uid
* uid
* figi
* isin
* ticker
* name

Так же используя метод [FindInstrument](/investAPI/instruments/#findinstrument) можно найти базовый актив фьючерса. 
Для этого достаточно передать в query значение параметра `basic_asset_position_uid` возвращаемое методами [GetFutureBy](/investAPI/instruments/#futureby) и [GetFutures](/investAPI/instruments/#futures).


###Доступность торговли инструмента через API

Для получения информации о возможности торговли инструментом через API в сервисе инструментов в методе [FindInstrument](/investAPI/instruments/#findinstrument) существует параметр `api_trade_available_flag`.
Если api_trade_available_flag = true, то торговля инструментом через API доступна.

