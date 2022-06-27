# Инструкции по работе с Git, используя возможности Markdown.

### Основы
Git — это набор консольных утилит, которые отслеживают и фиксируют изменения в файлах (чаще всего речь идет об исходном коде программ, но вы можете использовать его для любых файлов на ваш вкус). 

Изначально Git был создан Линусом Торвальдсом при разработке ядра Linux. 

Однако инструмент так понравился разработчикам, что в последствии, он получил широкое распространение и его стали использовать в других проектах. С его помощью вы можете сравнивать, анализировать, редактировать, сливать изменения и возвращаться назад к последнему сохранению. 

Этот процесс называется контролем версий.

Для чего он нужен? 

* Ну во-первых, чтобы отследить изменения, произошедшие с проектом, со временем. Проще говоря, мы можем посмотреть как менялись файлы программы, на всех этапах разработки и при необходимости вернуться назад и что-то отредактировать. Часто бывают ситуации, когда, во вполне себе работающий код, вам нужно внести определенные правки или улучшить какой-то функционал, по желанию заказчика. Однако после внедрения нововведений, вы с ужасом понимаете, что все сломалось. У вас начинается судорожно дергаться глаз, а в воздухе повисает немой вопрос: “Что делать?” Без системы контроля версий, вам надо было бы долго напряженно просматривать код, чтобы понять как было до того, как все перестало работать. С Гитом же, все что нужно сделать - это откатиться на коммит назад.

* Во-вторых он чрезвычайно полезен при одновременной работе нескольких специалистов, над одним проектом. Без Гита случится коллапс, когда разработчики, скопировав весь код из главной папки и сделав с ним задуманное, попытаются одновременно вернуть весь код обратно.
Git является распределенным, то есть не зависит от одного центрального сервера, на котором хранятся файлы. Вместо этого он работает полностью локально, сохраняя данные в директориях на жестком диске, которые называются репозиторием. Тем не менее, вы можете хранить копию репозитория онлайн, это сильно облегчает работу над одним проектом для нескольких людей. Для этого используются сайты вроде github и bitbucket.

### Установка

Установить git на свою машину очень просто:

* Linux — нужно просто открыть терминал и установить приложение при помощи пакетного менеджера вашего дистрибутива. Для Ubuntu команда будет выглядеть следующим образом:

> sudo apt-get install git

* Windows — мы рекомендуем git for windows, так как он содержит и клиент с графическим интерфейсом, и эмулятор bash.

* OS X — проще всего воспользоваться homebrew. После его установки запустите в терминале:

> brew install git

Если вы новичок, клиент с графическим интерфейсом(например GitHub Desktop и Sourcetree) будет полезен, но, тем не менее, знать команды очень важно.

### Настройка

Итак, мы установили git, теперь нужно добавить немного настроек. Есть довольно много опций, с которыми можно играть, но мы настроим самые важные: наше имя пользователя и адрес электронной почты. Откройте терминал и запустите команды:

> git config --global user.name "My Name"
> git config --global user.email email@example.com

Теперь каждое наше действие будет отмечено именем и почтой. Таким образом, пользователи всегда будут в курсе, кто отвечает за какие изменения - это вносит порядок.

Git хранит весь пакет конфигураций в файле .gitconfig, находящемся в вашем локальном каталоге. Чтобы сделать эти настройки глобальными, то есть применимыми ко всем проектам, необходимо добавить флаг –global. Если вы этого не сделаете, они будут распространяться только на текущий репозиторий.
Для того, чтобы посмотреть все настройки системы, используйте команду:

> git config --list

Для удобства и легкости зрительного восприятия, некоторые группы команд в Гит можно выделить цветом, для этого нужно прописать в консоли:

> git config --global color.ui true
> git config --global color.status auto
> git config --global color.branch auto

Если вы не до конца настроили систему для работы, в начале своего пути - не беда. Git всегда подскажет разработчику, если тот запутался, например:

Команда **git --help** - выводит общую документацию по git
Если введем **git log --help** - он предоставит нам документацию по какой-то определенной команде (в данном случае это - log).

Если вы вдруг сделали опечатку - система подскажет вам нужную команду
После выполнения любой команды - отчитается о том, что вы сделали не так.

