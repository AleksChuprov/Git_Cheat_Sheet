## Инициализация репозитория

### Сделать папку репозиторием — git init

Чтобы Git начал отслеживать изменения в проекте, папку с файлами этого проекта нужно сделать Git-репозиторием (от англ. repository — «хранилище»). Для этого следует переместиться в неё и ввести команду git init (от англ. initialize — «инициализировать»).

Например, создайте папку first-project и сделайте её Git-репозиторием: перейдите в неё с помощью команды cd и выполните git init.

Также git init выведет сообщение вида Initialized empty Git repository in <_ваша папка с проектом_>/.git/ (англ. «инициализирован пустой Git-репозиторий в <_ваша папка_>/.git/»). В подпапке .git Git будет хранить всю служебную информацию.

Команда git init — одна из редко применяемых, ведь репозиторий создаётся один раз, а пользоваться им можно сколько угодно долго.

#### «Разгитить» папку, если что-то пошло не так, — rm -rf .git

Если вы случайно сделали Git-репозиторием не ту папку, её можно «разгитить». Для этого нужно удалить скрытую подпапку .git.

'
cd <папка с репозиторием> # перешли в папку

rm -rf .git # удалили подпапку .git
'

#### Разберём подробнее, что такое -rf:

ключ -r (от англ. recursive — «рекурсивно») позволяет удалять папки вместе с их содержимым;
ключ -f (от англ. force — «заставить») избавит вас от вопросов вроде «Вы точно хотите удалить этот файл? А этот? И этот тоже?».

Будьте осторожны: в подпапке .git хранится история изменений. Если удалить .git, то вся история проекта будет стёрта без возможности восстановления — останется только последняя версия файлов.

#### Проверить состояние репозитория — git status

После инициализации репозитория first-project запустите команду git status (от англ. status — «статус», «состояние») — она показывает текущее состояние репозитория.

#### Подведём итоги:

Инициализировать репозиторий можно с помощью команды git init.
Проверить статус, или состояние, репозитория поможет команда git status.
Если вы ошиблись и случайно инициализировали не ту папку, можно «разгитить» её — удалить скрытую подпапку .git.

## Добавляем файлы в репозиторий

Вы инициализировали Git-репозиторий, но в нём пока ничего нет. В этом уроке разберём, как добавить туда файлы.
Подготовить файлы к сохранению — git add
Добавим в репозиторий два файла. Например, файл todo.txt, в котором будет список дел, и readme.txt для информации о проекте.

Создайте файлы todo.txt и readme.txt в папке first-project и запустите git status, чтобы посмотреть, что изменилось.

`touch todo.txt`
`touch readme.txt
` #создали файлы todo.txt и readme.txt

`git status` # проверили статус

Git сообщит, что в папке first-project есть untracked files (от англ. track — «следить», untracked — «неотслеженный», «неотслеживаемый») — ещё не отслеживаемые файлы readme.txt и todo.txt.

Состояние untracked значит, что Git ещё не хранит информацию о версиях файла и не может отследить, как он изменялся.
Сейчас в first-project два файла. Мы хотим отслеживать состояние обоих, поэтому можем использовать команду git add --all (от англ. add — «добавить» + от англ. all — «всё»). Ключ, или флаг, --all позволяет подготовить к сохранению все файлы в репозитории.

`git add --all` # подготовили к сохранению все файлы в репозитории
`git status` # проверили статус

Добавлять файлы можно и по одному, без ключа --all.

`git add todo.txt`
`git add readme.txt`
`git status`

Также можно добавить текущую папку целиком — в этом случае все файлы в ней тоже будут добавлены. Обратиться к текущей папке в Bash позволяет точка (.).

`git add .` # добавить всю текущую папку
`git status`

Вы можете использовать любой из этих вариантов — результат будет одинаковый.

Получилось! Файлы, которые отмечены зелёным, теперь отслеживаются и готовы к сохранению. Но сохранения пока не произошло, потому что команда `git add` только запоминает текущее содержимое (контент) файла.

Если сейчас отредактировать любой из «зелёных» файлов в папке first-project, он перейдёт в состояние modified (англ. «изменённый») и будет и в «зелёном», и в «красном» списках.

