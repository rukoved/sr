# Работа с Docker для проекта Drupal

Здесь собраны все команды и настройки для работы с Docker‑контейнерами в проекте `~/Projects/sr`.  
Сервисы: `drupal`, `db` (MariaDB), `phpmyadmin`.

---

## 🚀 Запуск проекта

1. Войти в папку проекта:

   ```bash
   cd ~/Projects/sr
Установить Docker (если ещё не установлен):

bash
sudo apt update
sudo apt install docker.io docker-compose --no-install-recommends
sudo systemctl enable --now docker
Запустить контейнеры в фоне:

bash
export UID=$(id -u)
export GID=$(id -g)
docker compose down
docker compose up -d
Проверить, что всё запущено:

bash
docker compose ps
В столбце STATUS у всех контейнеров должно быть Up.

🌐 Доступ к сервисам
Сайт Drupal: http://localhost:8080

phpMyAdmin: http://localhost:8081

Пользователь базы: drupal, пароль: XXX

Root‑пользователь: root, пароль: drupal_root

⚙️ Основные команды Docker для этого проекта
Посмотреть логи Drupal:

bash
docker compose logs drupal
Посмотреть логи базы:

bash
docker compose logs db
Зайти в контейнер Drupal:

bash
docker compose exec drupal bash
Зайти в контейнер MariaDB:

bash
docker compose exec db bash
mysql -u root -p
Остановить все контейнеры:

bash
docker compose down
Перезапустить только Drupal:

bash
docker compose restart drupal
🧼 Как пересобрать/обновить проект
Если что‑то «сломалось», можно полностью перезапустить:

bash
cd ~/Projects/sr
docker compose down
docker volume rm sr_db_data   # подставь точное имя, если отличается
docker compose up -d
После этого:

база будет чистая,

но docker-compose.yml и settings.php останутся.

🔧 Если контейнеры не встают
Посмотреть ошибки:

bash
docker compose logs
Если в db пишет про MYSQL_ROOT_PASSWORD или пользователя drupal:

зайти в db и выставить пароли заново:

bash
docker compose exec db bash
mysql -u root -p
ALTER USER 'drupal'@'%' IDENTIFIED BY 'XXX';
FLUSH PRIVILEGES;
EXIT;
🧩 Рекомендации по правам и Docker
Файл web/sites/default/settings.php должен принадлежать тебе:

bash
cd ~/Projects/sr
sudo chown -R nata:nata web/sites/default
sudo chmod 755 web/sites/default
sudo chmod 644 web/sites/default/settings.php
В docker-compose.yml у блока drupal включено:

text
user: "${UID}:${GID}"
Чтобы контейнер работал от твоего пользователя.

© Натали rukoved
