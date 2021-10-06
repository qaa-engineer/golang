# Установка Go и настройка локальной среды программирования в macOS


<div class="content-body tutorial-content" data-growable-markdown="">
  
  <h3 id="Введение">Введение</h3>

<p><a href="https://golang.org">Go</a> — это язык программирования, созданный Google в результате разочарования в других языках. Разработчикам постоянно приходилось выбирать между эффективным языком программирования с очень длительным временем компиляции и удобным языком программирования, не отличающимся эффективностью в производственной среде. Язык Go был разработан, чтобы одновременно обеспечить все три преимущества: высокую скорость компиляции, удобство программирования и эффективное исполнение в производственной среде.</p>

<p>Go — это универсальный язык программирования, который можно использовать для различных проектов программирования. Он особенно хорошо подходит для сетевых программ/распределенных систем и заработал себе репутацию «языка облака». Он дает современным программистам больше возможностей благодаря мощному набору инструментов, позволяет устранить разногласия по поводу форматирования, делая формат частью спецификации языка, а также упрощает развертывание за счет компиляции в единый двоичный файл. Язык Go очень простой в обучении и имеет небольшой набор ключевых слов, что делает его идеальным вариантом как для начинающих, так и для опытных программистов.</p>

<p>В этом руководстве вы научитесь устанавливать Go на локальном компьютере macOS и настраивать среду программирования через командную строку.</p>

<h2 id="Предварительные-требования">Предварительные требования</h2>

<p>Вам потребуется компьютер macOS с административным доступом и подключением к Интернету.</p>

<h2 id="Шаг-1-—-Открытие-терминала">Шаг 1 — Открытие терминала</h2>

<p>Основную часть установки и настройки мы будем выполнять через командную строку — текстовый интерфейс взаимодействия с компьютером. Вместо нажатия на кнопки вы вводите текст и получаете от компьютера обратную связь в текстовом формате. Командная строка, также называемая «оболочка», помогает изменять и автоматизировать многие повседневные задачи, выполняемые на компьютерах. Это необходимый и очень важный инструмент для разработчиков программного обеспечения.</p>

<p>Терминал macOS — это приложение, которое вы можете использовать для доступа к интерфейсу командной строки. Вы можете найти его в Finder, как и любое другое приложение. Для этого перейдите в папку «Приложения», а затем в папку «Утилиты». В этой папке дважды нажмите на приложение Terminal, чтобы открыть его как любое другое приложение. Также вы можете использовать поиск Spotlight, удерживая клавиши <code>CMD</code> и <code>ПРОБЕЛ</code> и вводя Terminal в появляющемся поле.</p>

<p class="growable"><img src="https://assets.digitalocean.com/articles/eng_python/OSXSetUp/MacOSXSetUp.png" alt="Терминал macOS"></p>

<p>Существует множество разнообразных команд терминала, с помощью которых вы можете выполнять множество различных задач. Статья <a href="https://www.digitalocean.com/community/tutorials/an-introduction-to-the-linux-terminal">Введение в терминал Linux</a> поможет вам лучше сориентироваться в работе с терминалом Linux, который похож на терминал macOS.</p>

<p>Вы открыли терминал и теперь вы можете загрузить и установить пакет инструментов для разработчиков <a href="https://developer.apple.com/xcode/">Xcode</a>, который вам потребуется для установки Go.</p>

<h2 id="Шаг-2-—-Установка-xcode">Шаг 2 — Установка Xcode</h2>

