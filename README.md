1. Сортировка выбором (Selection Sort)

Описание
Алгоритм на каждом проходе находит минимальный элемент в неотсортированной части массива и меняет его местами с первым элементом этой части.

Код на C++:

void selectionSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        swap(arr[i], arr[minIndex]);
    }
}

Описание кода:
Внешний цикл проходит по всем элементам. Внутренний цикл ищет минимальный элемент в оставшейся части массива. После нахождения минимума он меняется местами с текущим элементом.

Временная сложность:

    Худший случай: O(n2)O(n2)

    Средний случай: O(n2)O(n2)

    Лучший случай: O(n2)O(n2)

2. Сортировка обменом (Bubble Sort)

Описание
Алгоритм многократно проходит по массиву, сравнивая соседние элементы и меняя их местами, если они стоят в неправильном порядке.

Код на C++
cpp

void bubbleSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
            }
        }
    }
}

Описание кода
Внешний цикл определяет количество проходов. Внутренний цикл попарно сравнивает соседние элементы и меняет их местами, если необходимо. После каждого прохода наибольший элемент "всплывает" в конец.

Временная сложность

    Лучший случай: O(n)O(n)

    Средний случай: O(n2)O(n2)

    Худший случай: O(n2)O(n2)

3. Сортировка вставками (Insertion Sort)

Описание
Алгоритм строит отсортированную последовательность, по одному элементу за раз, вставляя каждый новый элемент в правильную позицию среди уже отсортированных.

Код на C++
cpp

void insertionSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}

Описание кода
На каждом шаге берётся очередной элемент (key) и вставляется в отсортированную часть массива слева от него, сдвигая элементы при необходимости.

Временная сложность

    Лучший случай: O(n)O(n)

    Средний случай: O(n2)O(n2)

    Худший случай: O(n2)O(n2)

4. Сортировка слиянием (Merge Sort)

Описание
Алгоритм разделяет массив на две половины, рекурсивно сортирует каждую, а затем объединяет (сливает) их в один отсортированный массив.

Код на C++
cpp

void merge(vector<int>& arr, int left, int mid, int right) {
    vector<int> temp(right - left + 1);
    int i = left, j = mid + 1, k = 0;
    
    while (i <= mid && j <= right) {
        if (arr[i] <= arr[j]) temp[k++] = arr[i++];
        else temp[k++] = arr[j++];
    }
    while (i <= mid) temp[k++] = arr[i++];
    while (j <= right) temp[k++] = arr[j++];
    for (int p = 0; p < k; p++) {
        arr[left + p] = temp[p];
    }
}

void mergeSort(vector<int>& arr, int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }
}

Описание кода
Функция mergeSort рекурсивно делит массив. Функция merge объединяет два отсортированных подмассива в один, сравнивая элементы по очереди.

Временная сложность

    Все случаи: O(nlog⁡n)O(nlogn)

5. Сортировка Шелла (Shell Sort)

Описание
Улучшенная версия сортировки вставками. Сравниваются элементы, стоящие на определённом расстоянии (шаге), которое постепенно уменьшается до 1.

Код на C++
cpp

void shellSort(vector<int>& arr) {
    int n = arr.size();
    for (int gap = n / 2; gap > 0; gap /= 2) {
        for (int i = gap; i < n; i++) {
            int temp = arr[i];
            int j;
            for (j = i; j >= gap && arr[j - gap] > temp; j -= gap) {
                arr[j] = arr[j - gap];
            }
            arr[j] = temp;
        }
    }
}

Описание кода
Внешний цикл задаёт последовательность шагов (здесь — n/2, n/4, ... 1). Внутренние циклы выполняют сортировку вставками внутри подмассивов, образованных текущим шагом.

Временная сложность

    Зависит от выбора шага. В худшем случае: O(n2)O(n2), для лучших последовательностей: O(nlog⁡2n)O(nlog2n)

6. Быстрая сортировка (Quick Sort)

Описание
Алгоритм выбирает опорный элемент, разделяет массив на две части: элементы меньше опорного и больше опорного, затем рекурсивно сортирует эти части.

Код на C++
cpp

int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high];
    int i = low - 1;
    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return i + 1;
}

