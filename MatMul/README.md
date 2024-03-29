# Лабораторная работая "MatMul"
## Описание 

За основу была взята лабораторная работа с прошлых курсов по предмету *Параллельное программирование*.

Для перемножения матриц на CPU используется функция sequential, на вход данной функции подаются три массива: входные и выходная матрица, а также три, которые отвечают за размерность данных матриц. Здесь используется макрос библиотеки cuBLAS: #define IDX2C(i,j,ld) (((j)*(ld))+(i)), где «i» — это строка, «j» — столбец, а «ld» — ведущее измерение, которое в случае хранения по столбцам представляет собой количество строк выделенной матрицы.

Для перемножения матриц на GPU используется функция gpu_blas_mmul, на вход подаются такие же параметры. Здесь используется функция cublasDgemm() из библиотеки Cublas, которая выполняет умножение матрицы на матрицу в виде $C = alphaAB + betaC$. Функция cublasDgemm использует объект cublasHandle_t handle, который содержит в себе контекст библиотеки cuBLAS и выделяет ресурсы на GPU, подбирая параметры GRID_SIZE и BLOCK_SIZE.

## Результаты

| Dimension	| Время GPU,c |	Время CPU,c	| Ускорение |
| ------------- | ------------- | ------------- | ------------- |
| 100	| 0,019684	| 0,00442	| 0,224547
| 200	| 0,006754	| 0,037201	| 5,507995
| 400	| 0,002258	| 0,331576	| 146,844995
| 800	| 0,017449	| 3,583434	| 205,366152
| 1600 | 	0,09895	| 49,813386	| 503,419767
| 2000 | 0,18311	| 78,179455	| 426,953497

**Графики ускорения и времени**
<div>
  <img src="https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/b4410eb2-e33d-48e1-b834-f1d7ff365399" width="500" height="400"/>&nbsp;
  <img src="https://github.com/stillysyw/HPC-SamaraUniversity-2023/assets/154344530/cf4a3796-1d14-48ad-89ba-3e22291846c5" width="500" height="400"/>&nbsp;
</div>

Из результатов можно сделать вывод, с увеличением размерности матриц ускорение увеличивается, так как при параллельной обработке матриц можно на нескольких нитях одновременно обрабатывать несколько умножений. Однако при размерности матриц 2000, ускорение уменьшилось. Это может быть связано с синхронизацией потоков или передачей данных от девайса к хосту или наоборот.

## Код лабораторной
Ссылка на google colab: https://colab.research.google.com/drive/1eK_gOHrxpvdDsICZAME0g21G0kr2qUai?hl=ru#scrollTo=t1pWVNYwNvxI