Также Гит прогнозирует дальнейшие варианты развития событий и всегда направит разработчика, не знающего, куда двигаться дальше.

Тут стоит отметить, что подсказывать система будет на английском, но не волнуйтесь, со временем вы изучите несложный алгоритм ее работы и будете разговаривать с ней на одном языке.

### Создание нового репозитория

Как мы отметили ранее, git хранит свои файлы и историю прямо в папке проекта. Чтобы создать новый репозиторий, нам нужно открыть терминал, зайти в папку нашего проекта и выполнить команду init. Это включит приложение в этой конкретной папке и создаст скрытую директорию .git, где будет храниться история репозитория и настройки.
Создайте на рабочем столе папку под названием git_exercise. Для этого в окне терминала введите:

> mkdir Desktop/git_exercise/
> cd Desktop/git_exercise/
> git init

Командная строка должна вернуть что-то вроде:

Initialized empty Git repository in /home/user/Desktop/git_exercise/.git/
Это значит, что наш репозиторий был успешно создан, но пока что пуст. Теперь создайте текстовый файл под названием hello.mb и сохраните его в директории git_exercise.

### Определение состояния

**status** — это еще одна важнейшая команда, которая показывает информацию о текущем состоянии репозитория: актуальна ли информация на нём, нет ли чего-то нового, что поменялось, и так далее. Запуск git status на нашем свежесозданном репозитории должен выдать:

> git status
> On branch master
> Initial commit
> Untracked files:
> (use "git add ..." to include in what will be committed)
> hello.mb

Сообщение говорит о том, что файл hello.mb неотслеживаемый. Это значит, что файл новый и система еще не знает, нужно ли следить за изменениями в файле или его можно просто игнорировать. Для того, чтобы начать отслеживать новый файл, нужно его специальным образом объявить.

### Подготовка файлов

В git есть концепция области подготовленных файлов. Можно представить ее как холст, на который наносят изменения, которые нужны в коммите. Сперва он пустой, но затем мы добавляем на него файлы (или части файлов, или даже одиночные строчки) командой add и, наконец, коммитим все нужное в репозиторий (создаем слепок нужного нам состояния) командой commit.

В нашем случае у нас только один файл, так что добавим его:

> git add hello.mb

Если нам нужно добавить все, что находится в директории, мы можем использовать

>  git add -A

Проверим статус снова, на этот раз мы должны получить другой ответ:

> git status
> On branch master
> Initial commit
> Changes to be committed:
> (use "git rm --cached ..." to unstage)
> new file: hello.mb

Файл готов к коммиту. Сообщение о состоянии также говорит нам о том, какие изменения относительно файла были проведены в области подготовки — в данном случае это новый файл, но файлы могут быть модифицированы или удалены.

### Фиксация изменений

##### Как сделать коммит

Представим, что нам нужно добавить пару новых блоков в html-разметку (index.html) и стилизовать их в файле style.css. Для сохранения изменений, их необходимо закоммитить. Но сначала, мы должны обозначить эти файлы для Гита, при помощи команды git add, добавляющей (или подготавливающей) их к коммиту.

Добавлять их можно по отдельности:

> git add index.html
> git add css/style.css

или вместе - всё сразу:

> git add .

Конечно добавлять всё сразу удобнее, чем прописывать каждую позицию отдельно. Однако, тут надо быть внимательным, чтобы не добавить по ошибке ненужные элементы. Если же такое произошло изъять оттуда ошибочный файл можно при помощи команды

> git reset:
> git reset css/style.css

Теперь создадим непосредственно сам коммит

> git commit -m 'Add some code'

Флажок -m задаст commit message - комментарий разработчика. Он необходим для описания закоммиченных изменений. И здесь работает золотое правило всех комментариев в коде: «Максимально ясно, просто и содержательно обозначь написанное!»

##### Как посмотреть коммиты
Для просмотра все выполненных фиксаций можно воспользоваться историей коммитов. Она содержит сведения о каждом проведенном коммите проекта. 

Запросить ее можно при помощи команды:

> git log

В ней содержиться вся информация о каждом отдельном коммите, с указанием его хэша, автора, списка изменений и даты, когда они были сделаны. Отследить интересующие вас операции в списке изменений, можно по хэшу коммита, при помощи команды git show :

> git show hash_commit