void quickSort(vector<int>& arr, int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

Описание кода
Функция partition выбирает опорный элемент (здесь — последний) и перераспределяет элементы так, чтобы слева были меньшие, а справа — большие. Функция quickSort рекурсивно применяется к полученным частям.

Временная сложность

    Лучший и средний случай: O(nlog⁡n)O(nlogn)

    Худший случай: O(n2)O(n2)

7. Пирамидальная сортировка (Heap Sort)

Описание
Алгоритм строит из массива двоичную кучу (max-heap), затем последовательно извлекает максимальный элемент и перестраивает кучу.

Код на C++
cpp

void heapify(vector<int>& arr, int n, int i) {
    int largest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;
    
    if (left < n && arr[left] > arr[largest]) largest = left;
    if (right < n && arr[right] > arr[largest]) largest = right;
    if (largest != i) {
        swap(arr[i], arr[largest]);
        heapify(arr, n, largest);
    }
}

void heapSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = n / 2 - 1; i >= 0; i--) {
        heapify(arr, n, i);
    }
    for (int i = n - 1; i > 0; i--) {
        swap(arr[0], arr[i]);
        heapify(arr, i, 0);
    }
}

Описание кода
Функция heapify поддерживает свойство кучи. heapSort сначала строит кучу, затем многократно извлекает корень (максимум) и перестраивает кучу для оставшихся элементов.

Временная сложность

    Все случаи: O(nlog⁡n)O(nlogn)

8. Последовательный поиск (Linear Search)

Описание
Алгоритм последовательно проверяет каждый элемент массива до тех пор, пока не найдет искомый элемент или не проверит все элементы.

Код на C++
cpp

int linearSearch(vector<int>& arr, int target) {
    for (int i = 0; i < arr.size(); i++) {
        if (arr[i] == target) {
            return i;
        }
    }
    return -1;
}

Описание кода
Простой цикл for проходит по всем элементам массива и сравнивает их с целевым значением.

Временная сложность

    Все случаи: O(n)O(n)

9. Бинарный поиск (Binary Search)

Описание
Алгоритм работает на отсортированном массиве. На каждом шаге он сравнивает искомый элемент с элементом в середине массива и, в зависимости от результата, продолжает поиск в левой или правой половине.

Код на C++
cpp

int binarySearch(vector<int>& arr, int target) {
    int left = 0, right = arr.size() - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) return mid;
        if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}

Описание кода
Алгоритм поддерживает две границы поиска — left и right. На каждой итерации вычисляется середина (mid). Если элемент не найден, границы смещаются, исключая неподходящую половину.

Временная сложность

    Все случаи: O(log⁡n)O(logn)

10. Интерполирующий поиск (Interpolation Search)

Описание
Улучшение бинарного поиска для равномерно распределенных данных. Позиция для сравнения вычисляется по формуле интерполяции, что может ускорить поиск.

Код на C++
cpp

int interpolationSearch(vector<int>& arr, int target) {
    int low = 0, high = arr.size() - 1;
    while (low <= high && target >= arr[low] && target <= arr[high]) {
        int pos = low + ((target - arr[low]) * (high - low)) / (arr[high] - arr[low]);
        if (arr[pos] == target) return pos;
        if (arr[pos] < target) low = pos + 1;
        else high = pos - 1;
    }
    return -1;
}

Описание кода
Аналогичен бинарному поиску, но позиция pos вычисляется по формуле интерполяции, что позволяет ближе "подпрыгнуть" к искомому элементу.

Временная сложность

    В среднем случае: O(log⁡log⁡n)O(loglogn)

    В худшем случае: O(n)O(n)

11. Поиск Фибоначчи (Fibonacci Search)

Описание
Алгоритм использует числа Фибоначчи для определения позиций разделения в отсортированном массиве. Является вариантом бинарного поиска без использования операции деления.

Код на C++
cpp

