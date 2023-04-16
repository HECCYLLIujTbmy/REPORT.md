## Laboratory work II

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

## Tasks

- [ ] 1. Создать публичный репозиторий с названием **lab02** и с лиценцией **MIT**
- [ ] 2. Сгенирировать токен для доступа к сервису **GitHub** с правами **repo**
- [ ] 3. Ознакомиться со ссылками учебного материала
- [ ] 4. Выполнить инструкцию учебного материала
- [ ] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
$ export GITHUB_USERNAME=HECCYLLIujTbmy
$ export GITHUB_EMAIL=<адрес_почтового_ящика>
$ export GITHUB_TOKEN=<сгенирированный_токен>
$ alias edit=<nano|vi|vim|subl>
```

```sh
$ cd ${GITHUB_USERNAME}/workspace
$ source scripts/activate
```

```sh
$ mkdir ~/.config
$ cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
$ git config --global hub.protocol https
```

```sh
$ mkdir projects/lab02 && cd projects/lab02
$ git init

```sh
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint: 
hint:   git config --global init.defaultBranch <name>
hint: 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint:   git branch -m <name>
Initialized empty Git repository in /home/kali/HECCYLLIujTbmy/workspace/projects/lab02/.git/
```

```sh
$ git config --global user.name ${GITHUB_USERNAME}
$ git config --global user.email ${GITHUB_EMAIL}
# check your git global settings
$ git config -e --global
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git
```

```sh
$ git pull origin master
Username for 'https://github.com': HECCYLLIujTbmy
Password for 'https://HECCYLLIujTbmy@github.com': 
remote: Repository not found.
fatal: repository 'https://github.com/HECCYLLIujTbmy/lab02.git/' not found P.S забыл создать репозиторий
```
```sh
$ touch README.md
$ git status

On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md

nothing added to commit but untracked files present (use "git add" to track)
```
```sh
$ git add README.md
$ git commit -m"added README.md"

[master (root-commit) 0a2c152] added README.md
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README.md

$ git push origin master
Username for 'https://github.com': HECCYLLIujTbmy
Password for 'https://HECCYLLIujTbmy@github.com': 
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 238 bytes | 238.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote: 
remote: Create a pull request for 'master' on GitHub by visiting:
remote:      https://github.com/HECCYLLIujTbmy/lab02/pull/new/master
remote: 
To https://github.com/HECCYLLIujTbmy/lab02.git
 * [new branch]      master -> master
```

Добавить на сервисе **GitHub** в репозитории **lab02** файл **.gitignore**
со следующем содержимом:

```sh
*build*/
*install*/
*.swp
.idea/
```

```sh
$ git pull origin master
From https://github.com/HECCYLLIujTbmy/lab02
 * branch            master     -> FETCH_HEAD
Already up to date.
$ git log
сommit 0a2c15243ddeb6af431b1c546c5e7296e89f86bb (HEAD -> master, origin/master)
Author: HECCYLLIujTbmy <sokolovskijvladislav23@gmail.com>
Date:   Sat Apr 15 14:17:07 2023 -0400

    added README.md

```

```sh
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
```

```sh
$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
```

```sh
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
```

```sh
$ cat > examples/example2.cpp <<EOF
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
```

```sh
$ edit README.md
```

```sh
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        examples/
        include/
        sources/

nothing added to commit but untracked files present (use "git add" to track)

$ git add .
$ git commit -m"added sources"

[master 6edd28b] added sources
 4 files changed, 29 insertions(+)
 create mode 100644 examples/example1.cpp
 create mode 100644 examples/example2.cpp
 create mode 100644 include/print.hpp
 create mode 100644 sources/print.cpp

$ git push origin master
Username for 'https://github.com': HECCYLLIujTbmy
Password for 'https://HECCYLLIujTbmy@github.com': 
Enumerating objects: 10, done.
Counting objects: 100% (10/10), done.
Delta compression using up to 2 threads
Compressing objects: 100% (7/7), done.
Writing objects: 100% (9/9), 922 bytes | 922.00 KiB/s, done.
Total 9 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/HECCYLLIujTbmy/lab02.git
   0a2c152..6edd28b  master -> master

```

## Report

```sh
$ cd ~/workspace/
$ export LAB_NUMBER=02
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}

Cloning into 'tasks/lab02'...
remote: Enumerating objects: 96, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 96 (delta 0), reused 1 (delta 0), pack-reused 93
Receiving objects: 100% (96/96), 1.29 MiB | 1.86 MiB/s, done.
Resolving deltas: 100% (28/28), done.
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
Error: Got Net::HTTPUnauthorized from gist: {"message":"Requires authentication","documentation_url":"https://docs.github.com/rest/reference/gists#create-a-gist"} P.S не понял, почему именно так, гист использовал с правами repo
```

## Homework

