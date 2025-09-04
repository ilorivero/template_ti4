# 💾 Banco de Dados

Este documento descreve a arquitetura, o modelo e as coleções/tabelas do banco de dados utilizado no projeto.

## Tecnologia Escolhida

* **Nome:** Cloud Firestore (Google Firebase)
* **Tipo:** NoSQL (Banco de Dados de Documentos)
* **Motivo da Escolha:** Escalabilidade, sincronização em tempo real e integração facilitada com o Flutter através do ecossistema Firebase.

## Modelo Entidade-Relacionamento (MER)

O diagrama abaixo representa a relação entre as principais coleções do nosso banco de dados.

![Diagrama do Banco de Dados](https://via.placeholder.com/800x400.png?text=Diagrama+Entidade-Relacionamento)
*(Substitua a imagem por um diagrama real, criado em ferramentas como draw.io ou Lucidchart)*

## Descrição das Coleções

### Coleção `users`

Armazena as informações de todos os usuários do aplicativo (tutores e cuidadores).

* **Caminho:** `/users/{userId}`

| Campo           | Tipo      | Descrição                                         | Exemplo                               |
| --------------- | --------- | ------------------------------------------------- | ------------------------------------- |
| `uid`           | `string`  | ID único do usuário (gerado pelo Firebase Auth).  | `"abc123xyz"`                         |
| `displayName`   | `string`  | Nome de exibição do usuário.                      | `"João da Silva"`                     |
| `email`         | `string`  | Endereço de e-mail.                               | `"joao.silva@email.com"`              |
| `photoURL`      | `string`  | URL da foto de perfil.                            | `"https://.../photo.jpg"`             |
| `userType`      | `string`  | Tipo de usuário (`tutor` ou `cuidador`).          | `"tutor"`                             |
| `createdAt`     | `timestamp` | Data e hora de criação do registro.             | `September 04, 2025 at 10:00:00 AM UTC-3` |

### Coleção `caregivers_profiles`

Armazena informações adicionais específicas dos usuários que são cuidadores.

* **Caminho:** `/caregivers_profiles/{userId}`

| Campo         | Tipo      | Descrição                                 | Exemplo                   |
| ------------- | --------- | ----------------------------------------- | ------------------------- |
| `bio`         | `string`  | Uma breve biografia sobre o cuidador.     | `"Amo animais e... "`     |
| `pricePerHour`| `number`  | Preço cobrado por hora de serviço.        | `50.00`                   |
| `rating`      | `number`  | Média das avaliações (de 0 a 5).          | `4.8`                     |
| `location`    | `geopoint`| Localização do cuidador.                  | `Latitude, Longitude`     |

### Coleção `bookings`

Armazena os agendamentos realizados na plataforma.

* **Caminho:** `/bookings/{bookingId}`

| Campo         | Tipo        | Descrição                                 | Exemplo                   |
| ------------- | ----------- | ----------------------------------------- | ------------------------- |
| `tutorId`     | `reference` | Referência ao documento do tutor na coleção `users`. | `users/abc123xyz`         |
| `caregiverId` | `reference` | Referência ao documento do cuidador na coleção `users`. | `users/def456uvw`       |
| `startTime`   | `timestamp` | Início do serviço.                        | `...`                     |
| `endTime`     | `timestamp` | Fim do serviço.                           | `...`                     |
| `totalPrice`  | `number`    | Preço total do agendamento.               | `150.00`                  |
| `status`      | `string`    | Status (`pending`, `confirmed`, `completed`, `canceled`). | `"confirmed"`           |