<p>Xcode — это <em>интегрированная среда разработки</em> (IDE), состоящая из различных инструментов разработки программного обеспечения для macOS. Вы можете проверить установку Xcode, введя в окне терминала следующую команду:</p>
<div class="code-toolbar"><div class="context"><pre class="code-pre command prefixed language-bash"><code class="code-highlight  language-bash"><ul class="prefixed"><li class="line" data-prefix="$">xcode-select -p
</li></ul></code></pre><span style="font-size: 0px; line-height: 0; opacity: 0; pointer-events: none; position: absolute;">&nbsp;</span></div><div class="toolbar"><div class="toolbar-item"><button>Copy</button></div></div></div>
<p>Следующие результаты означают, что среда разработки Xcode установлена:</p>
<pre class="code-pre "><code><div class="secondary-code-label " title="Output">Output</div>/Library/Developer/CommandLineTools
</code></pre>
<p>Если вы получили сообщение об ошибке, выполните установку <a href="https://itunes.apple.com/us/app/xcode/id497799835?mt=12&amp;ign-mpt=uo%3D2">Xcode через App Store</a> в браузере, используя параметры по умолчанию.</p>

<p>После установки Xcode вернитесь в окно терминала. Теперь вам нужно установить отдельное приложение Command Line Tools Xcode с инструментами командной строки. Для этого введите следующую команду:</p>
<div class="code-toolbar"><div class="context"><pre class="code-pre command prefixed language-bash"><code class="code-highlight  language-bash"><ul class="prefixed"><li class="line" data-prefix="$">xcode-select --install
</li></ul></code></pre><span style="font-size: 0px; line-height: 0; opacity: 0; pointer-events: none; position: absolute;">&nbsp;</span></div><div class="toolbar"><div class="toolbar-item"><button>Copy</button></div></div></div>
<p>Теперь вы установили Xcode и приложение Command Line Tools, и мы готовы к установке диспетчера пакетов Homebrew.</p>

<h2 id="Шаг-3-—-Установка-и-настройка-homebrew">Шаг 3 — Установка и настройка Homebrew</h2>

<p>Хотя терминал macOS обладает многими функциями, совпадающими с функциями терминалов Linux и других систем Unix, в нем отсутствует встроенный диспетчер пакетов, основанный на передовом опыте. <strong>Диспетчер пакетов</strong> — это набор программных инструментов для автоматизации процессов установки, в число которых входят начальная установка программного обеспечения, обновление и настройка программного обеспечения, а также удаление программного обеспечения в случае необходимости. Диспетчер пакетов обеспечивает централизованное хранение установочных файлов и может обслуживать все программные пакеты в системе в распространенных форматах. <a href="https://brew.sh/"><strong>Homebrew</strong></a> — это бесплатная система управления пакетами с открытым исходным кодом для macOS, упрощающая установку программного обеспечения в macOS.</p>

<p>Для установки Homebrew введите в окно терминала следующее:</p>
<div class="code-toolbar"><div class="context"><pre class="code-pre command prefixed language-bash"><code class="code-highlight  language-bash"><ul class="prefixed"><li class="line" data-prefix="$">/usr/bin/ruby -e <span class="token string">"<span class="token variable"><span class="token variable">$(</span><span class="token function">curl</span> -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install<span class="token variable">)</span></span>"</span>
</li></ul></code></pre><span style="font-size: 0px; line-height: 0; opacity: 0; pointer-events: none; position: absolute;">&nbsp;</span></div><div class="toolbar"><div class="toolbar-item"><button>Copy</button></div></div></div>
<p>Диспетчер Homebrew создан на языке Ruby и поэтому он изменит путь Ruby на вашем компьютере. Команда <code>curl</code> извлекает скрипт из заданного URL. Этот скрипт объясняет, какие операции будут выполнены, а затем приостанавливает процесс в ожидании вашего подтверждения. Так вы получаете большой объем обратной связи по работе скрипта в вашей системе, а также возможность проверить выполнение процесса.</p>

<p>Если вам потребуется ввести пароль, учтите, что нажимаемые клавиши не отображаются в окне терминала, но их ввод регистрируется. Просто нажмите клавишу <code>Return</code> после завершения ввода пароля. В противном случае нажмите клавишу <code>y</code> («Да»), чтобы подтвердить установку.</p>

<p>Просмотрим флаги, связанные с командой <code>curl</code>:</p>

