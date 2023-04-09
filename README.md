# 10.3_ElasticStack_Aleksandr_Molokov

## Задание 1

Вам необходимо поднять в докере и связать между собой:

- elasticsearch (hot и warm ноды);
- logstash;
- kibana;
- filebeat.

Logstash следует сконфигурировать для приёма по tcp json-сообщений.

Filebeat следует сконфигурировать для отправки логов docker вашей системы в logstash.

В директории [help](./help) находится манифест docker-compose и конфигурации filebeat/logstash для быстрого 
выполнения этого задания.

Результатом выполнения задания должны быть:

- скриншот `docker ps` через 5 минут после старта всех контейнеров (их должно быть 5);
- скриншот интерфейса kibana;
- docker-compose манифест (если вы не использовали директорию help);
- ваши yml-конфигурации для стека (если вы не использовали директорию help).

# Ответ
Создал ВМ в YandexCloud, запустил docker-compose результат на скриншоте

![yandexcloud start containers](https://user-images.githubusercontent.com/109212419/230673890-9b28f573-8096-41e3-aa77-c98a67e94ad0.jpg)

Контейнеры es-hot и es-warm падали после 1 минуты
![ноды отключаются из-за слишком большого объема расходуемой памяти](https://user-images.githubusercontent.com/109212419/230674168-8022d915-8e49-4aa7-a815-541559c29128.jpg)

решил проблему вводом команды sudo sysctl -w vm.max_map_count=262144
![Команда чтоб контейнеры не падали с ошибкой по памяти](https://user-images.githubusercontent.com/109212419/230674205-e624136c-29a6-4d46-9b78-dc152fe8dce9.jpg)

Через 5 минут все контейнеры работают
![контейнера после 5 минут](https://user-images.githubusercontent.com/109212419/230674547-b4c97a37-3b15-4f8f-95a9-9ff692b1256f.jpg)

Состояние нод и кластера Elasticsearch (все вроде нормально)

![состояние нод и кластера](https://user-images.githubusercontent.com/109212419/230794568-9207a6ed-5672-49d3-929a-8165e50204bf.jpg)

# Скриншоты docker-compose up

![docker-compose up](https://user-images.githubusercontent.com/109212419/230794816-4b62608e-9900-426b-b972-63ff6b40c65d.jpg)

![docker-compose up filebeat](https://user-images.githubusercontent.com/109212419/230794825-b7ac4d2f-243e-44a5-bea2-8f39d2785e5c.jpg)

![docker-compose up filebeat 1](https://user-images.githubusercontent.com/109212419/230794834-7ad444bc-00fb-4a87-8ece-821beff4c6a4.jpg)

![docker-compose up kibana](https://user-images.githubusercontent.com/109212419/230794843-10d3b3fc-3758-4988-a253-688a3321bb0c.jpg)

![docker-compose up logstash](https://user-images.githubusercontent.com/109212419/230794852-e966f9ef-c6f9-48e2-b6c9-c6e5325c9d9d.jpg)


Kibana запустилась

![kibana start](https://user-images.githubusercontent.com/109212419/230674256-dec8d972-7d59-4205-863e-76aed365888d.jpg)

В разделе Index managment пусто
![index menagment](https://user-images.githubusercontent.com/109212419/230674577-89928661-5753-4d1b-8547-74df00c36da6.jpg)



## Задание 2

Перейдите в меню [создания index-patterns  в kibana](http://localhost:5601/app/management/kibana/indexPatterns/create) и создайте несколько index-patterns из имеющихся.

Перейдите в меню просмотра логов в kibana (Discover) и самостоятельно изучите, как отображаются логи и как производить поиск по логам.

В манифесте директории help также приведенно dummy-приложение, которое генерирует рандомные события в stdout-контейнера.
Эти логи должны порождать индекс logstash-* в elasticsearch. Если этого индекса нет — воспользуйтесь советами и источниками из раздела «Дополнительные ссылки» этого задания.
 
