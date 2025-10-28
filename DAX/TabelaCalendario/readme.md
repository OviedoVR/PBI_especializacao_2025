# Tabela Calendário no Power BI

Pode ser criada manualmente ou via DAX.

Vantagens:

- Permite trabalhar melhor com filtros;
- Maior granularidade nos dados;
- Boa prática (modelagem de dados).

Criando com DAX:

1. Vá para a guia "Modelagem".
2. Selecione "Nova Tabela".
3. Cole o código abaixo na barra de fórmulas e ajuste as datas de início e fim conforme necessário.

```dax
CalendarTable = 
VAR StartDate = DATE(2020, 1, 1)  // Altere para a data de início desejada
VAR EndDate = DATE(2030, 12, 31)  // Altere para a data de fim desejada
RETURN
    ADDCOLUMNS(
        CALENDAR(StartDate, EndDate),
        "Year", YEAR([Date]),
        "Month", FORMAT([Date], "MMMM"),
        "Month Number", MONTH([Date]),
        "Quarter", "Q" & QUARTER([Date]),
        "Day", DAY([Date]),
        "Day of Week", FORMAT([Date], "dddd"),
        "Weekday Number", WEEKDAY([Date], 2)  // 1 = Domingo, 2 = Segunda
    )
```

Isso criará uma tabela de calendário completa que você pode usar em suas análises.

Caso você já tenha um coluna de data, o código fica:

```dax
CalendarTable = 
VAR StartDate = MIN(SuaTabela[Data])  // Data mínima da coluna
VAR EndDate = MAX(SuaTabela[Data])    // Data máxima da coluna
RETURN
    ADDCOLUMNS(
        CALENDAR(StartDate, EndDate),
        "Year", YEAR([Date]),
        "Month", FORMAT([Date], "MMMM"),
        "Month Number", MONTH([Date]),
        "Quarter", "Q" & QUARTER([Date]),
        "Day", DAY([Date]),
        "Day of Week", FORMAT([Date], "dddd"),
        "Weekday Number", WEEKDAY([Date], 2)
    )
```
