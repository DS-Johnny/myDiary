## Diagrama Entidade-Relacionamento (ER)

```text
+------------------+
|      users       |
+------------------+
| id PK            |
| username         |
| email            |
| password_hash    |
| avatar_url       |
| created_at       |
| updated_at       |
+------------------+
         |
         | 1:N
         |
+------------------+
|     entries      |
+------------------+
| id PK            |
| user_id FK       |
| type_id FK       |
| title            |
| content          |
| audio_url        |
| entry_date       |
| favorite         |
| created_at       |
| updated_at       |
+------------------+
      |        |
      |        |
      |        +----------------------+
      |                               |
      |                               |
      | N:1                           | N:N
      |                               |
+------------------+        +------------------+
|   entry_types    |        |    entry_tags    |
+------------------+        +------------------+
| id PK            |        | entry_id FK      |
| name             |        | tag_id FK        |
+------------------+        +------------------+
                                     |
                                     | N:1
                                     |
                             +------------------+
                             |       tags       |
                             +------------------+
                             | id PK            |
                             | name             |
                             +------------------+
```

## Relacionamentos

| Origem | Relacionamento | Destino |
|--------|:--------------:|---------|
| `users` | 1:N | `entries` |
| `entry_types` | 1:N | `entries` |
| `entries` | N:N | `tags` (via `entry_tags`) |

## Tabelas

### users

Armazena as informações de autenticação e perfil dos usuários.

### entries

Tabela principal da aplicação. Cada registro representa um conteúdo criado pelo usuário.

Tipos possíveis:

- Diário
- Documento
- Frase
- Áudio

### entry_types

Define o tipo de cada registro.

| id | name |
|---:|------|
| 1 | diary |
| 2 | document |
| 3 | quote |
| 4 | audio |

### tags

Lista de tags utilizadas para organizar os registros.

### entry_tags

Tabela de relacionamento entre `entries` e `tags`, permitindo que um registro possua várias tags e que uma mesma tag seja utilizada em diferentes registros.