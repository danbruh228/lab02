# Laboratory work II

Данная лабораторная работа посвещена изучению систем контроля версий на примере Git.

$ open https://git-scm.com
Tasks

 1. Создать публичный репозиторий с названием lab02 и с лиценцией MIT
 2. Сгенирировать токен для доступа к сервису GitHub с правами repo
 3. Ознакомиться со ссылками учебного материала
 4. Выполнить инструкцию учебного материала
 5. Составить отчет и отправить ссылку личным сообщением в Slack
Tutorial

$ export GITHUB_USERNAME=<имя_пользователя>
$ export GITHUB_EMAIL=<адрес_почтового_ящика>
$ export GITHUB_TOKEN=<сгенирированный_токен>
$ alias edit=<nano|vi|vim|subl>
$ cd ${GITHUB_USERNAME}/workspace
$ source scripts/activate
$ mkdir ~/.config
$ cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
$ git config --global hub.protocol https
$ mkdir projects/lab02 && cd projects/lab02
$ git init
$ git config --global user.name ${GITHUB_USERNAME}
$ git config --global user.email ${GITHUB_EMAIL}
# check your git global settings
$ git config -e --global
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git
$ git pull origin master
$ touch README.md
$ git status
$ git add README.md
$ git commit -m"added README.md"
$ git push origin master
Добавить на сервисе GitHub в репозитории lab02 файл .gitignore со следующем содержимом:

*build*/
*install*/
*.swp
.idea/
$ git pull origin master
$ git log
$ mkdir sources
$ mkdir include
$ mkdir examples
$ cat > sources/print.cpp <<EOF
#include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
EOF
$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
$ cat > examples/example2.cpp <<EOF
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
$ edit README.md
$ git status
$ git add .
$ git commit -m"added sources"
$ git push origin master
Report

$ cd ~/workspace/
$ export LAB_NUMBER=02
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
Homework

Part I

Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
Создайте файл hello_world.cpp в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу Hello world на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку using namespace std;.
Добавьте этот файл в локальную копию репозитория.
Закоммитьте изменения с осмысленным сообщением.
Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение Hello world from @name, где @name имя пользователя.
Закоммитьте новую версию программы. Почему не надо добавлять файл повторно git add?
Запуште изменения в удалёный репозиторий.
Проверьте, что история коммитов доступна в удалёный репозитории.
Part II

Note: Работать продолжайте с теми же репоззиториями, что и в первой части задания.

В локальной копии репозитория создайте локальную ветку patch1.
Внесите изменения в ветке patch1 по исправлению кода и избавления от using namespace std;.
commit, push локальную ветку в удалённый репозиторий.
Проверьте, что ветка patch1 доступна в удалёный репозитории.
Создайте pull-request patch1 -> master.
В локальной копии в ветке patch1 добавьте в исходный код комментарии.
commit, push.
Проверьте, что новые изменения есть в созданном на шаге 5 pull-request
В удалённый репозитории выполните слияние PR patch1 -> master и удалите ветку patch1 в удаленном репозитории.
Локально выполните pull.
С помощью команды git log просмотрите историю в локальной версии ветки master.
Удалите локальную ветку patch1.
Part III

Note: Работать продолжайте с теми же репоззиториями, что и в первой части задания.

Создайте новую локальную ветку patch2.
Измените code style с помощью утилиты clang-format. Например, используя опцию -style=Mozilla.
commit, push, создайте pull-request patch2 -> master.
В ветке master в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
Убедитесь, что в pull-request появились конфликтны.
Для этого локально выполните pull + rebase (точную последовательность команд, следует узнать самостоятельно). Исправьте конфликты.
Сделайте force push в ветку patch2
Убедитель, что в pull-request пропали конфликтны.
Вмержите pull-request patch2 -> master.
Links

hub
GitHub
Bitbucket
Gitlab
LearnGitBranching
Copyright (c) 2015-2021 The ISC Authors