int fibonacciSearch(vector<int>& arr, int target) {
    int n = arr.size();
    int fibMMm2 = 0; // (m-2)-ое число Фибоначчи
    int fibMMm1 = 1; // (m-1)-ое число Фибоначчи
    int fibM = fibMMm2 + fibMMm1; // m-ое число Фибоначчи

    while (fibM < n) {
        fibMMm2 = fibMMm1;
        fibMMm1 = fibM;
        fibM = fibMMm2 + fibMMm1;
    }

    int offset = -1;
    while (fibM > 1) {
        int i = min(offset + fibMMm2, n - 1);
        if (arr[i] < target) {
            fibM = fibMMm1;
            fibMMm1 = fibMMm2;
            fibMMm2 = fibM - fibMMm1;
            offset = i;
        } else if (arr[i] > target) {
            fibM = fibMMm2;
            fibMMm1 = fibMMm1 - fibMMm2;
            fibMMm2 = fibM - fibMMm1;
        } else {
            return i;
        }
    }
    if (fibMMm1 && arr[offset + 1] == target) return offset + 1;
    return -1;
}

Описание кода:

    Алгоритм находит наименьшее число Фибоначчи, большее или равное размеру массива. Затем использует числа Фибоначчи для сужения диапазона поиска, сравнивая элемент в вычисленной позиции с целевым.

Временная сложность

    Все случаи: O(log⁡n)O(logn)





2. Сортировка обменом (Bubble Sort)

Описание
Алгоритм многократно проходит по массиву, сравнивая соседние элементы и меняя их местами, если они стоят в неправильном порядке.

Код на C++
cpp

void bubbleSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
            }
        }
    }
}

Описание кода
Внешний цикл определяет количество проходов. Внутренний цикл попарно сравнивает соседние элементы и меняет их местами, если необходимо. После каждого прохода наибольший элемент "всплывает" в конец.

Временная сложность

    Лучший случай: O(n)O(n)

    Средний случай: O(n2)O(n2)

    Худший случай: O(n2)O(n2)

3. Сортировка вставками (Insertion Sort)

Описание
Алгоритм строит отсортированную последовательность, по одному элементу за раз, вставляя каждый новый элемент в правильную позицию среди уже отсортированных.

Код на C++
cpp

void insertionSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}

Описание кода
На каждом шаге берётся очередной элемент (key) и вставляется в отсортированную часть массива слева от него, сдвигая элементы при необходимости.

Временная сложность

    Лучший случай: O(n)O(n)

    Средний случай: O(n2)O(n2)

    Худший случай: O(n2)O(n2)

4. Сортировка слиянием (Merge Sort)

Описание
Алгоритм разделяет массив на две половины, рекурсивно сортирует каждую, а затем объединяет (сливает) их в один отсортированный массив.

Код на C++
cpp

void merge(vector<int>& arr, int left, int mid, int right) {
    vector<int> temp(right - left + 1);
    int i = left, j = mid + 1, k = 0;
    
    while (i <= mid && j <= right) {
        if (arr[i] <= arr[j]) temp[k++] = arr[i++];
        else temp[k++] = arr[j++];
    }
    while (i <= mid) temp[k++] = arr[i++];
    while (j <= right) temp[k++] = arr[j++];
    for (int p = 0; p < k; p++) {
        arr[left + p] = temp[p];
    }
}

void mergeSort(vector<int>& arr, int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }
}

Описание кода
Функция mergeSort рекурсивно делит массив. Функция merge объединяет два отсортированных подмассива в один, сравнивая элементы по очереди.

Временная сложность

    Все случаи: O(nlog⁡n)O(nlogn)

5. Сортировка Шелла (Shell Sort)

Описание
Улучшенная версия сортировки вставками. Сравниваются элементы, стоящие на определённом расстоянии (шаге), которое постепенно уменьшается до 1.

Код на C++
cpp

void shellSort(vector<int>& arr) {
    int n = arr.size();
    for (int gap = n / 2; gap > 0; gap /= 2) {
        for (int i = gap; i < n; i++) {
            int temp = arr[i];
            int j;
            for (j = i; j >= gap && arr[j - gap] > temp; j -= gap) {
                arr[j] = arr[j - gap];
            }
            arr[j] = temp;
        }
    }
}

Описание кода
Внешний цикл задаёт последовательность шагов (здесь — n/2, n/4, ... 1). Внутренние циклы выполняют сортировку вставками внутри подмассивов, образованных текущим шагом.

Временная сложность

    Зависит от выбора шага. В худшем случае: O(n2)O(n2), для лучших последовательностей: O(nlog⁡2n)O(nlog2n)

6. Быстрая сортировка (Quick Sort)

Описание
Алгоритм выбирает опорный элемент, разделяет массив на две части: элементы меньше опорного и больше опорного, затем рекурсивно сортирует эти части.

