# ☕ Spring Boot AI Backend Service (`SpringAiDemo`)

<div align="center">

![Java](https://img.shields.io/badge/Java-17%2B-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.5.9-6DB33F?style=for-the-badge&logo=spring&logoColor=white)
![Spring AI](https://img.shields.io/badge/Spring_AI-1.1.2-6DB33F?style=for-the-badge&logo=spring&logoColor=white)
![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4o%20%7C%20DALL--E--2-412991?style=for-the-badge&logo=openai&logoColor=white)

Backend API service for the **Spring AI Full-Stack Suite**, powered by **Spring Boot 3.5.9**, **Java 17**, and **Spring AI 1.1.2**.

</div>

---

## 📋 Architecture & Core Services

This service exposes REST APIs on port `8080` and configures cross-origin requests (`CORS`) via [WebConfig.java](file:///d:/imp/Study/Project/SpringAiDemo/SpringAiDemo/src/main/java/com/example/SpringAiDemo/WebConfig.java) to enable communication with the React frontend running on `http://localhost:3000`.

### Core AI Beans & Services
1. **[ChatService.java](file:///d:/imp/Study/Project/SpringAiDemo/SpringAiDemo/src/main/java/com/example/SpringAiDemo/ChatService.java)**
   * Wraps `org.springframework.ai.chat.model.ChatModel` to execute OpenAI text prompts.
   * `getResponse(prompt)`: Standard execution.
   * `getResponseOptions(prompt)`: Utilizes `OpenAiChatOptions` tailored for model `gpt-4o` with `temperature(0.4)` and `maxTokens(200)`.

2. **[ImageService.java](file:///d:/imp/Study/Project/SpringAiDemo/SpringAiDemo/src/main/java/com/example/SpringAiDemo/ImageService.java)**
   * Wraps `org.springframework.ai.openai.OpenAiImageModel` to generate visual assets using `dall-e-2`.
   * Accepts dynamic parameters for count (`n`), height, and width, returning structured `ImageResponse` output containing public URLs.

3. **[RecipeService.java](file:///d:/imp/Study/Project/SpringAiDemo/SpringAiDemo/src/main/java/com/example/SpringAiDemo/RecipeService.java)**
   * Leverages Spring AI's `PromptTemplate` to inject user-provided ingredients, cuisine style, and dietary constraints into a structured cooking instruction prompt sent to `gpt-4o`.

---

## 🛠️ Getting Started

### 1. Configure OpenAI API Key
Before running the Spring Boot backend, set your OpenAI secret key:

**Option 1: Environment Variable (Recommended)**
```bash
# PowerShell
$env:SPRING_AI_OPENAI_API_KEY="sk-proj-..."

# Linux / macOS
export SPRING_AI_OPENAI_API_KEY="sk-proj-..."
```

**Option 2: `application.properties`**
Update [src/main/resources/application.properties](file:///d:/imp/Study/Project/SpringAiDemo/SpringAiDemo/src/main/resources/application.properties):
```properties
spring.application.name=SpringAiDemo
spring.ai.openai.api-key=sk-proj-your-api-key-here
```

### 2. Build & Run
From this folder (`SpringAiDemo/SpringAiDemo`), execute:
```bash
mvn clean install
mvn spring-boot:run
```
The server will start on **`http://localhost:8080`**.

---

## 🔌 Endpoints Overview

| HTTP Method | Endpoint | Parameters | Service Handler |
| :---: | :--- | :--- | :--- |
| `GET` | `/ask-ai` | `prompt` (string) | `ChatService.getResponse` |
| `GET` | `/ask-ai-options` | `prompt` (string) | `ChatService.getResponseOptions` |
| `GET` | `/generate-image` | `prompt`, `n`, `width`, `height` | `ImageService.generateImage` |
| `GET` | `/reciepe-creator` | `ingredients`, `cuisine`, `dietaryRestrcitions` | `RecipeService.createRecipe` |
