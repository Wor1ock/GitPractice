# Инициализация репозитория
**git init**  
Одна из редко применяемых команд, ведь репозиторий создаётся один раз, а пользоваться им можно сколько угодно долго.
Создаёт файл *.git* который хранит всю историю коммитов. Без файла репозиторий не может существовать.  
**rm -rf .git**  
Позволяет рекурсивно форсированно удалить репозиторий  
**git status**  
Показывает текущее состояние репозитория. В любой непонятной ситуации стоит посмотреть состояние (статус) репозитория, а потом решить, что делать дальше.  
**git add**  
Позволяет подготовить файлы к сохранению. Но сохранения пока не произошло, потому что команда *git add* только запоминает текущее содержимое (контент) файла.  
* git add . или git add -A/--all  
Добавит папку целиком.  
* git add %filename.txt  
Добавит конкретный файл.  


**git commit -m "текст коммита"**  
Команда git add не сохраняет содержимое файлов в репозитории. Само сохранение, или фиксацию состояния файлов, называют коммитом (от англ. commit — «совершать» «фиксировать»). «Сделать коммит» значит сохранить текущую версию файла.  
**git log**  
Позволяет посмотреть историю коммитов.  
**git remote add origin**  
Команде необходимо передать два параметра: имя удалённого репозитория и его URL. С помощью *git remote -v* можно убедиться, что репозитории связаны.  
*git remote add origin git@github.com:Wor1ock/GitPractice.git*  
**git push**  
В первый раз эту команду нужно вызвать с флагом -u и параметрами origin (имя удалённого репозитория) и main или master (название текущей ветки).  
git push -u origin main


# Работа с файлами
**git restore --staged %file**
Удаляет файл из индекса. Полезно, если случайно индексировал временный файл.
**git reset --hard %commitHash**
Позволяет откатить проект к коммиту с указанным хэшем.
**git restore %file**
Позволяет отменить изменения у файла и вернуться к закоммиченной версии.


# Про Git и GitHub  
* Git — это консольный инструмент для работы с локальными и удалёнными репозиториями. Он не связан напрямую ни с одной из платформ и развивается отдельно от них.  
* GitHub — платформа, которая работает с Git и упрощает командное взаимодействие.  


# Про SSH (Secure Shell)  
Это сетевой протокол. Он обеспечивает безопасный обмен данными в сети. С помощью этого протокола можно получать данные с удалённого компьютера или отправлять их на него. Трафик шифруется, поэтому протокол безопасен.  
*ls -la .ssh/* - позволяет проверить наличие ключа  
*ssh-keygen -t ed25519 -C "%userMailOnGitHub"* - позволяет сгенерировать ключ  
*ssh -T git@github.com* - соединяет с сервером GitHub  


# Команды консоли
**clip < %file**   
Копирует содержимое файла в буфер обмена.  
**echo > %file.txt**  
Позволяет создать/заменить файл.  
**type %file.txt**  
Выводит содержимое файла в консоль. Аналогично работает команда *cat*.  

# Хэш коммитов  
Хеширование (от англ. hash, «рубить», «крошить», «мешанина») — это способ преобразовать набор данных и получить их *отпечаток*.  
Информация о коммите — это набор данных: когда был сделан коммит, содержимое файлов в репозитории на момент коммита и ссылка на предыдущий (или родительский) коммит.  
Хеш — основной идентификатор коммита.  
**git log --oneline**  
Позволяет получить сокращённый лог. В сокращённом логе выводятся сокращённые хеши — их можно использовать точно так же, как и полные. Она самостоятельно подберёт оптимальное количество символов.  

# Файл HEAD  
Он указывает на коммит, который сделан последним (то есть на самый новый). Если нужно передать последний коммит, то вместо его хеша можно просто написать слово HEAD — Git поймёт, что вы имели в виду последний коммит.  

# Статусы файлов в Git
Staging area также называют index (англ. «каталог») или cache.  

```mermaid
graph LR;
  untracked -- "git add" --> staged + tracked;
  staged    -- "git commit" --> tracked;
  tracked   -- "изменения" --> modified;
  modified  -- "git add" --> staged;
```