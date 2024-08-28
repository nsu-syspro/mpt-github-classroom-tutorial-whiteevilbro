# Знакомство с GitHub Classroom

Добро пожаловать в GitHub Classroom.

Каждое задание в этой системе представляет собой ваш персональный GitHub репозиторий,
в который вы будете загружать решение и автоматически проверять его корректность.
При этом преподаватель может просматривать все загруженные вами решения,
а также оставлять комментарии и замечания по коду решений.

> Везде далее запись вида
> ```console
> $ echo "Hello World!"
> Hello world!
> ```
> будет означать, что в командной строке необходимо выполнить команду `echo "Hello World!"`,
> а `$` символизирует приглашение к вводу в командной строке, *его вводить не нужно*.  
> Строчки без `$` символизируют ожидаемый вывод команды, *его вводить не нужно*, на него нужно просто посмотреть.

## Настройка окружения

> [!NOTE]
> Настройку окружения достаточно выполнить один раз.

Для работы с GitHub из командной строки вам потребуется установить утилиты `git` и `gh`.

Например с помощью следующей команды если у вас Ubunutu:

```console
$ sudo apt install git gh
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Suggested packages:
  git-daemon-run | git-daemon-sysvinit git-doc git-email git-gui gitk gitweb git-cvs git-mediawiki git-svn
The following NEW packages will be installed:
  gh git
0 upgraded, 2 newly installed, 0 to remove and 63 not upgraded.
Need to get 12.0 MB of archives.
After this operation, 64.6 MB of additional disk space will be used.
Get:1 http://archive.ubuntu.com/ubuntu mantic/universe amd64 gh amd64 2.27.0+dfsg1-1build1 [8,412 kB]
Get:2 http://archive.ubuntu.com/ubuntu mantic/main amd64 git amd64 1:2.40.1-1ubuntu1 [3,583 kB]
Fetched 12.0 MB in 2s (5,194 kB/s)
Selecting previously unselected package gh.
(Reading database ... 182114 files and directories currently installed.)
Preparing to unpack .../gh_2.27.0+dfsg1-1build1_amd64.deb ...
Unpacking gh (2.27.0+dfsg1-1build1) ...
Selecting previously unselected package git.
Preparing to unpack .../git_1%3a2.40.1-1ubuntu1_amd64.deb ...
Unpacking git (1:2.40.1-1ubuntu1) ...
Setting up gh (2.27.0+dfsg1-1build1) ...
Setting up git (1:2.40.1-1ubuntu1) ...
Processing triggers for man-db (2.11.2-3) ...
```


Затем нужно авторизоваться в GitHub с помощью

```console
$ gh auth login
? What account do you want to log into? GitHub.com
? What is your preferred protocol for Git operations? HTTPS
? Authenticate Git with your GitHub credentials? Yes
? How would you like to authenticate GitHub CLI? Login with a web browser

! First copy your one-time code: XXXX-YYYY
Press Enter to open github.com in your browser... 
✓ Authentication complete.
- gh config set -h github.com git_protocol https
✓ Configured git protocol
✓ Logged in as <your-github-username>
```

Также требуется задать электронную почту и имя пользователя для `git`:

```console
$ git config --global user.email "you@example.com"
$ git config --global user.name "Your Name"
```

> [!NOTE]
> Имя пользователя `user.name` принято указывать в формате *Имя Фамилия* на английском языке,
> однако ничего не мешает указать просто свой ник в GitHub.

## Клонирование репозитория

Чтобы начать работу с заданием, требуется *клонировать* репозиторий задания к себе на компьютер,
то есть создать локальную копию всего репозитория.

Для этого скопируйте и выполните команду клонирования, которая указана в выпадающем меню `Code` на вкладке `GitHub CLI`.

![](/images/clone-repo.png)

```console
$ gh repo clone nsu-syspro/mpt-github-classroom-tutorial-<your-github-username>
Cloning into 'mpt-github-classroom-tutorial-<your-github-username>'...
remote: Enumerating objects: 24, done.
remote: Counting objects: 100% (24/24), done.
remote: Compressing objects: 100% (17/17), done.
remote: Total 24 (delta 1), reused 4 (delta 0), pack-reused 0
Receiving objects: 100% (24/24), 5.80 KiB | 594.00 KiB/s, done.
Resolving deltas: 100% (1/1), done.
```

В результате создастся директория `mpt-github-classroom-tutorial-<your-github-username>`
с полной копией репозитория задания, в которую можно перейти с помощью

```console
$ cd `mpt-github-classroom-tutorial-<your-github-username>`
```

