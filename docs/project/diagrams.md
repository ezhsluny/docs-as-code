# Диаграммы

## Диаграмма последовательности

```mermaid
sequenceDiagram
    actor HR as HR-специалист
    participant System as Система
    participant Model as ML-модель (NLP/NER)
    participant DB as Хранилище данных

    HR->>System: Открыть резюме и нажать «Анализировать»
    System->>Model: Передать текст резюме
    Model-->>System: Вернуть извлечённые сущности и уверенность
    System->>System: Нормализовать данные
    System->>DB: Сохранить структурированные данные
    DB-->>System: Подтвердить сохранение

    alt Уверенность ниже порога или ошибка извлечения
        System-->>HR: Сообщить о необходимости ручной проверки
    else Успешное извлечение
        System-->>HR: Показать блоки «Навыки», «Образование», «Опыт работы»
    end
```

## Диаграмма классов

```mermaid
classDiagram
    class User {
        +int id
        +string name
        +string role
    }

    class Resume {
        +int id
        +string fileName
        +string text
        +string status
    }

    class ResumeAnalysis {
        +int id
        +list skills
        +list education
        +list experience
        +float confidence
    }

    class Vacancy {
        +int id
        +string title
        +list requiredSkills
        +string description
    }

    class MatchResult {
        +int id
        +float score
        +list matchedRequirements
        +list missingRequirements
    }

    User "1" --> "*" Resume : загружает
    Resume "1" --> "1" ResumeAnalysis : анализируется в
    User "1" --> "*" Vacancy : создаёт
    ResumeAnalysis "*" --> "*" Vacancy : сравнивается через
    ResumeAnalysis "1" --> "*" MatchResult : формирует
    Vacancy "1" --> "*" MatchResult : оценивается в
```