### Part I

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге
```sh
git config --global hub.protocol https        
                                                                                                                                                    
┌──(kali㉿kali)-[~/HECCYLLIujTbmy/workspace]
└─$ mkdir projects/lab02dz && cd projects/lab02dz
                                                                                                                                                    
┌──(kali㉿kali)-[~/HECCYLLIujTbmy/workspace/projects/lab02dz]
└─$ git init                              
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint: 
hint:   git config --global init.defaultBranch <name>
hint: 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint:   git branch -m <name>
Initialized empty Git repository in /home/kali/HECCYLLIujTbmy/workspace/projects/lab02dz/.git/
                                                                                                                                                    
┌──(kali㉿kali)-[~/HECCYLLIujTbmy/workspace/projects/lab02dz]
└─$ git config --global user.name ${GITHUB_USERNAME}
                                                                                                                                                    
┌──(kali㉿kali)-[~/HECCYLLIujTbmy/workspace/projects/lab02dz]
└─$ git config --global user.email ${GITHUB_EMAIL}
                                                                                                                                                    
┌──(kali㉿kali)-[~/HECCYLLIujTbmy/workspace/projects/lab02dz]
└─$ git config -e --global
                                                                                                                                                    
┌──(kali㉿kali)-[~/HECCYLLIujTbmy/workspace/projects/lab02dz]
└─$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02dz.git
                                                                                                                                                    
┌──(kali㉿kali)-[~/HECCYLLIujTbmy/workspace/projects/lab02dz]
└─$ git pull origin master                                                 
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 218 bytes | 218.00 KiB/s, done.
From https://github.com/HECCYLLIujTbmy/lab02dz
 * branch            master     -> FETCH_HEAD
 * [new branch]      master     -> origin/master
                                                                                                                                                    
┌──(kali㉿kali)-[~/HECCYLLIujTbmy/workspace/projects/lab02dz]
└─$ touch README.md
                                                                                                                                                    
┌──(kali㉿kali)-[~/HECCYLLIujTbmy/workspace/projects/lab02dz]
└─$ git status
On branch master
nothing to commit, working tree clean
                                                                                                                                                    
┌──(kali㉿kali)-[~/HECCYLLIujTbmy/workspace/projects/lab02dz]
└─$ git add README.md
                                                                                                                                                    
┌──(kali㉿kali)-[~/HECCYLLIujTbmy/workspace/projects/lab02dz]
└─$ git commit -m "added README.md"
On branch master
nothing to commit, working tree clean
                                                                                                                                                    
┌──(kali㉿kali)-[~/HECCYLLIujTbmy/workspace/projects/lab02dz]
└─$ git push origin master         
Username for 'https://github.com': HECCYLLIujTbmy
Password for 'https://HECCYLLIujTbmy@github.com': 
Everything up-to-date
                                                                                                                                                    
┌──(kali㉿kali)-[~/HECCYLLIujTbmy/workspace/projects/lab02dz]
└─$ mkdir sources
```

3. Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.

```sh
cat > sources/hello_world.cpp<<EOF 
heredoc> #include <iostream>
heredoc> using namespace std;
heredoc> int main()
heredoc> {
heredoc> cout<<"TTpuBeT Mup";     
heredoc> }
heredoc> EOF  
```
4. Добавьте этот файл в локальную копию репозитория.
```sh
git add sources/hello_world.cpp
```
5. Закоммитьте изменения с *осмысленным* сообщением.
```sh
it commit -m "added hello_world.cpp"
[master 681df98] added hello_world.cpp
 1 file changed, 6 insertions(+)
 create mode 100644 sources/hello_world.cpp
 ```
6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.

```sh
edit sources/hello_world.cpp
```
7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?
```sh
git commit -m "new hello_world.cpp"
[master 4c756dc] new hello_world.cpp
 1 file changed, 5 insertions(+), 1 deletion(-)
```
8. Запуште изменения в удалёный репозиторий.

```sh
git push origin master
Username for 'https://github.com': HECCYLLIujTbmy
Password for 'https://HECCYLLIujTbmy@github.com': 
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 2 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 485 bytes | 485.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/HECCYLLIujTbmy/lab02dz.git
   681df98..4c756dc  master -> master
```
9. Проверьте, что история коммитов доступна в удалёный репозитории.

### Part II

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. В локальной копии репозитория создайте локальную ветку `patch1`.
```sh
git checkout -b patch1  
Switched to a new branch 'patch1'
```
2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.
```sh
edit hello_world.cpp
```
3. **commit**, **push** локальную ветку в удалённый репозиторий.
```sh
git commit -m "fixedl hello_world.cpp"
On branch patch1
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        new_hello_world.cpp

nothing added to commit but untracked files present (use "git add" to track)
```
```sh
git push origin patch1                
Username for 'https://github.com': HECCYLLIujTbmy
Password for 'https://HECCYLLIujTbmy@github.com': 
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
remote: 
remote: Create a pull request for 'patch1' on GitHub by visiting:
remote:      https://github.com/HECCYLLIujTbmy/lab02dz/pull/new/patch1
remote: 
To https://github.com/HECCYLLIujTbmy/lab02dz.git
 * [new branch]      patch1 -> patch1
 ```
 
4. Проверьте, что ветка `patch1` доступна в удалёный репозитории.
5. Создайте pull-request `patch1 -> master`.
6. В локальной копии в ветке `patch1` добавьте в исходный код комментарии.
7. **commit**, **push**.
8. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request
9. В удалённый репозитории выполните  слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.
10. Локально выполните **pull**.
11. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.
12. Удалите локальную ветку `patch1`.

### Part III

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. Создайте новую локальную ветку `patch2`.
2. Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.
3. **commit**, **push**, создайте pull-request `patch2 -> master`.
4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
5. Убедитесь, что в pull-request появились *конфликтны*.
6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.
7. Сделайте *force push* в ветку `patch2`
8. Убедитель, что в pull-request пропали конфликтны. 
9. Вмержите pull-request `patch2 -> master`.

## Links

- [hub](https://hub.github.com/)
- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2015-2021 The ISC Authors
```
