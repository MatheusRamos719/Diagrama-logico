# Banco de Dados - Modelo Entidade-Relacionamento

## Diagrama ER

```mermaid
erDiagram
    UBS {
        int id_ubs PK "🔑"
        string cnes UK "🔒"
        string nome
        string endereco
        string cidade
        string estado
        decimal latitude
        decimal longitude
    }
    
    Paciente {
        int id_paciente PK "🔑"
        string nome
        date data_nascimento
        string sexo
        string telefone
        string endereco
        int id_ubs FK
    }
    
    Profissional {
        int id_profissional PK "🔑"
        string nome
        string login UK "🔒"
        string senha_hash
        enum perfil
        int id_ubs FK
    }
    
    Exame {
        int id_exame PK "🔑"
        enum tipo_exame
        decimal score_ia
        string caminho_imagem
        timestamp data_hora
        int id_paciente FK
        int id_profissional_responsavel FK
        int id_ubs_coleta FK
    }
    
    UBS ||--o{ Paciente : "atende"
    UBS ||--o{ Profissional : "lotado em"
    UBS ||--o{ Exame : "local de coleta"
    Paciente ||--o{ Exame : "realiza"
    Profissional ||--o{ Exame : "responsável por"
```

## Cardinalidades

| Símbolo | Significado |
|---------|-------------|
| ||--o{ | Um para muitos (1 : N) |
| ||--|| | Um para um (1 : 1) |
| }o--o{ | Muitos para muitos (N : N) |