Ну а если вдруг нам нужно переделать commit message и внести туда новый комментарий, можно написать следующую конструкцию:

> git commit --amend -m 'Новый комментарий'

В данном случае сообщение последнего коммита перезапишется. Но злоупотреблять этим не стоит, поскольку эта операция опасная и лучше ее делать до отправки коммита на сервер.

### Удаленные репозитории
Сейчас наш коммит является локальным — существует только в директории .git на нашей файловой системе. Несмотря на то, что сам по себе локальный репозиторий полезен, в большинстве случаев мы хотим поделиться нашей работой или доставить код на сервер, где он будет выполняться.

##### 1. Что такое удаленный репозиторий
Репозиторий, хранящийся в облаке, на стороннем сервисе, специально созданном для работы с git имеет ряд преимуществ. Во-первых - это своего рода резервная копия вашего проекта, предоставляющая возможность безболезненной работы в команде. А еще в таком репозитории можно пользоваться дополнительными возможностями хостинга. К примеру -визуализацией истории или возможностью разрабатывать вашу программу непосредственно в веб-интерфейсе.

**Клонирование**
Клонирование - это когда вы копируете удаленный репозиторий к себе на локальный ПК. Это то, с чего обычно начинается любой проект. При этом вы переносите себе все файлы и папки проекта, а также всю его историю с момента его создания. Чтобы склонировать проект, сперва, необходимо узнать где он расположен и скопировать ссылку на него.

> git clone https://ссылка_на_проект

При клонировании в текущий каталог, там будет создана папка, в которую поместятся все проектные файлы и скрытая директория .git, с самим репозиторием, или с необходимой информацией о нем. В такой ситуации, для клонируемого репозитория, по умолчанию, будет создана папка с одноименным названием, но его можно залить и в другую директорию, например:

> git clone https://ссылка_на_проект new-folder

##### 2. Подключение к удаленному репозиторию

Чтобы загрузить что-нибудь в удаленный репозиторий, сначала нужно к нему подключиться. Регистрация и установка может занять время, но все подобные сервисы предоставляют хорошую документацию.

Чтобы связать наш локальный репозиторий с репозиторием на GitHub, выполним следующую команду в терминале. Обратите внимание, что нужно обязательно изменить URI репозитория на свой.

> This is only an example. Replace the URI with your own repository address.
> git remote add origin https://ссылка_на_проект.git

Проект может иметь несколько удаленных репозиториев одновременно. Чтобы их различать, мы дадим им разные имена. Обычно главный репозиторий называется origin.

##### 3. Отправка изменений на сервер

Сейчас самое время переслать наш локальный коммит на сервер. Этот процесс происходит каждый раз, когда мы хотим обновить данные в удаленном репозитории.

Команда, предназначенная для этого - push. Она принимает два параметра: имя удаленного репозитория (мы назвали наш origin) и ветку, в которую необходимо внести изменения (master — это ветка по умолчанию для всех репозиториев).

> git push origin master
> Counting objects: 3, done.
> Writing objects: 100% (3/3), 212 bytes | 0 bytes/s, done.
> Total 3 (delta 0), reused 0 (delta 0)
> To https://ссылка_на_проект.git
> [new branch] master -> master

Эта команда немного похожа на git fetch, с той лишь разницей, что при помощи fetch мы импортируем коммиты в локальную ветку, а при применив push, мы экспортируем их из локальной в удаленную. 

Если вам необходимо настроить удаленную ветку используйте git remote. Однако пушить надо осторожно, ведь рассматриваемая команда перезаписывает безвозвратно все изменения. 

В большинстве случаев, ее используют, чтобы опубликовать выгружаемые локальные изменения в центральный репозиторий. А еще ее применяют для того, чтобы поделиться, внесенными в локальный репозиторий, нововведениями, с коллегами или другими удаленными участниками разработки проекта. 

Подытожив сказанное, можно назвать *git push* - командой выгрузки, а *git pull* и *git fetch* - командами загрузки или скачивания. 

После того как вы успешно запушили измененные данные, их необходимо внедрить или интегрировать, при помощи команды слияния *git merge*.

В зависимости от сервиса, который вы используете, вам может потребоваться аутентифицироваться, чтобы изменения отправились. Если все сделано правильно, то когда вы посмотрите в удаленный репозиторий при помощи браузера, вы увидите файл hello.mb

