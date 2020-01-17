---
title: スクリプト タスクとスクリプト コンポーネントの比較 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], comparing to Script component
- Script component [Integration Services], comparing to Script task
ms.assetid: 4b73753a-4239-491b-b7a6-abc63ba83d2d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e253e6a4e19982e5350161cde00bc7609ed7380d
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297009"
---
# <a name="comparing-the-script-task-and-the-script-component"></a>スクリプト タスクとスクリプト コンポーネントの比較

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  スクリプト タスクは [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] デザイナーの [制御フロー] ウィンドウで使用でき、スクリプト コンポーネントは [データ フロー] ウィンドウで使用できます。これら 2 つのタスクは、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージ内での目的がまったく異なります。 タスクは汎用の制御フロー ツールであるのに対し、コンポーネントはデータ フロー内で変換元、変換、または変換先としての役割を果たします。 ただし、目的は異なっても、コード作成に使用するツールや、開発者が使用できるパッケージ内のオブジェクトについては、スクリプト タスクとスクリプト コンポーネントには似通った点があります。 共通点と相違点を理解すると、このタスクとコンポーネントをより効率的に使用するために役立ちます。  
  
## <a name="similarities-between-the-script-task-and-the-script-component"></a>スクリプト タスクとスクリプト コンポーネントの共通点  
 スクリプト タスクとスクリプト コンポーネントには、次のような共通の機能があります。  
  
