﻿# Ollama C# Playground

這個實驗室旨在直接在 GitHub Codespaces 中使用 C# 範例測試 Phi-3，這是一種讓任何人都能在瀏覽器中完全試用 SLMs (小型語言模型) 的簡便方法。

## 如何測試

1. 使用倉庫頂部的 `程式碼` 按鈕建立一個新的 Codespace。選擇 [+ New with options ...]
![Create Codespace with options](./10NewCodespacesWithOptions.png)

1. 在選項頁面中，選擇名為 `Ollama with Phi-3 for C#` 的配置

**IMAGE GOES HERE**

1. 一旦 Codespace 被載入，它應該已經預先安裝了 [ollama](https://ollama.com/)，下載了最新的 Phi-3 模型，並且安裝了 [.NET 8](https://dotnet.microsoft.com/en-us/download)。

1. (可選) 使用 Codespace 終端機，要求 Ollama 執行 [phi3](https://ollama.com/library/phi3) 模型:

    ```shell
    ollama run phi3
    ```

4. 你可以從提示符向該模型發送訊息。

    ```shell
    >>> Write a joke about kittens
    ```

5. 幾秒鐘後，你應該會看到來自模型的回應流。

    ![run ollama and ask for a joke](./20ollamarunphi.gif)

1. 要了解與語言模型一起使用的不同技術，請查看 `.\src` 資料夾中的範例專案:

| Project | Description |
|---------|-------------|
| Sample01  | 這是一個範例專案，使用 Phi-3 託管在 ollama 模型中回答問題。 |
| Sample02  | 這是一個範例專案，使用 Semantic Kernel 實作一個控制台聊天。 |
| [Sample03](./src/Sample03/readme.md)  | 這是一個範例專案，使用本地嵌入和 Semantic Kernel 實作一個 RAG。查看本地 RAG 的詳細資訊[這裡](./src/Sample03/readme.md)。

## 如何執行一個範例

1. 打開終端並導航到所需的專案。例如，讓我們執行 `Sample02`，即控制台聊天。

    ```bash
    cd .\src\Sample02\
    ```

1. 使用以下命令執行專案

    ```bash
    dotnet run
    ```

1. 專案 `Sample02` 定義了一個自訂的系統訊息：

    ```csharp
    var history = new ChatHistory();
    history.AddSystemMessage("You are a useful chatbot. If you don't know an answer, say 'I don't know!'. Always reply in a funny ways. Use emojis if possible.");
    ```

1. 因此，當使用者問問題時，例如 `What is the capital of Italy?`，聊天將使用本地模式回應。

    輸出類似於以下內容：

    ![Chat running demo](./20SampleConsole.png)

## 影片指南

如果你想了解更多關於如何在 GitHub Repository 中使用 Codespaces 與 Ollama，請查看以下 3 分鐘 影片:

[![觀看影片](./40ytintro.jpg)](https://youtu.be/HmKpHErUEHM)