<ul>
<li>Флаг <code>-f</code> или <code>--fail</code> предписывает окну терминала не выводить документы HTML при ошибках сервера.</li>
<li>Флаг <code>-s</code> или <code>--silent</code> заглушает вывод <code>curl</code> так, что команда не отображает счетчик выполнения. В сочетании с флагом <code>-S</code> или <code>--show-error</code> этот флаг гарантирует вывод командой <code>curl</code> сообщения об ошибке в случае сбоя.</li>
<li>Флаг <code>-L</code> или <code>--location</code> предписывает команде <code>curl</code> повторить запрос в новое место, если сервер сообщает, что запрошенная страница перемещена в другое место.</li>
</ul>

<p>После завершения процесса установки мы поместим директорию Homebrew на верхний уровень переменной среды <code>PATH</code>. Благодаря этому установка Homebrew будет вызываться для инструментов, которые macOS может автоматически выбирать и которые могут запускаться против создаваемой нами среды разработки.</p>

<p>Вам следует создать или открыть файл <code>~/.bash_profile</code> с помощью текстового редактора командной строки <strong>nano</strong>, используя команду <code>nano</code>:</p>
<div class="code-toolbar"><div class="context"><pre class="code-pre command prefixed language-bash"><code class="code-highlight  language-bash"><span class="token function"></span><ul class="prefixed"><span class="token function"></span><li class="line" data-prefix="$"><span class="token function">nano</span> ~/.bash_profile
</li></ul></code></pre><span style="font-size: 0px; line-height: 0; opacity: 0; pointer-events: none; position: absolute;">&nbsp;</span></div><div class="toolbar"><div class="toolbar-item"><button>Copy</button></div></div></div>
<p>Когда файл откроется в окне терминала, введите следующую команду:</p>
<pre class="code-pre "><code>export PATH=/usr/local/bin:$PATH
</code></pre>
<p>Для сохранения изменений нажмите клавишу <code>CTRL</code> и букву <code>o</code>, а затем нажмите клавишу <code>RETURN</code>, когда система предложит вам сделать это. Теперь вы можете выйти из nano, нажав клавишу <code>CTRL</code> и букву <code>x</code>.</p>

<p>Для активации этих изменений выполните в терминале следующую команду:</p>
<div class="code-toolbar"><div class="context"><pre class="code-pre command prefixed language-bash"><code class="code-highlight  language-bash"><span class="token builtin class-name"></span><ul class="prefixed"><span class="token builtin class-name"></span><li class="line" data-prefix="$"><span class="token builtin class-name">source</span> ~/.bash_profile
</li></ul></code></pre><span style="font-size: 0px; line-height: 0; opacity: 0; pointer-events: none; position: absolute;">&nbsp;</span></div><div class="toolbar"><div class="toolbar-item"><button>Copy</button></div></div></div>
<p>После этого внесенные вами изменения переменной среды <code>PATH</code> вступят в силу.</p>

<p>Вы можете убедиться в успешной установке Homebrew с помощью следующей команды:</p>
<div class="code-toolbar"><div class="context"><pre class="code-pre command prefixed language-bash"><code class="code-highlight  language-bash"><ul class="prefixed"><li class="line" data-prefix="$">brew doctor
</li></ul></code></pre><span style="font-size: 0px; line-height: 0; opacity: 0; pointer-events: none; position: absolute;">&nbsp;</span></div><div class="toolbar"><div class="toolbar-item"><button>Copy</button></div></div></div>
<p>Если никакие обновления не требуются, на экране терминала появится следующее:</p>
<pre class="code-pre "><code><div class="secondary-code-label " title="Output">Output</div>Your system is ready to brew.
</code></pre>
<p>В ином случае может быть выведено предупреждение о необходимости запуска другой команды, например <code>brew update</code> для проверки актуальности установленной версии Homebrew.</p>

<p>После завершения установки Homebrew вы можете переходить к установке Go.</p>

<h2 id="Шаг-4-—-Установка-go">Шаг 4 — Установка Go</h2>

