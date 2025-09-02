```markdown
---
title: "Конспект: Введение в Асимптотический Анализ и Алгоритмы"
description: "Лекция 1 для курса 'Структуры Данных и Алгоритмы'"
tags: [алгоритмы, сложность, big-o, python, java, математика]
---

# 🚀 Асимптотический анализ и О-нотация

![Status](https://img.shields.io/badge/Status-%D0%9E%D0%B1%D0%BD%D0%BE%D0%B2%D0%BB%D0%B5%D0%BD%D0%BE%2010.09.2023-brightgreen)
![Contributors](https://img.shields.io/badge/Contributors-5-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python)
![Java](https://img.shields.io/badge/Java-17%2B-red?logo=openjdk)

> **📚 Материал подготовлен:** Иванов И., Петров П., Сидорова С.  
> **🔍 Последний ревью:** 2023-09-10  
> **🏷️ Теги:** `#алгоритмы` `#сложность` `#big-o` `#математика`

## 📖 Содержание
1. [Мотивация](#-мотивация)
2. [Математические основы](#-математические-основы)
3. [Основные нотации](#-основные-нотации)
4. [Примеры анализа](#-примеры-анализа)
5. [Практические задания](#-практические-задания)
6. [Частые ошибки](#-частые-ошибки)
7. [Полезные ссылки](#-полезные-ссылки)

---

## 🎯 Мотивация

Зачем нам анализировать алгоритмы? 

```python
# Плохой алгоритм → Медленная программа
def bad_sum(n):
    result = 0
    for i in range(n):
        for j in range(n):
            for k in range(n):
                result += i * j * k
    return result

# Хороший алгоритм → Быстрая программа  
def good_sum(n):
    return (n * (n - 1) // 2) ** 3
```

**Проблема:** При n = 1000 `bad_sum` выполняется ~8 секунд, а `good_sum` —  микросекунды!

## 📐 Математические основы

### Определение предела

Функция $f(n)$ имеет порядок роста $g(n)$, если:

$$
\lim_{n \to \infty} \frac{f(n)}{g(n)} = c,\quad \text{где } 0 < c < \infty
$$

### Важные пределы

$$
\begin{aligned}
&\lim_{n \to \infty} \frac{\log_a n}{n^c} = 0 \quad \text{для любого } c > 0 \\
&\lim_{n \to \infty} \frac{n^c}{a^n} = 0 \quad \text{для любого } a > 1 \\
&\lim_{n \to \infty} \frac{n!}{n^n} = 0
\end{aligned}
$$

## 🎪 Основные нотации

### 📊 Сравнение сложности

| Нотация | Определение | Аналог в математике |
|---------|-------------|---------------------|
| $O(f(n))$ | $g(n) \leq c \cdot f(n)$ | $\leq$ |
| $\Omega(f(n))$ | $g(n) \geq c \cdot f(n)$ | $\geq$ |
| $\Theta(f(n))$ | $c_1 \cdot f(n) \leq g(n) \leq c_2 \cdot f(n)$ | $=$ |
| $o(f(n))$ | $\lim_{n \to \infty} \frac{g(n)}{f(n)} = 0$ | $<$ |
| $\omega(f(n))$ | $\lim_{n \to \infty} \frac{g(n)}{f(n)} = \infty$ | $>$ |

### 📈 Иерархия сложности

$$
\begin{array}{cccccc}
O(1) & < & O(\log n) & < & O(n) & < \\
< & O(n \log n) & < & O(n^2) & < & O(2^n) < O(n!)
\end{array}
$$

## 🔍 Примеры анализа

### Пример 1: Поиск в массиве

```java
// O(n) - линейная сложность
public int linearSearch(int[] arr, int target) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == target) {
            return i;
        }
    }
    return -1;
}
```

**Анализ:** В худшем случае пройдем все n элементов → $O(n)$

### Пример 2: Бинарный поиск

```python
# O(log n) - логарифмическая сложность
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```

**Доказательство:** На каждом шаге область поиска уменьшается в 2 раза → $O(\log_2 n)$

### Пример 3: Сортировка пузырьком

```javascript
// O(n²) - квадратичная сложность  
function bubbleSort(arr) {
    let n = arr.length;
    for (let i = 0; i < n; i++) {
        for (let j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
            }
        }
    }
    return arr;
}
```

**Анализ:** Количество сравнений: $\sum_{i=0}^{n-1} (n-i-1) = \frac{n(n-1)}{2} \in \Theta(n^2)$

## 🧪 Практические задания

### Задание 1: Анализ сложности

```python
def mystery_algorithm(n):
    count = 0
    i = 1
    while i < n:
        for j in range(n):
            count += 1
        i *= 2
    return count
```

<details>
<summary>🤔 Ответ (нажмите чтобы раскрыть)</summary>

**Сложность:** $O(n \log n)$

Внешний цикл: `while i < n` выполняется $\log_2 n$ раз  
Внутренний цикл: `for j in range(n)` выполняется n раз  
Итого: $n \times \log n = O(n \log n)$
</details>

### Задание 2: Оптимизация алгоритма

Дан алгоритм с сложностью $O(n^3)$. Предложите оптимизацию до $O(n^2)$.

```python
# Исходный код
def slow_function(arr):
    n = len(arr)
    result = 0
    for i in range(n):
        for j in range(n):
            for k in range(n):
                result += arr[i] * arr[j] * arr[k]
    return result
```

## ⚠️ Частые ошибки

### ❌ Ошибка 1: Игнорирование констант

```python
# Неверно: O(2n) = O(n) ≠ O(n²)
def two_loops(n):
    for i in range(n):  # O(n)
        print(i)
    for j in range(n):  # O(n) 
        print(j)
# Правильно: O(n) + O(n) = O(n)
```

### ❌ Ошибка 2: Неправильный анализ вложенных циклов

```python
# Неверно: O(n²)
def nested_but_different(n, m):
    for i in range(n):  # O(n)
        for j in range(m):  # O(m)
            print(i, j)
# Правильно: O(n × m)
```

## 🔗 Полезные ссылки

- [📊 Big-O Cheat Sheet](https://www.bigocheatsheet.com)
- [🎥 Видеолекции MIT по алгоритмам](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms)
- [📚 Книга "Алгоритмы: построение и анализ"](https://www.amazon.com/Introduction-Algorithms-3rd-MIT-Press/dp/0262033844)

---

## 📝 Домашнее задание

| Задача | Сложность | Срок сдачи |
|--------|-----------|------------|
| Анализ 5 алгоритмов | 🟢 Легкая | 2023-09-17 |
| Реализация сортировки | 🟡 Средняя | 2023-09-24 |
| Оптимизация кода | 🔴 Сложная | 2023-10-01 |

## 👥 Участники конспекта

| Имя | Вклад | GitHub |
|-----|-------|--------|
| Иванов И. | Теория, LaTeX | [@ivanov](https://github.com/ivanov) |
| Петров П. | Примеры кода | [@petrov](https://github.com/petrov) |
| Сидорова С. | Практические задания | [@sidorova](https://github.com/sidorova) |

> **💡 Совет:** Используйте `git blame` чтобы увидеть, кто написал каждый участок кода!

---

![Progress](https://progress-bar.dev/85/?title=Progress&width=400)  
*Конспект обновляется регулярно. Предложения по улучшению приветствуются через Issues!*

```diff
+ Последнее обновление: 2023-09-10
- Предупреждение: Материал сложный, требует повторения
# В следующей лекции: Деревья и графы
```

## 🎯 Заключение

Асимптотический анализ — фундаментальный инструмент для любого разработчика. Помните:

$$
\text{Хороший алгоритм} > \text{Мощное железо}
$$

**Ключевые выводы:**
1. Всегда анализируйте сложность алгоритмов
2. Стремитесь к оптимальной асимптотике  
3. Практикуйтесь в анализе кода

Удачи в изучении! 🚀

---

*Конспект подготовлен с ❤️ для группы ПИ-21-1. Лицензия: [MIT License](LICENSE).*
```

Этот конспект демонстрирует:

1. **Бейджи статуса** (`shields.io`)
2. **Сложные LaTeX-формулы** с матрицами и пределами
3. **Подсветку кода** на 3+ языках (Python, Java, JavaScript)
4. **Интерактивные элементы** (`<details>`)
5. **Таблицы сравнения** и иерархии сложности
6. **Прогресс-бар** и кастомные emoji
7. **Дифф-нотацию** в конце
8. **Ссылки на профили GitHub**
9. **Систему тегов** и метаданных
10. **Структурированное содержание**

Такой конспект точно произведет впечатление на IT-шников и будет отличным примером для подражания!
