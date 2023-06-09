# Диаграмма состояний приложения

``` mermaid
stateDiagram-v2
    state "Ввод ФИО преподователя" as authorization

    state "Запрос в БД
            содержащую учебный план 
            на получение информации о преподавателе по ФИО" as DB_query_for_teacher_information
    
    state "Главная" as main
    state "Просмотр тем и заданий за прошлые семестры" as reviewing_themes_and_assignments
        note right of reviewing_themes_and_assignments: Диаграмма состояний этого окна\n представлена в файле history_of_tasks_state_diagram.md
    state "Раздел создания билетов" as ticket_creation_section
        note right of ticket_creation_section: Диаграмма состояний этого раздела\n представлена в файле ticket_creation_state_diagram.md
    state "Модальное диалоговое окно с информацией, 
            что данный преподаватель не найден" as teacher_error_window

    [*] --> authorization 
    authorization --> DB_query_for_teacher_information: при нажатии кнопки "Войти"
    
    DB_query_for_teacher_information --> main: если преподователь найден в базе
    DB_query_for_teacher_information --> teacher_error_window: если преподаватель не найден

    teacher_error_window --> authorization: при закрытии окна сообщения

    main --> authorization: при нажатии кнопки "Смена пользователя"
    main --> reviewing_themes_and_assignments: при нажатии кнокпи "История заданий"
    main --> ticket_creation_section: при нажатии кнопки\n "Создать новые билеты"


    ticket_creation_section --> main: при нажатии кнопки\n "Возврат на главную"
```
