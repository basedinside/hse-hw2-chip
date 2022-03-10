# HSE Homework 2 

[Ссылка на Google Colab](https://colab.research.google.com/drive/1PBy-PAv1M6SHt1BILcQKaF-apgJAqo4z?usp=sharing)

## FASTQC Анализ

|Replica 1 XHZ|Replica 1 OIN|Replica 2 JDD|Replica 2 JDD Trimmed|Control TIB|
|---          | ---         |          ---|                  ---|        ---|
|<img width="146" alt="image" src="https://user-images.githubusercontent.com/71254839/157738355-d61f8351-6d01-41ca-ba76-6a9ed0509a8e.png">|<img width="142" alt="image" src="https://user-images.githubusercontent.com/71254839/157738480-f775c662-4d2f-43b8-a13e-b26fbffa60a4.png">|<img width="145" alt="image" src="https://user-images.githubusercontent.com/71254839/157738550-b5f0a779-018c-4e07-a462-a7ba82fbd521.png">|<img width="144" alt="image" src="https://user-images.githubusercontent.com/71254839/157738617-3513ef30-9910-4c74-b4c7-e5a7434b2b46.png">|<img width="144" alt="image" src="https://user-images.githubusercontent.com/71254839/157738726-6dda7e2a-e8e9-4dfb-8870-1a011b3b0e2e.png">|

### XHZ Analysis

- Failure: Per Base Sequence Content выдается, если разница между ATCG больше 20% в любой из позиций. В нашем случае это возможно артефакты секвенирования.
<img width="443" alt="image" src="https://user-images.githubusercontent.com/71254839/157739768-af0b2791-51e5-486d-af1a-bbe8ce8c5551.png">

- Warning: Per Sequence GC Content выдается, если сумма девиаций от нормального распределения встречается больше, чем в 15% ридов. В нашем случае все нормально.
![image](https://user-images.githubusercontent.com/71254839/157740021-5e8c3edf-3590-4821-a3cb-2af2b222405f.png)

### OIN Analysis

Все более менее в норме, аналогично предыдущему образцу.
|![image](https://user-images.githubusercontent.com/71254839/157740318-25c66d97-7682-4d5d-a6d5-b5af82ada08c.png)|<img width="466" alt="image" src="https://user-images.githubusercontent.com/71254839/157740358-0053ce24-0418-469c-bf46-2978e8158a5d.png">|![image](https://user-images.githubusercontent.com/71254839/157740410-2d73cbb7-bb72-46c5-b4ee-6d3c4257a4de.png)|
|---|---|---|

### JDD Analysis

- Failure: Per Tile Sequence Quality

Для исправления ситуации решил сделать тримм. После тримма ситуация улучшилась
|До тримма|После тримма|
|---|---|
|![image](https://user-images.githubusercontent.com/71254839/157741560-d4929c67-a7af-40dd-89c9-e17c9bba7717.png)|![image](https://user-images.githubusercontent.com/71254839/157741609-1ea53ff8-7f6f-4b9b-9e5a-1f56e020ce64.png)|

Согласно документации mean Phred Score уменьшилась в несколько раз (с 5 до 2)

В остальном, ситуация аналогичная предыдущим случаям. Анализирую сразу для trimmed, поскольку дальше буду работать с ним.

|![image](https://user-images.githubusercontent.com/71254839/157741941-2bc76d6f-cc89-4173-b99e-bd8a105e90a7.png)|![image](https://user-images.githubusercontent.com/71254839/157741990-b8ed8d00-9ece-4bd3-90a2-85ab10c62b90.png)|
|---|---|

### TIB Analysis

Ситуация аналогичная предыдущим.

|![image](https://user-images.githubusercontent.com/71254839/157742416-18fc2f88-e6f1-406d-ba5b-677ca8f36aa2.png)|![image](https://user-images.githubusercontent.com/71254839/157742452-92774632-e627-46a0-b1a4-57ad924d4f06.png)|
|---|---|

## Таблица со статистикой

|Образец|Выровнялось уникально|Выровнялось неуникально|Не выравнялось|
|---|---|---|---|
|ENCFF169TIB|914798, 3.24%|3600159, 12.76%|2370628, 84.00%|
|ENCFF425JDD_trimmed|2099808, 3.19%|8349181, 12.69%|55348936, 84.12%|
|ENCFF553XHZ|767192, 3.14%|3096438, 12.68%|20565292, 84.18%|
|ENCFF708OIN|530779, 3.15%|2037577, 12.11%|14260538, 84.74%|

Такой большой процент невыравенных чтений связан с тем, что выравнивание производилось на одну хромосому

### VENN

|GEQ-JDD|JDD-GEQ|
|---|---|
|![image](https://user-images.githubusercontent.com/71254839/157746938-e5299d8a-d0fd-44d0-ab26-188f4fe10f7f.png)|![image](https://user-images.githubusercontent.com/71254839/157747022-8d0db47a-1954-46be-a436-8e2730bcbe59.png)|

Интересный случай, когда неважно кого с кем пересекать.

---

|GEQ-OIN|OIN-GEQ|
|---|---|
|![image](https://user-images.githubusercontent.com/71254839/157747171-665e6a4e-8132-4dd4-9c32-0c56a0165ab5.png)|![image](https://user-images.githubusercontent.com/71254839/157747216-808738bd-d920-478e-b903-34977dd728cc.png)|


|GEQ-XHZ|XHZ-GEQ|
|---|---|
|![image](https://user-images.githubusercontent.com/71254839/157747361-9a139b48-ccbe-4944-a0d3-06a4b1824782.png)|![image](https://user-images.githubusercontent.com/71254839/157747418-4b89047d-7ba2-4f8f-aac4-79c132e9c957.png)|

В этих случаях можно отметить несколько наблюдений. Во-первых, от того, какое множетсво будет выбрано первым, зависит число пересечений. Во-вторых, наблюдается относительно небольшое число пересечений. 

Первую особенность можно объяснить тем, что мы по-разному инициализируем пересечения. Вторая особенность может быть связана с тем, что мы сравнивали наши пики (только 1 хромосома) и пики со всего генома. 

## Бонус

| ![image](https://github.com/basedinside/hse-hw2-chip/blob/main/Pic/result_xkv.png)|
|---|
|Распределение вряд ли совпадает с полученным экспериментально, это может быть по многим причинам|
