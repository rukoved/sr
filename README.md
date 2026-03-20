# Проект Drupal 11 на Docker

Этот проект — локальный сайт Drupal 11, развёрнутый через Docker (MariaDB, Apache, phpMyAdmin).  
Вся структура подключена к Git‑репозиторию на GitHub, но некоторые файлы исключены из Git по соображениям безопасности.

---

## 🧱 Структура проекта

- `docker-compose.yml` — запуск контейнеров (`drupal`, `db`, `phpmyadmin`).  
- `web/` — ядро Drupal, модули, темы, конфигурации.  
- `.gitignore` — файлы, которые **не попадают** в Git.

---

## ⚙️ Запуск проекта

1. Выйти в папку проекта:

   ```bash
   cd ~/Projects/sr
Установить Git (если ещё не установлен):

bash
sudo apt update
sudo apt install git
Запустить Docker‑стек:

bash
export UID=$(id -u)
export GID=$(id -g)
docker compose down
docker compose up -d
Проверить, что всё работает:

Сайт: http://localhost:8080

phpMyAdmin: http://localhost:8081

База: db (пользователь drupal, пароль XXX).

🔐 Подключение к GitHub (токен)
Создать personal access token на GitHub:
Settings → Developer settings → Personal access tokens → Tokens (classic)

Note: sr-project

Scope: repo

Скопировать токен.

Подключить репозиторий к локальному проекту (если ещё не подключен):

bash
git remote set-url origin https://rukoved@github.com/rukoved/sr.git
При первом git push:

Username: rukoved

Password: <ваш токен>.

Включить сохранение логина/токена:

bash
git config --global credential.helper store
📦 Как отправлять изменения в Git
Перед каждым пулем.persistent_commit:

bash
cd ~/Projects/sr
git status
git add .
git commit -m "Описание изменений"
git pull --no-rebase origin main
git push origin main
Если ветка main ещё не синхронизирована в первый раз:

bash
git pull --no-rebase --allow-unrelated-histories origin main
git push origin main
🚫 Файлы, которые НЕ попадают в Git
В .gitignore уже прописаны строки, чтобы Git не трогал:

*.log

web/sites/default/settings.php

web/sites/default/files

web/sites/default/settings.local.php

docker-compose.override.yml

.env

Это делает репозиторий безопасным и чистым.

🧹 Удаление лишнего репозитория на GitHub
Если вдруг был создан пустой репозиторий, который не нужен:

Открыть его на GitHub.

Перейти: Settings → Danger Zone → Delete this repository.

Ввести полное имя репозитория вида rukoved/имя_репозитория.

Ввести пароль (если запросит).

Нажать Delete this repository.

© Натали rukoved
