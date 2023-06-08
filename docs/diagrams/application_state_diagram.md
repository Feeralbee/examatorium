# Диаграмма состояний приложения

``` mermaid
stateDiagram-v2
    state "Ввод ФИО преподователя" as authorization
    state "Главная" as main
    
    state "Запрос в БД содержащую\n учебный план\n на получение информации\n о преподавателе по ФИО" as DB_query_for_teacher_information

    state "Модальное диалоговое окно\n с информацией,\n что данный преподаватель\n не найден" as teacher_error_window

    [*] --> authorization 
    authorization --> DB_query_for_teacher_information

    DB_query_for_teacher_information --> main: если преподователь\n найден в базе
    DB_query_for_teacher_information --> teacher_error_window: если преподаватель\n не найден
    
    teacher_error_window --> authorization: возврат\n на страницу авторизации

    main --> authorization: смена преподавателя
```
