classDiagram
    class Животное {
        +String имя
        +void есть()
    }
    class Собака {
        +void лаять()
    }
    Животное <|-- Собака
