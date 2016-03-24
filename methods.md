Основное различие методов GET и POST состоит в способе передачи данных веб-формы обрабатывающему скрипту, а именно:
- Метод GET отправляет скрипту всю собранную информацию формы как часть URL:
```
http://www.test.com/user?login=admin&name=komtet
```
- Метод POST передает данные таким образом, что пользователь сайта уже не видит передаваемые скрипту данные:
```
http://www.test.com/user
```
GET передает данные серверу используя URL, когда POST передает данные, используя тело HTTP запроса.

Длина URL'а ограничена 1024 символами, это и будет верхним ограничением для данных, которые можно отослать GET'ом.

POST может отправлять гораздо большие объемы данных. Лимит устанавливается веб-сервером и обычно равен около 2MB.

Передача данных методом POST более безопасна, чем методом GET, так как секретные данные (например пароль) не отображаются напрямую в web-клиенте пользователя (в отличии от URL, который виден почти всегда).