Код на C++
cpp

int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high];
    int i = low - 1;
    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return i + 1;
}

void quickSort(vector<int>& arr, int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

Описание кода
Функция partition выбирает опорный элемент (здесь — последний) и перераспределяет элементы так, чтобы слева были меньшие, а справа — большие. Функция quickSort рекурсивно применяется к полученным частям.

Временная сложность

    Лучший и средний случай: O(nlog⁡n)O(nlogn)

    Худший случай: O(n2)O(n2)

7. Пирамидальная сортировка (Heap Sort)

Описание
Алгоритм строит из массива двоичную кучу (max-heap), затем последовательно извлекает максимальный элемент и перестраивает кучу.

Код на C++
cpp

void heapify(vector<int>& arr, int n, int i) {
    int largest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;
    
    if (left < n && arr[left] > arr[largest]) largest = left;
    if (right < n && arr[right] > arr[largest]) largest = right;
    if (largest != i) {
        swap(arr[i], arr[largest]);
        heapify(arr, n, largest);
    }
}

void heapSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = n / 2 - 1; i >= 0; i--) {
        heapify(arr, n, i);
    }
    for (int i = n - 1; i > 0; i--) {
        swap(arr[0], arr[i]);
        heapify(arr, i, 0);
    }
}

Описание кода
Функция heapify поддерживает свойство кучи. heapSort сначала строит кучу, затем многократно извлекает корень (максимум) и перестраивает кучу для оставшихся элементов.

Временная сложность

    Все случаи: O(nlog⁡n)O(nlogn)

8. Последовательный поиск (Linear Search)

Описание
Алгоритм последовательно проверяет каждый элемент массива до тех пор, пока не найдет искомый элемент или не проверит все элементы.

Код на C++
cpp

int linearSearch(vector<int>& arr, int target) {
    for (int i = 0; i < arr.size(); i++) {
        if (arr[i] == target) {
            return i;
        }
    }
    return -1;
}

Описание кода
Простой цикл for проходит по всем элементам массива и сравнивает их с целевым значением.

Временная сложность

    Все случаи: O(n)O(n)

9. Бинарный поиск (Binary Search)

Описание
Алгоритм работает на отсортированном массиве. На каждом шаге он сравнивает искомый элемент с элементом в середине массива и, в зависимости от результата, продолжает поиск в левой или правой половине.

Код на C++
cpp

int binarySearch(vector<int>& arr, int target) {
    int left = 0, right = arr.size() - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) return mid;
        if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}

Описание кода
Алгоритм поддерживает две границы поиска — left и right. На каждой итерации вычисляется середина (mid). Если элемент не найден, границы смещаются, исключая неподходящую половину.

Временная сложность

    Все случаи: O(log⁡n)O(logn)

10. Интерполирующий поиск (Interpolation Search)

Описание
Улучшение бинарного поиска для равномерно распределенных данных. Позиция для сравнения вычисляется по формуле интерполяции, что может ускорить поиск.

Код на C++
cpp

int interpolationSearch(vector<int>& arr, int target) {
    int low = 0, high = arr.size() - 1;
    while (low <= high && target >= arr[low] && target <= arr[high]) {
        int pos = low + ((target - arr[low]) * (high - low)) / (arr[high] - arr[low]);
        if (arr[pos] == target) return pos;
        if (arr[pos] < target) low = pos + 1;
        else high = pos - 1;
    }
    return -1;
}

Описание кода
Аналогичен бинарному поиску, но позиция pos вычисляется по формуле интерполяции, что позволяет ближе "подпрыгнуть" к искомому элементу.

Временная сложность

    В среднем случае: O(log⁡log⁡n)O(loglogn)

    В худшем случае: O(n)O(n)

11. Поиск Фибоначчи (Fibonacci Search)

Описание
Алгоритм использует числа Фибоначчи для определения позиций разделения в отсортированном массиве. Является вариантом бинарного поиска без использования операции деления.

Код на C++
cpp




Описание кода
Алгоритм находит наименьшее число Фибоначчи, большее или равное размеру массива. Затем использует числа Фибоначчи для сужения диапазона поиска, сравнивая элемент в вычисленной позиции с целевым.

Временная сложность

    Все случаи: O(log⁡n)O(logn)


