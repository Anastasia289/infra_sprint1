# Kittygram 

## Описание проекта:
Kittygram — социальная сеть для обмена фотографиями любимых питомцев. Проект состоит из бэкенд-приложения на Django и фронтенд-приложения на React.

## Инструкция по запуску:

### Клонируйте репозиторий:   
git@github.com:Anastasia289/infra_sprint1.git
   
### Настройте бэкенд приложения:
- Перейдите в директорию бэкенд-приложения проекта.
- Создайте виртуальное окружение:  
python3 -m venv venv
- Активируйте виртуальное окружение:  
source venv/bin/activate
- Установите зависимости:  
pip install -r requirements.txt
- Перейдите в директорию с файлом manage.py и
примените миграции:  
python3 manage.py migrate
-Создайте суперпользователя:  
python3 manage.py createsuperuser
- Добавьте в список ALLOWED_HOSTS внешний IP сервера, localhost и домен
- Соберите статику бэкенд-приложения:  
python3 manage.py collectstatic
- Скопируйте директорию static_backend/ в директорию /var/www/название_проекта/:  
sudo cp -r путь_к_директории_с_бэкендом/static_backend /var/www/название_проекта


### Настройте фронтенд приложения
- Находясь в директории с фронтенд-приложением, установите зависимости для него:  
npm i
- Из директории с фронтенд-приложением выполните команду:  
npm run build
- Скопируйте статику фронтенд-приложения в директорию по умолчанию:  
sudo cp -r путь_к_директории_с_фронтенд-приложением/build/. /var/www/имя_проекта/

### Установите и настройте WSGI-сервер Gunicorn

- Установите пакет gunicorn:  
pip install gunicorn==20.1.0
- Перейдите в директорию с файлом manage.py, и запустите Gunicorn:  
gunicorn --bind 0.0.0.0:8000 backend.wsgi
- Создайте файл конфигурации юнита systemd для Gunicorn в директории
/etc/systemd/system/. Назовите его по шаблону gunicorn_название_проекта.service:
sudo nano /etc/systemd/system/gunicorn_название_проекта.service
- Добавьте в код данные из файла infra_sprint1
/infra/gunicorn_kittygram.service
- Запустите  
sudo systemctl start gunicorn_название_проекта
- Чтобы systemd следил за работой демона Gunicorn, запускал его при старте системы
и при необходимости перезапускал, используйте команду:  
sudo systemctl enable gunicorn_название_проекта

### Установите и настройте веб- и прокси-сервера Nginx
- Установите Nginx:  
sudo apt install nginx -y
- Запустите Nginx командой:  
sudo systemctl start nginx
- Обновите настройки Nginx. Для этого откройте файл конфигурации веб-сервера…
sudo nano /etc/nginx/sites-enabled/default
…очистите содержимое файла и запишите новые настройки. Данные возьмите из файла infra_sprint1/infra/default
- Сохраните изменения в файле, закройте его и проверьте на корректность:  
sudo nginx -t
- Перезагрузите конфигурацию Nginx:  
sudo systemctl reload nginx


## Технологии:

Python  
Django  
React  
Nginx  
Gunicorn  
Certbot  

## Автор: 
   
Анастасия Богданова   
bogdanovanastja@yandex.ru  
@lyckkkyday
