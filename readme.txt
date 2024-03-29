Принцип работы:
Есть 2 глобальные хэш-таблицы: vocab и checker
Vocab:
- Нужен для того что бы за O(1) время получать все анаграмы по полученному слову.
- В ключе хранит хэш слова в виде строки. Значение: массив слов которые выдают одинаковый хэш после хэш-функции
Checker:
- Нужен для того что бы за O(1) время проверять какие слова уже проходили через хэш, что бы не дублировать слова в массиве.
Хэш-функция:
- Расщепляет слово на слайс рун(так как слово может содержать любые символы UTF-8).
- Далее сортирует руны функцие sort.StableSort().
- Time-complexity: O(nlog(n)). N-количество символов в слове. (sort.StableSort() имеет time-complexity O(nlog(n)))

Альтернативное решение:
- Можно сделать хэш-функцию с time-complexity: O(n).
- Функция базируется на уникальном свойстве простых чисел.
- Каждый символ будет иметь аналог в виде простого числа. Например: a->2, b->3, c->5, d->7 ...
- Умножение простых чисел, никогда не совпадет с умножением других простых чисел. В этом и есть их уникальное свойство.
- Однако, я решил не имплементировать данное решение, из-за возможной integer overflow проблемы:
    - Если на вход придет большая строка с редкими символами, чьи эквиваленты простых чисел большие, то их переумножение
    - превысит допустимый диапозон чисел int64(9,223,372,036,854,775,807) или даже uint64(18,446,744,073,709,551,615)

// Примерная функция реализации хэша с простыми числами
var primeNumbers = []int{2, 3, 5, 7 ,11, 13, 17 .....}
func alternativeHashFunc(word string) int {
    var hash int = 1
    runes := []rune(word)
    for _, r := range runes {
        hash *= primeNumbers[r]
    }
    return hash
}