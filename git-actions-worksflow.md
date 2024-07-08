---

Щоб виконати pull request на GitHub та вказати рецензента, виконайте наступні кроки:

1. **Створіть гілку**:
   - Створіть нову гілку для своїх змін.
   - Виконайте зміни в цій гілці.
   - Відправте гілку на віддалений репозиторій.
   
   ```sh
   git checkout -b new-feature-branch
   # Виконайте свої зміни
   git add .
   git commit -m "Опис ваших змін"
   git push origin new-feature-branch
   ```

2. **Виконайте pull request**:
   - Перейдіть на сторінку вашого репозиторію на GitHub.
   - Натисніть на вкладку "Pull requests".
   - Натисніть "New pull request".
   - Виберіть гілку з вашими змінами та гілку, в яку хочете зробити pull request (зазвичай це `main` або `master`).
   - Натисніть "Create pull request".
   - Введіть заголовок та опис для вашого pull request.

3. **Вкажіть рецензента**:
   - Після створення pull request, на правій панелі буде опція "Reviewers".
   - Натисніть на "Reviewers" і виберіть користувача або користувачів, яких хочете призначити рецензентами.

Також, це можна зробити за допомогою інтерфейсу командного рядка GitHub CLI:

1. **Встановіть GitHub CLI**:
   - Якщо у вас ще не встановлено GitHub CLI, встановіть його, слідуючи інструкціям на [GitHub CLI](https://cli.github.com/).

2. **Аутентифікуйтеся в GitHub**:
   - Використовуйте команду `gh auth login` для аутентифікації в GitHub.

3. **Створіть pull request**:
   - Виконайте команду `gh pr create` для створення pull request.
   - Використовуйте опцію `--reviewer` для вказання рецензента.

   ```sh
   gh pr create --base main --head new-feature-branch --title "Ваш заголовок PR" --body "Опис ваших змін" --reviewer <ім'я_користувача>
   ```

Таким чином, ви можете створити pull request і призначити рецензента через веб-інтерфейс GitHub або за допомогою GitHub CLI.

---

Щоб створити нову гілку для своїх змін у Git, виконайте наступні кроки:

1. **Переконайтеся, що ви знаходитесь у вашому локальному репозиторії**:
   - Відкрийте термінал і перейдіть у каталог вашого репозиторію.
   
   ```sh
   cd /шлях/до/вашого/репозиторію
   ```

2. **Оновіть свою поточну гілку**:
   - Зазвичай перед створенням нової гілки корисно переконатися, що у вас останні зміни з віддаленого репозиторію.
   
   ```sh
   git checkout main  # або інша гілка, від якої ви хочете створити нову
   git pull origin main  # витягніть останні зміни з віддаленого репозиторію
   ```

3. **Створіть і перейдіть на нову гілку**:
   - Використовуйте команду `git checkout -b`, щоб створити нову гілку і відразу ж перейти на неї.
   
   ```sh
   git checkout -b new-feature-branch
   ```

4. **Переконайтеся, що ви перебуваєте на новій гілці**:
   - Ви можете перевірити це за допомогою команди `git status` або `git branch`.
   
   ```sh
   git status
   # або
   git branch
   ```

5. **Зробіть зміни у своєму проекті**:
   - Виконайте необхідні зміни у вашому проекті.

6. **Додайте та закомітьте зміни**:
   - Після внесення змін, додайте файли до індексу і закомітьте їх.
   
   ```sh
   git add .
   git commit -m "Опис ваших змін"
   ```

7. **Відправте нову гілку на віддалений репозиторій**:
   - Використовуйте команду `git push` для відправки нової гілки на віддалений репозиторій.
   
   ```sh
   git push origin new-feature-branch
   ```

Тепер ви успішно створили нову гілку, внесли зміни, закомітили їх і відправили на віддалений репозиторій. Ви готові створити pull request для злиття цих змін з основною гілкою.

---

GitHub Actions дозволяє вам автоматизувати робочі процеси, включаючи тестування програмного коду. Щоб налаштувати автоматичне тестування програмного коду за допомогою GitHub Actions, виконайте наступні кроки:

1. **Створіть файл конфігурації GitHub Actions**:
   - Перейдіть у ваш репозиторій на GitHub.
   - Створіть директорію `.github/workflows` у корені вашого репозиторію, якщо вона ще не існує.
   - У цій директорії створіть новий файл, наприклад `ci.yml`.

2. **Налаштуйте робочий процес у файлі `ci.yml`**:
   - У файлі `ci.yml` ви можете визначити робочий процес для тестування вашого коду. Наприклад, для проекту на Python це може виглядати так:

   ```yaml
   name: CI

   on:
     push:
       branches: [ main ]
     pull_request:
       branches: [ main ]

   jobs:
     build:

       runs-on: ubuntu-latest

       steps:
       - name: Checkout repository
         uses: actions/checkout@v2

       - name: Set up Python
         uses: actions/setup-python@v2
         with:
           python-version: '3.8'

       - name: Install dependencies
         run: |
           python -m pip install --upgrade pip
           pip install -r requirements.txt

       - name: Run tests
         run: |
           pytest
   ```

   - Ось що робить цей приклад:
     - Визначає ім'я робочого процесу як `CI`.
     - Виконує робочий процес при кожному пуші або pull request на гілку `main`.
     - Виконує дії на останній версії Ubuntu.
     - Виконує кроки:
       - Перевіряє репозиторій.
       - Налаштовує Python версії 3.8.
       - Встановлює залежності з файлу `requirements.txt`.
       - Запускає тести з допомогою `pytest`.

3. **Збережіть і закомітьте файл `ci.yml`**:
   - Додайте файл у ваш репозиторій, закомітьте зміни і запуште їх у віддалений репозиторій.

   ```sh
   git add .github/workflows/ci.yml
   git commit -m "Add CI workflow"
   git push origin main
   ```

4. **Перевірте статус робочого процесу**:
   - Після пушу змін, перейдіть у вкладку "Actions" у вашому репозиторії на GitHub.
   - Ви побачите список робочих процесів, що були виконані або виконуються. Натисніть на конкретний робочий процес, щоб переглянути деталі виконання.

Тепер ваш код буде автоматично тестуватися при кожному пуші або створенні pull request на гілку `main`. Ви можете налаштовувати і розширювати цей процес відповідно до ваших потреб.

---

Опис формату файлів для GitHub Actions можна знайти в офіційній документації GitHub. Ось основні ресурси, де ви можете знайти інформацію:

1. **Основна документація по GitHub Actions**:
   - [GitHub Actions Documentation](https://docs.github.com/en/actions)

2. **Workflow syntax for GitHub Actions** (синтаксис файлів робочих процесів):
   - [Workflow syntax for GitHub Actions](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions)

3. **Специфікації і приклади різних компонентів файлів робочих процесів**:
   - [Events that trigger workflows](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows): Опис тригерів, які можуть запускати робочі процеси.
   - [Jobs](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#jobs): Опис визначення і налаштування джобів у робочих процесах.
   - [Steps](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#jobsjob_idsteps): Опис кроків, які виконуються у джобах.
   - [Runners](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#jobsjob_idruns-on): Вказівка середовища, де виконуються джоби.

4. **Додаткові довідники і приклади**:
   - [Examples of workflows](https://docs.github.com/en/actions/using-workflows/workflow-examples): Приклади різних робочих процесів для популярних мов програмування і фреймворків.
   - [Creating and using secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets): Як створювати і використовувати секрети в GitHub Actions.

Ці ресурси допоможуть вам зрозуміти структуру файлів робочих процесів для GitHub Actions і налаштувати автоматизацію відповідно до ваших потреб.

---

Текст скрипта, який тестує код програми в GitHub Actions, описується у файлах робочих процесів (workflow files). Ці файли зазвичай розміщуються в каталозі `.github/workflows` вашого репозиторію і мають формат YAML. 

Ось основні кроки для створення скрипта, який тестує код програми:

1. **Створення файлу робочого процесу**:
   - В каталозі вашого репозиторію створіть директорію `.github/workflows`, якщо вона ще не існує.
   - В цій директорії створіть новий файл, наприклад `test.yml`.

2. **Описання робочого процесу у файлі YAML**:
   - В цьому файлі опишіть робочий процес, який буде виконувати тести вашого коду.

Ось приклад базового робочого процесу для тестування Node.js програми:

```yaml
name: Node.js CI

on: [push, pull_request]

jobs:
  build:

    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [12.x, 14.x, 16.x]

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v2
      with:
        node-version: ${{ matrix.node-version }}

    - name: Install dependencies
      run: npm install

    - name: Run tests
      run: npm test
```

У цьому прикладі робочий процес виконує наступні кроки:

1. **Запуск на події push і pull_request**.
2. **Визначення джоба `build`**, який виконується на останній версії Ubuntu.
3. **Стратегія матриці**: Виконує тести на різних версіях Node.js (12.x, 14.x, 16.x).
4. **Кроки (`steps`)**:
   - **Checkout**: Завантажує код з вашого репозиторію.
   - **Setup Node.js**: Налаштовує відповідну версію Node.js.
   - **Install dependencies**: Встановлює залежності за допомогою `npm install`.
   - **Run tests**: Запускає тести за допомогою `npm test`.

### Додаткові ресурси для налаштування тестів:

1. **GitHub Actions: Testing your code**:
   - [Testing your code with GitHub Actions](https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs#running-tests)
   
2. **Examples of workflows**:
   - [GitHub Actions workflow examples](https://docs.github.com/en/actions/using-workflows/workflow-examples)

Ці ресурси допоможуть вам створити і налаштувати власний робочий процес для автоматичного тестування коду вашої програми за допомогою GitHub Actions.

---

В операційній системі `ubuntu-latest` в GitHub Actions для встановлення необхідних інструментів, таких як тестові фреймворки чи бібліотеки, ви можете використовувати різні інструменти пакетного менеджменту та команди. У цьому контексті, для тестування коду зазвичай використовуються команди пакетних менеджерів, таких як `apt`, `npm`, `pip`, тощо, залежно від середовища та мови програмування.

Ось приклади, як можна встановити тестові інструменти для різних мов програмування:

### Для Node.js (JavaScript/TypeScript)
Використовуючи `npm` для встановлення тестових пакетів:

```yaml
name: Node.js CI

on: [push, pull_request]

jobs:
  build:

    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [12.x, 14.x, 16.x]

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v2
      with:
        node-version: ${{ matrix.node-version }}

    - name: Install dependencies
      run: npm install

    - name: Run tests
      run: npm test
```

### Для Python
Використовуючи `pip` для встановлення тестових пакетів:

```yaml
name: Python application

on: [push, pull_request]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: '3.x'

    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt

    - name: Run tests
      run: |
        pytest
```

### Для Java
Використовуючи `maven` для запуску тестів:

```yaml
name: Java CI

on: [push, pull_request]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Set up JDK 11
      uses: actions/setup-java@v2
      with:
        java-version: '11'

    - name: Build with Maven
      run: mvn -B package --file pom.xml

    - name: Run tests
      run: mvn test
```

### Для C# (.NET)
Використовуючи `dotnet` для запуску тестів:

```yaml
name: .NET

on: [push, pull_request]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Setup .NET Core
      uses: actions/setup-dotnet@v2
      with:
        dotnet-version: '3.1.x'

    - name: Install dependencies
      run: dotnet restore

    - name: Build
      run: dotnet build --no-restore

    - name: Run tests
      run: dotnet test --no-build --verbosity normal
```

### Для загальних системних команд
Використовуючи `apt` для встановлення пакетів:

```yaml
name: Install system dependencies

on: [push, pull_request]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Install dependencies
      run: sudo apt-get update && sudo apt-get install -y <package-name>

    - name: Run tests
      run: <command-to-run-tests>
```

### Короткий підсумок
Для встановлення тестових інструментів і виконання тестів на `ubuntu-latest` у GitHub Actions, вам потрібно додати відповідні кроки у ваш робочий процес (workflow), що описаний у файлі YAML у каталозі `.github/workflows`. Залежно від вашої мови програмування і середовища, ви можете використовувати різні пакетні менеджери та інструменти для встановлення залежностей і запуску тестів.

---

Для встановлення власної програми тестування в операційну систему `ubuntu-latest` в GitHub Actions, вам потрібно створити файл конфігурації для робочого процесу (workflow) у форматі YAML. Цей файл міститиме кроки для завантаження, встановлення та запуску вашої програми тестування. Нижче наведено приклад того, як це можна зробити.

Припустимо, ваша програма тестування розташована у вашому репозиторії та має скрипт установки.

### Приклад GitHub Actions Workflow для встановлення та запуску власної програми тестування

1. Створіть файл `.github/workflows/test.yml` у вашому репозиторії.
2. Додайте до цього файлу наступний вміст, налаштувавши його відповідно до ваших потреб:

```yaml
name: CI

on: [push, pull_request]

jobs:
  test:

    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: '3.x'

    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt

    - name: Install custom test program
      run: |
        chmod +x install_my_test_program.sh
        ./install_my_test_program.sh

    - name: Run custom tests
      run: |
        ./my_test_program --run-tests
```

### Пояснення кроків

1. **Checkout repository**: Використовуємо офіційну дію `actions/checkout`, щоб клонувати репозиторій до середовища виконання.
2. **Set up Python**: Налаштовуємо Python середовище, якщо ваша програма залежить від Python. Якщо ваша програма написана іншою мовою, ви можете пропустити цей крок або налаштувати середовище відповідно до вашої мови.
3. **Install dependencies**: Встановлюємо залежності вашої програми. Якщо ваша програма використовує інший пакетний менеджер, замініть ці команди на відповідні.
4. **Install custom test program**: Виконуємо скрипт установки вашої програми тестування. Ви можете змінити цей крок залежно від способу установки вашої програми.
5. **Run custom tests**: Запускаємо вашу програму тестування.

### Приклад скрипта установки (`install_my_test_program.sh`)

```sh
#!/bin/bash

# Приклад встановлення залежностей вашої програми
sudo apt-get update
sudo apt-get install -y some-dependency

# Встановлення вашої програми
# Припустимо, що ваш код містить компіляцію або інші дії
make install

# Або якщо ваша програма є скриптом, переконайтеся, що він має права на виконання
chmod +x my_test_program
```

### Виконання тестів

У вашому скрипті для запуску тестів (`./my_test_program --run-tests`) ви можете вказати команду для запуску ваших тестів. Це може бути будь-яка команда, яка запускає ваші тести та повертає відповідний код виходу залежно від результатів тестів.

Цей приклад є загальним шаблоном і може бути налаштований відповідно до специфічних вимог вашої програми та середовища.

---

Файл `install_my_test_program.sh` має бути розміщений у вашому репозиторії. Зазвичай, його кладуть у кореневу директорію репозиторію, щоб було зручно посилатися на нього з файлу GitHub Actions. Ось більш детальний приклад:

1. Структура вашого репозиторію може виглядати так:
    ```
    .
    ├── .github
    │   └── workflows
    │       └── test.yml
    ├── install_my_test_program.sh
    ├── my_test_program
    ├── Makefile
    ├── requirements.txt
    └── ...
    ```

2. Зміст файлу `install_my_test_program.sh`:
    ```sh
    #!/bin/bash

    # Приклад встановлення залежностей вашої програми
    sudo apt-get update
    sudo apt-get install -y some-dependency

    # Встановлення вашої програми
    # Припустимо, що ваш код містить компіляцію або інші дії
    make install

    # Або якщо ваша програма є скриптом, переконайтеся, що він має права на виконання
    chmod +x my_test_program
    ```

3. Зміст файлу `.github/workflows/test.yml`:
    ```yaml
    name: CI

    on: [push, pull_request]

    jobs:
      test:

        runs-on: ubuntu-latest

        steps:
        - name: Checkout repository
          uses: actions/checkout@v2

        - name: Set up Python
          uses: actions/setup-python@v2
          with:
            python-version: '3.x'

        - name: Install dependencies
          run: |
            python -m pip install --upgrade pip
            pip install -r requirements.txt

        - name: Install custom test program
          run: |
            chmod +x install_my_test_program.sh
            ./install_my_test_program.sh

        - name: Run custom tests
          run: |
            ./my_test_program --run-tests
    ```

Цей приклад передбачає, що скрипт `install_my_test_program.sh` знаходиться в кореневій директорії репозиторію. Файл конфігурації GitHub Actions (`test.yml`) посилається на цей скрипт для встановлення вашої програми тестування. Ви можете налаштувати шляхи і команди відповідно до структури вашого проєкту та потреб.

---

У YAML-файлах для GitHub Actions символ `|` використовується для позначення блоку тексту, який буде збережено з новими рядками. Це дозволяє писати багато рядків коду або тексту в одному значенні ключа. В контексті файлів конфігурації GitHub Actions цей символ часто застосовується для написання скриптів або команд, які потрібно виконати.

Ось приклад зі значенням `run` в YAML-файлі GitHub Actions:

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: '3.x'

    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt

    - name: Install custom test program
      run: |
        chmod +x install_my_test_program.sh
        ./install_my_test_program.sh

    - name: Run custom tests
      run: |
        ./my_test_program --run-tests
```

В цьому прикладі блок `run: |` дозволяє писати багато рядків команд, які будуть виконані послідовно. Це еквівалентно написанню команд у скрипті оболонки. Нові рядки зберігаються як частина значення і виконуються як є.

Якщо `|` не використовувати, і команди написати в один рядок, їх потрібно було б розділяти спеціальними символами, такими як `&&` для команд оболонки.

```yaml
- name: Install dependencies
  run: python -m pip install --upgrade pip && pip install -r requirements.txt
```

---

Щоб замінити тестування на запуск простого Bash-скрипта "Hello World" в GitHub Actions, ви можете змінити конфігураційний файл YAML наступним чином:

```yaml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Run Hello World script
      run: |
        echo "Hello World"
```

Цей файл робить наступне:
1. Визначає роботу, яка запускається при пушах або запитах на злиття в гілку `main`.
2. Вказує, що робота буде виконуватись на останній версії Ubuntu.
3. Виконує кроки:
   - Клонування репозиторію з GitHub.
   - Запуск Bash-команди `echo "Hello World"`, яка виведе "Hello World" в лог.

Якщо у вас є окремий Bash-скрипт, який ви хочете запустити, наприклад, `hello_world.sh`, ви можете додати його в репозиторій і змінити конфігурацію таким чином:

```yaml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Make hello_world.sh executable
      run: chmod +x hello_world.sh

    - name: Run Hello World script
      run: ./hello_world.sh
```

У цьому випадку `hello_world.sh` повинен виглядати приблизно так:

```bash
#!/bin/bash
echo "Hello World"
```

Не забудьте зробити скрипт виконуваним за допомогою команди `chmod +x hello_world.sh` перед комітом у репозиторій.

---

Щоб налаштувати GitHub Actions для виконання завдань лише на гілці `test`, ви можете змінити конфігураційний файл YAML наступним чином:

```yaml
name: CI

on:
  push:
    branches: [ test ]
  pull_request:
    branches: [ test ]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Make hello_world.sh executable
      run: chmod +x hello_world.sh

    - name: Run Hello World script
      run: ./hello_world.sh
```

Цей файл налаштовує GitHub Actions таким чином:
1. Виконує завдання тільки при пушах або запитах на злиття (pull request) в гілку `test`.
2. Вказує, що робота буде виконуватись на останній версії Ubuntu.
3. Виконує наступні кроки:
   - Клонування репозиторію з GitHub.
   - Змінює права на виконання для скрипта `hello_world.sh`.
   - Запускає скрипт `hello_world.sh`.

Ось кроки, як це зробити:
1. Створіть новий файл `.github/workflows/ci.yml` (або змініть існуючий) у вашому репозиторії.
2. Додайте або замініть вміст файлу на наведений вище приклад.
3. Переконайтесь, що скрипт `hello_world.sh` знаходиться в кореневій директорії вашого репозиторію і має наступний вміст:

```bash
#!/bin/bash
echo "Hello World"
```

4. Зробіть цей файл виконуваним, якщо це ще не зроблено:
   ```bash
   chmod +x hello_world.sh
   ```

5. Закомітьте і запуште ці зміни в гілку `test`.

Після цього GitHub Actions буде запускати ваш скрипт тільки при пушах або запитах на злиття в гілку `test`.

---

Для того щоб побачити вивід скрипта `hello_world.sh` під час його виконання через GitHub Actions, вам необхідно звернутися до вкладки "Actions" у вашому репозиторії GitHub:

1. **Перейдіть в GitHub репозиторій**: Відкрийте свій репозиторій на GitHub.

2. **Оберіть вкладку "Actions"**: У верхній частині сторінки репозиторію оберіть вкладку "Actions". Це відкриє сторінку зі списком ваших workflows (робочих процесів).

3. **Оберіть відповідний workflow**: Знайдіть і оберіть workflow, який ви хочете перевірити. У вашому випадку це буде workflow, який ви налаштували для тестування скрипта `hello_world.sh`.

4. **Перегляньте вивід дій**: У вкладці "Jobs" ви побачите список кроків (steps), які виконує ваш workflow. Кожен крок має кнопку "View logs", за допомогою якої можна переглянути вивід цього конкретного кроку.

5. **Перегляньте вивід скрипта**: Оберіть крок, який відповідає виконанню скрипта `hello_world.sh`. У вікні деталей кроку ви побачите весь вивід, який скрипт вивів під час свого виконання.

Це дасть вам можливість побачити всі виведені дані з вашого скрипта, які відображаються в GitHub Actions.

---

Щоб побачити текст, який виводить скрипт `hello_world.sh` під час його виконання через командний рядок (термінал) у вашій операційній системі, ось що ви можете зробити:

1. **Відкрийте термінал**: Запустіть термінал на вашій операційній системі (наприклад, Terminal у macOS або Linux, Command Prompt у Windows).

2. **Перейдіть у директорію зі скриптом**: Використовуйте команду `cd` для переходу у директорію, де знаходиться ваш скрипт `hello_world.sh`.

   ```bash
   cd /шлях/до/директорії/з/скриптом
   ```

3. **Виконайте скрипт**: Введіть команду для виконання скрипта `hello_world.sh`. Приклад для Linux чи macOS:

   ```bash
   ./hello_world.sh
   ```

   Для Windows (якщо ви використовуєте Git Bash або інший термінал):

   ```bash
   bash hello_world.sh
   ```

4. **Перегляньте вивід**: Після виконання скрипта ви побачите весь вивід (текст), який він вивів у терміналі.

Якщо ви хочете, щоб якесь інше середовище, таке як GitHub Actions, виконувало цей скрипт, вам потрібно буде перевірити вивід у веб-інтерфейсі GitHub Actions, як я пояснив у попередній відповіді.

---

Вкладка "jobs" зазвичай знаходиться в розділі GitHub Actions для конкретного workflow файлу. Ось як можна знайти цю вкладку:

1. **Увійдіть у свій репозиторій на GitHub**: Зайдіть на сторінку вашого репозиторію на GitHub.

2. **Перейдіть до вкладки Actions**: У верхньому меню вашого репозиторію знайдіть вкладку "Actions" і клацніть на неї.

3. **Виберіть workflow**: Оберіть потрібний workflow зі списку на лівій стороні екрану. Якщо у вас є кілька workflow файлів, виберіть той, де ви хочете переглянути вкладку "jobs".

4. **Перейдіть до вкладки "jobs"**: Після вибору конкретного workflow файлу, ви побачите верхній рядок з різними вкладками, такими як "Overview", "Jobs", "Run workflow", і т.д. Клацніть на вкладку "Jobs".

Ця вкладка показує вам інформацію про виконані робочі процеси (jobs) для обраного workflow файлу, включаючи їхні стани, часи виконання та інші важливі дані, пов'язані з виконанням вашого GitHub Actions workflow.

---

Можливо, що ви не бачите цих вкладок через кілька потенційних причин:

1. **Відсутність налаштованого GitHub Actions**: Якщо ваш репозиторій не містить конфігурацій для GitHub Actions (файлу `.github/workflows/`), вкладка "Actions" може бути неактивною або пустою. У цьому випадку потрібно створити або додати конфігураційні файли для GitHub Actions.

2. **Відсутність доступу**: Якщо у вас обмежений доступ до репозиторію або вам не надані права на перегляд вкладок "Actions", ви не зможете бачити інформацію про виконані робочі процеси (jobs).

3. **Проблеми з відображенням**: Іноді відображення вкладок може бути порушено через проблеми з кешуванням браузера чи інші технічні проблеми.

Щоб упевнитися, що ви можете бачити вкладки "Overview", "Jobs", "Run workflow" для свого GitHub Actions workflow, переконайтеся в наступному:

- Ваш репозиторій має налаштований файл для GitHub Actions у каталозі `.github/workflows/`.
- Ви маєте достатні права доступу до цього репозиторію для перегляду вкладок "Actions".
- Перевірте, чи не виникли технічні проблеми з відображенням сторінки; можливо, спробуйте перезавантажити сторінку або очистити кеш браузера.

Якщо у вас є конкретні проблеми з відображенням вкладок, може бути корисно перевірити документацію GitHub або звернутися до підтримки GitHub для допомоги.

---

У файлах конфігурації для GitHub Actions, ключове слово `uses` використовується для визначення сторонніх дій (actions) або інших робочих процесів, які мають бути виконані. Воно вказує на репозиторій і версію дії, яку потрібно використовувати. 

Ось кілька прикладів того, як `uses` може бути використано:

### Використання сторонньої дії з GitHub Marketplace
```yaml
name: CI

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Set up Node.js
      uses: actions/setup-node@v2
      with:
        node-version: '14'
    - run: npm install
    - run: npm test
```
У цьому прикладі `uses: actions/checkout@v2` і `uses: actions/setup-node@v2` означають, що будуть використовуватись дії з GitHub Marketplace, які перевіряють код і налаштовують Node.js відповідно.

### Використання дії з поточного репозиторію
Якщо у вас є дія в тому ж репозиторії, де знаходиться ваш workflow, ви можете використовувати її таким чином:
```yaml
steps:
- name: Run a local action
  uses: ./path/to/your/action
```
У цьому випадку `./path/to/your/action` - це відносний шлях до вашої дії всередині репозиторію.

### Використання дії з іншого репозиторію
Ви також можете використовувати дію з іншого репозиторію:
```yaml
steps:
- name: Use a third-party action
  uses: owner/repository@version
```
У цьому випадку `owner/repository@version` вказує на конкретний репозиторій і версію дії.

### Приклад повного робочого процесу
```yaml
name: CI

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Use a third-party action
      uses: owner/repository@v1.0.0
    - name: Run a script
      run: echo "Hello, World!"
```
У цьому прикладі спочатку виконується дія `actions/checkout@v2` для перевірки коду з репозиторію, потім виконується стороння дія `owner/repository@v1.0.0`, і нарешті, виконується простий скрипт `echo "Hello, World!"`.

Ключ `uses` дуже потужний інструмент, який дозволяє використовувати вже існуючі дії з GitHub Marketplace або з вашого власного репозиторію для створення складних і гнучких робочих процесів.

---

Так, скрипти, які виконуються в межах GitHub Actions, можуть записувати дані у файли в репозиторії. Однак, для того, щоб ці зміни були закомічені назад у репозиторій, вам потрібно належним чином налаштувати дії GitHub Actions для коміту і пушу цих змін.

Ось приклад workflow, який створює файл, записує у нього дані та закомічує ці зміни назад у репозиторій:

### Приклад workflow:

```yaml
name: Commit changes

on: 
  push:
    branches:
      - main

jobs:
  commit-changes:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Create a new file
      run: echo "Hello, World!" > newfile.txt

    - name: Configure git
      run: |
        git config --global user.name 'github-actions[bot]'
        git config --global user.email 'github-actions[bot]@users.noreply.github.com'

    - name: Add changes to git
      run: git add .

    - name: Commit changes
      run: |
        git commit -m "Add newfile.txt"
        git push
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### Пояснення:

1. **Checkout repository**: Завантажує репозиторій для роботи з ним.
2. **Create a new file**: Створює новий файл і записує в нього "Hello, World!".
3. **Configure git**: Налаштовує git з іменем та електронною поштою для коміту.
4. **Add changes to git**: Додає новий файл до git.
5. **Commit changes**: Виконує коміт з повідомленням "Add newfile.txt" і пушить зміни назад у репозиторій. Використовує `GITHUB_TOKEN` для аутентифікації.

Цей приклад демонструє базовий спосіб, як можна створювати або змінювати файли та закомічувати їх назад у репозиторій за допомогою GitHub Actions. Використовуйте `GITHUB_TOKEN`, який автоматично надається для робочого процесу і має потрібні дозволи для виконання комітів.

---

Щоб викликати свій скрипт лише при пуші файла з конкретним іменем у GitHub Actions, ви можете використовувати розділ `paths` у вашому workflow. Це дозволяє вам обмежити запуск робочого процесу до певних файлів або директорій.

Ось приклад workflow, який запускається лише при пуші файла з ім'ям `specific-file.txt`:

```yaml
name: Run script on specific file push

on:
  push:
    paths:
      - specific-file.txt

jobs:
  run-script:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Run my script
      run: ./my_script.sh
```

### Пояснення:

1. **on.push.paths**: Ця секція визначає, що workflow повинен запускатися лише при пуші змін у файл `specific-file.txt`.
2. **jobs.run-script**: Описує роботу, яка виконується на останній версії Ubuntu.
3. **steps**:
   - **Checkout repository**: Завантажує репозиторій для роботи з ним.
   - **Run my script**: Виконує ваш скрипт `my_script.sh`.

З таким налаштуванням ваш workflow буде запускатися лише тоді, коли файл з іменем `specific-file.txt` змінюється і пушиться в репозиторій.

---

Щоб викликати свій скрипт лише при пуші будь-якого файла в конкретну директорію у GitHub Actions, ви можете використовувати розділ `paths` у вашому workflow. Це дозволяє вам обмежити запуск робочого процесу до змін у певних директоріях.

Ось приклад workflow, який запускається лише при пуші будь-якого файла у директорію з ім'ям `my-directory`:

```yaml
name: Run script on push to specific directory

on:
  push:
    paths:
      - my-directory/**

jobs:
  run-script:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Run my script
      run: ./my_script.sh
```

### Пояснення:

1. **on.push.paths**: Ця секція визначає, що workflow повинен запускатися лише при пуші змін у файли в директорії `my-directory` та її піддиректорії (завдяки використанню `**`).
2. **jobs.run-script**: Описує роботу, яка виконується на останній версії Ubuntu.
3. **steps**:
   - **Checkout repository**: Завантажує репозиторій для роботи з ним.
   - **Run my script**: Виконує ваш скрипт `my_script.sh`.

З таким налаштуванням ваш workflow буде запускатися лише тоді, коли будь-який файл у директорії `my-directory` змінюється і пушиться в репозиторій.

---

В GitHub Actions символи `**` є частиною шаблону (pattern) для шляхів файлів і директорій, які використовуються для визначення умов запуску робочих процесів (workflows).

### Пояснення:

- **`*`**: Замінює будь-яку кількість символів у назві файлу чи директорії, за винятком символа `/`. 
- **`**`**: Замінює будь-яку кількість символів, включаючи `/`. Це дозволяє включити всі файли і піддиректорії в заданій директорії.

### Приклади:

1. **`my-directory/*`**: Включає всі файли безпосередньо в директорії `my-directory`, але не включає файли у піддиректоріях.
2. **`my-directory/**`**: Включає всі файли та піддиректорії в директорії `my-directory` на всіх рівнях вкладеності.

### Приклад у контексті GitHub Actions:

```yaml
on:
  push:
    paths:
      - my-directory/**
```

У цьому прикладі `my-directory/**` означає:

- Робочий процес буде запускатися при пуші змін у будь-який файл або піддиректорію в `my-directory`.
- Це включає файли у будь-якій вкладеній піддиректорії, незалежно від рівня вкладеності.

Таким чином, `**` дозволяє охопити всі файли і піддиректорії в заданій директорії, роблячи умову запуску максимально широкою для цієї директорії.

---

Використання одного або двох зірочок (`*` або `**`) в шаблонах шляхів в GitHub Actions має різні значення і застосовується залежно від того, які файли чи директорії ви хочете охопити.

### Різниця між `*` і `**`

1. **Одна зірочка (`*`)**:
   - Замінює будь-яку кількість символів у назві файлу чи директорії, за винятком символа `/`.
   - Використовується для включення файлів лише в одній конкретній директорії.
   
   **Приклад**:
   ```yaml
   on:
     push:
       paths:
         - my-directory/*
   ```
   У цьому прикладі `my-directory/*` означає, що робочий процес буде запускатися при пуші змін у будь-який файл безпосередньо в директорії `my-directory`, але не включає файли у піддиректоріях.

2. **Дві зірочки (`**`)**:
   - Замінює будь-яку кількість символів, включаючи `/`.
   - Використовується для включення файлів у будь-якій піддиректорії, незалежно від рівня вкладеності.
   
   **Приклад**:
   ```yaml
   on:
     push:
       paths:
         - my-directory/**
   ```
   У цьому прикладі `my-directory/**` означає, що робочий процес буде запускатися при пуші змін у будь-який файл або піддиректорію в `my-directory`, включаючи файли на всіх рівнях вкладеності.

### Чому тут не одна зірочка (`*`)

Якщо ви хочете охопити всі файли і піддиректорії в заданій директорії на всіх рівнях вкладеності, вам потрібно використовувати дві зірочки (`**`). 

**Наприклад**:
```yaml
on:
  push:
    paths:
      - my-directory/**
```
Це означає, що робочий процес буде запускатися при пуші змін у будь-який файл або піддиректорію в `my-directory` на будь-якому рівні вкладеності.

Якщо ви використовували б одну зірочку (`*`), то робочий процес запускався б тільки при зміні файлів безпосередньо в `my-directory` і не включав би зміни в піддиректоріях.

**Приклад з однією зірочкою**:
```yaml
on:
  push:
    paths:
      - my-directory/*
```
Це означає, що робочий процес буде запускатися тільки при пуші змін у файли безпосередньо в `my-directory`, але не включатиме зміни в будь-якій піддиректорії.

Отже, використання двох зірочок (`**`) забезпечує більш широкий діапазон включення файлів і піддиректорій, що може бути необхідним для певних сценаріїв.

---

Зберігати результати роботи запущеного скрипта можна декількома способами, залежно від того, куди ви хочете зберегти ці результати. Ось кілька поширених підходів:

### 1. Збереження у файл
Ви можете перенаправити вивід скрипта у файл, використовуючи команду `>` для перезапису файлу або `>>` для додавання до файлу:

```bash
./my_script.sh > output.txt   # Перезаписати файл
./my_script.sh >> output.txt  # Додати до файлу
```

### 2. Збереження у змінну
Результати роботи скрипта можна зберегти у змінну для подальшого використання у скрипті:

```bash
output=$(./my_script.sh)
echo "$output"
```

### 3. Збереження у базу даних
Ви можете налаштувати скрипт для запису результатів у базу даних. Наприклад, використовуючи команду `mysql` для MySQL:

```bash
mysql -u username -p password -e "INSERT INTO results (output) VALUES ('$output');"
```

### 4. Використання системи логування
Ви можете налаштувати скрипт для запису логів за допомогою системних інструментів логування, таких як `logger`, або використовувати власні механізми логування:

```bash
logger "This is a log message from my_script.sh"
```

### 5. Використання інструментів для зберігання результатів тестування
Якщо ви використовуєте інструменти CI/CD, такі як GitHub Actions, Jenkins, або GitLab CI, ви можете зберігати результати у вигляді артефактів або спеціальних файлів звітів.

**Приклад для GitHub Actions:**

```yaml
name: Run my script and save output

on: [push]

jobs:
  run-script:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Run script
      run: ./my_script.sh > output.txt

    - name: Upload output
      uses: actions/upload-artifact@v2
      with:
        name: output
        path: output.txt
```

### 6. Збереження в хмарне сховище
Ви можете налаштувати скрипт для збереження результатів у хмарні сховища, такі як AWS S3, Google Cloud Storage, або Azure Blob Storage:

```bash
aws s3 cp output.txt s3://my-bucket/output.txt
```

Кожен із цих методів має свої переваги та підходить для різних випадків використання. Виберіть той, який найкраще відповідає вашим потребам.

---

У GitHub Actions можна зберегти результати роботи скрипта, використовуючи артефакти. Артефакти дозволяють зберігати файли, створені під час виконання робочого процесу, і робити їх доступними для завантаження або використання в інших частинах робочого процесу.

Ось приклад того, як зберегти результати роботи скрипта у GitHub Actions:

### 1. Створіть GitHub Actions робочий процес

Створіть файл `.github/workflows/save_script_output.yml` у вашому репозиторії з таким вмістом:

```yaml
name: Run script and save output

on: [push]

jobs:
  run-script:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Run script
      run: |
        echo "Running script..."
        ./my_script.sh > output.txt
        cat output.txt

    - name: Upload output as artifact
      uses: actions/upload-artifact@v2
      with:
        name: script-output
        path: output.txt
```

### 2. Створіть скрипт

Створіть файл `my_script.sh` у кореневій директорії вашого репозиторію з таким вмістом:

```bash
#!/bin/bash

echo "Hello, World!"
```

Не забудьте надати скрипту права на виконання:

```bash
chmod +x my_script.sh
```

### 3. Пояснення робочого процесу

- **name: Run script and save output**: Назва робочого процесу.
- **on: [push]**: Робочий процес запускається при кожному пуші до репозиторію.
- **jobs**: Визначає роботу в робочому процесі.
  - **run-script**: Ім'я роботи.
    - **runs-on: ubuntu-latest**: Вказує, що робота повинна запускатися на останній версії Ubuntu.
    - **steps**: Кроки для виконання роботи.
      - **Checkout repository**: Завантажує код репозиторію.
      - **Run script**: Запускає ваш скрипт `my_script.sh` і зберігає його вивід у файл `output.txt`.
      - **Upload output as artifact**: Завантажує файл `output.txt` як артефакт з ім'ям `script-output`.

### 4. Перегляд артефактів

Після того, як робочий процес завершиться, ви зможете побачити завантажені артефакти на сторінці виконання робочого процесу в GitHub Actions. 

1. Перейдіть на вкладку "Actions" у вашому репозиторії.
2. Виберіть відповідне виконання робочого процесу.
3. Перейдіть на вкладку "Summary" або "Artifacts", де ви знайдете посилання на завантажений артефакт `script-output`.

Це дозволить вам завантажити та переглянути результат роботи вашого скрипта.

---

Крім збереження результатів роботи скрипта як артефактів, існують інші способи отримання результатів виконання скрипта в GitHub Actions:

1. **Вивід в консоль**: Вивід результатів у консольний лог під час виконання робочого процесу. Ви можете переглянути ці результати на сторінці виконання робочого процесу в GitHub.

2. **Використання GitHub Actions Outputs**: Ви можете зберігати результати виводу як змінні, які можуть бути використані в інших кроках робочого процесу.

### Приклад використання виводу в консоль

```yaml
name: Run script and output to console

on: [push]

jobs:
  run-script:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Run script
      run: |
        echo "Running script..."
        ./my_script.sh
```

### Приклад використання GitHub Actions Outputs

```yaml
name: Run script and use output

on: [push]

jobs:
  run-script:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Run script and set output
      id: run-script
      run: |
        echo "Running script..."
        result=$(./my_script.sh)
        echo "::set-output name=script_result::$result"

    - name: Use script output
      run: echo "The result of the script is: ${{ steps.run-script.outputs.script_result }}"
```

У цьому прикладі ми використовуємо `::set-output` для збереження виводу скрипта як змінної `script_result`. Цю змінну можна використовувати в інших кроках робочого процесу.

### Використання секретів та змінних оточення

Іноді результати роботи скрипта можуть бути конфіденційними або використовуватися для подальших дій. У такому випадку ви можете використовувати секрети та змінні оточення.

```yaml
name: Run script and use environment variables

on: [push]

jobs:
  run-script:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Run script and set environment variable
      run: |
        echo "Running script..."
        result=$(./my_script.sh)
        echo "RESULT=$result" >> $GITHUB_ENV

    - name: Use script output from environment variable
      run: echo "The result of the script is: ${{ env.RESULT }}"
```

У цьому прикладі ми використовуємо `$GITHUB_ENV` для збереження результату в змінну оточення `RESULT`, яку потім можна використовувати в інших кроках.

### Використання зовнішніх сервісів

Ви можете надсилати результати роботи скрипта на зовнішні сервіси, такі як вебхуки, API серверів, або в чат-системи (наприклад, Slack).

```yaml
name: Run script and send result to webhook

on: [push]

jobs:
  run-script:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Run script
      run: |
        echo "Running script..."
        result=$(./my_script.sh)
        curl -X POST -H "Content-Type: application/json" -d "{\"text\": \"The result of the script is: $result\"}" https://hooks.example.com/webhook
```

У цьому прикладі ми надсилаємо результат скрипта на вебхук.

Всі ці методи допоможуть вам отримати результати роботи скрипта виконаного в GitHub Actions відповідно до ваших потреб.

---

У GitHub Actions ви можете завантажити файли, створені скриптом під час виконання робочого процесу, використовуючи артефакти. Артефакти - це файли або набори файлів, які можуть бути збережені та використані для подальшої обробки або розгортання.

Ось приклад, як ви можете зберегти файли як артефакти в GitHub Actions:

```yaml
name: Build and Deploy

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Build artifact
      run: |
        # Ваші команди для створення файлів
        echo "Hello, world!" > output.txt
        mkdir -p artifacts
        cp output.txt artifacts/

    - name: Upload artifact
      uses: actions/upload-artifact@v2
      with:
        name: my-artifact
        path: artifacts/
```

У цьому прикладі:

1. Крок `Build artifact` виконує команди, які створюють файли. У даному випадку, це створення файлу `output.txt`.
2. Крок `Upload artifact` використовує дію `actions/upload-artifact@v2` для завантаження артефактів. Всі файли з директорії `artifacts/` будуть завантажені як артефакти з ім'ям `my-artifact`.

Після виконання цього робочого процесу, ви зможете знайти завантажені артефакти на вкладці "Artifacts" на сторінці виконання вашого робочого процесу в GitHub. Вони будуть доступні для завантаження або подальшого використання.

---

Для завантаження артефактів у режимі командного рядка (CLI) з GitHub Actions, ви можете використовувати GitHub API разом із інструментами для роботи з HTTP-запитами, наприклад `curl` або `wget`. Ось приклад як це можна зробити за допомогою `curl`:

1. **Отримання інформації про робочий процес:**
   Спочатку вам потрібно знати ідентифікатор вашого робочого процесу та ідентифікатор артефакту. Це можна знайти на сторінці виконання робочого процесу у GitHub.

2. **Завантаження артефакту за допомогою `curl`:**
   Ви можете виконати HTTP-запит до GitHub API, щоб отримати артефакт. Ось команда `curl`, яка завантажує артефакт з GitHub Actions:

   ```bash
   # Замініть значення змінних на свої
   GITHUB_TOKEN=ваш_токен
   OWNER=власник
   REPO=репозиторій
   RUN_ID=ідентифікатор_робочого_процесу
   ARTIFACT_NAME=ім'я_артефакту

   curl \
     -sSL \
     -H "Authorization: token $GITHUB_TOKEN" \
     -H "Accept: application/vnd.github.v3.raw" \
     "https://api.github.com/repos/$OWNER/$REPO/actions/runs/$RUN_ID/artifacts/$ARTIFACT_NAME/zip" \
     -o $ARTIFACT_NAME.zip
   ```

   Пояснення параметрів `curl`:
   - `-sSL`: Вказує `curl` утилізувати SSL і не виводити повідомлення про прогрес.
   - `-H "Authorization: token $GITHUB_TOKEN"`: Додає заголовок авторизації з вашим персональним токеном GitHub.
   - `-H "Accept: application/vnd.github.v3.raw"`: Вказує GitHub використовувати формат даних `raw` для артефактів.
   - `"https://api.github.com/repos/$OWNER/$REPO/actions/runs/$RUN_ID/artifacts/$ARTIFACT_NAME/zip"`: URL для отримання артефакту в ZIP-форматі.
   - `-o $ARTIFACT_NAME.zip`: Вказує ім'я, під яким потрібно зберегти завантажений ZIP-файл артефакту.

Ця команда завантажить артефакт у ZIP-форматі і збереже його як `$ARTIFACT_NAME.zip` у поточній директорії вашого терміналу.

---

Щоб надіслати електронний лист із скрипта GitHub Actions (Workflow), ви можете скористатися дією GitHub Actions для відправлення електронної пошти. Один із найпопулярніших способів — використовувати GitHub Action, який називається `dawidd6/action-send-mail`.

Ось приклад, як налаштувати такий робочий процес (workflow) у вашому репозиторії:

1. Спочатку потрібно створити файл робочого процесу у вашому репозиторії. Для цього створіть файл `.github/workflows/send_email.yml` (або іншу назву за вашим вибором).

2. Додайте наступний вміст у цей файл:

```yaml
name: Send Email

on:
  push:
    branches:
      - main

jobs:
  send_mail:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Send email
        uses: dawidd6/action-send-mail@v3
        with:
          server_address: smtp.example.com
          server_port: 587
          username: ${{ secrets.SMTP_USERNAME }}
          password: ${{ secrets.SMTP_PASSWORD }}
          subject: GitHub Actions Notification
          body: This is a test email sent from a GitHub Actions workflow.
          to: recipient@example.com
          from: sender@example.com
```

3. Ось що означають різні частини цього файлу:

- `name`: Ім'я вашого робочого процесу.
- `on`: Визначає подію, яка запустить робочий процес. У цьому випадку він запускається на `push` до гілки `main`.
- `jobs`: Визначає різні завдання у робочому процесі. У цьому випадку у нас є одне завдання `send_mail`.
- `runs-on`: Вказує, на якому типі сервера (runner) буде виконуватися завдання. У цьому випадку використовується `ubuntu-latest`.
- `steps`: Визначає кроки, які будуть виконані у рамках завдання. У цьому прикладі є два кроки: `Checkout repository` і `Send email`.

4. У кроці `Send email` використовуються такі параметри:
   - `server_address`: Адреса вашого SMTP-сервера.
   - `server_port`: Порт вашого SMTP-сервера.
   - `username`: Ім'я користувача для автентифікації на SMTP-сервері (ви використовуєте секрети GitHub для безпечного зберігання облікових даних).
   - `password`: Пароль для автентифікації на SMTP-сервері (також використовує секрети GitHub).
   - `subject`: Тема електронного листа.
   - `body`: Текст електронного листа.
   - `to`: Адреса отримувача.
   - `from`: Адреса відправника.

5. Щоб використовувати секрети GitHub для безпечного зберігання облікових даних SMTP, перейдіть до налаштувань вашого репозиторію на GitHub, знайдіть розділ `Secrets` і додайте секрети `SMTP_USERNAME` та `SMTP_PASSWORD` з відповідними значеннями.

Після цього ваш робочий процес буде відправляти електронний лист щоразу, коли ви будете пушити зміни до гілки `main`.

---

У GitHub Actions ви можете використовувати дії (actions) з публічних репозиторіїв інших користувачів. Ці дії зазвичай визначені у файлі `action.yml` у корені репозиторію або у підкаталозі `.github/actions`.

Ось кроки для використання дій з публічного репозиторію іншого користувача у вашому робочому процесі:

1. **Знайдіть потрібну дію**: Спочатку знайдіть потрібну дію у публічному репозиторії. Наприклад, ви хочете використовувати дію з репозиторію `username/repo`.

2. **Перегляньте файл `action.yml`**: Переконайтесь, що цей репозиторій має файл `action.yml`, який визначає дію.

3. **Додайте дію до вашого робочого процесу**: Додайте цю дію до вашого workflow YAML файлу.

Ось приклад використання дії з публічного репозиторію:

```yaml
name: Example Workflow

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Use custom action from another repository
        uses: username/repo@version
        with:
          some-input: some-value
```

### Пояснення:

- `name`: Ім'я вашого workflow.
- `on`: Визначає події, які запускають workflow. У цьому випадку workflow запускається на `push` до гілки `main`.
- `jobs`: Визначає робочі завдання у workflow.
- `runs-on`: Вказує, на якому типі сервера буде виконуватися завдання.
- `steps`: Кроки у завданні.

У кроці `Use custom action from another repository`:
- `uses`: Вказує дію з публічного репозиторію. Тут `username/repo@version` — це ім'я користувача, назва репозиторію і версія (тег або хеш коміту) відповідної дії.
- `with`: Передача параметрів дії (опціонально). Це залежить від того, які параметри визначені у файлі `action.yml` у цьому репозиторії.

### Приклад:

Якщо ви хочете використовувати дію з репозиторію `actions/cache` для кешування залежностей:

```yaml
name: Caching Example

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Cache dependencies
        uses: actions/cache@v2
        with:
          path: node_modules
          key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
          restore-keys: |
            ${{ runner.os }}-node-
```

### Пошук дій:

- **GitHub Marketplace**: Можна знайти багато готових дій у [GitHub Marketplace](https://github.com/marketplace?type=actions).
- **Документація**: Документація або README файли публічних репозиторіїв також можуть містити приклади використання їхніх дій.

Завжди перевіряйте README або документацію відповідної дії, щоб переконатися, що ви правильно передаєте параметри та використовуєте потрібну версію.

---

У GitHub Actions ви можете вказати версію дії, яку хочете використовувати, за допомогою тегів, хешів комітів або гілок. Ось як це можна зробити:

### Використання тегів

Теги є найбільш поширеним способом визначення версії, оскільки вони зазвичай асоціюються зі стабільними релізами. Наприклад, щоб використовувати версію 1.2.3 дії, ви можете вказати тег `v1.2.3`:

```yaml
- name: Use custom action from another repository
  uses: username/repo@v1.2.3
```

### Використання хешів комітів

Якщо ви хочете використовувати певний коміт, ви можете вказати хеш коміту. Це гарантує, що ви завжди використовуєте точну версію коду, навіть якщо теги або гілки зміняться:

```yaml
- name: Use custom action from another repository
  uses: username/repo@<commit-sha>
```

### Використання гілок

Ви також можете використовувати гілки, але це менш стабільний спосіб, оскільки гілки можуть змінюватися. Наприклад, для використання останньої версії з гілки `main`:

```yaml
- name: Use custom action from another repository
  uses: username/repo@main
```

### Приклади

#### Використання конкретного тегу

```yaml
- name: Checkout repository
  uses: actions/checkout@v2
```

#### Використання конкретного коміту

```yaml
- name: Cache dependencies
  uses: actions/cache@f7636a14efb0b5c5d12e8e8d5a48bc7c29d5fb16
```

#### Використання гілки

```yaml
- name: Setup Node.js environment
  uses: actions/setup-node@main
```

### Додаткові ресурси

- **GitHub Marketplace**: Можете знайти багато дій і їхню документацію на [GitHub Marketplace](https://github.com/marketplace?type=actions).
- **README файли**: У публічних репозиторіях часто міститься інформація про те, як використовувати їхні дії, включаючи приклади та доступні версії.

### Перевірка версії

Щоб переконатися, що ви використовуєте правильну версію, звертайте увагу на документацію відповідної дії, де часто надаються рекомендації щодо версій, а також можна знайти список доступних тегів у самому репозиторії на GitHub.

---

Для того щоб інші користувачі могли використовувати версію дії вашого репозиторію, ви можете створити тег або випустити реліз для вашої дії. Це дозволяє вказати конкретну версію дії при використанні у GitHub Actions. Нижче наведено кроки для створення тегу та випуску релізу.

### Крок 1: Створення тегу

1. **Створення тегу локально**:
   Ви можете створити тег локально та потім надіслати його до GitHub.
   ```sh
   git tag -a v1.0.0 -m "Release version 1.0.0"
   git push origin v1.0.0
   ```

2. **Створення тегу на GitHub**:
   Ви також можете створити тег безпосередньо на GitHub через інтерфейс користувача:
   - Перейдіть до репозиторію на GitHub.
   - Натисніть на вкладку "Releases" (Релізи).
   - Натисніть на кнопку "Draft a new release" (Створити новий реліз).
   - У полі "Tag version" введіть назву тегу, наприклад, `v1.0.0`.
   - У полі "Release title" введіть назву релізу.
   - Додайте опис релізу та натисніть "Publish release" (Опублікувати реліз).

### Крок 2: Вказання версії дії у вашому workflow

Після створення тегу або релізу інші користувачі можуть використовувати вашу дію, вказавши тег у своїх workflow. Наприклад:

```yaml
- name: Use custom action
  uses: your-username/your-repo@v1.0.0
```

### Приклад файлу дії (action.yml)

Щоб створити дію, переконайтеся, що у вашому репозиторії є файл `action.yml`, який визначає параметри вашої дії. Ось приклад `action.yml`:

```yaml
name: "My Custom Action"
description: "This is a custom GitHub Action"
author: "Your Name <your.email@example.com>"
inputs:
  example-input:
    description: "An example input"
    required: true
    default: "default value"
outputs:
  example-output:
    description: "An example output"
runs:
  using: "node12"
  main: "index.js"
```

### Поради

- **Використання семантичного версіонування**: Рекомендується використовувати семантичне версіонування (SemVer) для ваших тегів, наприклад, `v1.0.0`, `v1.1.0`, `v2.0.0`.
- **Оновлення README**: Додайте інструкції у ваш `README.md` файл, щоб інші користувачі знали, як використовувати вашу дію та які версії доступні.
- **Автоматизація релізів**: Ви можете автоматизувати процес створення тегів та релізів за допомогою GitHub Actions.

Таким чином, інші користувачі зможуть легко вказати версію вашої дії у своїх workflow, використовуючи тег або реліз, який ви створили.

---

