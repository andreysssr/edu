
# GIT

---

Настройка
- [`git config` - Настройка конфигурации GIT](#config)

Инициализация git репозитория
- [`git init` - Создание GIT репозитория](#init)
- [`git clone` - Клонирование GIT репозитория](#clone)

Игнорирование файлов 
- [`.gitignore` - Настройка игнорирования файлов](#ignore)
- [`git check-ignore` - Проверка игнорируемых файлов](#ignore_files)

Работа над текущими изменениями 
- [`git add` - Добавление содержимого файла в индекс](#add)
- [`git mv` - Перемещение или переименование файла, каталога или символьной ссылки](#mv)
- [`git restore` - Восстановление файлов в рабочем каталоге](#restore)
- [`git rm` - Удаление файлов из рабочего каталога и индекса](#rm)
- [`git clean`  - Удаление неотслеживаемых файлов из директории](#clean)
- [`git stash` - Убрать незакомиченные изменения в тайник](#stash)

Просмотреть состояние и историю
- [`git status` - Вывод состояния рабочего каталога](#status)
- [`git ls-files` - выводит список отслеживаемых файлов в индексе](#ls_files) 
- [`git log` - Вывод истории коммитов](#log)
- [`git show` - Вывод различных типов объектов](#show)
- [`git grep` - Вывод строк, соответствующих шаблону](#grep)
- [`git diff` - Вывод разницы между коммитами, коммитом и рабочим каталогом и т.д.](#diff)
- [`git bisect` - Выполнение двоичного поиска коммита, который вносит ошибку](#bisect)

Cоздавайте, отмечайте и корректируйте свою общую историю
- [`git branch` - Вывод списка, создание или удаление веток](#branch)
- [`git commit` - Запись изменений в репозиторий](#commit)
- [`git merge` - Объединение одной или нескольких историй разработки вместе](#merge)
- [`git rebase` - Повторное применение коммитов над верхушкой другой ветки](#rebase)
- [`git reset` - Сброс текущего состояния HEAD на указанное состояние](#reset)
- [`git revert` - Отмена коммита на предыдущий коммит](#revert)

Коллективная работа
- [`git tag` - Создание, вывод списка, удаление или проверка метки, подписанной с помощью GPG](#tag)
- [`git remote` - Добавление, удаление удалённых репозиториев](#remote)
- [`git fetch` - Загрузка объектов и ссылок из другого репозитория](#fetch)
- [`git pull` - Извлечение изменений и объединение с другим репозиторием или локальной веткой](#pull)
- [`git push` - Обновление внешних ссылок и связанных объектов](#push)

---

## Настройка

<a name="config"><h3>`git config` - Настройка конфигурации GIT</h3></a>

```bash
# установка имени и email для всех проектов
git config --global user.name "Your Name"
git config --global user.email "name@example.com"

# настройка изменений перевода строк при сохранении в репозиторий
git config --global core.autocrlf input     # для Linux/Mac
git config --global core.autocrlf true      # для Windows

# название ветки по умолчанию при инициализации репозитория - `git init`
git config --global init.defaultBranch main

# создание псевдонима - восстановление всех файлов в промежуточной области
git config --global alias.unstage "restore --staged ."

# Удаление по одному параметру
git config --unset user.name
git config --unset user.email

# Удаление всей секции [user]
git config --remove-section user

# Включить параметры –extended-regexp и -n команды grep.
git config --global grep.extendRegexp true
git config --global grep.lineNumber true     # включает номера строк в файле - где найдена строка

# Установить файл `.gitignore` для всех проектов
git config --global core.excludesFile ~/.gitignore
git config --global core.excludesFile "C:\Users\<USERNAME>\.gitignore"

# Установка `.gitattributes` глобального файла атрибутов для всех проектов
git config --global core.attributesFile ~/.gitattributes
git config --global core.attributesFile "C:\Users\<USERNAME>\.gitattributes"

# Просмотр выбранной конфигурации
git config --list --local   # local  (cat .git/config)
git config --list --global  # global (cat ~/.gitconfig)
git config --list --system  # system (cat /etc/gitconfig)

# Вывести все настройки
git config --list

# Вывести настройки и файлы где они указаны
git config --list --show-origin

# Открыть в редакторе глобальный конфиг файл
git config --global --edit
git config --global -e
```

Устанавливаем редактор по умолчанию
```
nano                          git config --global core.editor "nano -w"
Atom                          git config --global core.editor "atom --wait"
Vim                           git config --global core.editor "vim --nofork"
Visual Studio Code            git config --global core.editor "code --wait"

------------------------------
Windows - [Program Files] или [Program Files (x86)]

Notepad (Windows 64-bit)      git config core.editor notepad
Notepad++ (Windows 64-bit)    git config --global core.editor "'C:\Program Files\Notepad\notepad.exe' -multiInst -notabbar -nosession -noPlugin"
Gvim (Windows 64-bit)         git config --global core.editor "'C:\Program Files\Vim\vim72\gvim.exe' --nofork '%*'" 
Sublime Text (Windows 64-bit) git config --global core.editor "'C:\Program Files\Sublime Text 3\sublime_text.exe' -w" 
Textpad (Windows 64-bit)      git config --global core.editor "'C:\Program Files\TextPad 5\TextPad.exe' -m" 
WordPad                       git config --global core.editor "'C:\Program Files\Windows NT\Accessories\wordpad.exe'"

Notepad++ (Windows 32-bit)    git config --global core.editor "'C:/Program Files (x86)/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"
Sublime Text (Windows 32-bit) git config --global core.editor "'C:/Program Files (x86)/sublime text 3/subl.exe' -w"
------------------------------
Linux - Ubuntu

Gedit (Linux)                 git config --global core.editor "gedit --wait --new-window"
Scratch (Linux)               git config --global core.editor "scratch-text-editor"
Kate (Linux)                  git config --global core.editor "kate"

------------------------------
macOS

BBEdit (Mac, with command line tools) git config --global core.editor "bbedit -w"
TextEdit (macOS)              git config --global --add core.editor "open -W -n"
Sublime Text (macOS)          git config --global core.editor "/Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl --new-window --wait"
```

---
## Инициализация `git` репозитория

<a name="init"><h3>`git init` - Создание GIT репозитория</h3></a>

```bash
# инициализация git репозитория
git init # создаёт в директории подкаталог .git 
```

---

<a name="clone"><h3>`git clone` - Клонирование GIT репозитория</h3></a>

```bash
# клонирование git репозитория
git clone https://github.com/andreysssr/andreysssr

git clone <url>
git clone <url> dir_name # клонировать проект в диеркторию dir_name
git clone <url> .        # клонировать проект в текущую директорию

git clone ~/old ~/new

git clone git://...
git clone ssh://...
git clone https://...
```

---
## Игнорирование файлов

<a name="ignore"><h3>`.gitignore` - Настройка игнорирования файлов</h3></a>

`.gitignore` - правила

```
Вы можете добавить к шаблону двойную звездочку, чтобы он соответствовал каталогам в любом месте репозитория.
**/logs           #  logs/debug.log, logs/monday/foo.bar, build/logs/debug.log

двойную звездочку для сопоставления файлов по их имени и имени их родительского каталога.
**/logs/debug.log # logs/debug.log, build/logs/debug.log, !! logs/build/debug.log

Звездочка — это подстановочный знак, который соответствует нулю или более символам.
*.log             # debug.log, foo.log, .log, logs/debug.log

Добавление восклицательного знака к шаблону отменяет его.
*.log
!important.log    # debug.log !! logs/important.log

Добавление косой черты соответствует файлам только в корне репозитория.
/debug.log        # debug.log !! logs/debug.log
debug.log         # debug.log, logs/debug.log

Знак вопроса соответствует ровно одному символу.
debug?.log        # debug0.log, debugg.log !! debug10.log

Квадратные скобки также можно использовать для сопоставления одного символа из указанного диапазона.
debug[0-9].log    # debug0.log, debug1.log !! debug10.log

Квадратные скобки соответствуют одному символу из указанного набора.
debug[01].log     # debug0.log, debug1.log !! debug2.log, debug01.log

Восклицательный знак может использоваться для соответствия любому символу, кроме одного из указанного набора.
debug[!01].log    # debug2.log !! debug0.log, debug1.log, debug01.log

Диапазоны могут быть числовыми или буквенными.
debug[a-z].log    # debuga.log, debugb.log !! debug1.log

Если вы не добавите косую черту, шаблон будет соответствовать как файлам, так и содержимому каталогов с этим именем. В примере слева игнорируются как каталоги, так и файлы с именем logs .
logs              # logs, logs/debug.log, logs/latest/foo.bar, build/logs, build/logs/debug.log

Добавление косой черты указывает, что шаблон является каталогом. Все содержимое любого каталога в репозитории, соответствующего этому имени, включая все его файлы и подкаталоги, будет игнорироваться.
logs/             # logs/debug.log, logs/latest/foo.bar, build/logs/foo.bar, build/logs/latest/debug.log

Двойная звездочка соответствует нулю или более каталогам.
logs/**/debug.log # logs/debug.log, logs/monday/debug.log, logs/monday/pm/debug.log

Шаблоны, определяющие файл в определенном каталоге, относятся к корню репозитория. 
logs/debug.log    # logs/debug.log !! debug.log, build/logs/debug.log

В именах каталогов также можно использовать подстановочные знаки.
logs/*day/debug.log # logs/monday/debug.log, logs/tuesday/debug.log !! logs/latest/debug.log

---
# text comment
name              # /name.log, /name/file.txt, /lib/name.log
name/             # /name/file.txt, /name/log/name.log !! /name.log
name.file         # /name.file, /lib/name.file
/name.file        # /name.file, !! /lib/name.file
lib/name.file     # /lib/name.file <=> name.file, /test/lib/name.file
**/lib/name.file  # /lib/name.file, /test/lib/name.file
**/name           # /name/log.file, /lib/name/log.file, /name/lib/log.file

/lib/**/name      # /lib/name/log.file, /lib/test/name/log.file, /lib/test/ver1/name/log.file !! /name/log.file
*.file            # /name.file, /lib/name.file
*name/            # /lastname/log.file, /firstname/log.file
name?.file        # /names.file, /name1.file !! /names1.file
name[a-z].file    # /names.file, /nameb.file !! /name1.file
name[abc].file    # /namea.file, /nameb.file !! /names.file
name[!abc].file   # /names.file, /namex.file !! /namesb.file
*.file            # /name.file, /lib/name.file
debug[!01].log    # debug2.log !! debug0.log, debug1.log, debug01.log
  
---
name/
!name/secret.log  # /name/file.txt, /name/log/name.log !! /name/secret.log
---
*.file
!name.file        # /log.file, /lastname.file !! /name.file
---
*.file
!name/*.file
junk.*            # /log.file, /name/log.file !! /name/junk.file
```
---
- Пустые строки игнорируются
- `# text comment` - Строки, начинающиеся с #, игнорируются.
---
- `name` -	Все файлы `name`, папки `name`, а также файлы и папки в любой папке `name`.
  - Совпадает:
    - `/name.log`
    - `/name/file.txt`
    - `/lib/name.log`
---
- `name/` -	Окончание на `/` указывает, что шаблон предназначен для папки. Соответствует всем файлам и папкам в папке `name` - с любым именем.	
  - Совпадает:
    - `/name/file.txt`
    - `/name/log/name.log`
  - Не совпадает:
    - `/name.log`
---
- `name.file` - Все файлы с `name.file`	
  - Совпадает:
    - `/name.file`
    - `/lib/name.file`
---
- `/name.file` - Начиная с `/` указывает, что шаблон соответствует только файлам в корневой папке.
  - Совпадает:
    - `/name.file`
  - Не совпадает:
    - `/lib/name.file`
---
- `lib/name.file` - Шаблоны, определяющие файлы в определенных папках, всегда относятся к корню (даже если вы не начинаете с `/` )	
  - Совпадает:
    - `/lib/name.file`
  - Не совпадает:
    - `name.file`
    - `/test/lib/name.file`
---
- `**/lib/name.file` - Начало с `**` перед `/` указывает, что оно соответствует любой папке в репозитории. Не только в корне.	
    - Совпадает:
      - `/lib/name.file`
      - `/test/lib/name.file`
---
- `**/name` - Все папки `name`, а также файлы и папки в любой папке `name`.	
  - Совпадает:
      - `/name/log.file`
      - `/lib/name/log.file`
      - `/name/lib/log.file`
---
- `/lib/**/name` - Все папки `name`, а также файлы и папки в любой папке `name` внутри папки lib.	
  - Совпадает:
    - `/lib/name/log.file`
    - `/lib/test/name/log.file`
    - `/lib/test/ver1/name/log.file`
  - Не совпадает:
    - `/name/log.file`
---
- `*.file` - Все файлы с расширением `.file`	
  - Совпадает:
    - `/name.file`
    - `/lib/name.file`
---
- `*name/` - Все папки, заканчивающиеся на `name`	
  - Совпадает:
    - `/lastname/log.file`
    - `/firstname/log.file`
---
- `name?.file` - `?` соответствует одному неспецифическому символу	
  - Совпадает:
    - `/names.file`
    - `/name1.file`
  - Не совпадает:
    - `/names1.file`
---
- `name[a-z].file` - `[диапазон]` соответствует одному символу в указанном диапазоне (в данном случае символу в диапазоне от a до z, который также может быть числовым).
  - Совпадает:
    - `/names.file`
    - `/nameb.file`
  - Не совпадает:
    - `/name1.file`
---
- `name[abc].file` - `[set]` соответствует одному символу из указанного набора символов (в данном случае `a`, `b` или `c`)	
  - Совпадает:
    - `/namea.file`
    - `/nameb.file`
  - Не совпадает:
    - `/names.file`
---
- `name[!abc].file` - `[!set]` соответствует одному символу, кроме тех, которые указаны в наборе символов (в данном случае `a`, `b` или `c`)
  - Совпадает:
    - `/names.file`
    - `/namex.file`
  - Не совпадает:
    - `/namesb.file`
---
- `*.file` - Все файлы с расширением `.file`	
  - Совпадает:
    - `/name.file`
    - `/lib/name.file`
---
- `name/` 
- `!name/secret.log` - `!` указывает отрицание или исключение. Соответствует всем файлам и папкам в любой папке `name`, кроме `name/secret.log`	
  - Совпадает:
    - `/name/file.txt`
    - `/name/log/name.log`
  - Не совпадает:
    - `/name/secret.log`
---
- `*.file`
- `!name.file` - `!` указывает отрицание или исключение. Все файлы с расширением `.file`, кроме `name.file`.	
  - Совпадает:
    - `/log.file`
    - `/lastname.file`
  - Не совпадает:
    - `/name.file`
---
- `*.file`
- `!name/*.file`
- `junk.*` - Добавление новых шаблонов после отрицания приведет к повторному игнорированию предыдущего отрицаемого файла. Все файлы с расширением `.file`, кроме файлов в папке с `name`. Если только имя файла не `junk.file`
  - Совпадает:
    - `/log.file`
    - `/name/log.file`
  - Не совпадает:
    - `/name/junk.file`
---

<a name="ignore_files"><h3>`git check-ignore` - Проверка игнорирования пути / файла</h3></a>

Проверить игнорирование пути `install/sometthing`
```bash
git check-ignore -v "install/sometthing"
```

Проверить игнорирование пути `.idea`
```bash
git check-ignore -v ".idea" # проверить игнорируется ли директория .idea
git check-ignore -v *
git check-ignore -vn *      # Можно выводить и папки/файлы, к которым правила игнорирования не применяются
git check-ignore -vn .*     # скрытые файлы и папки (в linux),
```
---

## Работа над текущими изменениями

<a name="add"><h3>`git add` - Добавление содержимого файла в индекс</h3></a>

```bash

git add .               # добавить все файлы в текущей папке - новые, изменённые, удалённые файлы из текущей директории и её поддиректорий
git add file1           # добавить в индекс указанный файл (был изменён, был удалён или это новый файл)
git add file1 file2     # добавить файлы file1 и file2
git add -n .            # показать какие файлы будут добавлены (не добавляя их на самом деле)
git add -i              # запустить интерактивную оболочку для добавления в индекс только выбранных файлов
git add -p              # показать новые/изменённые файлы по очереди с указанием их изменений и вопросом об отслеживании/индексировании
git add -p file1        # интерактивно выбирайте части (куски) файла для подготовки.
git add *.php           # добавить все файлы в текущей папке с расширением .php
git add "*.php"         # добавить все файлы в проекте с расширением .php
git add someDir/*.php	# добавить все файлы в папке someDir с расширением .php
git add someDir/        # добавить все файлы в папке someDir
git add --force file1   # добавить файл в индекс принудительно не обращая внимания на его игнорирование в файле .gitignore
git add -f file1        # то же самое что и (git add --force file1) 
```

<a name="mv"><h3>`git mv` - Перемещение или переименование файла, каталога или символьной ссылки</h3></a>

```bash
git mv <old_file> <new_file> # Переместить или переименовать файл
git mv text.txt test_new.txt # переименовать файл «text.txt» в «test_new.txt» и проиндексировать это изменение
git mv readme_new.md folder/ # переместить файл readme_new.md в директорию folder/ (должна существовать) и проиндексировать это изменение
```

<a name="restore"><h3>`git restore` - Восстановление файлов в рабочем каталоге</h3></a>

```bash
git restore --staged file.js           # Удаление файла из промежуточной области
git restore --staged file1.js file2.js # Удаление файлов из file1.js file2.js промежуточной области
git restore --staged .                 # Удаление всех файлов из промежуточной области
git restore --staged *                 # Удаление всех файлов из промежуточной области
git restore --staged *.js              # Удаление всех файлов .js из промежуточной области

git restore file1.js                   # Отменить изменения в рабочем каталоге
git restore file1.js file2.js          # Отменить изменения в рабочем каталоге
git restore *.js                       # Отменить изменения в рабочем каталоге
git restore .                          # Отменить изменения в рабочем каталоге
git restore --source=HEAD~1 file1.js   # Восстановить файл file1.js из предыдущей фиксации
git restore --source=feature/send-email toc.txt # Восстановить файл toc.txt из другой ветки feature/send-email
git restore --source=19defe58 toc.txt           # Восстановить файл toc.txt из коммита 19defe58
```

<a name="rm"><h3>`git rm` - Удаление файлов из рабочего каталога и индекса</h3></a>

```bash
git rm text.txt             # удалить файл из промежуточной области и директории
git rm -f text.txt          # удалить файл из индекса и из директории
git rm -r log/              # удалить всё содержимое отслеживаемой директории log/ и проиндексировать это изменение
git rm ind*                 # удалить все отслеживаемые файлы с именем, начинающимся на «ind» в текущей директории и проиндексировать это изменение
git rm --cached readme.txt  # удалить из промежуточной области файл (ФАЙЛ ОСТАНЕТСЯ НА МЕСТЕ) 
git rm --cached -r bin/     # удалить из промежуточной области рекурсивно содержимое директории bin
                            # (часто используется для нечаянно добавленных в отслеживаемые файлов)
```

<a name="clean"><h3>`git clean` - Удаление неотслеживаемых файлов из директории</h3></a>

```bash
git clean            # удалить неотслеживаемые файлы из текущей директории
git clean bin/       # удалить неотслеживаемые файлы из директории bin
git clean -n         # показать файлы которые будут удалены (не удаляя их)
git clean -f         # удалить файлы которые выводил командой (git clean -n)
git clean -n -d      # показать директории и файлы которые будут удалены (не удаляя их)
git clean -df        # удалить неотслеживаемые файлы и директории
git clean -i         # интерактивная удаление файлов
git clean -x         # также удалить игнорируемые файлы
git clean -X         # удалить только игнорируемые файлы
git clean -e *.txt   # удалить неотслеживаемые файлы c расширением txt
```

<a name="stash"><h3>`git stash` - Убрать незакомиченные изменения в тайник</h3></a>

```bash
git stash                           # положить во временное хранилище все отслеживаемые файлы.
git stash save -u                   # Сохранять изменения в рабочем дереве, включая неотслеживаемые файлы.
git stash push --all                # добавить в тайник все файлы (отслеживаемые и не отслеживаемые)
git stash push -am "My new stash."  # добавить в тайник все файлы с описанием
git stash push -m "New tax rules."  # добавить в тайник все отслеживаемые файлы с описанием
git stash push -u -m "message"      # добавить в тайник все отслеживаемые и не отслеживаемые файлы с описанием
git stash list                      # Вывести список всех тайников
git stash show stash@{1}            # Показывает данный тайник
git stash show 1                    # ярлык для stash@{1}
git stash pop                       # восстановить последние файлы, положенные во временное хранилище и удалить из stash эти данные
git stash pop 3                     # восстановить файлы под номером 3 и удалить эти файлы
git stash apply 1                   # применить изменения из хранилища под индексом 1 к рабочему каталогу
git stash apply 3                   # восстановить файлы под номером 3 и не удалять эти файлы
git stash drop                      # удалить элемент под номером (0)
git stash drop 0                    # Удалить тайник 0
git stash drop 1                    # Удалить тайник 1
git stash drop 2                    # удалить элемент под номером (2), если такого элемента нет - выведет сообщение об ошибке
git stash clear                     # Удалить все тайники
```

Пример

```bash
git stash push -m "text 1" 
git stash push -m "text 2" 
git stash push -m "text 3"

git stash list
# stash@{0}: On main: text 3
# stash@{1}: On main: text 2
# stash@{2}: On main: text 1

git stash pop 1               # возвращает изменения (text 2) находятся под индексом (1)

git stash list
# stash@{0}: On main: text 3
# stash@{1}: On main: text 1  # индексация сохранённых данных в кармане сдвинулась

git stash apply 0

git stash list
# stash@{0}: On main: text 3
# stash@{1}: On main: text 1

git stash pop 1

git stash list
# stash@{0}: On main: text 3
```

---

## Просмотреть состояние и историю

<a name="status"><h3>`git status` - Вывод состояния рабочего каталога</h3></a>

```bash
git status           # вывести состояние репозитория
git status -s        # вывести коротко состояние репозитория
git status -sb       # вывести название текущей ветки
git status -u        # вывести неотслеживаемые файлы
git status -su       # вывести коротко неотслеживаемые файлы
git status --ignored # вывести список игнорируемых файлов
```

<a name="ls-files"><h3>`git ls-files` - выводит список отслеживаемых файлов в индексе</h3></a>

```bash
git ls-files         # выводит список отслеживаемых файлов
git ls-files --eol   # показывать окончания строк файлов
git ls-files -o      # показать другие файлы
git ls-files -i      # показывать игнорируемые файлы
git ls-files -t      # определить статус файла с помощью тегов
```

<a name="log"><h3>`git log` - Вывод истории коммитов</h3></a>

```bash
git log                         # просмотр истории коммитов
git log master                  # показать коммиты в указанной ветке
git log -2                      # показать последние 2 коммита в активной ветке
git log -2 --stat               # показать последние 2 коммита и статистику внесенных ими изменений
git log -p -22                  # показать последние 22 коммита и внесенную ими разницу на уровне строк
git log --graph -10             # показать последние 10 коммитов с ASCII-представлением ветвления
git log --since=2.weeks         # показать коммиты за последние 2 недели
git log --after '2018-06-30'    # показать коммиты, сделанные после указанной даты
git log index.html              # показать историю изменений файла index.html (только коммиты)
git log -5 index.html           # показать историю изменений файла index.html, последние 5 коммитов (только коммиты)
git log -p index.html           # показать историю изменений файла index.html (коммиты и изменения)
git log -G'myFunction' -p       # показать все коммиты, в которых менялись строки с myFunction (в кавычках регулярное выражение)
git log -L '/<head>/','/<\/head>/':index.html # показать изменения от указанного до указанного регулярных выражений в указанном файле
git log toc.txt                 # все коммиты которые изменили содержимое файла
git log -- toc.txt              # если git не может понять что это файл - его отделяют двумя дефисами
git log --follow file           # Отображает историю фиксации файла, включая его переименования.

git log --grep fix              # показать коммиты, в описании которых есть буквосочетание fix (регистрозависимо, только коммиты текущей ветки)
git log --grep fix -i           # показать коммиты, в описании которых есть буквосочетание fix (регистроНЕзависимо, только коммиты текущей ветки)
git log --grep 'fix(ing|me)' -P # показать коммиты, в описании которых есть совпадения для регулярного выражения (только коммиты текущей ветки)
git log --grep="GUI"            # коммиты в сообщение которых есть слово "GUI" (операция чувствительна к регистру)
git log --grep="<text>"         # Найти текст в сообщениях о фиксации (полезно для поиска конкретных изменений)

git log --pretty=format:"%h - %an, %ar : %s" -4                    # показать последние 4 коммита с форматированием выводимых данных
git log --pretty=format:"%h %ad | %s%d [%an]" --graph --date=short # мой формат вывода, висящий на алиасе оболочки
git log --pretty=format:"hello"
git log --pretty=format:"hello %an"
git log --pretty=format:"%an committed %H"
git log --pretty=format:"%an committed %h"
git log --pretty=format:"%an committed %h on %cd"
git log --pretty=format:"%Cgreen%an committed %h on %cd"
git log --pretty=format:"%Cgreen%an%Creset committed %h on %cd"
git log --pretty=format:"%Cred%an%Creset committed %h on %cd"
git log --pretty=format:"%Cblue%an%Creset committed %h on %cd"

git log fb0d184..edb3594        # просмотр диапазона коммитов, первый - более старый, второй - новый коммит
git log master..branch_99       # показать коммиты из ветки branch_99, которые не влиты в master
git log branch_99..master       # показать коммиты из ветки master, которые не влиты в branch_99
git log master...branch_99 --boundary -- graph # показать коммиты из указанных веток, начиная с их расхождения (коммит расхождения будет показан)
git log master..bugfix/signup-form             # Вывести коммиты которые находятся в ветке bugfix/signup-form и не находятся в ветке master

git log --oneline               # просмотр коммитов в 1 строку
git log --all                   # показать все коммиты
git log --graph                 # показать коммиты с включением псевдографики
git log --reverse               # Просмотр коммитов в 1 строку в обратном порядке

git log --stat                  # просмотр статистики по исправлениями
git log --stat -3               # просмотр информации по 3 последним коммитам
git log --stat toc.txt          # вывести статистику изменений файла
git log --stat                  # Показывает список измененных файлов
git log --stat file.txt         # Показывает статистику (количество изменений) для файла file.txt
git log --patch file.txt        # Показывает исправления (изменения), примененные к файлу file.txt
git log --patch                 # просмотр исправлений в файлах
git log --patch -- toc.txt      # просмотреть все изменения связанные с файлом 
git log --patch -1 -- toc.txt   # количество коммитов для вывода 1 
git log --patch -2 -- toc.txt   # количество коммитов для вывода 2
git log --patch -3              # количество коммитов для вывода 3.
git log --patch toc.txt         # вывести фактические изменения в файле
git log --author="Mosh"         # фильтрация по автору
git log --before="2020-08-17"   # Фильтрация по дате до "2020-08-17"
git log --after="2020-08-17"    # Фильтрация по дате после "2020-08-17"
git log --after="yesterday"     # yesterday - вчерашние
git log --after="one week ago"  # one week ago - недельной давности

git log --since=<date>          # Показать историю коммитов с определенной даты
git log --until=<date>          # Показать историю коммитов до определенной даты

# Фильтрация по содержимому
git log -S"hello()"             # все коммиты в которых добавили строку - hello()
git log -S"OBJECTIVES"          # все коммиты в которых добавили строку - OBJECTIVES
git log -S"OBJECTIVES" --patch 
```

<a name="show"><h3>`git show` - Вывод различных типов объектов</h3></a>

```bash
git show                   # покажет информацию по коммиту на котором находится указатель HEAD
git show 60d6582           # показать изменения из коммита с указанным хешем
git show HEAD              # Показывает последний коммит
git show HEAD~             # показать данные о предыдущем коммите в активной ветке
git show @~                # аналогично предыдущему - HEAD~
git show HEAD~2            # Два шага до последнего коммита
git show HEAD~3            # показать данные о коммите, который был 3 коммита назад
git show master~2          # показать данные о коммите, который был 2 коммита назад в указанной ветке
git show @~:index.html     # показать контент указанного файла на момент предыдущего (от HEAD) коммита
git show :/"подвал"        # показать самый новый коммит, в описании которого есть указанное слово (из любой ветки)
git show v1.0              # тег
git show HEAD~1:.gitignore # Для просмотра только внесённых данных 
git show HEAD:file.js      # Показывает версию file.js, сохраненную в последнем коммите.
git show HEAD~2:file1.txt  # Показывает версию файла, который был 2 коммита назад

# увидеть окончательные изменения в файле
git show HEAD~2:sections/creating-snapshots/staging-changes.txt 

# увидеть файлы которые были добавлены, изменены или удалены в этом коммите
git show HEAD~2 --name-only
git show HEAD~2 --name-only --oneline

# увидеть файлы которые были добавлены, изменены или удалены в этом коммите с указанием действия (добавлен, изменен, удалён)
git show HEAD~2 --name-status

# увидеть окончательные изменения в файле
git show HEAD~2:sections/creating-snapshots/staging-changes.txt 
```

<a name="grep"><h3>`git grep` - Вывод строк, соответствующих шаблону</h3></a>

```
Синтаксис команды grep

git grep <опции> "шаблон" <идентификатор-фиксации> <имя-файла>

git grep <options> "pattern" <commit-id> <file-name>
git grep [<options>] [-e] <pattern> [<rev>...] [[--] <path>...]
```

- `<options>`: этот аргумент является необязательным и может использоваться для изменения поведения команды grep.
- `pattern`: это шаблон, который мы хотим найти в зафиксированном коде.
- `<commit-id>`: этот аргумент является необязательным и может использоваться для поиска шаблона по определенному коммиту.
- `<file-name>`: этот аргумент является необязательным и может использоваться для поиска шаблона в конкретном файле.

```bash
git grep 'conf*'                     # Поиск слова "conf" вначале слова - в файлах, отслеживаемых Git. 
                                     # По умолчанию grep выполняет поиск учетом регистра
git grep -i hello                    # регистронезависимый поиск слова "hello"
git grep -o hello                    # отображать только совпадающую часть строки
git grep -c hello                    # отображать только количество строк, соответствующих шаблону поиска 
git grep -m 5 hello                  # максимальное количество результатов на файл - 5 строк
git grep --cached hello              # поиск в индексе, а не в рабочем дереве
git grep --untracked hello           # поиск как в отслеживаемых, так и в неотслеживаемых файлах
git grep 'time_t' -- '*.[ch]'        # Ищет time_t во всех отслеживаемых файлах .c и .h в рабочем каталоге и его подкаталогах.
git grep solution -- :^Documentation # Ищет решение, исключая файлы в документации.
git grep -e '#define' --and \( -e MAX_PATH -e PATH_MAX \) # Ищет строку, содержащую #define и (MAX_PATH или PATH_MAX).
git grep -E 'Книга*|автор'          # Файлы, содержащие слово «Книга» или «автор» с количеством найденых совпадений в файле
git grep --all-match -e NODE -e Unexpected                # Ищет строку с (NODE или Unexpected) в файлах, в которых есть строки, соответствующие обоим.
git grep -n second                   # Выводит в результате поиска номер строки - где встретилось слово "second" - file1:2:a second line
                                     # для вывода номера строки по умолчанию - "git config --global grep.lineNumber true"

git grep --break hello               # используется для печати пустой строки между совпадениями из разных файлов.
git grep --full-name hello           # используется для указания путей к выходным данным относительно верхнего каталога проекта.
git grep hello HEAD~1                # Искать строку "hello" в предыдущем коммите
git grep hello HEAD~2                # Искать строку "hello" во 2 коммите от теущего

git grep foo feature                 # Поиск строки "foo" в ветке "feature"

# Поиск по нескольким коммитам
git grep hello HEAD HEAD~1 feature   # Поиск строки "hello" в текущем коммите, в предыдущем коммите, и коммите на который указывет ветка "feature"
```

<a name="diff"><h3>`git diff` - Вывод разницы между коммитами, коммитом и рабочим каталогом и т.д.</h3></a>

```bash
git diff                             # Показывает изменения между рабочим каталогом и промежуточной областью (индексом).
git diff HEAD                        # Отображение разницы между текущим каталогом и последней фиксацией
git diff index.html                  # сравнить файл из рабочей директории и индекс
git diff --color-words               # сравнить рабочую директорию и индекс, показать отличия в словах (неотслеживаемые файлы ИГНОРИРУЮТСЯ)
git diff --staged                    # Отображает изменения между промежуточной областью (индексом) и последней фиксацией.
git diff --cached                    # Отображает изменения между промежуточной областью (индексом) и последней фиксацией.
git diff --name-only master feature  # посмотреть что сделано в ветке feature по сравнению с веткой master, показать только имена файлов
git diff --stat                      # Быстрый просмотр изменений в рабочем каталоге с момента последней фиксации.
git diff master feature              # посмотреть что сделано в ветке feature по сравнению с веткой master
git diff master...feature            # посмотреть что сделано в ветке feature с момента (коммита) расхождения с master
git diff 60d6582 ca49180             # Отображает различия между двумя коммитами.
git diff HEAD~2 HEAD                 # посмотреть что изменилось в последних 3 комитах
git diff HEAD~2 HEAD audience.txt    # посмотреть что изменилось в последних 3 комитах в файле audience.txt

git diff HEAD~2 HEAD --name-status   # список файлов со статусами (М - модификация, А - добавление)
git diff HEAD~2 HEAD --name-only     # список файлов с именами

git diff --name-only bugfix/signup-form    # имя файлов в которых затронуты изменения
git diff --name-status bugfix/signup-form  # статистика файлов в которых затронуты изменения
```

<a name="bisect"><h3>`git bisect` - Выполнение двоичного поиска коммита, который вносит ошибку</h3></a>

```bash
# Процесс поиска ошибки в коммитах
# начало поиска ошибки
git bisect start

# указываем git что текущий коммит плохой
git bisect bad 

# указать идентификатор хорошего коммита
git bisect good ca49180

# запускаем приложение или проводим тесты
# если ошибка существует - значит она была в первой половине истории
# если коммит хороший - значит ошибка была внесена позже
# сообщаем git о фиксации (good - хорошая или bad - плохая)
git bisect good

# проводим тесты если они хорошие сообщаем об этом
git bisect good

# проводим тесты если они плохие сообщаем об этом
git bisect bad

# проводим тесты если они хорошие сообщаем об этом
git bisect good

# проводим тесты если они плохие сообщаем об этом
git bisect bad

# после найденного комита останавливаем поиск
git bisect reset
```

---

## Создавайте, отмечайте и корректируйте свою общую историю

<a name="branch"><h3>`git branch` - Вывод списка, создание или удаление веток</h3></a>

```bash
# Показать
git branch                       # показать список веток
git branch -v                    # показать список веток и последний коммит в каждой
git branch -vv                   # показывает как расходятся наши локальные и удалённые ветви отслеживания
git branch -r                    # показать удаленные ветки
git branch -a                    # показать все ветки(локальные и удаленные) 
git branch --merged              # показать ветки, уже слитые с активной
git branch --no-merged           # показать ветки, не слитые с активной
git branch -av                   # показать все локальные и удалённые ветки
git branch -avv                  # показать все ветки и связи локальных с удаленными ветками
git branch -r --merged           # Список всех удаленных веток, которые были объединены в текущую ветку.
git branch -r --no-merged        # Список всех удаленных веток, еще не объединенных в текущую ветку.
git branch -rvva                 # список всех удаленных веток, связанные удалённые и локальные ветки

# Создать
git branch new_branch            # создать новую ветку с указанным именем на текущем коммите
git branch new_branch 071f3bd    # создать новую ветку с указанным именем на указанном коммите

# Создать и перейти на ветку
git switch -C bugfix/login-form  # создадим ветку и переключимся на неё
git checkout -b new_branch       # создать новую ветку с указанным именем и перейти в неё
git checkout -b <branch_name> <remote_name>/<remote_branch> # Создайте новую ветку на основе удаленной ветки.

# Перейти 
git checkout new_branch          # перейти в указанную ветку
git switch bugfix                # перейти на ветку bugfix

# Переименовать
git branch -m new_branch_name    # переименовать локально ТЕКУЩУЮ ветку в new_branch_name
git branch -M main               # переименовать текущую ветку в main
git branch -m dev fix            # переименовать локально ветку - dev в ветку - fix
git branch -m old_name new_name  # переименовать локально ветку old_name в new_name
git branch -m new_name           # переименовать локально ТЕКУЩУЮ ветку в new_branch_name
git push origin :old_branch_name new_branch_name # применить переименование в удаленном репозитории

# Переместить
git checkout -B master 071f3bd   # переместить ветку с указанным именем на указанный коммит и перейти в неё
git branch -f master 071f3bd     # переместить ветку master на указанный коммит
git branch -f master master~2    # переместить ветку master на 2 коммита назад
git branch -f dev 071f3bd        # переместить ветку dev на указанный коммит
git branch -f dev dev~2          # переместить ветку dev на 2 коммита назад

# Установить удалённую ветку
# Отслеживайте удаленную ветку и настройте автоматическую синхронизацию локальной ветки с ней.
git branch --track <branch_name> <remote_name>/<remote_branch>

# Привязать удалённую ветку в удалённом репозитории с текущей веткой
git branch -u <remote_name>/<remote_branch> # установить ветку как отслеживаемую
git branch -u origin/main main              # установить ветку как отслеживаемую

# Удалить
git branch --unset-upstream <branch_name>   # Удалите связь отслеживания между локальной и удаленной веткой.
git branch -d <branch-name>	     # Удаляет указанную ветку.
git branch -d bugfix/signup-form # Удаление ветки (используется, если её изменения уже влиты в главную ветку)
git branch -D bugfix/signup-form # Принудительное удаление ветки (если изменения ещё не влиты в главную ветку)

# Восстановить удалённую ветку
git branch fix 071f3bd           # восстановить удалённую ветку 

# Создать локальную ветку в нашем репозитории которая сопоставляется с удалённой веткой отслеживания
git switch -C feature/change-password origin/feature/change-password 
```

<a name="commit"><h3>`git commit` - Запись изменений в репозиторий</h3></a>

```bash
git commit -m "Name of commit"     # зафиксировать в коммите проиндексированные изменения (закоммитить), добавить сообщение
git commit -a -m "Name of commit"  # проиндексировать отслеживаемые файлы (ТОЛЬКО отслеживаемые, но НЕ новые файлы) и закоммитить, добавить сообщение
git commit -am "Name of commit"    # проиндексировать отслеживаемые файлы (ТОЛЬКО отслеживаемые, но НЕ новые файлы) и закоммитить, добавить сообщение

# Все команды, приведённые ниже можно выполнять ТОЛЬКО если коммиты еще не были отправлены в удалённый репозиторий.
git commit --amend                 # изменить последний коммит и оставить сообщение последнего коммита
git commit --amend -m "New message commit"  # Изменить последний коммит и указать другое сообщение
```

<a name="merge"><h3>`git merge` - Объединение одной или нескольких историй разработки вместе</h3></a>

```bash
git checkout -B master 5589877          # переместить ветку с указанным именем на указанный коммит и перейти в неё
git merge hotfix                        # влить в ветку, в которой находимся, данные из ветки hotfix
git merge hotfix -m "Горячая правка"    # влить в ветку, в которой находимся, данные из ветки hotfix (указано сообщение коммита слияния)
git merge hotfix --log                  # влить в ветку, в которой находимся, данные из ветки hotfix, показать редактор описания коммита, добавить в него сообщения вливаемых коммитов
git merge --no-ff bugfix                # Создает фиксацию слияния без fast-forward, даже если возможна быстрая перемотка.
git merge hotfix --no-ff                # влить в ветку, в которой находимся, данные из ветки hotfix, запретить простой сдвиг указателя, изменения из hotfix
                                        # «останутся» в ней, а в активной ветке появится только коммит слияния

git merge feature/change-password       # влить в активную ветку изменения из ветки feature
git merge bugfix/change-password        # влить в активную ветку изменения из ветки feature
git merge feature                       # влить в активную ветку изменения из ветки feature
git merge origin/master                 # произвести слияние удалённого и локального репозитория
git merge origin/main                   # выполнить слияние удалённой ветки с нашей
git merge upstream/master               # вливаем стянутую ветку master удалённого репозитория upstream в свою ветку master

git merge --squash bugfix/photo-upload  # Выполняет сквош-слияние. Cоздает один коммит вместо слияния
git merge --abort                       # Прерывает слияние

git merge-base master feature           # показать хеш последнего общего коммита для двух указанных веток
git merge --no-commit --no-ff <branch_name> # Выполните пробный прогон слияния без фактического объединения ветвей.
```

<a name="rebase"><h3>`git rebase` - Повторное применение коммитов над верхушкой другой ветки</h3></a>

```bash
git rebase master                # перебазировать ветку по ветке master
git rebase --onto master feature # перенести коммиты активной ветки на master, начиная с того места, в котором активная ветка отделилась от ветки feature
git rebase --abort               # прервать конфликтный rebase, вернуть рабочую директорию и индекс к состоянию до начала rebase
git rebase --continue            # продолжить конфликтный rebase (сработает только после разрешения конфликта и индексации такого разрешения)

# Отменить текущую операцию перебазирования
git rebase --abort

# Интерактивное перебазирование для:
# - редактирования, 
# - объединения, 
# - изменения порядка, 
# - удаления коммитов.
git rebase -i

# Перебазировать коммиты из текущей ветки в удаленную ветку в интерактивном режиме.
git rebase -i <remote_name>/<remote_branch>

git rebase -i master
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit

```

<a name="reset"><h3>`git reset` - Сброс текущего состояния HEAD на указанное состояние</h3></a>

```bash
git reset --hard <commit>    # Перемещает указатель ветки на указанную коммит, отбрасывая все изменения в промежуточной области и рабочем каталоге.
git reset --mixed <commit>   # Перемещает указатель ветки на указанный коммит, отбрасывая все изменения в промежуточной области, сохраняя изменения в рабочем каталоге.
git reset --soft <commit>    # Перемещает указатель ветки на указанную коммит, сохраняя изменения в промежуточной области и рабочем каталоге.

# Если <commit> не указан - берётся текущий хеш указателя HEAD
# Если не указан модификатор hard, mixed, soft - по умолчанию используется модификатор mixed

git reset --hard             # наши изменения исчезнут и мы получим чистый каталог 
git reset --hard HEAD        # наши изменения исчезнут и мы получим чистый каталог 
git reset --hard feature@{1} # переместить указатель ветки feature на один коммит назад, обновить рабочую директорию и индекс
git reset --hard @~          # передвинуть HEAD (и ветку) на предыдущий коммит, рабочую директорию и индекс сделать такими, какими они были в момент предыдущего коммита
git reset --hard 75e2d51     # передвинуть HEAD (и ветку) на коммит с указанным хешем, рабочую директорию и индекс сделать такими, какими они были в момент указанного коммита
git reset --hard HEAD~       # сдвигаем указатель (ветку) master на 1 коммит назад
git reset --hard HEAD~1      # передвинуть HEAD (и ветку) на предыдущий коммит
git reset --hard HEAD~3      # отменяем последние 3 коммита
git reset --hard 75e2d51     # передвинуть HEAD (и ветку) на коммит с указанным хешем, рабочую директорию и индекс сделать такими, какими они были в момент указанного коммита

git reset --mixed HEAD       # по умолчанию используется вариант --mixed, поэтому его можно не указывать
git reset HEAD               # то же самое что и вы (git reset --mixed HEAD)
git reset                    # убрать из индекса все добавленные в него изменения (в рабочей директории все изменения сохранятся), антипод git add
git reset readme.txt         # убрать из индекса изменения указанного файла (в рабочей директории изменения сохранятся)
git reset HEAD~              # передвинуть HEAD (и ветку) на предыдущий коммит, рабочую директорию оставить как есть, индекс сделать таким, каким он был в момент предыдущего коммита (удобнее, чем git reset --soft HEAD~, если индекс нужно задать заново)
git reset HEAD~1             # передвинуть HEAD (и ветку) на предыдущий коммит
git reset @~                 # передвинуть HEAD (и ветку) на предыдущий коммит, рабочую директорию оставить как есть, индекс сделать таким, каким он был в момент предыдущего коммита (удобнее, чем git reset --soft @~, если индекс нужно задать заново)

git reset --soft @~          # передвинуть HEAD (и ветку) на предыдущий коммит, но в рабочей директории и индексе оставить все изменения
git reset --soft @~2         # то же, но передвинуть HEAD (и ветку) на 2 коммита назад
git reset --soft HEAD~       # передвинуть HEAD (и ветку) на предыдущий коммит, но в рабочей директории и индексе оставить все изменения
git reset --soft HEAD~1      # удалить коммит и вернуть, но оставить последний коммит в промежуточной области
git reset --soft HEAD~2      # то же, но передвинуть HEAD (и ветку) на 2 коммита назад

git reset --hard             # прекратить это прерванное слияние, вернуть рабочую директорию и индекс как было в момент коммита, на который указывает HEAD, а я пойду немного поплачу
git reset --merge            # прекратить это прерванное слияние, но оставить изменения, не закоммиченные до слияния (для случая, когда слияние делается не на чистом статусе)
git reset --abort            # то же, что и строкой выше
```

<a name="revert"><h3>`git revert` - Отмена коммита на предыдущий коммит</h3></a>

```bash
git revert <commit>	            # Создает новый коммит, который отменяет изменения, внесенные указанным коммитом.

git revert HEAD --no-edit       # создать новый коммит, отменяющий изменения последнего коммита без запуска редактора сообщения
git revert b9533bb --no-edit    # то же, но отменяются изменения, внесённые коммитом с указанным хешем (b9533bb)

git revert HEAD                 # заменить последнюю фиксацию предыдущей
git revert HEAD~2               # заменить последнюю фиксацию на вторую с конца
git revert HEAD~3..HEAD         # отменить последние 3 фиксации
git revert HEAD~n...HEAD        # Возврат диапазона коммитов

git reset --hard HEAD~3         # отменяем последние 3 коммита
git revert --no-commit HEAD~3.. # git вносит изменения в промежуточную область

git revert --abort              # прервать изменение
git revert --continue           # продолжить изменение (и изменить предлагаемое название коммита на своё)
```

---

## Коллективная работа

<a name="tag"><h3>`git tag` - Создание, вывод списка, удаление или проверка метки, подписанной с помощью GPG</h3></a>

```bash
git tag                                     # вывести все теги
git tag -n                                  # вывести все теги и описание
git tag -n -l 'v1.*'                        # показать все теги, которые начинаются с 'v1.*'

git tag v1.0.0                              # создать тег с указанным именем на коммите, на который указывает HEAD
git tag -a -m 'В продакшен!' v1.0.1 master  # создать тег с описанием на том коммите, на который смотрит ветка master
git tag v1.0 023d0d0                        # создать тег для более ранней фиксации

git tag -a <tag_name> -m "tag message"      # Создание аннотированного тега с сообщением
git tag -a v1.1  -m "My version 1.1"        # Создание аннотированного тега
git tag -a v0.1 50db987 -m "My version 0.1" # Создание аннотированного тега для коммита 50db987

git tag -d <tag_name>                       # Удаление определенного тега
git tag -d v1.0.0                           # удалить тег с указанным именем(ами)
```

<a name="remote"><h3>`git remote` - Добавление, удаление удалённых репозиториев</h3></a>

```bash
git remote -v              # показать список удалённых репозиториев, связанных с локальным
git remote remove origin   # убрать привязку удалённого репозитория с сокр. именем origin
git remote add origin https://github.com:nicothin/test.git # добавить удалённый репозиторий (с сокр. именем origin) с указанным URL
git remote rm origin       # удалить привязку удалённого репозитория
git remote show origin     # получить данные об удалённом репозитории с сокращенным именем origin
git remote add origin https://github.com:nicothin/test.git # добавляем предварительно созданный пустой удаленный репозиторий
git remote add upstream https://github.com/andreysssr/php-xdebug.git # добавляем удаленный репозиторий: сокр. имя — upstream, URL мастер-репозитория
git remote rename upstream base # переименовать удалённый репозиторий `upstream` в `base`
git remote rm base # удалить удалённый репозиторий base 

# Список удаленных репозиториев
git remote

# Добавить удаленный репозиторий
git remote add <name> <url>

# Удалить удаленный репозиторий
git remote rm <remote_name>

# Отображение информации о конкретном удаленном репозитории
git remote show <remote_name>

# Показать ветки отслеживания для удаленных репозиториев
git remote show <remote_name> --verbose
git remote show origin

# Получайте обновления из всех удаленных репозиториев.
git remote update

# Переименование удаленного репозитория
git remote rename <old_name> <new_name>
git remote rename upstream base # переименовать удалённый репозиторий

# Измените URL-адрес удаленного репозитория
git remote set-url <name> <new_url>

# Удалите устаревшие ветки удаленного отслеживания.
git remote prune <remote_name>

git remote	# Перечисляет все удаленные репозитории.
git remote add <name> <url> # Добавляет новый удаленный репозиторий с указанным именем и URL-адресом.

git remote add origin git@github.com:andreysssr/cheatsheets.git
git remote add origin https://github.com/andreysssr/cheatsheets.git
git remote add upstream git@github.com:andreysssr/cheatsheets.git

git remote -v              # показать список удалённых репозиториев, связанных с локальным    

git remote remove origin   # убрать привязку удалённого репозитория с сокр. именем origin
git remote rm origin       # удалить привязку удалённого репозитория

git remote show origin     # получить данные об удалённом репозитории с сокращенным именем origin

# список удалённых репозиториев
git remote

# подробная информация об удалённом репозитории
git remote -v 

# удаляет ветви которые не существуют на удалённом сервере
git remote prune origin

git remote # Списки отслеживаемых репозиториев
git remote add <remote-name> <remote-url> # Добавляет пульт в этот проект
git remote update # Обновление локального пульта до последней версии (полезно, когда нужно проверить чужие PR)
```

<a name="fetch"><h3>`git fetch` - Загрузка объектов и ссылок из другого репозитория</h3></a>

```bash
git fetch                  # Извлекает изменения из удаленного репозитория, включая новые ветки и фиксации.
git fetch upstream         # стягиваем все ветки мастер-репозитория, но пока не сливаем со своими
git fetch origin           # загрузить все коммиты из удалённого репозитория
git fetch origin branch    # указываем удалённый репозиторий и ветку которую нужно загрузить
git fetch -p               # Получайте обновления из удаленного репозитория и удаляйте устаревшие ветки удаленного отслеживания.
git fetch --prune          # Удаляет все ветки удаленного отслеживания, которые больше не существуют в удаленном репозитории.

```

<a name="pull"><h3>`git pull` - Извлечение изменений и объединение с другим репозиторием или локальной веткой</h3></a>

```bash
git pull origin            # влить изменения с удалённого репозитория (все ветки)
git pull origin master     # влить изменения с удалённого репозитория (только указанная ветка)
git pull --rebase

git pull <remote_name> <remote_branch> # Извлечь изменения из удаленной ветки
git pull	Fetches changes from the remote repository and merges them into the current branch.
git pull <remote>          # Извлекает изменения из указанного удаленного репозитория и объединяет их с текущей веткой.
git pull --rebase          # Извлекает изменения из удаленного репозитория и перебазирует текущую ветку в обновленную ветку.

```

<a name="push"><h3>`git push` - Обновление внешних ссылок и связанных объектов</h3></a>

```bash
# привязать локальную ветку (feature/change-password) в удалённую (origin/feature/change-password)
git push --set-upstream origin feature/change-password
# (-u) это сокращённая запись (--set-upstream)
git push -u origin feature/change-password
git push -u origin master     # отправляем данные из локального репозитория в удаленный (в ветку master)

git push                      # отправляем коммит с быстрым критическим изменением в master в удалённом репозитории
git push --all                # Отправляет все ветки в удаленный репозиторий.
git push --tags               # отправить в удалённый репозиторий со всеми тегами
git push -f                   # форсировать отправку в удалённый репозиторий 
git push --force     

git push -u origin master     # отправить изменения и связать удалённую ветку origin/master с веткой master
git push origin master        # отправить в удалённый репозиторий (с сокр. именем origin) данные своей ветки master
git push --tags               # отправить в удалённый репозиторий со всеми тегами
git push -f                   # форсировать отправку в удалённый репозиторий 
git push --force    

git push origin v1.0          # отправить тег в удаленный репозиторий
git push origin --delete v1.0 # Удаление тега из удалённого репозитория `origin`

git push origin :old_branch_name new_branch_name # применить переименование в удаленном репозитории
git push origin :old_name new_name               # применить переименование в удаленном репозитории

git push -d origin feature/change-password       # удалить эту ветку в удалённом репозитории
git push --delete origin branch_name_here        # удалить удаленную ветку в Git
```