##### 4. Запрос изменений с сервера

Если вы сделали изменения в вашем удаленном репозитории, другие пользователи могут скачать изменения при помощи команды pull.

> git pull origin master
> From https://ссылка_на_проект
> branch master -> FETCH_HEAD
> Already up-to-date.

Так как новых коммитов с тех пор, как мы склонировали себе проект, не было, никаких изменений доступных для скачивания нет.

##### Как удалить локальный репозиторий

Вам не понравился один из ваших локальных Git-репозиториев и вы хотите стереть его со своей машины. Для этого вам всего лишь надо удалить скрытую папку «.git» в корневом каталоге репозитория. Сделать это можно 3 способами:

Проще всего вручную удалить эту папку «.git» в корневом каталоге «Git Local Warehouse».

Также удалить, не устраивающий вас, репозиторий можно на github. Открываете нужный вам объект и переходите в пункт меню Настройки. Там, прокрутив ползунок вниз, вы попадете в зону опасности, где один из пунктов будет называться «удаление этого хранилища».

Последний метод удаления локального хранилища через командную строку, для этого в терминале необходимо ввести следующую команду:

> cd repository-path/
> rm -r .git

### Ветвление

Во время разработки новой функциональности считается хорошей практикой работать с копией оригинального проекта, которую называют веткой. Ветви имеют свою собственную историю и изолированные друг от друга изменения до тех пор, пока вы не решаете слить изменения вместе. Это происходит по набору причин:

* Уже рабочая, стабильная версия кода сохраняется.

* Различные новые функции могут разрабатываться параллельно разными программистами.

* Разработчики могут работать с собственными ветками без риска, что кодовая база поменяется из-за чужих изменений.

* В случае сомнений, различные реализации одной и той же идеи могут быть разработаны в разных ветках и затем сравниваться.

##### 1. Создание новой ветки

Основная ветка в каждом репозитории называется master. Чтобы создать еще одну ветку, используем команду branch *name*

> git branch amazing_new_feature

Это создаст новую ветку, пока что точную копию ветки master.

##### 2. Переключение между ветками

Сейчас, если мы запустим branch, мы увидим две доступные опции:

> git branch
> amazing_new_feature
> master

master — это активная ветка, она помечена звездочкой. Но мы хотим работать с нашей "новой потрясающей фичей", так что нам понадобится переключиться на другую ветку. Для этого воспользуемся командой *checkout*, она принимает один параметр — имя ветки, на которую необходимо переключиться.

> git checkout amazing_new_feature

В Git ветка — это отдельная линия разработки. Git checkout позволяет нам переключаться как между удаленными, так и меду локальными ветками. Это один из способов получить доступ к работе коллеги или соавтора, обеспечивающий более высокую продуктивность совместной работы. Однако тут надо помнить, что пока вы не закомитили изменения, вы не сможете переключиться на другую ветку. В такой ситуации нужно либо сделать коммит, либо отложить его, при помощи команды git stash, добавляющей текущие незакоммиченные изменения в стек изменений и сбрасывающей рабочую копию до HEAD'а репозитория.

##### 3. Слияние веток

Наша "потрясающая новая фича" будет еще одним текстовым файлом под названием feature.mb. Мы создадим его, добавим и закоммитим:

> git add feature.txt
> git commit -m "New feature complete."

Изменения завершены, теперь мы можем переключиться обратно на ветку master.

> git checkout master

Теперь, если мы откроем наш проект в файловом менеджере, мы не увидим файла feature.mb, потому что мы переключились обратно на ветку master, в которой такого файла не существует. Чтобы он появился, нужно воспользоваться merge для объединения веток (применения изменений из ветки amazing_new_feature к основной версии проекта).

> git merge amazing_new_feature

Теперь ветка master актуальна. Ветка amazing_new_feature больше не нужна, и ее можно удалить.

> git branch -d awesome_new_feature

Если хотите создать копию удаленного репозитория - используйте *git clone*. Однако если вам нужна только определенная его ветка, а не все хранилище - после *git clone* выполните следующую команду в соответствующем репозитории:

> git checkout -b <имя ветки> origin/<имя ветки>

После этого, новая ветка создается на машине автоматически.

### Как удалять ветки в Git?

