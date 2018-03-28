# -1.5.-
# Имеется группа студентов, у каждого из которых есть следующие характеристики: имя, фамилия, пол, предыдущий опыт в программировании (бинарная переменная), 5 оцененных по 10-бальной шкале домашних работ, оценка за экзамен по 10-балльной шкале. Необходимо написать программу, которая в зависимости от запроса пользователя будет выводить:

students_results = [{'name': 'Ivan', 'lastname': 'Petrov', 'gender': 'Male', 'experience': True, 'results': {'homework': [7, 8, 10, 6, 7], 'exam': [8]}},
{'name': 'Victor', 'lastname': 'Eliseev', 'gender': 'Male', 'experience': True, 'results': {'homework': [7, 7, 6, 6, 7], 'exam': [8]}},
{'name': 'Anton', 'lastname': 'Sobolev', 'gender': 'Male', 'experience': False, 'results': {'homework': [5, 6, 7, 5, 7], 'exam': [6]}},
{'name': 'Anna', 'lastname': 'Ivanova', 'gender': 'Female', 'experience': False, 'results': {'homework': [9, 8, 8, 6, 10], 'exam': [9]}},
{'name': 'Anna', 'lastname': 'Egorova', 'gender': 'Female', 'experience': False, 'results': {'homework': [9, 8, 8, 6, 10], 'exam': [9]}},
{'name': 'Ekaterina', 'lastname': 'Sokolova', 'gender': 'Female', 'experience': True, 'results': {'homework': [7, 6, 5, 6, 7], 'exam': [6]}}
]

# print(students_results)

# среднюю оценку за домашние задания и за экзамен по всем группе в следующем виде:
#         Средняя оценка за домашние задания по группе: X
#         Средняя оценка за экзамен: Y
# где X и Y - вычисляемые значения;

# def avg_results(students_results_list, type_of_work):
#   sum_results = 0
#   for i in range(len(students_results_list)):
#     sum_results += sum(students_results_list[i]['results'][type_of_work])/float(len(students_results_list[i]['results'][type_of_work]))
#   avg_res = round(sum_results / float(len(students_results_list)),2)
#   return avg_res

# def avg_results(students_results_list, type_of_work):
#   sum_results = 0
#   for student in students_results_list:
#     sum_results += sum(student['results'][type_of_work])/float(len(student['results'][type_of_work]))
#   avg_res = round(sum_results / float(len(students_results_list)),2)
#   return avg_res

def avg_results(students_results_list, type_of_work):
  results_list = []
  for student in students_results_list:
    results_list += student['results'][type_of_work]
  avg_res = round(sum(results_list) / float(len(results_list)),2)
  return avg_res


X = avg_results(students_results, 'homework')
print('Средняя оценка за домашние задания по группе: ', X)

Y = avg_results(students_results, 'exam')
print('Средняя оценка за экзамен: ', Y)


# среднюю оценку за домашние задания и за экзамен по группе в разрезе: а)пола б)наличия опыта в виде:
#         Средняя оценка за домашние задания у мужчин: A
#         Средняя оценка за экзамен у мужчин: B
#         Средняя оценка за домашние задания у женщин: C
#         Средняя оценка за экзамен у женщин: D
        
#         Средняя оценка за домашние задания у студентов с опытом: E
#         Средняя оценка за экзамен у студентов с опытом: F        
#         Средняя оценка за домашние задания у студентов без опыта: G
#         Средняя оценка за экзамен у студентов без опыта: H
# где A, B, C, D, E, F, G, H - вычисляемые значения;

def list_slice_gender(students_results_list, gender_value):
  students_results_list_slice = []
  for i in range(len(students_results_list)):
    if students_results_list[i]['gender'] == gender_value:
      students_results_list_slice.append(students_results_list[i])
  return students_results_list_slice


A = avg_results(list_slice_gender(students_results,'Male'),'homework')
print('Средняя оценка за домашние задания у мужчин: ', A)

B = avg_results(list_slice_gender(students_results,'Male'),'exam')
print('Средняя оценка за экзамен у мужчин: ', B)

C = avg_results(list_slice_gender(students_results,'Female'),'homework')
print('Средняя оценка за домашние задания у женщин: ', C)

D = avg_results(list_slice_gender(students_results,'Female'),'exam')
print('Средняя оценка за экзамен у женщин: ', D)


def list_slice_experience(students_results_list, experience_value):
  students_results_list_slice = []
  for i in range(len(students_results_list)):
    if students_results_list[i]['experience'] == experience_value:
      students_results_list_slice.append(students_results_list[i])
  return students_results_list_slice

E = avg_results(list_slice_experience(students_results,True),'homework')
print('Средняя оценка за домашние задания у студентов с опытом: ',E)

F = avg_results(list_slice_experience(students_results,True),'exam')
print('Средняя оценка за экзамен у студентов с опытом: ',F)        

G = avg_results(list_slice_experience(students_results,False),'homework')
print('Средняя оценка за домашние задания у студентов без опыта: ',G)

H = avg_results(list_slice_experience(students_results,False),'exam')
print('Средняя оценка за экзамен у студентов без опыта: ',H)

# определять лучшего студента, у которого будет максимальный балл по формуле 0.6 * его средняя оценка за домашние задания + 0.4 * оценка за экзамен в виде:
# Лучший студент: S с интегральной оценкой Z
# если студент один или:
# Лучшие студенты: S... с интегральной оценкой Z
# если студентов несколько, где S - имя/имена студентов, Z - вычисляемое значение.

def student_result_compound(student):
  homework_result = round(sum(student['results']['homework'])/float(len(student['results']['homework'])) , 2)
  exam_result = student['results']['exam'][0]
  score_compound = round(0.6 * homework_result + 0.4 * exam_result,2)
  return score_compound

score_compound_list = []
for student in students_results:
  score_compound_list.append(student_result_compound(student))
  

def best_students(students_results_list,score_compound_list):
  best_students_list =[]
  max_score = max(score_compound_list)
  for student in students_results_list:
    if student_result_compound(student) == max_score:
      best_students_list.append(student['name'] + ' ' + student['lastname'])
  best_students_list_sring = " ".join(str(x) for x in best_students_list)
  return best_students_list_sring

print(best_students(students_results,score_compound_list))

S = best_students(students_results,score_compound_list)
Z = max(score_compound_list)
if score_compound_list.count(Z) == 1:
   print('Лучший студент: ', S, 'с интегральной оценкой ',Z)
else:
  print('Лучшие студенты: ', S, 'с интегральной оценкой ',Z)


# Студентов должно быть не менее 6. 
# Код должен быть грамотно декомпозирован (максимально используйте функции).
