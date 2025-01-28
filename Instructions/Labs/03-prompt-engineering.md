# ラボ 03: アプリでプロンプトエンジニアリングを活用する

## ラボシナリオ

Azure OpenAI サービスを使用する際、開発者がプロンプトをどのように形作るかが、生成AIモデルの応答に大きく影響します。Azure OpenAI モデルは、明確かつ簡潔な方法でリクエストされた場合に、コンテンツを調整および形式化することができます。この演習では、似たようなコンテンツに対して異なるプロンプトが AI モデルの応答をどのように形作り、要求を満たすためにどのように役立つかを学びます。

この演習のシナリオでは、野生動物マーケティングキャンペーンに取り組んでいるソフトウェア開発者の役割を果たします。生成AIを活用して広告メールを改善し、チームに適用できる可能性のある記事を分類する方法を模索しています。演習で使用されるプロンプトエンジニアリングの技術は、さまざまなユースケースに同様に適用できます。

## ラボの目的
このラボでは、次のタスクを完了します：

- タスク 1: チャットプレイグラウンドでプロンプトエンジニアリングを適用する
- タスク 2: Cloud Shell でアプリケーションをセットアップする
- タスク 3: アプリケーションを構成する
- タスク 4: アプリケーションを実行する

## 推定時間: 60 分

### タスク 1: チャットプレイグラウンドでプロンプトエンジニアリングを適用する

このタスクでは、プロンプトエンジニアリングがプレイグラウンドでモデルの応答をどのように改善するかを、動物の名前を使った楽しい名前の Python アプリの作成など、さまざまなプロンプトを試すことで検証します。

