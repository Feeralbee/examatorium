# Диаграмма состояний приложения

``` mermaid
stateDiagram-v2
    state "Ввод ФИО преподователя" as authorization

    state "Запрос в БД
            содержащую учебный план 
            на получение информации о преподавателе по ФИО" as DB_query_for_teacher_information
    
    state "Главная" as main
    state "Просмотр тем и заданий за прошлые семестры" as reviewing_themes_and_assignments
    note right of reviewing_themes_and_assignments: В этом окне преподаватель сможет ознакомится\n с темами и заданиями, которые давал студентам \nза прошлые семместры. \n Диаграмма состояний этого окна\n представлена в файле history_of_tasks_state_diagram.md
    state "Раздел создания билетов" as ticket_creation_section
    state "Модальное диалоговое окно с информацией, 
            что данный преподаватель не найден" as teacher_error_window

    [*] --> authorization 
    authorization --> DB_query_for_teacher_information
    
    DB_query_for_teacher_information --> main: если преподователь найден в базе
    DB_query_for_teacher_information --> teacher_error_window: если преподаватель не найден

    teacher_error_window --> authorization: возврат на страницу авторизации

    main --> authorization: смена преподавателя
    main --> reviewing_themes_and_assignments: Создается новое дополнительное окно
    main --> ticket_creation_section
    note right of ticket_creation_section: Диаграмма состояний этого раздела\n представлена в файле ticket_creation_state_diagram.md

    ticket_creation_section --> main: возврат на главную страницу
```
