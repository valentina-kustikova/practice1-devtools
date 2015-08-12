# Практика 1. Инструменты разработки программного обеспечения

[![Build Status](https://travis-ci.org/Itseez-NNSU-SummerSchool2015/practice1-devtools.svg)](https://travis-ci.org/Itseez-NNSU-SummerSchool2015/practice1-devtools)

## Цели

__Цель данной работы__ - реализовать набор простых фильтров, а именно фильтра 
сглаживания посредством вычисления среднего по окрестности, линейного фильтра 
с произвольным ядром, медианного фильтра, горизонтального фильтра Собеля. 
В задаче предполагается, что задана двумерная матрица с элементами типа 
`unsigned char`. Также для некоторых фильтров имеется размер ядра, либо само 
ядро фильтра, которое используется для вычисления линейной свертки. По существу 
ядро также является двумерной матрицей.

Проект представляет собой инфраструктуру для проведения практики по освоению
следующих инструментов разработки:

  - Система контроля версий [Git](https://git-scm.com/book/en/v2).
  - [Google Test Framework](https://code.google.com/p/googletest).
  - Утилита [CMake](http://www.cmake.org) для сборки исходных кодов.

## Общая структура проекта

Структура проекта:

  - `3rdparty` - библиотека Google Test.
  - `include` - директория для размещения заголовочных файлов.
  - `samples` - директория для размещения демо-приложений.
  - `src` - директория с исходными кодами.
  - `test` - директория с тестами.
  - `.gitignore` - перечень файлов, игнорируемых Git.
  - `.travis.yml` - конфигурационный файл для системы автоматического 
     тестирования Travis-CI.
  - `CMakeLists.txt` - корневой файл для сборки проекта с помощью CMake.
  - `README.md` - информация о проекте, которую вы сейчас читаете.

В проекте содержатся следующие модули:

  - Общий модуль `matrix` (`./include/matrix.hpp`, `./src/matrix.cpp`),
    содержащий простейшую реализацию класса матриц. Предполагается, что он не
    редактируется при реализации фильтров.
  - Модуль `filters`( `./include/filters.hpp`, `./src/filters_opencv.cpp`, 
    `./src/filters_fabrics.cpp`), содержащий объявление асбстрактного класса
    фильтров и его наследника, который реализует перечисленные фильтры 
    средствами библиотеки OpenCV.
  - Тесты для класса матриц и фильтров (`matrix_test.cpp`, `filters_test.cpp`).
  - Пример использования фильтра (`matrix_sample.cpp`).

## Задачи

__Основные задачи__:

  1. Разработать программную реализацию сглаживания посредством вычисления 
     среднего по окрестности. 
  2. Реализовать линейный фильтр с произвольным ядром. 
  3. Разработать реализацию медианного фильтра.
  4. Реализовать горизонтальный фильтр Собеля.

__Дополнительные задачи__:
  1. Расширить реализацию класса матриц следующими операциями и тестами к ним:
     1. Транспонирование матрицы.
     2. Умножение матриц (в виде перегрузки операции).
     3. Поэлементные операции сложения и вычитания (в виде перегрузки операции).
     4. Методы инициализации фиксированной константой, инициализация единичной 
        матрицы, инициализация диагональной матрицы с фиксированной константой.
     5. Вычисление детерминанта.
  2. Расширить программную реализацию вертикальным фильтром Собеля и 
     морфологическими операциями эрозии и дилатации.

## Общие инструкции по работе с Git

В данном разделе описана типичная последовательность действий, которую 
необходимо выполнить перед тем, как начать работать с проектом. Далее 
для определенности используется репозиторий practice1-devtools.

  1. Создать аккаунт на [github.com](https://github.com), если такой
     отсутствует. Для определенности обозначим аккаунт `github-account`.

  2. Сделать fork репозитория
     <https://github.com/Itseez-NNSU-SummerSchool2015/practice1-devtools> (в
     терминологии Git upstream-репозиторий) к себе в личный профиль с названием
     github-account. В результате будет создана копия репозитория с названием
     <https://github.com/github-account/practice1-devtools>
     (origin-репозиторий).

  3. Клонировать [origin][origin] репозиторий к себе на локальный компьютер,
     воспользовавшись следующей командой:

  ```
  $ git clone https://github.com/github-account/practice1-devtools
  ```

  4. Настроить адрес upstream-репозитория (потребуется при обновлении локальной 
     версии репозитория):

  ```
  $ git remote add upstream https://github.com/Itseez-NNSU-SummerSchool2015/practice1-devtools
  ```

  5. Настроить имя пользователя, из под которого будут выполняться все операции
     с репозиторием Git:

  ```
  $ git config --global user.name "github-account"
  ```

Когда сделан форк репозитория у вас создается по умолчанию единственная ветка 
master. Тем не менее, при решении независимых задач следует создавать рабочие 
ветки. Далее показаны основные команды для управления ветками на примере ветки
`filter-implementation`.

  1. Получить список веток:
  
  ```
  $ git branch [-v]
  # [-v] - список с информацией о последних коммитах
  ```

  2. Создать ветку:

  ```
  $ git branch filter-implementation
  ```

  3. Создать ветку `filter-implementation` и перейти в нее:

  ```
  $ git checkout [-b] filter-implementation
  # [-b] - создание и переход в ветку <branch_name>
  ```
  4. Удалить ветку в локальном репозитории:

  ```
  $ git branch -d <branch_name>
  ```

  5. Удалить ветку на сервере:

  ```
  $ git push [remotename] :[branch]
  ```

При работе с файлами в ветке необходимо управлять изменениями. Далее приведен
перечень основных команд в предположении, что текущей рабочей веткой 
является `filter-implementation`.

  1. Получить список текущих изменений:
  
  ```
  $ git status
  ```
  
  2. Пометить файл как добавленный в текущую ветку репозитория (файл будет
     добавлен после выполнения команды `commit`):
  
  ```
  $ git add [<file_name>]
  # <file_name> - название файла для добавления в commit
    если вместо имени указан символ *, то будут добавлены все новые файлы, 
    расширение которых не указано в .gitignore
  ```

  3. Добавить изменения в текущую ветку локального репозитория:

  ```  
  $ git commit [-m "<message_to_commit>"] [-a]
  # [-a] - автоматически добавляет изменения для существующих на сервере файлов
    без выполнения команды git add
  # [--amend] - перезаписывает последний коммит (используется, если не забыты
    изменения)
  ```

  4. Разместить изменения, которые были добавлены в локальный репозиторий 
     с помощью команды `commit`:

  ```
  $ git push origin [filter-implementation]
  ```

  5. Удалить файлы или директории (!без опции -f для файлов, состояния 
     которых совпадают с состояниям на сервере):

  ```
  $ git rm [-f] [--cached]
  # [-f] - принудительное удаление (файла с измененным состоянием)
  # [--cached] - удаление файлов на сервере, но не в локальной директории
  ```

  6. Переименовать файлы (или 3 команды: `mv`, `git rm`, `git add`):

  ```
  $ git mv <file_from> <file_to>
  ```

Когда в проекте работает несколько человек, то вполне естественная ситуация -
необходимость слияния изменений и разрешение конфликтов.

  1. Слияние (вариант 1):

  ```
  $ git merge upstream/master - слияние изменений из ветки upstream в master
  $ git merge master - слияние изменений из ветки master в текущую ветку
  ```

  2. Слияние (вариант 2):

  ```
  $ git checkout <branch_name> - переход в ветку <branch_name> (при необходимости)
  $ git rebase <base_branch> [<branch_name>] - слияние изменений из ветки <base_branch> в ветку <branch_name>
  $ git checkout <base_branch>
  $ git merge <branch_name>
  ```

  3. Инструмент для разрешения конфликтов:

  ```
  $ git mergetool
  ```

## Сборка проекта с помощью CMake и Microsoft Visual Studio

В данном разделе описана типичная последовательность действий, которую 
необходимо выполнить для сборки проекта с использованием утилиты CMake и 
Microsoft Visual Studio. Далее для определенности выполняется сборка проекта 
из репозитория practice1-devtools.

  1. Сгенерируйте файлы решения и проектов с помощью утилиты CMake. Для этого
     можно воспользоваться графическим приложением, входящим в состав
     утилиты, либо выполнить следующую команду:

  ```
  $ cmake -DOpenCV_DIR="<OpenCVConfig.cmake-path>" -G <generator-name> <path-to-practice1-devtools>
  # <OpenCVConfig.cmake-path> - директория, в которой установлена 
    библиотека OpenCV и расположен файл OpenCVConfig.cmake
  # <generator-name> - название генератора, в случае тестовой
    инфраструктуры участников школы может быть "Visual Studio 10 Win64"
    (если в командной строке набрать cmake без параметров, то можно просмотреть
    список доступных генераторов)
  # <path-to-practice1-devtools> - путь до директории
    practice1-devtools, где лежат исходные коды проекта
  ```

  2. Откройте сгенерированный файл решения `practice1.sln`.

  3. Нажмите правой кнопкой мыши по проекту `ALL_BUILD` и выберите пункт
     `Rebuild` контекстного меню, чтобы собрать решение. В результате все
     бинарные файлы будут размещены в директории
     `practice1-devtools-build/bin`.
        

__Примечание:__ генератор проекта должен совпадать с версией Visual Studio, которая
использовалась при сборке OpenCV. В пакете OpenCV доступны библиотеки, собранные
под VS 2010, 2012, 2013.

## Общая последовательность действий

  1. Сделать форк upstream-репозитория (раздел 
     [Общие инструкции по работе с Git](https://github.com/valentina-kustikova/practice1-devtools#Общие-инструкции-по-работе-с-git)).
  2. Клонировать origin-репозиторий к себе на локальную машину(раздел 
     [Общие инструкции по работе с Git](https://github.com/valentina-kustikova/practice1-devtools#Общие-инструкции-по-работе-с-git)).
  3. Собрать проект и проверить его работоспособность, запустив тесты и пример
     (раздел [Сборка проекта с помощью 
     CMake и MS VS](https://github.com/valentina-kustikova/practice1-devtools#Сборка-проекта-с-помощью-cmake-и-microsoft-visual-studio)).
  4. Создать рабочую ветку для размещения реализаций фильтров (раздел 
     [Общие инструкции по работе с Git](https://github.com/valentina-kustikova/practice1-devtools#Общие-инструкции-по-работе-с-git)).
  5. Создать собственного наследника `FiltersSurname` от абстрактного класса фильтров.
  6. Реализовать последовательно все чисто виртуальные методы базового класса -
     методы фильтрации, перечисленные в разделе 
     [Основные задачи](https://github.com/valentina-kustikova/practice1-devtools#Задачи).
  7. При реализации каждого фильтра следует пересобрать проект и проверить 
     работоспособность тестов. Изменения необходимо постоянно фиксировать, выкладывая
     в рабочую ветку на сервер (раздел 
     [Общие инструкции по работе с Git](https://github.com/valentina-kustikova/practice1-devtools#Общие-инструкции-по-работе-с-git)).
  8. Сделать Pull Request в репозиторий upstream.
  9. Выбрать и решить одну из задач списка 
     [Дополнительные задачи](https://github.com/valentina-kustikova/practice1-devtools#Задачи).
     Необходимо проконтролировать, что задача не была выбрана другими 
     участниками школы. В противном случае, в основной репозиторий попадет
     первая полностью готовая реализация.

## Детальная инструкция по выполнению работы

  1. Проверить, что загруженная версия проекта собирается и успешно выполняются
     все тесты. Для этого необходимо выполнить следующую последовательность
     действий:
     1. Рядом с директорией `practice1-devtools` создайте
        `practice1-devtools-build`. В новой директории будут размещены файлы
        решения и проектов, сгенерированные с помощью CMake.
     2. Перейдите в директорию `practice1-devtools-build`:

      ```
      $ cd ./practice1-devtools-build
      ```

     
     3. Чтобы проверить работоспособность тестов, достаточно запустить
        `practice1_test.exe`. Если все тесты "зеленые", то можно двигаться
        дальше.

  2. Создать файл `filters_SURNAME.cpp` (файл с реализацией в файловой системе) 
     для собственных реализаций фильтров. В качестве шаблона необходимо 
     воспользоваться `filters_opencv.cpp`. Не забудьте после создания 
     файлов в файловой системе запустить еще раз CMake, чтобы подцепить 
     их в решение.

  3. Реализовать в созданном модуле необходимый набор из четырх фильтров 
     (фильтра сглаживания посредством вычисления среднего по окрестности, 
     линейного фильтра с произвольным ядром, медианного фильтра, 
     горизонтального фильтра Собеля). Прототипы методов фильтрации
     изменять нельзя! Не забывайте компилировать решение и проверять
     работоспособность тестов (см. п.7).

  4. После получения каждой стабильной версии не забудьте проверить
      работоспособность тестов и выложить изменения в ветку.

  ```
  $ git status # Получить список текущих изменений
  
  $ git add [<file_name>] # Добавить файл в репозиторий
  # <file_name> - название файла для добавления в commit
    если вместо имени указан символ *, то будут добавлены все новые файлы, 
    расширение которых не указано в .gitignore
  
  $ git commit [-m "<message_to_commit>"] [-a]
  # [-a] - автоматически добавляет изменения для существующих на сервере файлов
    без выполнения команды git add
  # [--amend] - перезаписывает последний коммит (используется, если не забыты
    изменения)
  
  $ git push origin filter-implementation
  ```

  5. Разработать пример использования фильтра. Разместить пример следует в
      модуле `filter_sample_SURNAME.cpp`. В качестве шаблона можно
      воспользоваться примером использования класса матриц.

  6. Не забудьте сделать Pull Request, чтобы проверить работоспособность тестов
      на Travis-CI и позволить преподавателям сделать ревью Вашего кода.

  7. При наличии времени можно расширить реализацию класса матриц операциями 
      и тестами к ним (перечень операций приведен в п.3 раздела "Цели и задачи").
      Также можно реализовать дополнительные фильтры (см. п.4 раздела "Цели 
      и задачи")

<!-- LINKS -->

[origin]: https://github.com/github-account/practice1-devtools
