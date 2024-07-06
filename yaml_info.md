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