<p>Вы можете использовать Homebrew для поиска всех доступных пакетов с помощью команды <code>brew search</code>. В этом руководстве мы будем искать пакеты или модули, связанные с Go:</p>
<div class="code-toolbar"><div class="context"><pre class="code-pre command prefixed language-bash"><code class="code-highlight  language-bash"><ul class="prefixed"><li class="line" data-prefix="$">brew search golang
</li></ul></code></pre><span style="font-size: 0px; line-height: 0; opacity: 0; pointer-events: none; position: absolute;">&nbsp;</span></div><div class="toolbar"><div class="toolbar-item"><button>Copy</button></div></div></div>
<p><span class="note"><strong>Примечание</strong>. В этом руководстве не используется команда <code>brew search go</code>, поскольку она возвращает слишком много результатов. Поскольку <code>go</code> — очень короткое слово, и ему может соответствовать много пакетов, в качестве поискового запроса обычно используют <code>golang</code>. Эта практика также обычно применяется при поиске статей по Go в Интернете. Термин <em>Golang</em> происходит от названия домена Go, а именно <code>golang.org</code>.<br></span></p>

<p>Терминал выведет список модулей, которые вы можете установить:</p>
<pre class="code-pre "><code><div class="secondary-code-label " title="Output">Output</div>golang  golang-migrate
</code></pre>
<p>В этом списке будет и Go. Переходите к установке:</p>
<div class="code-toolbar"><div class="context"><pre class="code-pre command prefixed language-bash"><code class="code-highlight  language-bash"><ul class="prefixed"><li class="line" data-prefix="$">brew <span class="token function">install</span> golang
</li></ul></code></pre><span style="font-size: 0px; line-height: 0; opacity: 0; pointer-events: none; position: absolute;">&nbsp;</span></div><div class="toolbar"><div class="toolbar-item"><button>Copy</button></div></div></div>
<p>В окне терминала будет отображаться информация по процессу установки Go. Установка может занять несколько минут.</p>

<p>Чтобы проверить, какую версию Go вы установили, введите следующую команду:</p>
<div class="code-toolbar"><div class="context"><pre class="code-pre command prefixed language-bash"><code class="code-highlight  language-bash"><ul class="prefixed"><li class="line" data-prefix="$">go version
</li></ul></code></pre><span style="font-size: 0px; line-height: 0; opacity: 0; pointer-events: none; position: absolute;">&nbsp;</span></div><div class="toolbar"><div class="toolbar-item"><button>Copy</button></div></div></div>
<p>Эта команда выводит номер установленной версии Go. По умолчанию устанавливается самая последняя стабильная версия Go.</p>

<p>В будущем для обновления Go вы можете использовать следующие команды, которые сначала обновляют Homebrew, а затем — Go. Сейчас это не требуется, поскольку вы только что установили последнюю версию:</p>
<div class="code-toolbar"><div class="context"><pre class="code-pre command prefixed language-bash"><code class="code-highlight  language-bash"><ul class="prefixed"><li class="line" data-prefix="$">brew update
</li><li class="line" data-prefix="$">brew upgrade golang
</li></ul></code></pre><span style="font-size: 0px; line-height: 0; opacity: 0; pointer-events: none; position: absolute;">&nbsp;</span></div><div class="toolbar"><div class="toolbar-item"><button>Copy</button></div></div></div>
<p><code>brew update</code> обновляет версию Homebrew, благодаря чему у вас будет самая актуальная информация о пакетах, которые вы хотите установить. Команда <code>brew upgrade golang</code> обновит пакет <code>golang</code> до последней доступной версии.</p>

<p>Рекомендуется регулярно проверять актуальность установленной версии Go.</p>

<p>Теперь вы установили Go на своем компьютере и можете перейти к созданию рабочего пространства для ваших проектов Go.</p>

<h2 id="Шаг-5-—-Создание-рабочего-пространства-go">Шаг 5 — Создание рабочего пространства Go</h2>

