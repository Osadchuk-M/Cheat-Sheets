# Unittest module

### Code example:

    import unittest


    class TestHomework(unittest.TestCase):
        def setUp(self):
            self.value = 2

        def test_lorem(self):
            self.assertEqual(self.value, 2)

        def tearDown(self):
            del self.value

    if __name__ == '__main__':
        unittest.main()

### Плюси:
* доступий в стандартній бібліотеці
* виводить зрозумілі повідомлення про помилки
* вміє автоматично знаходити тести

### Мінуси:
* API унаслідований від JAVA
* Заставляє писати багато лишнього коду
* читати unittest складніше, ніж доктести і тести, що використовують assert
        
## Замітки
* функція unittest.main загружає всі тести поточного модуля і запускає їх
* Тест - метод екземпляру unittest.TestCase, який починається на test
* методи setUp і tearDown запускаються до і після кожного тесту відповідно

## Основні методи unittest.TestCase

| unittest.TestCase method  |  description           |
| ------------------------- | ---------------------- |
| assertEqual(a, b)         |   a == b               |
| assertNotEqual(a, b)      |   a != b               |
| assertTrue(x)             |   bool(x) is True      |
| assertFalse(x)            |   bool(x) is False     |
| assertIs(a, b)            |   a is b               |
| assertIsNot(a, b)         |   a is not b           |
| assertIsNone(x)           |   x is None            |
| assertIsNotNone(x)        |   x is not None        |
| assertIn(a, b)            |   a in b               |
| assertNotIn(a, b)         |   a not in b           |
| assertIsInstace(a, b)     |   isinstance(a, b)     |
| assertNotIsInstanse(a, b) |   not isinstance(a, b) |