|機能|[説明]|  
|-------------|-----------------|  
|デザイン時の 2 つのモード|タスクとコンポーネントのどちらの場合も、最初にエディターでプロパティを指定し、次に開発環境に切り替えてコードを記述します。|  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA)|タスクもコンポーネントも、同じ VSTA IDE を使用し、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic または [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# で記述されたコードをサポートします。|  
|スクリプトのプリコンパイル|[!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 以降では、すべてのスクリプトがプリコンパイルされます。 以前のバージョンでは、スクリプトをプリコンパイルするかどうかを指定できました。<br /><br /> スクリプトがバイナリ コードに事前コンパイルされるため、実行速度が向上しますが、パッケージ サイズは増加します。|  
|デバッグ|タスクおよびコンポーネントの両方で、設計環境におけるコードのデバッグ時に、ブレークポイントを使用したステップ実行がサポートされます。 詳細については、「[スクリプト タスクのコーディングおよびデバッグ](../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)」および「[スクリプト コンポーネントのコーディングおよびデバッグ](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)」を参照してください。|  
  
## <a name="differences-between-the-script-task-and-the-script-component"></a>スクリプト タスクとスクリプト コンポーネントの相違点  
 スクリプト タスクとスクリプト コンポーネントには、次のような顕著な相違点があります。  
  
|機能|スクリプト タスク|スクリプト コンポーネント|  
|-------------|-----------------|----------------------|  
|制御フローとデータ フロー|スクリプト タスクはデザイナーの [制御フロー] タブで設定され、パッケージのデータ フローの外で実行されます。|スクリプト コンポーネントはデザイナーの [データ フロー] ページで設定され、データ フロー タスク内で変換元、変換、または変換先のいずれかを表します。|  
|用途|スクリプト タスクはほとんどの汎用タスクを実行できます。|スクリプト コンポーネントでは、変換元、変換、または変換先のどれを作成するかを指定する必要があります。|  
|実行|スクリプト タスクは、パッケージ ワークフロー内のある時点でカスタム コードを実行します。 ループ コンテナーまたはイベント ハンドラー内に配置しない限り、実行されるのは 1 回のみです。|スクリプト コンポーネントも実行されるのは 1 回のみですが、通常、メイン処理ルーチンはデータ フロー内のデータ行ごとに 1 回ずつ実行されます。|  
|エディター|**[スクリプト タスク エディター]** には次の 3 つのページがあります: **[全般]** 、 **[スクリプト]** 、 **[式]** 。 **ReadOnlyVariables** プロパティ、**ReadWriteVariables** プロパティ、および **ScriptLanguage** プロパティのみがユーザーが記述できるコードに直接影響を与えます。|**[スクリプト変換エディター]** には、最大で次の 4 つのページがあります: **[入力列]** 、 **[入力および出力]** 、 **[スクリプト]** 、 **[接続マネージャー]** 。 この各ページで設定するメタデータやプロパティにより、コードを記述する際に使用できる、自動生成された基本クラスのメンバーが指定されます。|  
|パッケージの操作|パッケージの他の機能にアクセスするには、スクリプト タスク用に記述するコードで **Dts** プロパティを使用します。 **Dts** プロパティは、**ScriptMain** クラスのメンバーです。|スクリプト コンポーネントのコードでは、型指定されたアクセサー プロパティを使用して、変数や接続マネージャーなど、特定のパッケージ機能にアクセスします。<br /><br /> **PreExecute** メソッドでは、読み取り専用変数にのみアクセスできます。 **PostExecute** メソッドでは、読み取り専用変数および読み取り/書き込み変数の両方にアクセスできます。<br /><br /> これらのメソッドの詳細については、「[スクリプト コンポーネントのコーディングおよびデバッグ](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)」を参照してください。|  
|変数の使用|スクリプト タスクでは、**Dts** オブジェクトの <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> プロパティを使用して、タスクの <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadOnlyVariables%2A> プロパティおよび <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadWriteVariables%2A> プロパティで使用できる変数にアクセスします。 例:<br /><br /> [Visual Basic]<br /><br /> `Dim myVar as String` <br /> `myVar = Dts.Variables("MyStringVariable").Value.ToString`<br /><br /> [C#]<br /><br /> `string myVar;` <br /> `myVar = Dts.Variables["MyStringVariable"].Value.ToString();`|スクリプト コンポーネントでは、自動生成された基本クラスの型指定されたアクセサー プロパティを使用します。このプロパティは、コンポーネントの <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadOnlyVariables%2A> プロパティおよび <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadWriteVariables%2A> プロパティから作成されます。 例:<br /><br /> [Visual Basic]<br /><br /> `Dim myVar as String` <br /> `myVar = Me.Variables.MyStringVariable`<br /><br /> [C#]<br /><br /> `string myVar;` <br /> `myVar = this.Variables.MyStringVariable;`|  
|接続の使用|スクリプト タスクでは、**Dts** オブジェクトの <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> プロパティを使用して、パッケージで定義された接続マネージャーにアクセスします。 例:<br /><br /> [Visual Basic]<br /><br /> `Dim myFlatFileConnection As String` <br /> `myFlatFileConnection = _     DirectCast(Dts.Connections("Test Flat File Connection").AcquireConnection(Dts.Transaction), _     String)`<br /><br /> [C#]<br /><br /> `string myFlatFileConnection;` <br /> `myFlatFileConnection = (Dts.Connections["Test Flat File Connection"].AcquireConnection(Dts.Transaction) as String);`|スクリプト コンポーネントでは、自動生成された基本クラスの型指定されたアクセサー プロパティを使用します。このプロパティは、エディターの [接続マネージャー] ページでユーザーが入力した、接続マネージャーの一覧から作成されます。 例:<br /><br /> [Visual Basic]<br /><br /> `Dim connMgr As IDTSConnectionManager100` <br /> `connMgr = Me.Connections.MyADONETConnection`<br /><br /> [C#]<br /><br /> `IDTSConnectionManager100 connMgr;` <br /> `connMgr = this.Connections.MyADONETConnection;`|  
|イベントの発生|スクリプト タスクでは、**Dts** オブジェクトの <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A> プロパティを使用してイベントを発生させます。 例:<br /><br /> [Visual Basic]<br /><br /> `Dts.Events.FireError(0, "Event Snippet", _     ex.Message & ControlChars.CrLf & ex.StackTrace, _     "", 0)`<br /><br /> [C#]<br /><br /> `Dts.Events.FireError(0, "Event Snippet", ex.Message + "\r" + ex.StackTrace, "", 0);`|スクリプト コンポーネントでエラー、警告、情報メッセージを発生させるには、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> プロパティから返される <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> インターフェイスのメソッドを使用します。 例:<br /><br /> [Visual Basic]<br /><br /> `Dim myMetadata as IDTSComponentMetaData100 myMetaData = Me.ComponentMetaData myMetaData.FireError(...)`|  
|ログ記録|スクリプト タスクでは、**Dts** オブジェクトの <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> メソッドを使用して、有効なログ プロバイダーに情報を記録します。 例:<br /><br /> [Visual Basic]<br /><br /> `Dim bt(0) As Byte Dts.Log("Test Log Event", _     0, _     bt)`<br /><br /> [C#]<br /><br /> `byte[] bt = new byte[0];` <br /> `Dts.Log("Test Log Event", 0, bt);`|スクリプト コンポーネントでは、自動生成された基本クラスの <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> メソッドを使用して、有効なログ プロバイダーに情報を記録します。 例:<br /><br /> [Visual Basic]<br /><br /> `Dim bt(0) As Byte`<br /><br /> `Me.Log("Test Log Event", _`<br /><br /> `0, _`<br /><br /> `bt)`<br /><br /> [C#]<br /><br /> `byte[] bt = new byte[0]; this.Log("Test Log Event", 0, bt);`|  
|結果の返送|スクリプト タスクでは、**Dts** オブジェクトの <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> プロパティ、および場合によって <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> プロパティを使用して、ランタイムに結果を通知します。|スクリプト コンポーネントはデータ フロー タスクの一部として実行され、プロパティを使用して結果をレポートすることはありません。|  
  
## <a name="see-also"></a>参照  
 [スクリプト タスクによるパッケージの拡張](../../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md)   
 [スクリプト コンポーネントによるデータ フローの拡張](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)   
  
  