<p>Вы установили Xcode, Homebrew и Go и теперь можете переходить к созданию рабочего пространства для программирования.</p>

<p>На корневом уровне рабочего пространства Go имеются две директории:</p>

<ul>
<li><code>src</code>: это директория с исходными файлами Go. Исходный файл или файл исходного кода — это файл, который вы пишете на языке программирования Go. Компилятор Go использует исходные файлы для создания исполняемого двоичного файла.</li>
<li><code>bin</code>: директория, содержащая исполняемые файлы, которые были созданы и установлены инструментами Go. Исполняемые файлы — это двоичные файлы, которые запускаются в системе и выполняют задачи. Обычно это программы, скомпилированные из вашего исходного кода или из другого загруженного исходного кода Go.</li>
</ul>

<p>Субдиректория <code>src</code> может содержать несколько репозиториев контроля версий (например, <a href="https://git-scm.com/">Git</a>, <a href="https://www.mercurial-scm.org/">Mercurial</a> и <a href="http://bazaar.canonical.com">Bazaar</a>). При импорте сторонних двоичных файлов вашей программой вы увидите такие директории, как <code>github.com</code> или <code>golang.org</code>. Если вы используете репозиторий кода, например <code>github.com</code>, вы также помещаете в эту директорию свои проекты и файлы исходного кода. Это обеспечивает канонический импорт кода в ваш проект. <em>Канонический</em> импорт — это операция импорта, которая ссылается на полностью квалифицированный пакет, например <code>github.com/digitalocean/godo</code>.</p>

<p>Вот так выглядит типичное рабочее пространство:</p>
<pre class="code-pre plain"><code>.
├── bin
│   ├── buffalo                                      # command executable
│   ├── dlv                                          # command executable
│   └── packr                                        # command executable
└── src
    └── github.com
        └── digitalocean
            └── godo
                ├── .git                            # Git reposistory metadata
                ├── account.go                      # package source
                ├── account_test.go                 # test source
                ├── ...
                ├── timestamp.go
                ├── timestamp_test.go
                └── util
                    ├── droplet.go
                    └── droplet_test.go
</code></pre>
<p>Директория по умолчанию рабочего пространства Go в версии 1.8 совпадает с домашней директорией вашего пользователя с субдиректорией <code>go</code> или имеет адрес <code>$HOME/go</code>. Если вы используете версию Go ниже 1.8, лучше всего использовать для рабочего пространства адрес <code>$HOME/go</code>.</p>

<p>Введите следующую команду для создания структуры директорий рабочего пространства Go:</p>
<div class="code-toolbar"><div class="context"><pre class="code-pre command prefixed language-bash"><code class="code-highlight  language-bash"><span class="token function"></span><ul class="prefixed"><span class="token function"></span><li class="line" data-prefix="$"><span class="token function">mkdir</span> -p <span class="token environment constant">$HOME</span>/go/<span class="token punctuation">{</span>bin,src<span class="token punctuation">}</span>
</li></ul></code></pre><span style="font-size: 0px; line-height: 0; opacity: 0; pointer-events: none; position: absolute;">&nbsp;</span></div><div class="toolbar"><div class="toolbar-item"><button>Copy</button></div></div></div>
<p>Опция <code>-p</code> предписывает команде <code>mkdir</code> создать в директории все <code>родительские элементы</code>, даже если их еще не существует. При использовании параметров <code>{bin,src}</code> для команды <code>mkdir</code> создается набор аргументов, предписывающий ей создать директорию <code>bin</code> и директорию <code>src</code>.</p>

<p>Таким образом, обеспечивается размещение следующей структуры директорий:</p>
<pre class="code-pre plain"><code>└── $HOME
    └── go
        ├── bin
        └── src
</code></pre>
<p>До выпуска версии Go 1.8 обязательно было создавать локальную переменную среды с именем <code>$GOPATH</code>. Хотя это больше явно не требуется, создать такую переменную все равно полезно, поскольку многие сторонние инструменты зависят от ее использования.</p>

