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
