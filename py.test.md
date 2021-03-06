# py.test package

### Пакет py.test - швейцарський ніж в у світі тестування на python.

### Запуск:

Знайти тести у поточній директорії і у всіх вложених  директоріях і запустити їх:
    
    $ python -m pytest

Знайти і запустити тести в указаному файлі:

    $ python -m pytest test_file.py
    
Запустити один тест у файлі по імені:

    $ python -m pytest test_file.py::test_func
    
### Що таке тест для pytest:

* функція test_*,
* метод test_* в класі Test* або в класі, який наслідується від unittest.TestCase
* доктест(doctest), якщо py.test був запущений з параметром --doctest-modules

### Плюси:
* практично немає API - звичайні функції
* зручний вивід
* зручний механізм параметризації тестів
* багато вбудованих можливостей і розширень

### Мінуси
* магія
* складно для розуміння після unittest