1. [Azure AI Foundry ポータル](https://oai.azure.com/?azure-portal=true) で、左ペインの **Chat** プレイグラウンドに移動し、デプロイメントペインで **my-gpt-model** モデルが選択されていることを確認します。

1. デフォルトの **Give the model instructions and context** を確認し、それが *You are an AI assistant that helps people find information.*（あなたは、人々が情報を見つけるのを助けるAIアシスタントです。）であることを確認します。

1. **Chat session** で次のクエリを送信します：
    ```prompt
    What kind of article is this?
    ---
    Severe drought likely in California
    
    Millions of California residents are bracing for less water and dry lawns as drought threatens to leave a large swath of the region with a growing water shortage.
    
    In a remarkable indication of drought severity, officials in Southern California have declared a first-of-its-kind action limiting outdoor water use to one day a week for nearly 8 million residents.
    
    Much remains to be determined about how daily life will change as people adjust to a drier normal. But officials are warning the situation is dire and could lead to even more severe limits later in the year.
    ```
    
    >**任意:** 日本語訳のプロンプトは
    ```prompt
    この記事はどのような種類のものですか？
    ---
    カリフォルニアで深刻な干ばつの可能性

    干ばつが地域の広範囲にわたる水不足をもたらす恐れがあるため、カリフォルニア州の何百万人もの住民は水不足と乾燥した芝生に備えています。

    干ばつの深刻さを示す驚くべき兆候として、南カリフォルニアの当局者は、約800万人の住民に対して、屋外での水の使用を週に1日に制限するという初めての措置を宣言しました。

    人々が乾燥した日常に適応する中で、日常生活がどのように変わるかについては、多くが未確定です。しかし、当局者は状況が深刻であり、今年後半にはさらに厳しい制限に至る可能性があると警告しています。
    ```

応答は記事の説明を提供します。ただし、記事の分類のためのより具体的な形式が必要な場合を考えます。

1. **Setup** セクションで、**Give the model instructions and context** を `You are a news aggregator that categorizes news articles.`（あなたはニュース記事を分類するニュースアグリゲーターです）に変更します。

6. 新しいシステムメッセージの下で、**Add section** ボタンを選択し、**Examples** を選びます。次に次の例を追加します。

    **User:**
    ```prompt
    What kind of article is this?
    ---
    New York Baseballers Wins Big Against Chicago
    
    New York Baseballers mounted a big 5-0 shutout against the Chicago Cyclones last night, solidifying their win with a 3 run homerun late in the bottom of the 7th inning.
    
    Pitcher Mario Rogers threw 96 pitches with only two hits for New York, marking his best performance this year.
    
    The Chicago Cyclones' two hits came in the 2nd and the 5th innings but were unable to get the runner home to score.
    ```
    **Assistant:**
    ```prompt
    Sports
      ```

    
    >**任意:** 日本語訳のプロンプトは
   **User:**
    ```prompt
   この記事はどのような種類のものですか？
    ---
    ニューヨーク・ベースボールズがシカゴに大勝

    昨夜、ニューヨーク・ベースボールズはシカゴ・サイクロンズに対して5-0の大勝を収め、第7回裏の終盤に3ランホームランで勝利を確定させました。

    投手のマリオ・ロジャースは、ニューヨークのために96球を投げてわずか2安打を許し、今年の最高のパフォーマンスを記録しました。

    シカゴ・サイクロンズの2安打は第2回と第5回に出ましたが、ランナーをホームに戻すことができませんでした。
    ```
    **Assistant:**
    ```prompt
    スポーツ
      ```

7. 次のテキストで別の例を追加します。
    **User:**
    ```prompt
    Categorize this article:
    ---
    Joyous moments at the Oscars
    
    The Oscars this past week where quite something!
    
    Though a certain scandal might have stolen the show, this year's Academy Awards were full of moments that filled us with joy and even moved us to tears.
    These actors and actresses delivered some truly emotional performances, along with some great laughs, to get us through the winter.
    
    From Robin Kline's history-making win to a full performance by none other than Casey Jensen herself, don't miss tomorrows rerun of all the festivities.
    ```
    **Assistant:**
    ```prompt
    Entertainment
    ```

    
    >**任意:** 日本語訳のプロンプトは
   **User:** 
    ```prompt
    この記事はどのような種類のものですか？
    ---
    ニューヨーク・ベースボールズがシカゴに大勝

    昨夜、ニューヨーク・ベースボールズはシカゴ・サイクロンズに対して5-0の大勝を収め、第7回裏の終盤に3ランホームランで勝利を確定させました。

    投手のマリオ・ロジャースは、ニューヨークのために96球を投げてわずか2安打を許し、今年の最高のパフォーマンスを記録しました。

    シカゴ・サイクロンズの2安打は第2回と第5回に出ましたが、ランナーをホームに戻すことができませんでした。
    ``` 
    **Assistant:**
    ```prompt
    エンターテインメント
      ```
8. **Apply changes** ボタンを使用して、変更を保存します。

9. **Chat session** セクションで、次のプロンプトを再送信します：

    ```prompt
    What kind of article is this?
    ---
    Severe drought likely in California
    
    Millions of California residents are bracing for less water and dry lawns as drought threatens to leave a large swath of the region with a growing water shortage.
    
    In a remarkable indication of drought severity, officials in Southern California have declared a first-of-its-kind action limiting outdoor water use to one day a week for nearly 8 million residents.
    
    Much remains to be determined about how daily life will change as people adjust to a drier normal. But officials are warning the situation is dire and could lead to even more severe limits later in the year.
    ```
    >**任意:** 日本語訳のプロンプトは
   **User:**
    ```prompt
    この記事はどのような種類のものですか？
    ---
    カリフォルニアで深刻な干ばつの可能性

    干ばつが地域の広範囲にわたる水不足をもたらす恐れがあるため、カリフォルニア州の何百万人もの住民は水不足と乾燥した芝生に備えています。

    干ばつの深刻さを示す驚くべき兆候として、南カリフォルニアの当局者は、約800万人の住民に対して、屋外での水の使用を週に1日に制限するという初めての措置を宣言しました。

    人々が乾燥した日常に適応する中で、日常生活がどのように変わるかについては、多くが未確定です。しかし、当局者は状況が深刻であり、今年後半にはさらに厳しい制限に至る可能性があると警告しています。
    ```

    より具体的なシステムメッセージと期待されるクエリと応答の例を組み合わせることで、一貫した形式の結果を得ることができます。

10. **Give the model instructions and context** を `You are an AI assistant that helps people find information.`（あなたは人々が情報を見つけるのを助けるAIアシスタントです。）に設定し、例は設定しません。**Apply changes** をクリックして変更を保存し、その後 **Continue** をクリックして新しいセッションを開始し、チャットシステムの動作コンテキストを設定します。

11. **Chat session** セクションで、次のプロンプトを送信します：

    ```prompt
    # 1. Create a list of animals
    # 2. Create a list of whimsical names for those animals
    # 3. Combine them randomly into a list of 25 animal and name pairs
    ```

    >**任意:** 日本語訳のプロンプトは
    ```prompt
    # 1. 動物のリストを作成する
    # 2. それらの動物に対して風変わりな名前のリストを作成する
    # 3. ランダムに組み合わせて、25組の動物と名前のペアを作成する
    ```

    モデルは、プロンプトを満たすための回答を番号付きリストに分割して返す可能性があります。これは適切な応答ですが、実際に求めていたのは、モデルに指定したタスクを実行するPythonプログラムを記述してもらうことだと仮定します。

12. **Give the model instructions and context** を `You are a coding assistant helping write python code.`（あなたはPythonコードの作成を支援するコーディングアシスタントです）に変更し、変更を適用します。
13. モデルに次のプロンプトを再送信します：

    ```
    # 1. Create a list of animals
    # 2. Create a list of whimsical names for those animals
    # 3. Combine them randomly into a list of 25 animal and name pairs
    ```
    >**任意:** 日本語訳のプロンプトは
    ```prompt
    # 1. 動物のリストを作成する
    # 2. それらの動物に対して風変わりな名前のリストを作成する
    # 3. ランダムに組み合わせて、25組の動物と名前のペアを作成する
    ```


    モデルはコメントに基づいて Python コードで正しく応答するはずです。

### タスク 2: Cloud Shell にアプリケーションをセットアップする

このタスクでは、Azure で Cloud Shell 上で動作する短いコマンドラインアプリケーションを使用して Azure OpenAI モデルと統合します。新しいブラウザタブを開いて Cloud Shell を操作します。

1. [Azure ポータル](https://portal.azure.com?azure-portal=true)で、検索ボックス右側にある **[>_]** （*Cloud Shell*）ボタンを選択します。ポータルの下部に Cloud Shell ペインが開きます。

    ![検索ボックスの右側にあるアイコンをクリックして Cloud Shell を開始するスクリーンショット。](../media/cloudshell-launch-portal.png#lightbox)

2. Cloud Shell を初めて開いたときに、使用するシェルの種類（*Bash* または *PowerShell*）を選択するように求められる場合があります。**Bash** を選択します。このオプションが表示されない場合は、このステップをスキップします。

   ![](../media/cloudshell-bash.png)

3. ターミナルが開いたら、**Settings** をクリックして **Go to Classic Version** を選択します。

   ![](../media/classic-cloudshell.png)

4. ターミナルが起動したら、次のコマンドを入力してサンプルアプリケーションをダウンロードし、`azure-openai` というフォルダに保存します。

    ```bash
   rm -r azure-openai -f
   git clone https://github.com/MicrosoftLearning/mslearn-openai azure-openai
    ```

5. ファイルは **azure-openai** フォルダにダウンロードされます。この演習のためのラボファイルに移動するには、次のコマンドを使用します。

    ```bash
   cd azure-openai/Labfiles/03-prompt-engineering
    ```

    アプリケーションは C# と Python の両方が提供されており、プロンプトを提供するテキストファイルもあります。どちらのアプリも同じ機能を備えています。

6. 組み込みのコードエディタを開き、`prompts` で使用するプロンプトファイルを確認します。次のコマンドを使用して、コードエディタでラボファイルを開きます。

   ```bash
      code .
    ```

### タスク 3: アプリケーションを構成する

このタスクでは、提供された C# または Python アプリケーションの重要な部分を完成させ、非同期 API コールを使用して Azure OpenAI リソースを利用できるようにします。両方のアプリは同じ機能を備えています。

1. コードエディタで、使用する言語に応じて **CSharp** または **Python** フォルダを展開します。各フォルダには、Azure OpenAI 機能を統合するための言語固有のファイルが含まれています。

2. 使用する言語の構成ファイルを開きます。

    - C#: `appsettings.json`
    - Python: `.env`
    
3. 作成した Azure OpenAI リソースから **endpoint** と **key** を含むように構成値を更新し、デプロイしたモデル名 `my-gpt-model` を含めます。次に、左ペインからファイルを右クリックして **Save** をクリックし、ファイルを保存します。

4. 使用する言語のフォルダに移動して、必要なパッケージをインストールします。

    **C#**

    ```bash
   cd CSharp
   dotnet add package Azure.AI.OpenAI --version 1.0.0-beta.14
    ```

    **Python**
   
    ```bash
    cd Python
    pip install python-dotenv
    pip install openai==1.56.2
    ```

5. 使用する言語のフォルダに移動し、コードファイルを選択して必要なライブラリを追加します。

    **C#**: Program.cs

    ```csharp
   // Add Azure OpenAI package
   using Azure.AI.OpenAI;
    ```

    **Python**: prompt-engineering.py

    ```python
    # Add Azure OpenAI package
    from openai import AsyncAzureOpenAI
    ```

6. 使用する言語のアプリケーションコードを開き、コメント ***Configure the Azure OpenAI client*** を次のように置き換え、クライアントを構成するための必要なコードを追加します。

    **C#**: Program.cs

    ```csharp
   // Initialize the Azure OpenAI client
   OpenAIClient client = new OpenAIClient(new Uri(oaiEndpoint), new AzureKeyCredential(oaiKey));
    ```

    **Python**: prompt-engineering.py

   ```python
    # Configure the Azure OpenAI client
    client = AsyncAzureOpenAI(
        azure_endpoint = azure_oai_endpoint, 
        api_key=azure_oai_key,  
        api_version="2024-02-15-preview"
        )
    ```
    >**メモ**: コードエディタに貼り付けた後、余分なスペースを削除してインデントを確認してください。

7. Azure OpenAI モデルを呼び出す関数で、リクエストをフォーマットしてモデルに送信するためのコードを追加します。

    **C#**: Program.cs

    ```csharp
           // Format and send the request to the model
         var chatCompletionsOptions = new ChatCompletionsOptions()
         {
             Messages =
             {
                 new ChatRequestSystemMessage(systemMessage),
                 new ChatRequestUserMessage(userMessage)
             },
             Temperature = 0.7f,
             MaxTokens = 800,
             DeploymentName = oaiDeploymentName
         };
         
         // Get response from Azure OpenAI
         Response<ChatCompletions> response = await client.GetChatCompletionsAsync(chatCompletionsOptions);
    ```

    **Python**: prompt-engineering.py

   ```python
    # Format and send the request to the model
    messages =[
        {"role": "system", "content": system_message},
        {"role": "user", "content": user_message},
    ]
    
    print("\nSending request to Azure OpenAI model...\n")

    # Call the Azure OpenAI model
    response = await client.chat.completions.create(
        model=model,
        messages=messages,
        temperature=0.7,
        max_tokens=800
    )
    ```
    >**メモ**: コードエディタに貼り付けた後、余分なスペースを削除してインデントを確認してください。

8. 修正されたコードは次のようになります：

    **C#**
      
      ```csharp
        // Implicit using statements are included
         using System.Text;
         using System.Text.Json;
         using Microsoft.Extensions.Configuration;
         using Microsoft.Extensions.Configuration.Json;
         using Azure;
         
         // Add Azure OpenAI package
         // Add Azure OpenAI package
         using Azure.AI.OpenAI;
         
         // Build a config object and retrieve user settings.
         IConfiguration config = new ConfigurationBuilder()
             .AddJsonFile("appsettings.json")
             .Build();
         string? oaiEndpoint = config["AzureOAIEndpoint"];
         string? oaiKey = config["AzureOAIKey"];
         string? oaiDeploymentName = config["AzureOAIDeploymentName"];
         
         bool printFullResponse = false;
         
         do {
             // Pause for system message update
             Console.WriteLine("-----------\nPausing the app to allow you to change the system prompt.\nPress any key to continue...");
             Console.ReadKey();
             
             Console.WriteLine("\nUsing system message from system.txt");
             string systemMessage = System.IO.File.ReadAllText("system.txt"); 
             systemMessage = systemMessage.Trim();
         
             Console.WriteLine("\nEnter user message or type 'quit' to exit:");
             string userMessage = Console.ReadLine() ?? "";
             userMessage = userMessage.Trim();
             
             if (systemMessage.ToLower() == "quit" || userMessage.ToLower() == "quit")
             {
                 break;
             }
             else if (string.IsNullOrEmpty(systemMessage) || string.IsNullOrEmpty(userMessage))
             {
                 Console.WriteLine("Please enter a system and user message.");
                 continue;
             }
             else
             {
                 await GetResponseFromOpenAI(systemMessage, userMessage);
             }
         } while (true);
         
         async Task GetResponseFromOpenAI(string systemMessage, string userMessage)  
         {   
             Console.WriteLine("\nSending prompt to Azure OpenAI endpoint...\n\n");
         
             if(string.IsNullOrEmpty(oaiEndpoint) || string.IsNullOrEmpty(oaiKey) || string.IsNullOrEmpty(oaiDeploymentName) )
             {
                 Console.WriteLine("Please check your appsettings.json file for missing or incorrect values.");
                 return;
             }
             
             // Configure the Azure OpenAI client
             // Initialize the Azure OpenAI client
             OpenAIClient client = new OpenAIClient(new Uri(oaiEndpoint), new AzureKeyCredential(oaiKey));
         
             // Format and send the request to the model
             // Format and send the request to the model
             var chatCompletionsOptions = new ChatCompletionsOptions()
             {
                 Messages =
                 {
                     new ChatRequestSystemMessage(systemMessage),
                     new ChatRequestUserMessage(userMessage)
                 },
                 Temperature = 0.7f,
                 MaxTokens = 800,
                 DeploymentName = oaiDeploymentName
             };
         
         // Get response from Azure OpenAI
         Response<ChatCompletions> response = await client.GetChatCompletionsAsync(chatCompletionsOptions);
             
             ChatCompletions completions = response.Value;
             string completion = completions.Choices[0].Message.Content;
             
             // Write response full response to console, if requested
             if (printFullResponse)
             {
                 Console.WriteLine($"\nFull response: {JsonSerializer.Serialize(completions, new JsonSerializerOptions { WriteIndented = true })}\n\n");
             }
         
             // Write response to console
             Console.WriteLine($"\nResponse:\n{completion}\n\n");
         }  
            
      ```
   
     **Python**
   


>**Note**: Make sure to indent the code by eliminating any extra white spaces after pasting it into the code editor.

9. To save the changes made to the file, right-click on the file from the left pane and hit **Save**

### Task 4: Run your application

In this task, you will run your configured app to send a request to your model and observe the response. You'll notice that the only difference between the options is the content of the prompt, while all other parameters (such as token count and temperature) remain consistent across requests.

1. In the folder of your preferred language, open **system.txt** in Cloudshell code editor. For each of the iterations, you'll enter the **System message** in this file and save it. Each iteration will pause first for you to change the system message.

2. In the Cloud Shell bash terminal, navigate to the folder for your preferred language.

3. If your using as **C#** language kindly open **CSharp.csproj** file replace with following code and save the file.

   ```
   <Project Sdk="Microsoft.NET.Sdk">
   
   <PropertyGroup>
   <OutputType>Exe</OutputType>
   <TargetFramework>net8.0</TargetFramework>
   <ImplicitUsings>enable</ImplicitUsings>
   <Nullable>enable</Nullable>
   </PropertyGroup>
   
    <ItemGroup>
    <PackageReference Include="Azure.AI.OpenAI" Version="1.0.0-beta.14" />
    <PackageReference Include="Microsoft.Extensions.Configuration" Version="8.0.*" />
    <PackageReference Include="Microsoft.Extensions.Configuration.Json" Version="8.0.*" />
    </ItemGroup>
   
    <ItemGroup>
      <None Update="appsettings.json">
        <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
       </None>
     </ItemGroup>
   
    </Project> 
   ```  
4. In the interactive terminal pane, ensure the folder context is the folder for your preferred language. Then enter the following command to run the application.

    - **C#**: `dotnet run`
    - **Python**: `python prompt-engineering.py`

    > **Tip**: You can use the **Maximize panel size** (**^**) icon in the terminal toolbar to see more of the console text.

5. For the first iteration, enter the following prompts:

    **System message**

    ```prompt
    You are an AI assistant
    ```
     ![](../media/system-1.png)

    **User message:**

    ```prompt
    Write an intro for a new wildlife Rescue
    ```
     ![](../media/x233.png)

6. Observe the output. The AI model will likely produce a good generic introduction to a wildlife rescue.
7. Next, enter the following prompts which specify a format for the response:

    **System message**

    ```prompt
    You are an AI assistant helping to write emails
    ```
    **User message:**

    ```prompt
    Write a promotional email for a new wildlife rescue, including the following: Rescue name is Contoso, it specializes in elephants, and a call for donations to be given at our website.
    ```
8. Observe the output. This time, you'll likely see the format of an email with the specific animals included, as well as the call for donations.
9. Next, enter the following prompts that additionally specify the content:

    **System message**

    ```prompt
    You are an AI assistant helping to write emails
    ```

    **User message:**

    ```prompt
    Write a promotional email for a new wildlife rescue, including the following: Rescue name is Contoso, it specializes in elephants, as well as zebras and giraffes, call for donations to be given at our website, include a list of the current animals we have at our rescue after the signature in the form of a table, these animals include elephants, zebras, gorillas, lizards, and jackrabbits.
    ```

10. Observe the output, and see how the email has changed based on your clear instructions.
11. Next, enter the following prompts where we add details about tone to the system message:

    **System message**

    ```prompt
    You are an AI assistant that helps write promotional emails to generate interest in a new business. Your tone is light, chit-chat oriented and you always include at least two jokes.
    ```

    **User message:**

    ```prompt
    Write a promotional email for a new wildlife rescue, including the following: Rescue name is Contoso, it specializes in elephants, as well as zebras and giraffes, call for donations to be given at our website, include a list of the current animals we have at our rescue after the signature in the form of a table, these animals include elephants, zebras, gorillas, lizards, and jackrabbits.
    ```

12. Observe the output. This time you'll likely see the email in a similar format, but with a much more informal tone. You'll likely even see jokes included!
13. For the final iteration, we're deviating from email generation and exploring *grounding context*. Here you provide a simple system message, and change the app to provide the grounding context as the beginning of the user prompt. The app will then append the user input, and extract information from the grounding context to answer our user prompt.
14. Open the file `grounding.txt` and briefly read the grounding context you'll be inserting.
15. In your app immediately after the comment ***Format and send the request to the model*** and before any existing code, add the following code snippet to read text in from `grounding.txt` to augment the user prompt with the grounding context.

    **C#**: Program.cs

    ```csharp
    // Format and send the request to the model
    Console.WriteLine("\nAdding grounding context from grounding.txt");
    string groundingText = System.IO.File.ReadAllText("grounding.txt");
    userMessage = groundingText + userMessage;
    ```

    **Python**: prompt-engineering.py

    ```python
    # Format and send the request to the model
    print("\nAdding grounding context from grounding.txt")
    grounding_text = open(file="grounding.txt", encoding="utf8").read().strip()
    user_message = grounding_text + user_message
    ```

16. Save the file and rerun your app.
17. Enter the following prompts (with the **system message** still being entered and saved in `system.txt`).

    **System message**

    ```prompt
    You're an AI assistant who helps people find information. You'll provide answers from the text provided in the prompt, and respond concisely.
    ```

    **User message:**

    ```prompt
    What animal is the favorite of children at Contoso?
    ```
   

## Summary

In this lab, you have accomplished the following:
-   Provision an Azure OpenAI resource
-   Deploy an OpenAI model within the Azure AI Foundry portal
-   Use the functionalites of the Azure OpenAI to generate and improvise code for your production applications.

### You have successfully completed the lab.
