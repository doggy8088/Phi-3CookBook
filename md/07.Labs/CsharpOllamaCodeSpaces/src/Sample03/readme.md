﻿# 完整本地 RAG 場景使用 Phi-3、SemanticKernel 和 TextMemory

## 簡介

歡迎來到使用 Phi-3、SemanticKernel 和 TextMemory 的完整本地 RAG 場景的儲存庫。這個專案展示了 Phi-3 的強大功能，這是一個突破性的 小型語言模型 (SLM)，正在重新定義開發者和企業的 AI 能力。

## 情境概述

展示場景旨在回答「Bruno 最喜歡的超級英雄是誰？」這個問題，使用兩種不同的方法:

1. 直接詢問 Phi-3 模型。
2. 新增一個語義記憶物件，載入粉絲事實資訊，然後提出問題。

## 全情境的重要性

Phi-3 代表了小型語言模型的一個重大飛躍，提供了性能和效率的獨特結合。它能夠獨立處理完整的場景，這簡化了開發過程並減少了整合的複雜性。

## 程式碼說明

這個控制台應用程式展示了在 Ollama 中託管的本地模型和語義記憶體用於搜尋的使用。該程式使用了幾個外部函式庫來進行相依性注入、配置和語義核心及記憶體功能。

## 如何測試

1. 開啟終端機並導航到當前專案。

    ```bash
    cd .\src\Sample03\
    ```

1. 使用以下命令執行專案

    ```bash
    dotnet run
    ```

1. 專案 `Sample03`，回答以下問題：

    ```csharp
    var question = "Bruno 最喜歡的超級英雄是誰？"
    ```

1. 首先將問題直接問 Phi-3 模型。然後，程式將以下資訊載入文字記憶體中，並再次問問題。

    ```csharp

    // 獲取嵌入生成服務
    var embeddingGenerator = kernel.Services.GetRequiredService<ITextEmbeddingGenerationService>();
    var memory = new SemanticTextMemory(new VolatileMemoryStore(), embeddingGenerator);    

    // 將事實添加到集合中
    const string MemoryCollectionName = "fanFacts";
    
    await memory.SaveInformationAsync(MemoryCollectionName, id: "info1", 
            text: "Gisela 最喜歡的超級英雄是蝙蝠俠");
    await memory.SaveInformationAsync(MemoryCollectionName, id: "info2", 
            text: "Gisela 最近看的超級英雄電影是《銀河護衛隊 3》");
    await memory.SaveInformationAsync(MemoryCollectionName, id: "info3", 
            text: "Bruno 最喜歡的超級英雄是無敵少俠");
    await memory.SaveInformationAsync(MemoryCollectionName, id: "info4", 
            text: "Bruno 最近看的超級英雄電影是《水行俠 II》");
    await memory.SaveInformationAsync(MemoryCollectionName, id: "info5", 
            text: "Bruno 不喜歡的超級英雄電影是《永恆族》");    
    ```

1. 一旦文字記憶體準備好，它將作為插件載入到核心中。

    ```csharp
    TextMemoryPlugin memoryPlugin = new(memory);
    
    // 將文字記憶體插件導入到核心中。
    kernel.ImportPluginFromObject(memoryPlugin);    
    ```

1. 這是在 Codespace 中執行的展示控制台應用程式：

    ![在 Codespace 中執行的展示控制台應用程式](./img/10RAGPhi3.gif)

## 參考資料

- [Phi-3 Microsoft Blog](https://aka.ms/phi3blog-april)
- [Phi-3 Technical Report](https://aka.ms/phi3-tech-report)
- [Phi-3 Cookbook](https://aka.ms/Phi-3CookBook)
- [生成式 AI for 初學者](https://github.com/microsoft/generative-ai-for-beginners)
- [語義核心主存放庫](https://github.com/microsoft/semantic-kernel)
- [智慧元件 - 本地嵌入](https://github.com/dotnet-smartcomponents/smartcomponents/blob/main/docs/local-embeddings.md)

