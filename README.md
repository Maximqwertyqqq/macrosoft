marks = input('Введите оценки через пробел:')
marks = marks.split(' ')
print('Анализ набора', marks)
growth = 1
growth = 1 #по умолчанию у всех рост
for i in range(len(marks)-1):
    if marks[i+1] < marks[i]: #если текущая оценка меньше следующей
        growth = -1
if growth == 1:
    print('Стабильная успеваемость!') #успеваемость не стабильна
else:
    print('Стабильной успеваемости нет')

#допиши вывод результатов