Например, откройте файл todo.txt в любом редакторе (подойдёт даже блокнот) и напишите в нём: 1. Пройти пару уроков по Git..

Сохраните изменения, а затем снова вызовите команду `git status` в консоли.

Файл todo.txt теперь есть и в «зелёном», и в «красном» списках:
зелёным отмечена пустая версия файла — в таком виде он был во время последнего запуска команды `git add`;
красным отмечена версия с текстом 1. Пройти пару уроков по Git..
Чтобы запомнить новое состояние файла, нужно снова ввести команду git add и передать в качестве параметра имя изменённого файла или ключ --all.

`git add todo.txt` # или
`git add --all`

Теперь файл todo.txt снова готов к сохранению! Будет сохранена последняя добавленная версия с текстом 1. Пройти пару уроков по Git..

Ура! Очередной урок позади. Подытожим:
Команда `git add` позволяет подготовить файл к сохранению.
Команда `git add --all` подготовит к сохранению сразу все файлы.
С помощью `git add .` можно добавить в репозиторий текущую папку со всеми файлами.

## Делаем первый коммит

Коммит — это одна из основных сущностей в Git (и в других системах контроля версий). Коммит гарантирует, что изменения будут сохранены в истории и при необходимости к ним можно будет «откатиться». Это как если бы вы могли выполнить операцию Ctrl+Z для целой папки (репозитория).

В этом уроке вы сделаете свой первый коммит.

### Выполнить коммит — `git commit`

Сделать коммит можно командой `git commit` c ключом `-m `(от англ. message — «сообщение»), который присваивает коммиту сообщение.

Обычно в таком сообщении поясняется, в чём именно состояли изменения. Это как заметки на полях: благодаря им проще читать и понимать текст. Сообщение коммита выполняет те же функции — улучшает понимание и упрощает навигацию. Оно пишется после ключа `-m` в кавычках.
Например, перейдите в папку first-project и выполните коммит со следующим комментарием.

`git commit -m 'Мой первый коммит!'`

После нажатия Enter текущая версия файлов будет сохранена в репозитории с сообщением Мой первый коммит!. Коммит (по названию команды `git commit`) — это по сути список файлов с их контентом.

Команда `git commit` выведет информацию о коммите.

- [master (root-commit) baa3b6e] значит:
  - коммит был в ветке master;
  - root-commit — это самый первый, или «корневой» (англ. root), коммит в ветке, у следующих коммитов такой надписи не будет;
  - baa3b6e — сокращённый идентификатор коммита (подробнее об этом мы ещё расскажем).
- 2 files changed, 1 insertion(+) значит:

  - изменились два файла (`readme.txt` и `todo.txt`);
  - одна строка была добавлена (1. Пройти пару уроков по Git.).

- Строки вида `create mode 100644 readme.txt` — это более подробная информация о новых (добавленных в Git) файлах.

      * `create` (англ. «создать») говорит, что файл был создан. Если бы файл был удалён, на этом месте было бы слово
      `delete` (англ. «удалить»).

  `mode 100644` сообщает, что это обычный файл. Также возможны варианты `100755` для исполняемых файлов (например, `что-нибудь.exe`) и `120000` для файлов-ссылок в Linux. Файлы-ссылки не содержат данных сами по себе, а только ссылаются на другие файлы — как «ярлыки» в Windows.

Обратите внимание: после того как вы сделали первый коммит, команда `git status` перестала выводить сообщение `No commits yet` (англ. «ещё нет коммитов»).

#### Ещё раз о разнице между `git add` и `git commit`

Сначала команда `git add` сообщает Git, какие именно файлы нужно сохранить и какую их версию. Затем с помощью команды `git commit` происходит само сохранение.

### Просматриваем историю коммитов

В этом уроке разберём, как вывести историю коммитов, — это понадобится для отслеживания того, что происходит в репозитории.

#### Просмотреть историю коммитов — `git log`

В самостоятельном задании прошлого урока вы сделали три коммита в ваш репозиторий. Чтобы увидеть их все, введите команду `git log` (от англ. log — «журнал [записей]»).

Обратите внимание, что по умолчанию `git log` выводит коммиты в обратном хронологическом порядке — последние коммиты оказываются первыми сверху. В этом можно убедиться, если посмотреть на дату и время их создания.

