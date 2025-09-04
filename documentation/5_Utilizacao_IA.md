# 🧠 05 - Utilização de Inteligência Artificial

Este documento descreve a arquitetura, os modelos e a integração de funcionalidades baseadas em Inteligência Artificial (IA) no projeto.

## 1. Objetivo da IA no Projeto

O principal objetivo de utilizar IA neste aplicativo é [descrever o objetivo principal aqui].

* **Exemplo 1 (Sistema de Recomendação):** *Sugerir os cuidadores mais compatíveis para um tutor com base no perfil do seu pet (espécie, porte, idade, comportamento) e nas avaliações de outros usuários com perfis semelhantes.*
* **Exemplo 2 (Processamento de Linguagem Natural):** *Analisar o sentimento das avaliações escritas para gerar uma pontuação de satisfação mais precisa e identificar pontos fortes ou fracos de um cuidador.*
* **Exemplo 3 (Visão Computacional):** *Verificar se a foto de perfil enviada por um usuário é de fato uma pessoa ou um animal, ou validar documentos de identificação.*

## 2. Modelo(s) e Tecnologia(s) Utilizada(s)

A tabela abaixo detalha os modelos e serviços de IA empregados.

| Finalidade do Modelo        | Tecnologia / Framework              | Como é Acessado (API/Embarcado) |
| --------------------------- | ----------------------------------- | ------------------------------- |
| **Sistema de Recomendação** | Python (Scikit-learn, Pandas)       | API REST em um servidor backend |
| **Análise de Sentimento** | Google Cloud Natural Language API   | Chamada de API direta         |
| **Chatbot de Suporte** | Google Dialogflow                   | SDK do Dialogflow / API REST    |
| **Reconhecimento de Imagem** | TensorFlow Lite                     | Modelo embarcado (.tflite)    |
| **[Adicionar outro modelo]** | [Framework]                         | [API / Embarcado]               |

## 3. Integração com o Aplicativo Flutter

A comunicação entre o aplicativo Flutter e os modelos de IA é realizada da seguinte forma:

### Para Modelos via API (Backend)

* **Fluxo:** O aplicativo Flutter faz uma requisição HTTP (usando pacotes como `http` ou `dio`) para um endpoint específico no nosso servidor backend.
* **Endpoint de Exemplo:** `POST /api/v1/recommendations`
* **Corpo da Requisição (Request Body):**
    ```json
    {
      "userId": "user123",
      "petProfile": {
        "species": "cachorro",
        "size": "medio",
        "temperament": ["calmo", "sociável"]
      }
    }
    ```
* **Resposta (Response):**
    ```json
    {
      "recommendations": [
        {"caregiverId": "caregiver456", "score": 0.95},
        {"caregiverId": "caregiver789", "score": 0.91}
      ]
    }
    ```

### Para Modelos Embarcados (On-Device)

* **Fluxo:** O modelo de IA (ex: um arquivo `.tflite`) é incluído nos assets do aplicativo. Utilizamos o pacote `tflite_flutter` para carregar o modelo na memória e executar inferências diretamente no dispositivo do usuário.
* **Vantagens:** Funcionamento offline, latência muito baixa e maior privacidade (os dados do usuário não saem do dispositivo).
* **Desvantagens:** Consome mais recursos do dispositivo (bateria, processamento) e os modelos precisam ser pequenos e otimizados.

## 4. Fluxo de Dados

1.  O usuário realiza uma ação no aplicativo (ex: abre a tela de busca por cuidadores).
2.  O aplicativo coleta os dados necessários (ex: perfil do pet do usuário).
3.  Os dados são enviados para o serviço de IA apropriado (API backend ou modelo local).
4.  O modelo processa os dados e retorna um resultado (ex: uma lista de IDs de cuidadores recomendados).
5.  O aplicativo recebe o resultado e atualiza a interface do usuário para exibi-lo de forma amigável.