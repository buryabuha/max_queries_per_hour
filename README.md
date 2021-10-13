На сайте стоит 2 тяжелых плагина, которые при каждой загрузке страницы делают к БД от 300 до 500 запросов (Query Monitor)
На хостинге стоит ограничение для каждого пользователя БД - 70 000 запросов.
При превышении доступ к БД блочится и возникает ошибка:

#1226 - User 'vh463378_wp1' has exceeded the 'max_queries_per_hour' resource (current value: 70000)

Решением стало создание 7ми пользователей с одинаковым паролем и рандомная их смена в файле wp-config.php

$mosConfig_users = array("vh463378_wp1", "vh463378_wp2", "vh463378_wp3", "vh463378_wp4", "vh463378_wp5", "vh463378_wp6", "vh463378_wp7");<br>
$mosConfig_user = $mosConfig_users[array_rand($mosConfig_users)];<br>
define( 'DB_USER', $mosConfig_user );

Код взят из:
https://joomlaportal.ru/faq/issues-and-solutions/319-oshibka-mysql-1226-prevysheno-dopustimoe-kolichestvo-zaprosov

Помимо этого интересно посмотреть общее количество запросов приходящее от разных пользователей БД. Сделать этого не удалось, предположительно потому что нет нужного доступа.

https://dba.stackexchange.com/questions/223303/how-to-determine-queries-per-hour-executed-by-a-particular-mysql-user
https://stackoverflow.com/questions/9842094/sql-how-can-i-get-the-number-of-executed-queries-per-database-or-hour-or