Если после выполнения команды вы видите, что в репозитории есть только один коммит или их нет вообще, вернитесь к прошлому уроку и убедитесь, что `git add` и `git commit` были вызваны в нужном порядке.

Супер! В этом небольшом, но важном уроке вы познакомились с командой `git log` — используйте её, чтобы оглянуться назад и посмотреть коммиты.

### Знакомство с GitHub

До этого момента вы использовали Git локально: сейчас проект `first-project` хранится только на вашем компьютере. Но одно из ключевых преимуществ Git — удобство командной работы над файлами. Чтобы поделиться репозиторием — например, с коллегами, — нужно завести его удалённую версию.
Процесс командной работы может выглядеть так: вы работаете над файлами проекта, например пишете код, на своём компьютере и сохраняете в локальном репозитории. Как только накапливается достаточно правок, чтобы поделиться ими с остальными, вы передаёте их на удалённый репозиторий. Там ваши коллеги смогут посмотреть то, что получилось, и даже скачать себе на компьютер.

Есть несколько платформ для такой командной работы. Самая популярная — GitHub. В нескольких следующих уроках покажем, как с ней работать.

Что такое GitHub

GitHub — платформа для хранения IT-проектов и совместной работы над ними с использованием Git. По сути, это сайт, куда можно загрузить файлы своего проекта для обмена с другими людьми.
С английского языка слово hub переводится как «узловая станция». И действительно, GitHub стал самым популярным сайтом для хранения Git-репозиториев. Многие крупные компании, такие как Google, Apple, Valve, используют GitHub для своих проектов.
GitHub подходит, чтобы отточить навыки работы с Git. Здесь можно завести аккаунт и вместе со своей командой работать над любыми задачами. Можно создавать проекты разных типов:

- приватный — только для вас;
- командный — только для членов команды;
- публичный — будет виден всем.

Также можно присоединиться к чужому open source проекту и работать над ним вместе с другими людьми со всего мира.
А ещё GitHub — это социальная сеть для разработчиков. С момента своего возникновения в
2008
2008 году она, согласно статистике, объединила десятки миллионов человек, дала им возможность для реализации идей и сотрудничества.

Git и платформы для удалённой работы
Git и GitHub — это два разных проекта, которые развиваются независимо друг от друга.
Git:

- консольный инструмент для работы с локальными и удалёнными репозиториями;
- проект с открытым исходным кодом.
  GitHub:
- платформа для размещения удалённых репозиториев;
- принадлежит компании Microsoft.
  Кроме GitHub, есть и другие платформы для командной работы. Например, GitLab и Bitbucket, которые тоже позволяют работать с Git. У каждой из этих платформ свои особенности и дополнительная функциональность:
- GitLab можно развернуть в виде сервера в приватной сети;
- Bitbucket — продукт компании Atlassian, поэтому он легко интегрируется с другими инструментами этой компании, такими как Jira.

В этом курсе вы будете взаимодействовать с GitHub. Но в целом эти платформы похожи, и если вы изучите одну из них, то переход на другую не будет проблемой.

Поздравляем: у вас появился новый друг в мире Git! Коротко напомним, о чём шла речь в этом уроке:

- GitHub — платформа, которая работает с Git и упрощает командное взаимодействие.
- Кроме GitHub, существуют и другие подобные платформы, например GitLab, Bitbucket и так далее.
- Git — это консольный инструмент для работы с локальными и удалёнными репозиториями. Он не связан напрямую ни с одной из платформ и развивается отдельно от них.

### Регистрация на GitHub

Вы познакомились с платформой GitHub — пришло время зарегистрироваться на ней. Поехали!
Инструкция по регистрации

1. В правом верхнем углу главной страницы GitHub нажмите на `Sign up` (англ. «зарегистрироваться»).
2. На экране будут последовательно появляться поля для ввода.
   2.1. Введите адрес электронной почты (англ. Enter your email).
   2.2. Придумайте пароль (англ. Create a password).
   2.3. Введите имя пользователя (англ. Enter a username).
