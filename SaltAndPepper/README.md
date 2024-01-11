# Лабораторная работа "Salt and pepper"

В данной лабораторной работе реализована функция добавления шума (Salt and pepper) на изображение. Далее произведена обработка зашумленного изображения с помощью медианного фильтра на CPU и GPU. Код написан на языке Python, для использования графического процессора применялась библиотека Numba.

Ссылка на google colab: https://colab.research.google.com/drive/1_ynIBxIGbTS4U-JjlxFwwTyQtQkUNIf5?usp=sharing

## Описание

Для добавления шума используется функция **noise_adding**.

Далее с помощью функции **median_filter_cpu** производится удаление шумов на CPU. Выбирается 9-точечный квадрат вокруг текущего пикселя, он преобразовывается в массив в котором ищется медиана. Медианное значение записывается в соответствующий пиксель фильтрованного изображения.

Проводится замер времени работы программы на CPU.

Далее реализована функция удаления шума на GPU **median_filter_gpu**. Функция получает координаты (i, j) текущего потока на GPU с использованием cuda.grid(2). Далее предусмотрена проверка на краевые пиксели. **if 0 < i < height - 1 and 0 < j < width** - данное условие гарантирует, что текущий поток не будет захватывать краевые пиксели. Параллельность вычислений в данной функции находится в том, что все потоки GPU обрабатывают различные пиксели изображения. Каждый поток отвечает за свой пиксель.

Проводится замер времени работы программы на GPU.

Далее меняется размер изображения и оно проходит вышеописаннную процедуру заново.

В конце рисуются графики и зависимости.

## Результаты

|  Размер изображения 506x675 |
| --  |
| ![image](https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/0330f5e3-bd84-44d7-97fc-19c3c30f9fff) ![image](https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/30d23eb9-1fe8-45c0-ad6f-0d0bec811f90) |
| ![image](https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/92387d82-1dc9-4388-9173-311ff62dd099) ![image](https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/cdfd8cd7-e13d-4bdf-b09b-fa02f0eb359b) |


| Размер изображения 675x900 |
| --  |
| ![image](https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/bb8d9856-4d80-43c6-b29f-6de3d8df2c16)  ![image](https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/5bdae8f6-b78f-4def-bc19-3d390dc70e8f) |
| ![image](https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/b782119b-0bc7-4471-b651-6ec2aca88350)  ![image](https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/2b24d249-93f2-4d85-8890-b239266426e9) |

| Размер изображения 900x1200 |
| --  |
| ![image](https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/2ad0999f-df51-45fa-b318-03a4c47646db) ![image](https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/883c5ea8-bde7-4c44-8713-c51f1a7b2a47) |
| ![image](https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/4a7407b5-8413-4987-8bec-f5dac22bf64d) ![image](https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/b7e4b814-ea81-46d2-9660-0ba1d5b71d73) |

| Размер изображения 1200x1600 |
| --  |
| ![image](https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/974b2948-90c3-4a69-8bd8-c9a4b8b8fc8a) ![image](https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/b7266e0a-ccd5-4af7-8679-8fd640b3cc02) |
| ![image](https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/adb20cdc-29c1-4b9e-8c76-d6875fa158b4) ![image](https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/8fef602b-e2aa-4a41-816f-a5b95a3f51b9) |

| Графики, зависимости |
| --  |
| ![image](https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/50b8753e-ccb2-44e2-8731-145c99ba5d5a) | 
| ![image](https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/7489ca38-a6ea-44dd-8037-6a1459a95278) |

**Сравнительный анализ был выполнен на основе 4 изображений разной размерности **(506x675 675x900 900x1200 1200x1600)**. С увеличением размера картинки, очевидно, что возрастает время работы как на CPU, так и на GPU. Коллосально быстрее работает GPU. Особенно заметно преимущество GPU, при возрастании ускорения при больших размерах изображения.**