<p>Вы можете задать переменную <code>$GOPATH</code> посредством ее добавления в файл <code>~/.bash_profile</code>.</p>

<p>Откройте файл <code>~/.bash_profile</code> с помощью <code>nano</code> или другого предпочитаемого текстового редактора:</p>
<div class="code-toolbar"><div class="context"><pre class="code-pre command prefixed language-bash"><code class="code-highlight  language-bash"><span class="token function"></span><ul class="prefixed"><span class="token function"></span><li class="line" data-prefix="$"><span class="token function">nano</span> ~/.bash_profile
</li></ul></code></pre><span style="font-size: 0px; line-height: 0; opacity: 0; pointer-events: none; position: absolute;">&nbsp;</span></div><div class="toolbar"><div class="toolbar-item"><button>Copy</button></div></div></div>
<p>Чтобы задать переменную <code>$GOPATH</code>, добавьте в файл следующую строку:</p>
<div class="code-label " title="~/.bash_profile">~/.bash_profile</div><div class="code-toolbar"><div class="context"><pre class="code-pre sh language-bash"><code class="code-highlight  language-bash"><span class="token builtin class-name">export</span> <span class="token assign-left variable">GOPATH</span><span class="token operator">=</span><span class="token environment constant">$HOME</span>/go</code></pre><span style="font-size: 0px; line-height: 0; opacity: 0; pointer-events: none; position: absolute;">&nbsp;</span></div><div class="toolbar"><div class="toolbar-item"><button>Copy</button></div></div></div>
<p>При компиляции и установке инструментов Go помещает их в директорию <code>$GOPATH/bin</code>. Для удобства субдиретория <code>/bin</code> рабочего пространства обычно добавляется в переменную <code>PATH</code> в файле <code>~/.bash_profile</code>:</p>
<div class="code-label " title="~/.bash_profile">~/.bash_profile</div><div class="code-toolbar"><div class="context"><pre class="code-pre sh language-bash"><code class="code-highlight  language-bash"><span class="token builtin class-name">export</span> <span class="token assign-left variable"><span class="token environment constant">PATH</span></span><span class="token operator">=</span><span class="token environment constant">$PATH</span><span class="token builtin class-name">:</span><span class="token variable">$GOPATH</span>/bin</code></pre><span style="font-size: 0px; line-height: 0; opacity: 0; pointer-events: none; position: absolute;">&nbsp;</span></div><div class="toolbar"><div class="toolbar-item"><button>Copy</button></div></div></div>
<p>Теперь в файле <code>~/.bash_profile</code> должны быть следующие записи:</p>
<div class="code-label " title="~/.bash_profile">~/.bash_profile</div><div class="code-toolbar"><div class="context"><pre class="code-pre sh language-bash"><code class="code-highlight  language-bash"><span class="token builtin class-name">export</span> <span class="token assign-left variable">GOPATH</span><span class="token operator">=</span><span class="token environment constant">$HOME</span>/go
<span class="token builtin class-name">export</span> <span class="token assign-left variable"><span class="token environment constant">PATH</span></span><span class="token operator">=</span><span class="token environment constant">$PATH</span><span class="token builtin class-name">:</span><span class="token variable">$GOPATH</span>/bin</code></pre><span style="font-size: 0px; line-height: 0; opacity: 0; pointer-events: none; position: absolute;">&nbsp;</span></div><div class="toolbar"><div class="toolbar-item"><button>Copy</button></div></div></div>
<p>Это позволит вам запускать любые компилируемые или загружаемые программы через инструменты Go в любом месте в вашей системе.</p>