3. Платформа спросит, хотите ли вы получать на почту рассылку с обновлениями и новостями (англ. Would you like to receive product updates and announcements via email?). Введите y, если хотите получать рассылку, или n, если не хотите.
4. Нажмите кнопку Continue (англ. «продолжить»).
5. GitHub предложит вам пройти капчу. Сделайте это.
6. После прохождения капчи нажмите Create account (англ. «создать аккаунт»).
7. Введите короткий код, который будет отправлен на указанный вами почтовый адрес.

Поздравляем! Вы успешно зарегистрировались на крупнейшем веб-хостинге проектов GitHub. Теперь у вас есть возможность работать бок о бок с миллионами профессионалов по всему миру, обмениваться идеями и развиваться.

### Создаём удалённый репозиторий

В прошлом уроке вы завели аккаунт на GitHub. Теперь разберём, как создать удалённый репозиторий, чтобы в будущем связать его с локальным.

### Инструкция по созданию репозитория на GitHub

1. Зайдите в свой профиль по ссылке https://github.com/username, где `username` — имя, которое вы указали при регистрации.

Эта страница — презентация вас и ваших проектов. Её видят другие пользователи. Надпись You don't have any public repositories yet (англ. «у вас пока нет публичных репозиториев») сообщает, что пока у вас нет проектов.

2. Создайте репозиторий. Для этого перейдите на вкладку Repositories (англ. «репозитории»), а затем нажмите на зелёную кнопку New (англ. «новый») справа.
3. Открылось окно создания нового репозитория. Назовите его `first-project`. Название удалённого репозитория необязательно должно совпадать с именем папки проекта у вас на компьютере. Но чтобы не путаться, будем называть их одинаково.

Другие поля вам пока не понадобятся. Смело нажимайте на зелёную кнопку Create repository (англ. «создать репозиторий») внизу.

Готово! Удалённый репозиторий создан. Страница с ним открывается автоматически.

Осталось связать удалённый репозиторий с локальным, который уже есть на вашем компьютере. GitHub предоставляет для этого инструкцию (пункт `…or push an existing repository from the command line`).
Но прежде, чтобы упростить работу с GitHub и сделать её более безопасной, вы научитесь генерировать SSH-ключи (от англ. Secure Shell — «безопасная оболочка»). Об этом в следующем уроке.

### Что такое SSH. Генерируем SSH-ключ

Представьте, что у вас есть ключ от двери, за которой хранится важный документ. Чтобы получить доступ к этому документу, вам нужно вставить ключ в замочную скважину и повернуть его. Поскольку ключ есть только у вас, ваш документ надёжно защищён от посторонних глаз.
Чтобы получить доступ к репозиторию на GitHub, вам тоже нужно предоставить ключ, который подтверждает вашу личность и права на чтение или изменение данных. Без этого ключа доступ будет ограничен. Об этом и пойдёт речь в уроке.

### Что такое SSH

Когда компьютеры обмениваются данными в сети, они следуют сетевым протоколам (англ. network protocols) — правилам обмена данными между компьютерами.
Один из наиболее распространённых сетевых протоколов — SSH (от англ. Secure Shell Protocol). Он обеспечивает безопасный обмен данными в сети. С помощью этого протокола можно получать данные с удалённого компьютера или отправлять их на него. Трафик шифруется, поэтому протокол безопасен.
SSH использует пару ключей для обеспечения безопасности — публичный и приватный:

- Приватный ключ (англ. private key) хранится только на вашем компьютере и не должен передаваться кому-либо ещё. Он используется для расшифровки данных.
- Публичный ключ (англ. public key) доступен всем и используется для шифрования данных. Они могут быть расшифрованы парным приватным ключом.

Только вы можете расшифровать данные с помощью приватного ключа, но любой владелец публичного ключа может их для вас зашифровать. Эти два ключа связаны и образуют SSH-пару. В будущем вы наверняка будете использовать их для взаимодействия с GitHub и другими удалёнными серверами.

### Проверка наличия SSH-ключа

Прежде чем генерировать SSH-ключи, убедитесь, что у вас их ещё нет. По умолчанию директория с SSH-ключами находится в домашней директории пользователя. Перейдите в неё.

`cd ~ `# перешли в домашнюю директорию

Обычно SSH-ключи находятся в директории `.ssh/`. Проверить наличие этой директории и файлов в ней можно с помощью следующей команды.

