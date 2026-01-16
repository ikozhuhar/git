### Learn Git

#### <a name='toc'>Содержание</a>
1. [Создание проекта](#create_project)
2. [Проверка состояния](#checking_status)
3. [Внесение изменений](#making_changes)
4. [Индексация изменений](#indexing_changes)
5. [Индексация и коммит](#indexing_and_committing)
6. [Коммит изменений](#commit_changes)
7. [Изменения, а не файлы](#changes,_not_files)
8. [История](#history)
9. [Команды Git](#command)
10. [Дополнительные материалы](#additional_materials)

```ruby
# Инициализация локального и подключения удаленного репозитория
git init
git remote add ikozhuhar-git-in git@dev-sr-git01:ikozhuhar/ikozhuhar-test.git

# Забираем данные из удаленного репозитория ikozhuhar-git-in из ветки master
git fetch ikozhuhar-git-in master
git merge ikozhuhar-git-in/master
git status

# Сохраняем изменения в локальом репозитории
git add -A
git commit -m "commit"

# Заливаем на удаленный репозиторий ikozhuhar-git-in в ветку master
git push -u ikozhuhar-git-in main:master
git status
```

#### 1. [[⬆]](#toc) <a name='create_project'>Создание проекта</a>
Цели: Научиться создавать Git-репозиторий с нуля.

```ruby
…or create a new repository on the command line
echo "# rainbow-remote" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:ikozhuhar/rainbow-remote.git
git push -u origin main

…or push an existing repository from the command line
git remote add origin git@github.com:ikozhuhar/rainbow-remote.git
git branch -M main
git push -u origin main
```

##### Создайте страницу «Hello, World»
```
mkdir work && cd work
echo "Hello, World" >> hello.html
```

##### Создайте репозиторий
Теперь у вас есть директория с одним файлом. Чтобы создать Git-репозиторий из этой директории, выполните команду `git init`.
```
git init
```
![image](https://github.com/user-attachments/assets/7660091a-153e-433b-bce6-bcc1194d332f)

##### Добавьте страницу в репозиторий
Теперь давайте добавим в репозиторий страницу «Hello, World».
```
git add hello.html
git commit -m "Initial Commit"
```
![image](https://github.com/user-attachments/assets/449c99ff-f6af-4378-acf8-e65c3a1057ef)



#### 2. [[⬆]](#toc) <a name='checking_status'>Проверка состояния</a>
Цели: Научиться проверять состояние репозитория.
##### Проверьте состояние репозитория
Используйте команду git status, чтобы проверить текущее состояние репозитория.
```
git status
```
![image](https://github.com/user-attachments/assets/3893b6ae-130a-45af-885d-d2851c03fee2)

Команда проверки состояния сообщила, что коммитить нечего. Это означает, что в репозитории уже хранится текущее состояние рабочих файлов, и нет никаких изменений, которые могли бы ожидать записи.



#### 3. [[⬆]](#toc) <a name='making_changes'>Внесение изменений</a>
Цель: Научиться отслеживать состояние рабочей директории.
##### Измените страницу «Hello, World»
```
echo "<h1>Hello, World</h1>" > hello.html
```
![image](https://github.com/user-attachments/assets/f5820a01-53eb-4d3d-a7ff-3c55606109be)

##### Проверьте состояние
```
git status
```
![image](https://github.com/user-attachments/assets/4749cef6-d4b1-4a3b-bc9f-8c191f6bf39b)
Первое, что нужно заметить, это то, что Git знает, что файл hello.html был изменен, но при этом эти изменения еще не зафиксированы в репозитории.  
Также обратите внимание на то, что сообщение о состоянии дает вам подсказку о том, что нужно делать дальше. Если вы хотите добавить эти изменения в репозиторий, используйте команду git add. В противном случае используйте команду git сheckout для отмены изменений.


#### 4. [[⬆]](#toc) <a name='indexing_changes'>Индексация изменений</a>
Цели: Научиться индексировать изменения для последующих коммитов.
##### Добавьте изменения
Теперь дайте команду Git проиндексировать изменения. Проверьте состояние:
```
git add hello.html
git status
```
![image](https://github.com/user-attachments/assets/d925e7e3-d27e-4256-b258-160fbc3cda89)  

Изменения файла hello.html были проиндексированы. Это означает, что Git теперь знает об изменении, но изменение пока не перманентно (читай, навсегда) записано в репозиторий. Следующий коммит будет включать в себя проиндексированные изменения.    
Если вы решили, что не хотите коммитить изменения, команда состояния напомнит вам о том, что с помощью команды `git reset` можно снять индексацию этих изменений.


#### 5. [[⬆]](#toc) <a name='indexing_and_committing'>Индексация и коммит</a>
Отдельный шаг индексации в Git позволяет вам разделять большие изменения на маленькие коммиты. Аналогия: вы помыли машину и заодно залили жидкость для очистки стекла — эти два изменения по своей сути независимы, а потому лучше пометить их отдельно. В противном случае, в истории изменений бачка для жидкости очистки стекла будет запись "Помыл машину", что не соответствует сути изменения и может запутать того, кто потом будет разбираться в этой истории.  

Предположим, что вы отредактировали три файла (`a.html`, `b.html`, и `c.html`). Теперь вы хотите закоммитить все изменения, при этом чтобы изменения в `a.html` и `b.html` были одним коммитом, в то время как изменения в `c.html` логически не связаны с первыми двумя файлами и должны идти отдельным коммитом.
```
git add a.html
git add b.html
git commit -m "Changes for a and b"
```
```
git add c.html
git commit -m "Unrelated change to c"
```
Разделяя индексацию и коммит, вы имеете возможность с легкостью настроить, что идет в какой коммит.


#### 6. [[⬆]](#toc) <a name='commit_changes'>Коммит изменений</a>
Цели: Научиться коммитить изменения в репозиторий.

##### Закоммитьте изменения

Достаточно об индексации. Давайте сделаем коммит того, что мы проиндексировали, в репозиторий.

Когда вы ранее использовали `git commit` для коммита первоначальной версии файла `hello.html` в репозиторий, вы включили метку `-m`, которая делает комментарий в командной строке. Команда `commit` позволит вам интерактивно редактировать комментарии для коммита. Теперь давайте это проверим.

Если вы опустите метку `-m` из командной строки, Git перенесет вас в редактор по вашему выбору. Редактор выбирается из следующего списка (в порядке приоритета):

1. переменная среды `GIT_EDITOR`
2. параметр конфигурации `core.editor`
3. переменная среды `VISUAL`
4. переменная среды `EDITOR`

> У меня переменная `EDITOR` установлена в vim. Если вы предпочитаете GUI-редактор, то теперь можно использовать VS Code в качестве [Git-редактора](https://code.visualstudio.com/docs/sourcecontrol/overview#_vs-code-as-git-editor).

Сделайте коммит сейчас и проверьте состояние.
```
git commit
```
![image](https://github.com/user-attachments/assets/f26ac3ba-b00b-4ceb-9fc6-53ff273e7216)
В первой строке введите комментарий: `Added h1 tag`. Сохраните файл и выйдите из редактора (для этого в редакторе по умолчанию (Vim) вам нужно нажать клавишу ESC, ввести :wq и нажать Enter). Вы увидите:

![image](https://github.com/user-attachments/assets/547d2028-3a69-43e2-9cc2-ee8873d4b9f5)
Строка «Waiting for Emacs...» получена из программы emacsclient, которая посылает файл в запущенную программу emacs и ждет его закрытия. Остальные выходные данные – стандартные коммит-сообщения.

##### Проверьте состояние

В конце давайте еще раз проверим состояние.
```
git status
```
![image](https://github.com/user-attachments/assets/8c9e39fd-3a8f-41ea-948a-e4531c31ee8f)

Рабочая директория чиста, можем продолжить работу.


#### 6. [[⬆]](#toc) <a name='changes,_not_files'>Изменения, а не файлы</a>
Цели: Понять, что Git работает с изменениями, а не файлами.

Большинство систем контроля версий работает с файлами: вы добавляете файл в систему, и она отслеживает изменения файла с этого момента.

Git фокусируется на изменениях в файле, а не самом файле. Когда вы осуществляете команду git add file, вы не говорите Git добавить файл в репозиторий. Скорее вы говорите, что Git надо отметить текущее состояние файла, коммит которого будет произведен позже.

Мы попытаемся исследовать эту разницу в данном уроке.

##### Первое изменение: Добавьте стандартные теги страницы
Измените страницу «Hello, World», чтобы она содержала стандартные теги `<html>` и `<body>`.

![image](https://github.com/user-attachments/assets/81f17f6d-0b1c-40cb-8679-9f27424c21b4)

```
git status
```
![image](https://github.com/user-attachments/assets/05f6ddef-46a2-493b-8435-92a39520dce6)


##### Добавьте это изменение
Теперь добавьте это изменение в индекс Git.
```
git add hello.html
```
![image](https://github.com/user-attachments/assets/e0155c0f-9764-4624-af25-c5844e81c093)

##### Коммит
Произведите коммит проиндексированного изменения (значение по умолчанию), а затем еще раз проверьте состояние.
```
git commit -m "Added standard HTML page tags"
git status
```
![image](https://github.com/user-attachments/assets/ff393d2e-8ebe-4b42-a954-07b43600d657)


#### 7. [[⬆]](#toc) <a name='history'>История</a>
Цели: Научиться просматривать историю проекта.

Получение списка произведенных изменений — функция команды `git log`.
```
git log
```
![image](https://github.com/user-attachments/assets/9dcdca44-7cb5-4c04-8486-d1908eae320f)  
Вот список всех трех коммитов в репозиторий, которые мы успели совершить.

##### Однострочная история
```
git log --pretty=oneline
```
![image](https://github.com/user-attachments/assets/0bb364a9-decd-4a2d-8230-462276514db2)

##### Контроль отображения записей
Вот еще интересные варианты просмотра истории:
```
git log --oneline --max-count=2
git log --oneline --since="5 minutes ago"
git log --oneline --until="5 minutes ago"
git log --oneline --author="Your Name"
git log --oneline --all
```
Существует огромное количество вариантов просмотра истории, вы можете порыться на странице руководства [git-log](https://git-scm.com/docs/git-log), чтобы увидеть их все.

##### Изощряемся

Вот что я использую для просмотра изменений, сделанных за последнюю неделю. Я добавлю `--author=ikozhuhar`, если я хочу увидеть только изменения, которые сделал я.
```
git log --all --pretty=format:"%h %cd %s (%an)" --since="7 days ago"
```

##### Конечный формат лога

Со временем, я решил, что для большей части моей работы мне подходит следующий формат лога.
```
git log --pretty=format:"%h %ad | %s%d [%an]" --date=short
```
![image](https://github.com/user-attachments/assets/88506f7a-0f0e-4c67-80e9-53ccd9dd7677)

*Давайте рассмотрим его в деталях:*
```
--pretty="..." — определяет формат вывода.
%h — укороченный хеш коммита.
%ad — дата коммита.
| — просто визуальный разделитель.
%s — комментарий.
%d — дополнения коммита («головы» веток или теги).
%an — имя автора.
--date=short — сохраняет формат даты коротким и симпатичным.
```

Таким образом, каждый раз, когда вы захотите посмотреть лог, вам придется много печатать. К счастью, существует несколько опций конфигурации Git, позволяющих настроить формат вывода истории по умолчанию:
```
git config --global format.pretty '%h %ad | %s%d [%an]'
git config --global log.date short
```


#### 8. [[⬆]](#toc) <a name='command'>Команды Git</a>

| Command | Description |
| ------- | ----------- |
| git commit | ... |
| git branch | ... |
| git checkout | ... |
| git cherry-pick | ... |
| git reset | ... |
| git revert | ... |
| git rebase | ... |
| git merge | ... |


```ruby
# Вход в консоль gitlab
gitlab-rails console

ПОИСК ПРОЕКТОВ

	# Посчитать общее количество проектов
	Project.count

	# Показать все проекты с именами
	Project.all.each do |project|
	  puts "#{project.id}: #{project.full_path}"
	end

	# Поиск конкретного проекта, если известно имя
	Project.find_by_full_path('группа/проект')

	# Поиск по части имени
	Project.where("path LIKE ?", "%payroll%")
	Project.where("name LIKE ?", "%zup%")

	# Показать все проекты одной группы
	group = Group.find_by_path('payroll')
	group.projects.each do |project|
	  puts project.full_path
	end
	
	# Экспорт всех проектов в файл
	File.open("/tmp/all_projects.txt", "w") do |file|
	  Project.all.each do |project|
		file.puts "#{project.id}: #{project.full_path}"
	  end
	end

	# Проверьте конкретно проект payroll/zup:
	project = Project.find_by_full_path('payroll/zup')
	project.id
	project.full_path
	project.visibility_level


ПОЛЬЗОВАТЕЛИ

	# Поиск пользователей
	User.find_by(username: 'username')
	User.find_by(email: 'user@example.com')
	User.where(admin: true)

	# Создание пользователя
	User.create!(username: 'newuser', email: 'test@test.com', name: 'New User', password: 'password')

	# Блокировка/разблокировка
	user.block!
	user.activate!

	# Назначение админом
	user.update(admin: true)

	# Управление пользователями
	User.find_by(username: 'username')
	user.update(admin: true)

	# Управление доступом
	project.add_developer(user)
	project.add_maintainer(user)

	# Проверка данных
	Project.count
	User.where(admin: true).count
	
	ПРАВА ДОСТУПА
	
	# Добавление пользователя в проект
	project.add_developer(user)
	project.add_maintainer(user)
	project.add_reporter(user)
	project.add_guest(user)

	# Удаление из проекта
	project.team.users.delete(user)

	# Проверка прав
	project.team.member?(user)
	user.can?(:read_project, project)


АДМИНИСТРИРОВАНИЕ

	# Статистика
	Project.count
	User.count
	Group.count

	# Поиск по email
	User.find_by_email('user@example.com')

	# Сброс пароля
	user.password = 'new_password'
	user.save!
	
ПОИСК ПРОБЛЕМ

	# Поиск заблокированных проектов
	Project.where(pending_delete: true)

	# Поиск неактивных пользователей
	User.where(state: 'blocked')

	# Проверка репозиториев
	project.repository.exists?
	project.repository.empty?

СОХРАНЕНИЕ ИЗМЕНЕНИЙ

	# Всегда используйте save! (с восклицательным знаком)
	user.save!
	project.save!
```

```ruby
Рекомендуют

1. Очистить старую конфигурацию
sudo gitlab-runner verify --delete

2. Затем зарегистрировать заново
sudo gitlab-runner register

sudo gitlab-ctl status

sudo gitlab-runner restart
sudo gitlab-runner status
sudo gitlab-runner list
sudo gitlab-runner verify

Рекомендуют

1. Очистить старую конфигурацию
sudo gitlab-runner verify --delete

2. Затем зарегистрировать заново
sudo gitlab-runner register

sudo gitlab-runner register \
  --url "http://dev-sr-git01.mip.ru" \
  --registration-token "ВАШ_ТОКЕН" \
  --executor "shell" \
  --description "Локальный runner на dev-sr-git01" \
  --tag-list "dev,shell"
!
Получить токен:
Получите токен через веб-интерфейс:
http://dev-sr-git01.mip.ru

Admin Area → Runners

Скопируйте Registration Token

Зарегистрируете runner:

sudo gitlab-runner register
# или одной командой
sudo gitlab-runner register --url "http://dev-sr-git01.mip.ru" --token "ВАШ_ТОКЕН" --executor "shell"


===============

sudo gitlab-redis-cli info stats | grep rejected
sudo gitlab-redis-cli info clients
ss -ln | grep :6379
sysctl net.core.somaxconn


redis['backlog'] = 2048
redis['maxclients'] = 15000
sudo sysctl -w net.core.somaxconn=2048 

В /etc/gitlab/gitlab.rb
redis['backlog'] = 512
redis['maxclients'] = 12000
redis['tcp_timeout'] = 30
redis['client_timeout'] = 30

sudo sysctl -w net.core.somaxconn=2048

gitlab-ctl reconfigure
gitlab-ctl restart

```

#### 8. [[⬆]](#toc) <a name='additional_materials'>Дополнительные материалы</a>

1. [Pro Git book](https://git-scm.com/book/ru/v2)