<p>Для обновления оболочки используйте следующую команду для загрузки созданных глобальных переменных:</p>
<div class="code-toolbar"><div class="context"><pre class="code-pre command prefixed language-bash"><code class="code-highlight  language-bash"><span class="token builtin class-name"></span><ul class="prefixed"><span class="token builtin class-name"></span><li class="line" data-prefix="$"><span class="token builtin class-name">.</span> ~/.bash_profile
</li></ul></code></pre><span style="font-size: 0px; line-height: 0; opacity: 0; pointer-events: none; position: absolute;">&nbsp;</span></div><div class="toolbar"><div class="toolbar-item"><button>Copy</button></div></div></div>
<p>Вы можете проверить обновление переменной <code>$PATH</code>, запустив команду <code>echo</code> и просмотрев результаты:</p>
<div class="code-toolbar"><div class="context"><pre class="code-pre command prefixed language-bash"><code class="code-highlight  language-bash"><span class="token builtin class-name"></span><ul class="prefixed"><span class="token builtin class-name"></span><li class="line" data-prefix="$"><span class="token builtin class-name">echo</span> <span class="token environment constant">$PATH</span>
</li></ul></code></pre><span style="font-size: 0px; line-height: 0; opacity: 0; pointer-events: none; position: absolute;">&nbsp;</span></div><div class="toolbar"><div class="toolbar-item"><button>Copy</button></div></div></div>
<p>Вы должны увидеть директорию <code>$GOPATH/bin</code> в своей домашней директории. Если вы вошли в систему под именем пользователя <code>sammy</code>, вы увидите путь <code>/Users/sammy/go/bin</code>.</p>
<pre class="code-pre sh"><code><div class="secondary-code-label " title="Output">Output</div><span class="highlight">/Users/sammy/go/bin</span>:/usr/local/sbin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
</code></pre>
<p>Вы создали корневую директорию рабочего пространства и задали переменную среды <code>$GOPATH</code>. Теперь вы сможете создавать будущие проекты со следующей структурой директорий. В этом примере предполагается, что вы используете <a href="https://www.github.com">github.com</a> в качестве репозитория:</p>
<pre class="code-pre plain"><code>$GOPATH/src/<span class="highlight">github.com</span>/<span class="highlight">username</span>/<span class="highlight">project</span>
</code></pre>
<p>Если вы работаете над проектом <a href="https://github.com/digitalocean/godo">https://github.com/digitalocean/godo</a>, он помещается в следующую директорию:</p>
<pre class="code-pre plain"><code>$GOPATH/src/<span class="highlight">github.com</span>/<span class="highlight">digitalocean</span>/<span class="highlight">godo</span>
</code></pre>
<p>Такая структура проектов делает их доступными с помощью инструмента <code>go get</code>. Также она делает проекты удобнее для чтения.</p>

<p>Для проверки вы можете использовать команду <code>go get</code> для доставки библиотеки <code>godo</code>:</p>
<div class="code-toolbar"><div class="context"><pre class="code-pre command prefixed language-bash"><code class="code-highlight  language-bash"><ul class="prefixed"><li class="line" data-prefix="$">go get github.com/digitalocean/godo
</li></ul></code></pre><span style="font-size: 0px; line-height: 0; opacity: 0; pointer-events: none; position: absolute;">&nbsp;</span></div><div class="toolbar"><div class="toolbar-item"><button>Copy</button></div></div></div>
<p>Мы можем увидеть успешную загрузку пакета <code>godo</code> посредством вывода директории:</p>
<div class="code-toolbar"><div class="context"><pre class="code-pre command prefixed language-bash"><code class="code-highlight  language-bash"><span class="token function"></span><ul class="prefixed"><span class="token function"></span><li class="line" data-prefix="$"><span class="token function">ls</span> -l <span class="token variable">$GOPATH</span>/src/github.com/digitalocean/godo
</li></ul></code></pre><span style="font-size: 0px; line-height: 0; opacity: 0; pointer-events: none; position: absolute;">&nbsp;</span></div><div class="toolbar"><div class="toolbar-item"><button>Copy</button></div></div></div>
<p>Результат должен выглядеть примерно так:</p>
<pre class="code-pre "><code><div class="secondary-code-label " title="Output">Output</div>-rw-r--r--  1 sammy  staff   2892 Apr  5 15:56 CHANGELOG.md
-rw-r--r--  1 sammy  staff   1851 Apr  5 15:56 CONTRIBUTING.md
.
.
.
-rw-r--r--  1 sammy  staff   4893 Apr  5 15:56 vpcs.go
-rw-r--r--  1 sammy  staff   4091 Apr  5 15:56 vpcs_test.go
</code></pre>
<p>На этом шаге вы создали рабочее пространство Go и настроили необходимые переменные среды. На следующем шаге мы протестируем рабочее пространство, запустив в нем код.</p>

