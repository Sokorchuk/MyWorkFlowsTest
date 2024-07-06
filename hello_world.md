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

