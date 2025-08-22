# Лабораторная работа №2 Первоначальна настройка git.

### Цель работы: Изучить идеологию и применение средств контроля версий и освоить умения по работе с git.
### Обучающийся группы НКАбд-04-24 Стешенко Артём Сергеевич

- [Задание](##Задание)
  - [Базовая настройка git](###-Базовая-настройка-git)
  - [Создайте ключи pgp](###-Создайте-ключи-pgp)
  - [Шаблон для рабочего пространства](###-Шаблон-для-рабочего-пространства)
  - [Настройка каталога курса](###Настройка-каталога-курса)
- [Заключение](##Заключение)

## Задание
 Создать базовую конфигурацию для работы с git.
 Создать ключ SSH.
 Создать ключ PGP. 
 Настроить подписи git.
 Зарегистрироваться на Github.
 Создать локальный каталог для выполнения заданий по предмету.
 Последовательность выполнения работы 
 Установка программного обеспечения
 Установка git 
 Установим git:
_dnf install git_
Установка gh
Fedora:
_dnf install gh_
### Базовая настройка git
Зададим имя и email владельца репозитория:

_git config --global user.name "Name Surname"_

_git config --global user.email "work@mail"_

Настроим utf-8 в выводе сообщений git:

_git config --global core.quotepath false_

Настройте верификацию и подписание коммитов git (см. Верификация коммитов git с помощью GPG).

Зададим имя начальной ветки (будем называть её master):

_git config --global init.defaultBranch master_

Параметр autocrlf:

_git config --global core.autocrlf input_

Параметр safecrlf:

_git config --global core.safecrlf warn_

Создайте ключи ssh

по алгоритму rsa с ключём размером 4096 бит:

_ssh-keygen -t rsa -b 4096_

по алгоритму ed25519:

_ssh-keygen -t ed25519_

![](https://github.com/Soiroys/study_2024-2025_os-intro/blob/master/labs/lab02/report/image/Снимок%20экрана%202025-08-22%20215836.png?raw=true)

### Создайте ключи pgp
Генерируем ключ

_gpg --full-generate-key_

Из предложенных опций выбираем:

тип RSA and RSA;

размер 4096;

выберите срок действия; значение по умолчанию — 0 (срок действия не истекает никогда).

GPG запросит личную информацию, которая сохранится в ключе:

Имя (не менее 5 символов).

Адрес электронной почты.

При вводе email убедитесь, что он соответствует адресу, используемому на GitHub.

Комментарий. Можно ввести что угодно или нажать клавишу ввода, чтобы оставить это поле пустым.

!()[https://github.com/Soiroys/study_2024-2025_os-intro/blob/master/labs/lab02/report/image/Снимок%20экрана%202025-08-23%20000433.png?raw=true]

#### Настройка github

Создайте учётную запись на https://github.com.

Заполните основные данные на https://github.com.


Добавление PGP ключа в GitHub

Выводим список ключей и копируем отпечаток приватного ключа:

_gpg --list-secret-keys --keyid-format LONG_v

Отпечаток ключа — это последовательность байтов, используемая для идентификации более длинного, по сравнению с самим отпечатком ключа.

Формат строки:

sec   Алгоритм/Отпечаток_ключа Дата_создания [Флаги] [Годен_до] ID_ключа
  

Cкопируйте ваш сгенерированный PGP ключ в буфер обмена:

_gpg --armor --export <PGP Fingerprint> | xclip -sel clip_

Перейдите в настройки GitHub (https://github.com/settings/keys), нажмите на кнопку New GPG key и вставьте полученный ключ в поле ввода.
![](https://github.com/Soiroys/study_2024-2025_os-intro/blob/master/labs/lab02/report/image/Снимок%20экрана%202025-08-22%20221147.png?raw=true)

### Настройка автоматических подписей коммитов git

Используя введёный email, укажите Git применять его при подписи коммитов:

_git config --global user.signingkey <PGP Fingerprint>_

_git config --global commit.gpgsign true_

_git config --global gpg.program $(which gpg2)_

Настройка gh

Для начала необходимо авторизоваться

_gh auth login_

Утилита задаст несколько наводящих вопросов.

Авторизоваться можно через броузер.
![](https://github.com/Soiroys/study_2024-2025_os-intro/blob/master/labs/lab02/report/image/Снимок%20экрана%202025-08-23%20000752.png?raw=true)

### Шаблон для рабочего пространства

Рабочее пространство для лабораторной работы

Репозиторий: https://github.com/yamadharma/course-directory-student-template.

Сознание репозитория курса на основе шаблона

Необходимо создать шаблон рабочего пространства (см. Рабочее пространство для лабораторной работы).

Например, для 2022–2023 учебного года и предмета «Операционные системы» (код предмета os-intro) создание репозитория примет следующий вид:

_mkdir -p ~/work/study/2022-2023/"Операционные системы"_

_cd ~/work/study/2022-2023/"Операционные системы"_

_gh repo create study_2022-2023_os-intro --template=yamadharma/course-directory-student-template --public_

_git clone --recursive git@github.com:<owner>/study_2022-2023_os-intro.git os-intro_



### Настройка каталога курса

Перейдите в каталог курса:

_cd ~/work/study/2022-2023/"Операционные системы"/os-intro_


Удалите лишние файлы:

_rm package.json_

Создайте необходимые каталоги:

_echo os-intro > COURSE_

_make_

Отправьте файлы на сервер:

_git add ._

_git commit -am 'feat(main): make course structure'_

_git push_

![](https://github.com/Soiroys/study_2024-2025_os-intro/blob/master/labs/lab02/report/image/Снимок%20экрана%202025-08-23%20000931.png?raw=true)


 ## Заключение 
Я изучил идеологию и применение средств контроля версий и освоить умения по работе с git.







