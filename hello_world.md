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

Для того щоб побачити вивід скрипта `hello_world.sh` під час його виконання через GitHub Actions, вам необхідно звернутися до вкладки "Actions" у вашому репозиторії GitHub:

1. **Перейдіть в GitHub репозиторій**: Відкрийте свій репозиторій на GitHub.

2. **Оберіть вкладку "Actions"**: У верхній частині сторінки репозиторію оберіть вкладку "Actions". Це відкриє сторінку зі списком ваших workflows (робочих процесів).

3. **Оберіть відповідний workflow**: Знайдіть і оберіть workflow, який ви хочете перевірити. У вашому випадку це буде workflow, який ви налаштували для тестування скрипта `hello_world.sh`.

4. **Перегляньте вивід дій**: У вкладці "Jobs" ви побачите список кроків (steps), які виконує ваш workflow. Кожен крок має кнопку "View logs", за допомогою якої можна переглянути вивід цього конкретного кроку.

5. **Перегляньте вивід скрипта**: Оберіть крок, який відповідає виконанню скрипта `hello_world.sh`. У вікні деталей кроку ви побачите весь вивід, який скрипт вивів під час свого виконання.

Це дасть вам можливість побачити всі виведені дані з вашого скрипта, які відображаються в GitHub Actions.

---

Вкладка "jobs" зазвичай знаходиться в розділі GitHub Actions для конкретного workflow файлу. Ось як можна знайти цю вкладку:

1. **Увійдіть у свій репозиторій на GitHub**: Зайдіть на сторінку вашого репозиторію на GitHub.

2. **Перейдіть до вкладки Actions**: У верхньому меню вашого репозиторію знайдіть вкладку "Actions" і клацніть на неї.

3. **Виберіть workflow**: Оберіть потрібний workflow зі списку на лівій стороні екрану. Якщо у вас є кілька workflow файлів, виберіть той, де ви хочете переглянути вкладку "jobs".

4. **Перейдіть до вкладки "jobs"**: Після вибору конкретного workflow файлу, ви побачите верхній рядок з різними вкладками, такими як "Overview", "Jobs", "Run workflow", і т.д. Клацніть на вкладку "Jobs".

Ця вкладка показує вам інформацію про виконані робочі процеси (jobs) для обраного workflow файлу, включаючи їхні стани, часи виконання та інші важливі дані, пов'язані з виконанням вашого GitHub Actions workflow.

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

