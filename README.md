## Лабораторная работа №02 Лагов Сергей ИУ8-22

*P.S.: Отчёт делал после полного выполнения лабораторной, поэтому возможны небольшие расхождения с названиями переменных, файлов или чем-то таким*
### Part I

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com)

```
    mkdir lab02.1
    cd lab02.1
    git init
    Initialized empty Git repository in /home/lagov/workspace/projects/lab02.1/.git/
```

`mkdir` - создаём директорию

`cd` - меняем директорию

`git init` - создание локального репозитория

2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдущем шаге

```
    git remote add origin https://github.com/snoreoh/lab02.1.git
    touch README.md
    git add README.md
    git commit -m"added README.md"
    git push origin master
```

`touch` - создание файла

`git add` - добавление в локальный репозиторий

`git commit` - коммитим его

`m` - означает, что дальше будет сообщение, которым надо будет закомментировать коммит

`"added README.md"` - указанное сообщение

`git push origin master` - загружаем его в удалённый репозиторий на ветку `master`

3. Создайте файл `helloworld.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`

```
    touch helloworld.cpp
    cat > helloworld.cpp << EOF
    > #include <iostream>
    > using namespace std;
    > int main()
    > {
    >   cout << "Hello World!" << endl;
    > }
    > EOF
```

`cat` - позволяет редактировать файл

4. Добавьте этот файл в локальную копию репозитория

```
    git add helloworld.cpp
```

5. Закоммитьте изменения с *осмысленным* сообщением

```
    git commit -m"added file.cpp"
```

6. Измените исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя

```
    nano helloworld.cpp
```

- Отредактировал что-то в стиле

```
    #include <iostream>
    using namespace std;
    int main()
    {
      string username;
      cout << "Enter your name: ";
      cin >> username;
      cout << "Hello World from " << username << endl;
    }
```

7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?

```
    git commit -m" updated file.cpp" -a
```

`a` - позволяет нам не загружать файл ещё раз

8. Запуште изменения в удалённый репозиторий

```
    git push origin master
```

9. Проверьте, что история коммитов доступна в удалённый репозитории

- Проверено, всё было доступно

### Part II

**Note:** *Работать продолжайте с теми же репозиториями, что и в первой части задания.*
1. В локальной копии репозитория создайте локальную ветку `patch1`

```
    git сheckout -b patch1
```

`checkout` - перемещение между ветками

`b` - означает, что действие происходит в локальном репозитории

2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`

```
    nano hello_world.cpp
```
- Опять же отредактировал как-то так

```
    #include <iostream>
    #include <string>
    int main()
    {
      std::string username;
      std::cout << "Enter your name: ";
      std::cin >> username;
      std::cout << "Hello World from " << username << std::endl;
    }
```

3. **commit**, **push** локальную ветку в удалённый репозиторий

```
    git commit -m"updated file.cpp" -a
    git push origin patch1
```

4. Проверьте, что ветка `patch1` доступна в удалённый репозитории

- Сделано, доступна

5. Создайте pull-request `patch1 -> master`

- Создан

6. В локальной копии в ветке `patch1` добавьте в исходный код комментарии

- Добавлен

7. **commit**, **push**

```
    nanohello_world.cpp
    git commit -m"specified some details on the code" -a
    git push origin patch1
```

- В редакторе добавляем незначительные изменения по типу комментариев. Как и что я менял, к сожалению, не помню

8. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request

- Проверено, изменения на месте

9. В удалённый репозитории выполните  слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории

```
    git checkout master
    git merge patch1
    git push origin master
    git push origin :patch1
```

`git merge patch1` - производит слияние `patch1` с текущей веткой (в нашем случае с `master`)

`git push origin :patch1` - удаляет ветку `patch1`

10. Локально выполните **pull**

```
    git pull origin master
```

`git pull origin master` - забирает изменения из удаленного репозитория и интегрирует их с изменениями в локальном репозитории

11. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`

```
    git log
```

- Выскакивает длиннющая история коммитов

12. Удалите локальную ветку `patch1`

```
    git branch -d patch1
```

`d` - означает удаление

- Удаляем ветку в локальном репозитории

### Part III

**Note:** *Работать продолжайте с теми же репозиториями, что и в первой части задания.*
1. Создайте новую локальную ветку `patch2`

```
    git checkout -b patch2
```

2. Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`

```
    sudo apt install clang-format
    clang-format -i -style=Mozilla hello_world.cpp
```

`sudo apt install clang-format` - устанавливаем необходимые вещи, как нам в консоли сказала Ubuntu

- Далее делаем то, о чём говорится в задании

3. **commit**, **push**, создайте pull-request `patch2 -> master`

```
    git commit -m"changed code style" -a
    git push origin patch2
```

4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык

- Изменено

5. Убедитесь, что в pull-request появились *конфликтны*
6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**

```
    git checkout master
    git pull origin master
    git checkout patch2
    git rebase master
    nano hello_world.cpp
    git add hello_world.cpp
    git rebase --continue
```

`git rebase master` - попытка объединить изменения, сделанные в одной ветке, с другой

`git rebase --continue` - после устранения конфликта мануально, объединяем изменения одной ветки с другой

7. Сделайте *force push* в ветку `patch2`

```
    git push --force origin patch2
```

`force` - насильный пуш. рискуем потерять чью-то правку

8. Убедитесь, что в pull-request пропали конфликтны

- Пропали

9. Вмёржите pull-request `patch2 -> master`

```
    git checkout master
    git merge patch2
```