Бывают ситуации, когда после слива каких-то изменений из рабочей ветки в исходную версию проекта, её, по правилам хорошего тона, необходимо удалить, чтобы она более не мешалась в вашем коде. Но как это сделать?

Для локально расположенных веток существует команда:

> git branch -d local_branch_name

где флажок -d являющийся опцией команды git branch - это сокращенная версия ключевого слова --delete, предназначенного для удаления ветки, а local_branch_name – название ненужной нам ветки.
Однако тут есть нюанс: удалить текущую ветку, в которую вы, в данный момент просматриваете - нельзя. Если же вы все-таки попытаетесь это сделать, система отругает вас и выдаст ошибку с таким содержанием:

> Error: Cannot delete branch local_branch_name checked out at название_директории

Так что при удалении ветвей, обязательно переключитесь на другой branch.

### Дополнительно

В последней части этого руководства мы расскажем о некоторых дополнительных трюках, которые могут вам помочь.

##### 1. Отслеживание изменений, сделанных в коммитах

У каждого коммита есть свой уникальный идентификатор в виде строки цифр и букв. Чтобы просмотреть список всех коммитов и их идентификаторов, можно использовать команду *git log*:

> git log
commit 48d094a28e720b6cf2c0a891ce775a96923410a6 (HEAD -> amazing_new_feature, master)
Author: AndreyITMetatech <rfandrey@yandex.ru>
Date:   Mon Jun 27 15:21:25 2022 +0300

Как вы можете заметить, идентификаторы довольно длинные, но для работы с ними не обязательно копировать их целиком — первых нескольких символов будет вполне достаточно. Чтобы посмотреть, что нового появилось в коммите, мы можем воспользоваться командой *git show*

> git show
> commit 48d094a28e720b6cf2c0a891ce775a96923410a6 (HEAD -> amazing_new_feature, master)
> Author: AndreyITMetatech <rfandrey@yandex.ru>
> Date:   Mon Jun 27 15:21:25 2022 +0300
> 
>    new feature complete
> 
> diff --git a/feature.mb b/feature.mb
> new file mode 100644
> index 0000000..e69de29

Чтобы увидеть разницу между двумя коммитами, используется команда diff (с указанием промежутка между коммитами) *git diff*

Мы сравнили первый коммит с последним, чтобы увидеть все изменения, которые были когда-либо сделаны. Обычно проще использовать git difftool, так как эта команда запускает графический клиент, в котором наглядно сопоставляет все изменения.

##### 2. Возвращение файла к предыдущему состоянию

Гит позволяет вернуть выбранный файл к состоянию на момент определенного коммита. Это делается уже знакомой нам командой *checkout*, которую мы ранее использовали для переключения между ветками. Но она также может быть использована для переключения между коммитами (это довольно распространенная ситуация для Гита - использование одной команды для различных, на первый взгляд, слабо связанных задач).

В следующем примере мы возьмем файл hello.mb и откатим все изменения, совершенные над ним к первому коммиту. Чтобы сделать это, мы подставим в команду идентификатор нужного коммита, а также путь до файла:

> git checkout 09bd8cc1 hello.mb

##### 3. Исправление коммита

Если вы опечатались в комментарии или забыли добавить файл и заметили это сразу после того, как закоммитили изменения, вы легко можете это поправить при помощи commit —amend. Эта команда добавит все из последнего коммита в область подготовленных файлов и попытается сделать новый коммит. Это дает вам возможность поправить комментарий или добавить недостающие файлы в область подготовленных файлов.

Для более сложных исправлений, например, не в последнем коммите или если вы успели отправить изменения на сервер, нужно использовать revert. Эта команда создаст коммит, отменяющий изменения, совершенные в коммите с заданным идентификатором.

Самый последний коммит может быть доступен по алиасу HEAD:

> git revert HEAD

Для остальных будем использовать идентификаторы:

> git revert b10cc123

При отмене старых коммитов нужно быть готовым к тому, что возникнут конфликты. Такое случается, если файл был изменен еще одним, более новым коммитом. И теперь git не может найти строчки, состояние которых нужно откатить, так как они больше не существуют.

##### 4. Разрешение конфликтов при слиянии

