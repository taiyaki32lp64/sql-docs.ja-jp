---
title: スクリプト タスクによる Active Directory へのクエリの実行 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], Active Directory access
- SSIS Script task, Active Directory access
- Script task [Integration Services], examples
- Active Directory [Integration Services]
ms.assetid: a88fefbb-9ea2-4a86-b836-e71315bac68e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 14fa2d0602f0c358cd400e0734e567e853a6db85
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71286824"
---
# <a name="querying-the-active-directory-with-the-script-task"></a>スクリプト タスクによる Active Directory へのクエリの実行

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージなどの企業データ処理アプリケーションでは、Active Directory に格納されている従業員の階級、役職、またはその他の特性に基づいて、個別にデータを処理する必要性が頻繁に生じます。 Active Directory は [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ディレクトリ サービスで、ユーザーに関するメタデータだけでなく、コンピューターやプリンターなどの他の組織資産に関するメタデータも集中して格納します。 Microsoft .NET Framework の **System.DirectoryServices** 名前空間では、Active Directory を使用して作業するためのクラスが用意されており、これを使用すると Active Directory が格納している情報に基づくデータ処理のワークフローを送信できます。  
  
> [!NOTE]  
>  複数のパッケージでより簡単に再利用できるタスクを作成する場合は、このスクリプト タスク サンプルのコードを基にした、カスタム タスクの作成を検討してください。 詳細については、「 [カスタム タスクの開発](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)」を参照してください。  
  
## <a name="description"></a>[説明]  
 次の例では、従業員の電子メール アドレスを格納する `email` 変数の値に基づき、従業員の名前、役職、および電話番号を Active Directory から取得します。 パッケージ内の優先順位制約は取得された情報を使用して、たとえば、優先度の低い電子メール メッセージを送信するか、または優先度の高いページを送信するかを従業員の役職に基づいて決定できます。  
  
#### <a name="to-configure-this-script-task-example"></a>このスクリプト タスクの例を構成するには  
  
1.  `email`、`name`、および `title` という 3 つの文字列変数を作成します。 `email` 変数の値に企業の有効な電子メール アドレスを入力します。  
  
2.  **[スクリプト タスク エディター]** の **[スクリプト]** ページで、`email` 変数を **ReadOnlyVariables** プロパティに追加します。  
  
3.  `name` および `title` 変数を **ReadWriteVariables** プロパティに追加します。  
  
4.  このスクリプト プロジェクトでは、参照を **System.DirectoryServices** 名前空間に追加します。  
  
5.  。 コードで **Imports** ステートメントを使用し、**DirectoryServices** 名前空間をインポートします。  
  
> [!NOTE]  
>  このスクリプトを正しく実行するには、組織のネットワーク上で Active Directory が使用され、この例で使用される従業員の情報が格納されている必要があります。  
  
### <a name="code"></a>コード  
  
```vb  
Public Sub Main()  
  
    Dim directory As DirectoryServices.DirectorySearcher  
    Dim result As DirectoryServices.SearchResult  
    Dim email As String  
  
    email = Dts.Variables("email").Value.ToString  
  
    Try  
        directory = New _  
            DirectoryServices.DirectorySearcher("(mail=" & email & ")")  
        result = directory.FindOne  
        Dts.Variables("name").Value = _  
            result.Properties("displayname").ToString  
        Dts.Variables("title").Value = _  
            result.Properties("title").ToString  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        Dts.Events.FireError(0, _  
            "Script Task Example", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
```  
  
```csharp  
public void Main()  
{  
    //  
    DirectorySearcher directory;  
    SearchResult result;  
    string email;  
  
    email = (string)Dts.Variables["email"].Value;  
  
    try  
    {  
        directory = new DirectorySearcher("(mail=" + email + ")");  
        result = directory.FindOne();  
        Dts.Variables["name"].Value = result.Properties["displayname"].ToString();  
        Dts.Variables["title"].Value = result.Properties["title"].ToString();  
        Dts.TaskResult = (int)ScriptResults.Success;  
    }  
    catch (Exception ex)  
    {  
        Dts.Events.FireError(0, "Script Task Example", ex.Message + "\n" + ex.StackTrace, String.Empty, 0);  
        Dts.TaskResult = (int)ScriptResults.Failure;  
    }  
  
}  
```  
  
## <a name="external-resources"></a>外部リソース  
  
-   social.technet.microsoft.com の技術記事「[SSIS での Active Directory 情報の処理](https://go.microsoft.com/fwlink/?LinkId=199588)」  
  
  
