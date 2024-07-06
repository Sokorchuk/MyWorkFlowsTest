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

