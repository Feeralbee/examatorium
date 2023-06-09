# Просмотр истории заданий и тем

``` mermaid
stateDiagram-v2
    
    state "Выбор предмета" as setting_subjects_filter
    state "Выбор группы" as setting_groups_filter
    state "Выбор семестра" as setting_semesters_filter
    
    state "Запрос в БД 
        на получение информации
        о предметах, которые относятся 
        к этому преподавателю" as DB_query_for_subjects_information 
    state "Запрос в БД на 
        получение информации о группах, 
        у которых ведет преподаватель 
        выбранный предмет" as DB_query_for_groups_information
    state "Запрос в БД на 
            получение информации о семместрах, 
            в период которых данный преподаватель
            вел у этой группы ранее выбранный предмет" as DB_query_for_semesters_information

    state "Запрос в БД 
            на получение данных 
            о темах и вопросах для экзамена, 
            по заданным ранее параметрам" as DB_query_for_topics_and_tasks

    state "Вывод данных в виде таблицы" as output_table

    [*] --> DB_query_for_subjects_information
        note right of [*]: Создается новое дополнительное окно\n В этом окне преподаватель сможет ознакомится\n с темами и заданиями, которые давал студентам \nза прошлые семместры.
    DB_query_for_subjects_information --> setting_subjects_filter: полученные предметы\n помещаются в выпадающий список
    
    setting_subjects_filter --> DB_query_for_groups_information: при выборе предмета

    DB_query_for_groups_information --> setting_subjects_filter: возможна смена параметра
    DB_query_for_groups_information --> setting_groups_filter: после выбора предмета \nстановится активным\n выпадающий список с группами.\n Полученные данные\n помещаются в него

    setting_groups_filter --> setting_subjects_filter
    setting_groups_filter --> DB_query_for_semesters_information: при выборе группы

    DB_query_for_semesters_information --> setting_subjects_filter
    DB_query_for_semesters_information --> setting_groups_filter
    DB_query_for_semesters_information --> setting_semesters_filter: после выбора группы \nстановится активным\n выпадающий список с семместрами.\n Полученные данные\n помещаются в него

    setting_semesters_filter --> setting_subjects_filter
    setting_semesters_filter --> setting_groups_filter
    setting_semesters_filter --> DB_query_for_topics_and_tasks: при выборе значения из выпадающего списка

    DB_query_for_topics_and_tasks --> setting_semesters_filter
    DB_query_for_topics_and_tasks --> setting_subjects_filter
    DB_query_for_topics_and_tasks --> setting_groups_filter
    DB_query_for_topics_and_tasks --> output_table

    output_table --> setting_semesters_filter
    output_table --> setting_subjects_filter
    output_table --> setting_groups_filter
```
