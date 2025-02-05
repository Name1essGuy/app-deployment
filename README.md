# Набор инструкций для выкладки шаблонного приложения на сервер
Данный набор набор инструкций предназначен для выкладки в публичный доступ шаблонного приложения, упакованного в контейнер docker.

## Выкладка сервиса на сервер
1. Установите ansible (если не сделали этого ранее)

2. Внесите изменения в файл `service/ansible/inventory`
   А именно:
   1. Укажите Ip-адрес вашего сервреа (можно использовать его доменное имя)
   2. Путь к файлу закрытого ключа на вашем ПК.
   3. Пользователя, от имени которого будет осуществлён доступ к серверу.

3. Внесите изменения в файл `service/ansible/service-deploy/defaults/main.yml`
   А именно:
   1. Url адрес для клонирования приложения по http
   2. Укажите папку, в которую будет клонировано приложение

4. Из папки `service/ansible` используйте:
   ```shell
   ansible-playbook -b service-playbook.yml
   ```

На сервере будет развёрнуто приложение, а так же запущен systemd unit, который будет запускать приложение по тегу сборки. Тег хранится в указанной вами папке проекта в файле `environment`.
Так же в этом файле можно изменить порты хоста и контейнера, на которых запускается приложение.