Помимо сценария, описанного в предыдущем пункте, конфликты регулярно возникают при слиянии ветвей или при отправке чужого кода. Иногда конфликты исправляются автоматически, но обычно с этим приходится разбираться вручную — решать, какой код остается, а какой нужно удалить.

Давайте посмотрим на примеры, где мы попытаемся слить две ветки под названием **john_branch** и **tim_branch**. И Тим, и Джон правят один и тот же файл: функцию, которая отображает элементы массива.

**Джон использует цикл**:

> // Use a for loop to console.log contents.
> for(var i=0; i<arr.length; i++) {
> console.log(arr[i]);
> }

**Тим предпочитает forEach**:

> // Use forEach to console.log contents.
> arr.forEach(function(item) {
> console.log(item);
> });

Они оба коммитят свой код в соответствующую ветку. Теперь, если они попытаются слить две ветки, они получат сообщение об ошибке:

> $ git merge tim_branch
> Auto-merging print_array.js
> CONFLICT (content): Merge conflict in print_array.js
> Automatic merge failed; fix conflicts and then commit the result.

Система не смогла разрешить конфликт автоматически, значит, это придется сделать разработчикам. Приложение отметило строки, содержащие конфликт:

> <<<<<<< HEAD // Use a for loop to console.log contents. for(var i=0; i<arr.length; i++) { console.log(arr[i]); } ======= // Use forEach to console.log contents. arr.forEach(function(item) { console.log(item); }); >>>>>>> Tim's commit.

Над разделителем ======= мы видим последний (HEAD) коммит, а под ним - конфликтующий. 

Таким образом, мы можем увидеть, чем они отличаются и решать, какая версия лучше. Или вовсе написать новую. В этой ситуации мы так и поступим, перепишем все, удалив разделители, и дадим git понять, что закончили.

> // Not using for loop or forEach.
> // Use Array.toString() to console.log contents.
> console.log(arr.toString());

Когда все готово, нужно закоммитить изменения, чтобы закончить процесс:

> git add -A
> git commit -m "Array printing conflict resolved."

Как вы можете заметить, процесс довольно утомительный и может быть очень сложным в больших проектах. Многие разработчики предпочитают использовать для разрешения конфликтов клиенты с графическим интерфейсом. (Для запуска нужно набрать *git mergetool*).

##### 5. Настройка .gitignore

В большинстве проектов есть файлы или целые директории, в которые мы не хотим (и, скорее всего, не захотим) коммитить. Мы можем удостовериться, что они случайно не попадут в git add -A при помощи файла .gitignore

1. Создайте вручную файл под названием .gitignore и сохраните его в директорию проекта.

2. Внутри файла перечислите названия файлов/папок, которые нужно игнорировать, каждый с новой строки.

3. Файл .gitignore должен быть добавлен, закоммичен и отправлен на сервер, как любой другой файл в проекте.

Вот хорошие примеры файлов, которые нужно игнорировать:

* Логи

* Артефакты систем сборки

* Папки node_modules в проектах node.js

* Папки, созданные IDE, например, Netbeans или IntelliJ

* Разнообразные заметки разработчика.

Файл .gitignore, исключающий все перечисленное выше, будет выглядеть так:

> .log
> build/
> node_modules/
> .idea/
> my_notes.txt

Символ слэша в конце некоторых линий означает директорию (и тот факт, что мы рекурсивно игнорируем все ее содержимое). Звездочка, как обычно, означает шаблон.

### Git bash и git.io
Руководствуясь часто встречающимися, при изучении системы, вопросами новичков, разберем еще несколько непонятных словосочетаний.

* Git Bash(Bourne Again Shell) — это приложение, являющееся эмулятором командной строки и предоставляющее, операционной системе, некоторые распространенные утилиты bash и собственно саму систему Git. Это терминал, используемый для взаимодействия с персональным компьютером, посредством письменных команд.

* URL-адреса хранилищ на Гитхабе могут быть довольно длинными, из-за больших имен репозиториев и файлов. Работать с такими ссылками очень не удобно.

### Заключение.

Вот и все! Моя инструкция по Git окончена. Я очень старался собрать всю самую важную информацию и изложить ее как можно более сжато и кратко.

Git довольно сложен, и в нем есть еще много функций и трюков.

Предалагаю посетить мой личный сайт: 

<**https://itmetatech.ru/**>
