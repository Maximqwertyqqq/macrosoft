marks = input('Введите оценки через пробел:')
marks = marks.split(' ')
a5 = 0
for mark in marks:
    if mark == '5':
       a5 += 1 
res = a5 / len(marks)*100
print('Получено пятёрок (%) -',res)

