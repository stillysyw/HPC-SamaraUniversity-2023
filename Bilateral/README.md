# Лабораторная работа "Bilateral filter"

В данной лабораторной работе реализована функция добавления размытия (Bilateral filter) на изображение через CPU и GPU. Код написан на языке Python, для использования графического процессора применялась библиотека Numba.

## Описание 

Реализация фильтра на CPU представлена в функции **bilateral_cpu**. Выбирается 9-точечный квадрат вокруг текущего пикселя, далее в ход идут формулы из методички.

Проводится замер времени работы программы на CPU.

Реализация фильтра на GPU схожа с реализацией на CPU и представлена в функции **bilateral_kern**. Функция получает координаты (i, j) текущего потока на GPU с использованием cuda.grid(2). Параллельность вычислений в данной функции находится в том, что все потоки GPU обрабатывают различные пиксели изображения. Каждый поток отвечает за свой пиксель.

Проводится замер времени работы программы на GPU.

Далее меняется размер изображения и оно проходит вышеописаннную процедуру заново.

В конце рисуются графики и зависимости.

## Результаты

**Размер изображения 506x675**

<img src="https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/59ef92c9-ebdd-4849-b1b4-4d261cce303a" width="300">
<img src="https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/ce458536-c8bb-4cda-9225-cc02d661c20f" width="300">
<img src="https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/4eb53a82-7754-404e-b0eb-cc9ca17becba" width="300">

##

**Размер изображения 675x900**

<img src="https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/394c1d39-64ca-442a-b31a-bfdd1803e190" width="300">
<img src="https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/fcdb769e-81f5-4547-a597-f6fd720b33ca" width="300">
<img src="https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/05417ca5-d965-41b8-a25b-59a8aa90a568" width="300">

##

**Размер изображения 900x1200**

<img src="https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/4f503662-9ec4-4af4-be63-f241a6261c34" width="300">
<img src="https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/08671417-6c36-4e5b-9a5a-c0615ddb4e8b" width="300">
<img src="https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/3e93eb08-b26f-4aba-a822-f93beb78029d" width="300">

##

**Размер изображения 1200x1600**

<img src="https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/75d96244-f70e-4081-acec-c1fe5462fb70" width="300">
<img src="https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/3fbce266-4a09-4c49-9d5c-76405269c10f" width="300">
<img src="https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/0a862c0e-b1fe-4ea5-90e5-a1b036938cfc" width="300">

##

**Графики, зависимости**

![image](https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/3198bc57-13c3-40da-8be2-71e2b7ae01a0)
![image](https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/757bdeab-fee4-4c1e-91bb-841428feae09)