`ls -la .ssh/` # вывели список созданных ключей

Если папка пустая или её нет, всё в порядке.

Если есть файлы с похожими названиями, SSH-ключи уже создавались:

- `id_dsa.pub`;
- `id_ecdsa.pub`;
- `id_ed25519.pub`;
- `id_rsa.pub`.
  Если вы не создавали эти файлы, удалите их все.

### Инструкция по генерации SSH-ключа

1. Для генерации SSH-пары можно использовать программу ssh-keygen. Откройте терминал и введите следующую команду.
   `ssh-keygen -t ed25519 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"`

Используйте электронную почту, к которой привязан ваш GitHub-аккаунт.
Если вы видите сообщение об ошибке, то, скорее всего, ваша система не поддерживает алгоритм шифрования `ed25519`. Ничего страшного: используйте другой алгоритм.

    ssh-keygen -t rsa -b 4096 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"`

После ввода отобразится такое сообщение.
`> Generating public/private rsa key pair`. # сгенерированы публичный и приватный ключи

2. Укажите место хранения ключей. Простой вариант — сделать домашний каталог пользователя путём по умолчанию. Для этого нажмите `Enter`.

macOS

`> Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]`

Windows

`> Enter a file in which to save the key (C:\Users\<имя_пользователя>\.ssh\):[Press enter]`

Теперь в указанной директории появится пара ключей.

3. Программа запросит кодовую фразу (англ. passphrase) для доступа к SSH-ключу. Вы можете оставить поле пустым. Для этого нажмите `Enter`, а затем ещё раз `Enter` для подтверждения.

`> Enter passphrase (empty for no passphrase): [Type a passphrase]`
`> Enter same passphrase again: [Type passphrase again]`

4. Готово! Теперь осталось проверить, что ключи действительно сгенерировались. Для этого вызовите эту команду.

`ls -a ~/.ssh`

На экране должны появиться два файла — один с расширением `.pub`, другой — без. Файл в `.pub` — публичный, им можно делиться с веб-сайтами или коллегами. Файл без расширения `.pub` — приватный. Ни в коем случае не передавайте его никому!

Замечательно! Подведём итоги:

- SSH — протокол, который обеспечивает безопасный обмен данными в сети и использует для этого ключи.
- SSH-ключ — ваш виртуальный идентификатор в GitHub. Как ключ от квартиры, он позволяет получить доступ к GitHub-репозиторию. Также SSH используется для доступа к другим удалённым серверам.
- SSH-ключ состоит из двух частей — публичной и приватной. Публичный ключ зашифрует данные, а приватный — расшифрует. Приватным ключом ни в коем случае нельзя делиться, иначе любой сможет расшифровать все ваши секреты!

### Привязываем SSH-ключ к GitHub

В прошлом уроке вы сгенерировали SSH-ключ, но он пока не привязан к аккаунту на GitHub. Исправим это.

#### Инструкция по связыванию SSH-ключа и GitHub-аккаунта

1. После выполнения команды `ssh-keygen` из предыдущего урока в директории `~/.ssh` будет создано два файла — `id_ed25519` и `id_ed25519.pub` (или `id_rsa` и `id_rsa.pub` — в зависимости от того, какой алгоритм вы использовали):

- id_ed25519/id_rsa — приватный ключ (файл без .pub в конце). Ни в коем случае не копируйте его и не делитесь им.
- id_ed25519.pub/id_rsa.pub — публичный ключ (на это указывает расширение .pub).
  Скопируйте содержимое файла с публичным ключом в буфер обмена.

macOS

`pbcopy < ~/.ssh/id_rsa.pub` # скопировать содержимое ключа в буфер обмена

`pbcopy < ~/.ssh/id_ed25519.pub` #для ed25519

Здесь используется команда `pbcopy` — она копирует поток данных в буфер обмена. Запись `pbcopy < ~/.ssh/id_rsa.pub `означает: «Скопируй в буфер обмена всё содержимое файла `~/.ssh/id_rsa.pub`».

В качестве альтернативы вы можете распечатать файл на экран с помощью cat `~/.ssh/id_rsa.pub` и скопировать его вручную.

Windows

`clip < ~/.ssh/id_rsa.pub` # скопировать содержимое ключа в буфер обмена