<h2 id="Шаг-6-—-Создание-простой-программы">Шаг 6 — Создание простой программы</h2>

<p>Вы настроили рабочее пространство Go и теперь можете создать простую программу “Hello, World!” Так вы убедитесь, что ваше рабочее пространство работает, и сможете лучше познакомиться с Go.</p>

<p>Поскольку вы создаете один исходный файл Go, а не фактический проект, вам не нужно находиться в рабочем пространстве.</p>

<p>Откройте в домашней директории редактор <code>nano</code> или другой текстовый редактор командной строки и создайте новый файл:</p>
<div class="code-toolbar"><div class="context"><pre class="code-pre command prefixed language-bash"><code class="code-highlight  language-bash"><span class="token function"></span><ul class="prefixed"><span class="token function"></span><li class="line" data-prefix="$"><span class="token function">nano</span> hello.go
</li></ul></code></pre><span style="font-size: 0px; line-height: 0; opacity: 0; pointer-events: none; position: absolute;">&nbsp;</span></div><div class="toolbar"><div class="toolbar-item"><button>Copy</button></div></div></div>
<p>Когда текстовый файл откроется в терминале, введите код программы:</p>
<div class="code-toolbar"><div class="context"><pre class="code-pre  language-go"><code class="code-highlight  language-go"><span class="token keyword">package</span> main

<span class="token keyword">import</span> <span class="token string">"fmt"</span>

<span class="token keyword">func</span> <span class="token function">main</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    fmt<span class="token punctuation">.</span><span class="token function">Println</span><span class="token punctuation">(</span><span class="token string">"Hello, World!"</span><span class="token punctuation">)</span>
<span class="token punctuation">}</span></code></pre><span style="font-size: 0px; line-height: 0; opacity: 0; pointer-events: none; position: absolute;">&nbsp;</span></div><div class="toolbar"><div class="toolbar-item"><button>Copy</button></div></div></div>
<p>Для выхода из nano нажмите клавиши <code>control</code> и <code>х</code>, а когда система предложит вам сохранить файл, нажмите клавишу <code>y</code>.</p>

<p>Этот код использует пакет <code>fmt</code> и вызывает функцию <code>Println</code> с <code>Hello, World!</code> в качестве аргумента. В результате фраза <code>Hello, World!</code> распечатывается на терминале при запуске программы.</p>

<p>После выхода из <code>nano</code> и возврата в оболочку запустите программу:</p>
<div class="code-toolbar"><div class="context"><pre class="code-pre command prefixed language-bash"><code class="code-highlight  language-bash"><ul class="prefixed"><li class="line" data-prefix="$">go run hello.go
</li></ul></code></pre><span style="font-size: 0px; line-height: 0; opacity: 0; pointer-events: none; position: absolute;">&nbsp;</span></div><div class="toolbar"><div class="toolbar-item"><button>Copy</button></div></div></div>
<p>Созданная программа <code>hello.go</code> выведет на терминале следующее:</p>
<pre class="code-pre "><code><div class="secondary-code-label " title="Output">Output</div>Hello, World!
</code></pre>
<p>На этом шаге вы использовали простую программу для подтверждения правильности настройки рабочего пространства Go.</p>

<h2 id="Заключение">Заключение</h2>

<p>Поздравляем! Вы настроили рабочее пространство программирования Go на своем локальном компьютере macOS и теперь можете начинать проект по программированию.</p>

</div>