> При клонировании репозитория можно явно задать имя директории, в которой окажется репозиторий.
>
> Например, следующая команда склонирует репозиторий в директорию `tutorial`:
> ```console
> $ gh repo clone nsu-syspro/mpt-github-classroom-tutorial-<your-github-username> tutorial
> Cloning into 'tutorial'...
> ...
> ```

## Выполнение задания

В директории с репозиторием можно создавать произвольную структуру файлов и директорий,
необходимую для выполнения задания.

> [!CAUTION]
> Директории `.git` и `.github` содержат служебные файлы и данные для работы `git` и системы GitHub Classroom,
> которые нельзя изменять самостоятельно.

В качестве тестового задания предлагается создать директорию `solution`, внутри которой создать bash-скрипт `hello.sh`,
который выводит на экран "Hello World!".

<details>
  <summary>Пример решения</summary>

  ### Возможное решение
  Предполагается, что текущая директория - это корень репозитория.

  ```console
  $ mkdir solution
  $ cat << EOF > solution/hello.sh
  echo "Hello World!"
  EOF
  ```

  > Последняя команда `cat` использует синтаксис [Here document](https://en.wikipedia.org/wiki/Here_document#Unix_shells)
  > для записи многострочного файла и может быть вставлена в терминал полностью, включая введенный текст с `echo` и `EOF`.
  ---
</details>

Для локальной проверки можно запустить полученный скрипт с помощью команды

```console
$ bash solution/hello.sh
Hello World!
```

## Отправка решения

Для отправки решения на сервер можно выполнить следующие команды в корне репозитория:

```console
$ git add solution/hello.sh
$ git commit -m 'Update solution'
[main 9a38f67] Update solution
 1 file changed, 1 insertion(+)
 create mode 100644 solution/hello.sh
$ git push
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (4/4), 390 bytes | 390.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/nsu-syspro/mpt-github-classroom-tutorial-<your-github-name>.git
   7586242..f356f32  main -> main
```

## Проверка решения

После отправки решения на сервер, автоматически запустятся тесты проверяющие корректность решения.
Результат можно посмотреть в *пулл-реквесте* [Feedback](/../../pull/1), доступном во вкладке `Pull requests`
на странице репозитория в браузере.

> [!IMPORTANT]
> Если *пулл-реквест* [Feedback](/../../pull/1) не создался автоматически, то необходимо создать его вручную
> с помощью следуюших заклинаний:
> ```console
> $ git branch feedback $(git log --format='%h' | tail -n1) && git commit --allow-empty -m 'Feedback' && git push origin main feedback
> $ gh repo set-default $(git remote get-url origin | sed 's/^.*://' | sed 's/\.git$//') && gh pr create --base feedback --title Feedback --body ''
> ```
> 
> Второе заклинание можно выполнить без утилиты `gh` через web-интерфейс GitHub перейдя по следующей ссылке
> (и подставив там ваш ник в GitHub в двух местах):
> ```
> https://github.com/nsu-syspro/mpt-github-classroom-tutorial-<your-github-name>/compare/nsu-syspro:mpt-github-classroom-tutorial-<your-github-name>:feedback...main
> ```
> 
> Затем нужно нажать **"Create pull request"**:
> 
> ![](/images/feedback-pr.png)
>
> Затем достаточно заполнить поле **"Title"** и нажать **"Create pull request"**:
> 
> ![](/images/feedback-pr-title.png)

> Можно открыть пулл-реквест [Feedback](/../../pull/1) напрямую из терминала:
> ```console
> $ gh pr view --web
> ```

> [!CAUTION]
> Пулл-реквест [Feedback](/../../pull/1) не надо закрывать или вливать!  
> Он создан, чтобы преподаватель мог видеть все, что вы изменили.

В случае успешного прохождения тестов внизу страницы будет написано **"All checks have passed"**.

![](/images/checks-passed.png)

В противном случае будет написано **"All checks have failed"** и нажав на ссылку **"Details"** можно
увидеть более детально, какие проверки не прошли и почему.

![](/images/checks-failed.png)

Требуется исправить ошибки сначала в локальном репозитории, а затем отправить исправленное решение
на сервер, чтобы автоматические проверки перезапустились.

## Обсуждение решения

В том же пулл-реквесте [Feedback](/../../pull/1) преподаватель может просматривать все версии вашего
решения и оставлять замечания, которые необходимо будет исправить.

> [!TIP]
> Для того, чтобы попросить преподавателя проверить ваше решение, достаточно *упомянуть* его в комментарии
> к пулл-реквесту, например:
> ```
> Please review @<teacher-github-username>
> ```