`clip < ~/.ssh/id_ed25519.pub` # для ed25519

Если `clip` не сработает, выведите содержимое файла с помощью `cat ~/.ssh/id_rsa.pub` или `cat ~/.ssh/id_ed25519.pub` и скопируйте вывод в буфер обмена из консоли.

1. Перейдите на GitHub и выберите пункт Settings (англ. «настройки») в меню аккаунта.

2. Перейдите на GitHub и выберите пункт Settings (англ. «настройки») в меню аккаунта.
3. В меню слева нажмите на пункт SSH and GPG keys.
4. В открывшейся вкладке выберите New SSH key (англ. «новый SSH-ключ»).
5. В поле Title (англ. «заголовок») напишите название ключа. Например, Personal key (англ. «личный ключ»).
6. В поле Key type (англ. «тип ключа») должно быть Authentication Key (англ. «ключ аутентификации»).
7. В поле Key скопируйте ваш ключ из буфера обмена.
8. Нажмите на кнопку Add SSH key (англ. «добавить SSH-ключ»).
9. Проверьте правильность ключа с помощью следующей команды.
   `ssh -T git@github.com`

Если это первый раз, когда вы используете Git, чтобы поделиться проектом на GitHub, появится похожее предупреждение.

`The authenticity of host 'github.com (140.82.121.4)' can't be established. ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU. This key is not known by any other names. Are you sure you want to continue connecting (yes/no/[fingerprint])?`

Это предупреждение сообщает, что вы никогда не соединялись с сервером GitHub. Поэтому Git не может гарантировать, что сервер является тем, за кого он себя выдаёт.
Для подтверждения подлинности сервер генерирует и публикует ключи SHA256. Вы можете проверить ключи GitHub по этой ссылке. Если ключ в предупреждении совпадает с тем, что вы видите на сайте, значит, сервер является действительным. Введите `yes`, чтобы продолжить. Вы увидите приветствие на экране.

`Hi %ВАШ_АККАУНТ%! You've successfully authenticated, but GitHub does not provide shell access.`

Если у вас возникли сложности при генерации или привязке SSH-ключей, посмотрите видеоинструкцию, в которой мы показываем всё по порядку.

Ура: теперь ваш ключ привязан к GitHub! Если вы установили кодовую фразу для SSH-ключа, её нужно будет вводить для работы с репозиторием.

### Связываем локальный и удалённый репозитории

Сейчас у вас есть локальный репозиторий `first-project`, который хранится на вашем компьютере, и удалённый репозиторий на GitHub. Вы сгенерировали SSH-ключ для безопасной работы и теперь готовы связать удалённый репозиторий с локальным.

#### Привязать удалённый репозиторий к локальному — `git remote add`

Перейдите на страницу удалённого репозитория, выберите тип SSH и скопируйте URL. Кнопка справа позволит сделать это мгновенно.

Откройте консоль, перейдите в каталог локального репозитория и введите команду `git remote add` (от англ. remote — «удалённый» и add — «добавить»).

`cd ~/dev/first-project`
`git remote add origin git@github.com:%ИМЯ_АККАУНТА%/first-project.git`

Команде необходимо передать два параметра: имя удалённого репозитория и его URL. В качестве имени используйте слово `origin`. А URL вы скопировали со страницы удалённого репозитория.

`origin` (англ. «источник») — стандартный псевдоним, с помощью которого можно обращаться к главному удалённому репозиторию (обычно такой репозиторий один). Это значительно упрощает работу.

Убедиться, что репозитории связаны, — `git remote -v`

Отлично: вы связали локальный репозиторий с удалённым. Осталось убедиться, что всё работает, с помощью следующей команды.

`git remote -v`
`origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (fetch)`
`origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (push)`

В выводе вы должны увидеть две строчки, аналогичные тем, что показаны выше.
Флаг `-v` — короткая форма флага `--verbose` (англ. «подробный»). Он позволяет показать больше информации в выводе.

Локальный и удалённый репозитории связаны! О том, как их синхронизировать, расскажем в следующем уроке.

### Синхронизируем локальный и удалённый репозитории

