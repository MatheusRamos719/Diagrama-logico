# Banco de Dados - Modelo Entidade-Relacionamento

## Diagrama ER

```mermaid
%%{init: {'theme': 'forest'}}%%
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
    
    Paciente }o--|| UBS : "pertence a"
    Profissional }o--|| UBS : "lotado em"
    Exame }o--|| UBS : "coletado em"
    Exame }o--|| Paciente : "pertence a"
    Exame }o--|| Profissional : "responsável por"
