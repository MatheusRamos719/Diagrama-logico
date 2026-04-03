# Meu Projeto - Banco de Dados

## Diagrama Entidade-Relacionamento

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

## Legenda das Cardinalidades

| Símbolo | Significado |
|---------|-------------|
| `\|\|--o\{` | Um para Muitos (1 : N) |
| `\|\|--\|\|` | Um para Um (1 : 1) |
| `}o--o\{` | Muitos para Muitos (N : N) |

## Relacionamentos

- **UBS** atende muitos **Pacientes**
- **UBS** tem muitos **Profissionais** lotados
- **UBS** é local de coleta de muitos **Exames**
- **Paciente** realiza muitos **Exames**
- **Profissional** é responsável por muitos **Exames**