Вы зарегистрировались на GitHub, сгенерировали SSH-ключ и привязали локальный репозиторий к удалённому. Самое сложное позади! Теперь разберём, как выкладывать свои правки на удалённый репозиторий. Но сначала немного о ветках.

#### Основная ветка

Мы упоминали, что каждый коммит сохраняет актуальное состояние файлов. Сами же коммиты хранятся в ветках (англ. branch).
Если коммит — это снимок состояния файлов, то ветка — временна́я шкала, на которой расположены эти снимки. Ветка всегда начинается от одного из коммитов.
В репозитории может существовать сразу несколько веток — параллельных историй изменений. Также они могут соединяться друг с другом.

Самая первая ветка в репозитории появляется автоматически и называется `main` (англ. «основная») или `master`. Её имя нужно указывать при отправке коммитов на удалённый репозиторий или при получении их из него.

main или master?
Раньше основная ветка в репозиториях, созданных на GitHub, называлась `master`, но с 1 октября 2020 года (после волны протестов движения Black Lives Matter) её переименовали в `main`.
Во всех репозиториях, созданных раньше этой даты, название основной ветки не поменялось. Поэтому в проектах, которые начали именно с `master`, и в руководствах по работе с Git вы по-прежнему можете встретить имя `master`.

#### Отправить изменения на удалённый репозиторий — `git push`

Вы уже прошли весь «цикл коммита»: подготовили файлы с помощью `git add`, закоммитили их с комментарием командой `git commit -m`. Осталось загрузить содержимое локального репозитория на GitHub. За это отвечает команда `git push` (от англ. push — «толкать»).
В первый раз эту команду нужно вызвать с флагом `-u` и параметрами `origin` (имя удалённого репозитория) и `main` или `master` (название текущей ветки). Флаг `-u` свяжет локальную ветку с одноимённой удалённой. Как вы связывали локальный и удалённый репозитории в предыдущем уроке, так же и здесь нужно дополнительно связать ветки.

`git push -u origin main` # Если команда приведёт к ошибке, попробуйте заменить main на master.

При взаимодействии с удалёнными репозиториями Git выводит в консоль отладочную информацию: количество объектов (файлов), которые отправляются на сервер, информацию о прогрессе сжатия и записи и так далее.
Если вы указывали кодовую фразу при настройке SSH-ключей, её нужно будет ввести.
Зайдите в репозиторий `first-project` на GitHub. Вы увидите, что в репозитории появились файлы с изменениями.

В дальнейшем при работе с удалённым репозиторием флаг `-u `можно опустить и писать просто `git push`.

#### Работа с графическим интерфейсом GitHub

GitHub предоставляет удобный интерфейс для работы с репозиторием. Например, нажмите на кнопку commit в правой части страницы, чтобы просмотреть все коммиты в репозитории.
Откроется окно с коммитами и их авторами.

Сообщение коммита в репозитории тоже является ссылкой.

Перейдите по ссылке, кликните на текст последнего коммита над репозиторием — так вы сможете увидеть все изменения, которые были внесены в репозиторий в этом коммите.

### Файл README.md

Чтобы другие пользователи, а также потенциальные клиенты или работодатели могли понять, что представляет собой проект, его нужно описать. Такое описание принято указывать в файле README.md (от англ. read — «прочитай» и me — «меня»). В этом уроке вы научитесь оформлять такие файлы.

#### Подробнее о том, зачем нужен README.md

Как правило, в README.md проекта можно найти следующую информацию:

1. Название проекта и его краткое описание: кем создан, для чего, какие решает задачи и какие закрывает проблемы.
2. Технологии, которые применяются в проекте. В чём его отличие от аналогичных.
3. Документация проекта — подробная инструкция о том, что представляет собой проект.
4. Планы проекта, если они есть.

#### Как создать и оформить README.md

README.md — текстовый файл, который можно создать командой `touch`, а затем редактировать так же, как и любой другой текстовый документ. Например, в блокноте.
Преимущество README.md в том, что средства командной работы (такие, как GitHub) могут отображать его содержимое в браузере в виде удобной разметки. Для этого нужно не просто залить текст, но и настроить шрифт, заголовки и отступы с помощью markdown. Маркда́ун — это специальный язык разметки. Он позволяет красиво отформатировать текстовый документ.
