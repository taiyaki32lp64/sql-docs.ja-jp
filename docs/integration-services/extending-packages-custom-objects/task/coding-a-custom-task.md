---
title: カスタム タスクのコーディング | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Validate method
- custom tasks [Integration Services], validating
- validation [Integration Services], design-time tasks
- SSIS custom tasks, validating
ms.assetid: dc224f4f-b339-4eb6-a008-1b4fe0ea4fd2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 23cea7d670916db9dfd13fa37170967a3c19d11c
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297127"
---
# <a name="coding-a-custom-task"></a>カスタム タスクのコーディング

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  <xref:Microsoft.SqlServer.Dts.Runtime.Task> 基本クラスを継承するクラスを作成し、<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> 属性をそのクラスに適用したら、基本クラスのプロパティとメソッドの実装をオーバーライドして、カスタム機能を提供する必要があります。  
  
## <a name="configuring-the-task"></a>タスクの構成  
  
### <a name="validating-the-task"></a>タスクの検証  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] パッケージのデザイン中に検証機能を使用して各タスクの設定を確認できるため、すべてのエラーを実行時にのみ見つけるのではなく、無効または不適切な設定が行われた場合、すぐにその問題を確認できます。 検証の目的は、タスクの正常な実行を妨げる無効な設定または接続が、タスクに含まれているかどうかを判別することです。 これによって、パッケージに含まれるタスクは、初回から正しく実行される可能性が高くなります。  
  
 検証機能は、カスタム コード内で **Validate** メソッドを使用することによって実装できます。 ランタイム エンジンは、タスク上の **Validate** メソッドを呼び出すことにより、タスクを検証します。 タスクの開発者は、タスクの検証が成功または失敗する条件を定義し、評価の結果をランタイム エンジンに通知する必要があります。  
  
#### <a name="task-abstract-base-class"></a>タスクの抽象基本クラス  
 <xref:Microsoft.SqlServer.Dts.Runtime.Task> 抽象基本クラスには **Validate** メソッドが用意されており、各タスクはこれをオーバーライドして検証条件を定義します。 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーは、パッケージのデザイン中、**Validate** メソッドを自動的に複数回呼び出します。さらに、警告またはエラーが発生した場合はユーザーに画面上で通知し、タスクの構成に関する問題を識別できるようにします。 タスクは、<xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 列挙から値を返し、警告およびエラー イベントを発生させることにより、検証結果を返します。 これらのイベントには、[!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーでユーザーに表示される情報が含まれています。  
  
 次に、いくつかの検証の例を挙げます。  
  
-   接続マネージャーは、特定のファイル名を検証します。  
  
-   接続マネージャーは、入力の種類が XML ファイルなどの必要な種類であることを検証します。  
  
-   データベースの入力が必要なタスクは、データベース以外の接続からデータを受け取れないことを確認します。  
  
-   タスクは、タスクのどのプロパティも、同じタスクに設定された他のプロパティと矛盾していないことを保証します。  
  
-   タスクは、タスクが使用する必要なすべてのリソースが実行時に使用できることを保証します。  
  
 検証する項目としない項目を決定する際には、パフォーマンスを考慮する必要があります。 たとえば、タスクへの入力で、低帯域またはトラフィックが混雑しているネットワーク経由の接続が使用されている場合があります。 その場合、リソースが使用可能かを検証する処理には、数秒かかる可能性があります。 別の検証では要求処理量が多いサーバーへのラウンド トリップが発生し、検証ルーチンの速度が遅くなる可能性があります。 検証可能なプロパティや設定は多数ありますが、すべてを検証するべきではありません。  
  
-   **Validate** メソッド内のコードは、タスクの実行前に <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> によっても呼び出され、検証が失敗した場合は <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> の実行が取り消されます。  
  
#### <a name="user-interface-considerations-during-validation"></a>検証時のユーザー インターフェイスについての検討事項  
 <xref:Microsoft.SqlServer.Dts.Runtime.Task> には、**Validate** メソッドのパラメーターとして、<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents> インターフェイスが含まれています。 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents> インターフェイスには、イベントをランタイム エンジンに送るためにタスクが呼び出すメソッドが含まれています。 検証中に警告またはエラー条件が発生すると、<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireWarning%2A> および <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireError%2A> メソッドが呼び出されます。 どちらの警告メソッドにも、エラー コード、ソース コンポーネント、説明、ヘルプ ファイル、ヘルプ コンテキスト情報などの同じパラメーターが必要です。 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーはこの情報に基づいて、エラーの発生をデザイン画面上で視覚的に通知します。 デザイナーによって提供される視覚的な通知には、デザイン画面上のタスクの横に表示される感嘆符のアイコンがあります。 この視覚的通知は、実行を続けるにはタスクの構成を追加する必要があることを示します。  
  
 感嘆符のアイコンによって、エラー メッセージを含むツールヒントも表示されます。 エラー メッセージは、タスクによってイベントの説明パラメーターに提供されます。 エラー メッセージは、[!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] の **[タスク一覧]** ペインにも表示されます。このペインは、すべての検証エラーを表示するための集中管理場所となります。  
  
#### <a name="validation-example"></a>検証例  
 次のコード例は、**UserName** プロパティを使用したタスクを示しています。 このプロパティは、検証に必要なものとして指定されています。 このプロパティが設定されていない場合、タスクはエラーを通知し、<xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult.Failure> 列挙から <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> を返します。 例外が発生すると、**Validate** メソッドは try/catch ブロックにラップされ、検証は失敗します。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
public class SampleTask : Task  
{  
  private string userName = "";  
  
  public override DTSExecResult Validate(Connections connections,  
     VariableDispenser variableDispenser, IDTSComponentEvents events,  
     IDTSLogging log)  
  {  
    try  
    {  
      if (this.userName == "")  
      {  
        //   Raise an OnError event.  
        events.FireError(0, "SampleTask", "The UserName property must be configured.", "", 0);  
        //   Fail validation.  
        return DTSExecResult.Failure;  
      }  
      //   Return success.  
      return DTSExecResult.Success;  
    }  
    catch (System.Exception exception)  
    {  
      //   Capture exceptions, post an error, and fail validation.  
      events.FireError(0, "Sampletask", exception.Message, "", 0);  
      return DTSExecResult.Failure;  
    }  
  }  
  public string UserName  
  {  
    get  
    {  
      return this.userName;  
    }  
    set  
    {  
      this.userName = value;  
    }  
  }  
}  
```  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Public Class SampleTask  
  Inherits Task  
  
  Private _userName As String = ""  
  
  Public Overrides Function Validate(ByVal connections As Connections, _  
     ByVal variableDispenser As VariableDispenser, _  
     ByVal events As IDTSComponentEvents, _  
     ByVal log As IDTSLogging) As DTSExecResult  
  
    Try  
      If Me._userName = "" Then  
        '   Raise an OnError event.  
        events.FireError(0, "SampleTask", "The UserName property must be configured.", "", 0)  
        '   Fail validation.  
        Return DTSExecResult.Failure  
      End If  
      '   Return success.  
      Return DTSExecResult.Success  
    Catch exception As System.Exception  
      '   Capture exceptions, post an error, and fail validation.  
      events.FireError(0, "Sampletask", exception.Message, "", 0)  
      Return DTSExecResult.Failure  
    End Try  
  
  End Function  
  
  Public Property UserName() As String  
    Get  
      Return Me._userName  
    End Get  
    Set(ByVal Value As String)  
      Me._userName = Value  
    End Set  
  End Property  
  
End Class  
```  
  
### <a name="persisting-the-task"></a>タスクの保存  
 通常、タスクに対して、カスタムの永続性を実装する必要はありません。 カスタムの永続性は、オブジェクトのプロパティで複合データ型が使用されている場合にのみ必要です。 詳細については、「[Integration Services 用のカスタム オブジェクトの開発](../../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)」を参照してください。  
  
## <a name="executing-the-task"></a>タスクの実行  
 このセクションでは、タスクによって継承およびオーバーライドされる **Execute** メソッドの使用方法について説明します。 また、タスクの実行結果についての情報を提供するさまざまな方法についても説明します。  
  
### <a name="execute-method"></a>Execute メソッド  
 パッケージに含まれるタスクは、[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のランタイムが **Execute** メソッドを呼び出すと実行されます。 タスクは、中心となるビジネス ロジックや機能をこのメソッドに実装し、メッセージを送信したり、<xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 列挙から値を返したり、**ExecutionValue** プロパティの **get** プロパティをオーバーライドしたりする方法で、実行結果を返します。  
  
 基本クラス <xref:Microsoft.SqlServer.Dts.Runtime.Task> には、既定で <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A> メソッドが実装されています。 カスタム タスクは、実行時の機能を定義するために、このメソッドをオーバーライドします。 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> オブジェクトはタスクをラップし、ランタイム エンジンやパッケージ内の他のオブジェクトと分離します。 そのため、タスクはパッケージ内での実行順序に関する位置を認識しているわけではなく、ランタイムによって呼び出されたときにのみ実行されます。 このアーキテクチャにより、実行中にタスクがパッケージを変更したときに発生する問題が回避されます。 タスクがパッケージ内の他のオブジェクトにアクセスするには、<xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A> メソッド内のパラメーターとして用意されているオブジェクトを使用する必要があります。 これらのパラメーターを使用すると、パッケージの安定度と信頼性を保証するために必要な分離性を保ちながら、イベントの発生、イベント ログへのエントリの記録、変数コレクションへのアクセス、およびトランザクション内のデータ ソースへの接続の登録を、タスクに実行させることができます。  
  
 次の表は、<xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A> メソッド内のタスクに対して提供されるパラメーターの一覧です。  
  
|パラメーター|[説明]|  
|---------------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Connections>|タスクで使用できる <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> オブジェクトのコレクションを含みます。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.VariableDispenser>|タスクで使用できる変数を含みます。 タスクは、VariableDispenser を介して変数を使用します。変数を直接使用することはありません。 変数ディスペンサーには、変数をロックまたはロック解除したり、デッドロックや上書きを防ぐ機能があります。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents>|イベントを生成してランタイム エンジンに送るためにタスクが呼び出すメソッドを含みます。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.IDTSLogging>|イベント ログにエントリを記録するためにタスクが使用するメソッドおよびプロパティを含みます。|  
|Object|トランザクション オブジェクトの一部がコンテナーである場合、そのオブジェクトを含みます。 この値はパラメーターとして、<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> オブジェクトの <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> メソッドに渡されます。|  
  
### <a name="providing-execution-feedback"></a>実行結果のフィードバックの送信  
 タスクは、タスクのコードを **try/catch** ブロックにラップし、ランタイム エンジンに例外が発生するのを防ぎます。 これにより、パッケージは予期せず停止することなく、実行を完了します。 ランタイム エンジンには、タスクの実行中に発生する可能性のあるエラー条件を処理するメカニズムが他にも用意されています。 このメカニズムには、エラー メッセージや警告メッセージの通知、<xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 構造からの戻り値、メッセージの通知、<xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> の戻り値、<xref:Microsoft.SqlServer.Dts.Runtime.Task.ExecutionValue%2A> プロパティによるタスクの実行結果に関する情報の公開などが含まれています。  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents> インターフェイスには、<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireWarning%2A> メソッドおよび <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireError%2A> メソッドがあり、タスクはこれらを呼び出して、エラー メッセージや警告メッセージをランタイム エンジンに通知できます。 どちらのメソッドにも、エラー コード、ソース コンポーネント、説明、ヘルプ ファイル、ヘルプ コンテキスト情報などのパラメーターが必要です。 タスクの構成に応じて、ランタイムは、イベントやブレークポイントを発生させたり、イベント ログに情報を記録したりする方法で、これらのメッセージに応答します。  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> は、実行結果に関する追加情報を提供するために使用可能な <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.ExecutionValue%2A> プロパティも提供します。 たとえば、タスクがその **Execute** メソッドの一部としてテーブルから行を削除すると、削除された行数は <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.ExecutionValue%2A> プロパティの値として返されます。 また、<xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> は <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.ExecValueVariable%2A> プロパティを提供します。 ユーザーはこのプロパティを使用して、タスクから返された <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.ExecutionValue%2A> を、タスクで認識可能な任意の変数にマップすることができます。 指定した変数を使用して、タスク間の優先順位制約を確立できます。  
  
### <a name="execution-example"></a>実行例  
 次のコード例では、**Execute** メソッドを実装する方法、およびオーバーライドされた **ExecutionValue** プロパティを示します。 このタスクでは、タスクの **fileName** プロパティで指定されたファイルが削除されます。 ファイルが存在しない場合、または **fileName** プロパティが空の文字列である場合、タスクは警告メッセージを通知します。 タスクは、<xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.ExecutionValue%2A> プロパティで、ファイルが削除されたかどうかを示す **Boolean** 値を返します。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
public class SampleTask : Task  
{  
  private string fileName = "";  
  private bool fileDeleted = false;  
  
  public override DTSExecResult Execute(Connections cons,  
     VariableDispenser vars, IDTSComponentEvents events,  
     IDTSLogging log, Object txn)  
  {  
    try  
    {  
      if (this.fileName == "")  
      {  
        events.FireWarning(0, "SampleTask", "No file specified.", "", 0);  
        this.fileDeleted = false;  
      }  
      else  
      {  
        if (System.IO.File.Exists(this.fileName))  
        {  
          System.IO.File.Delete(this.fileName);  
          this.fileDeleted = true;  
        }  
        else  
          this.fileDeleted = false;  
      }  
      return DTSExecResult.Success;  
    }  
    catch (System.Exception exception)  
    {  
      //   Capture the exception and post an error.  
      events.FireError(0, "Sampletask", exception.Message, "", 0);  
      return DTSExecResult.Failure;  
    }  
  }  
  public string FileName  
  {  
    get { return this.fileName; }  
    set { this.fileName = value; }  
  }  
  public override object ExecutionValue  
  {  
    get { return this.fileDeleted; }  
  }  
}  
```  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Public Class SampleTask  
  Inherits Task  
  
  Private _fileName As String = ""  
  Private _fileDeleted As Boolean = False  
  
  Public Overrides Function Execute(ByVal cons As Connections, _  
     ByVal vars As VariableDispenser, ByVal events As IDTSComponentEvents, _  
     ByVal log As IDTSLogging, ByVal txn As Object) As DTSExecResult  
  
    Try  
      If Me._fileName = "" Then  
        events.FireWarning(0, "SampleTask", "No file specified.", "", 0)  
        Me._fileDeleted = False  
      Else  
        If System.IO.File.Exists(Me._fileName) Then  
          System.IO.File.Delete(Me._fileName)  
          Me._fileDeleted = True  
        Else  
          Me._fileDeleted = False  
        End If  
      End If  
      Return DTSExecResult.Success  
    Catch exception As System.Exception  
      '   Capture the exception and post an error.  
      events.FireError(0, "Sampletask", exception.Message, "", 0)  
      Return DTSExecResult.Failure  
    End Try  
  
  End Function  
  
  Public Property FileName() As String  
    Get  
      Return Me._fileName  
    End Get  
    Set(ByVal Value As String)  
      Me._fileName = Value  
    End Set  
  End Property  
  
  Public Overrides ReadOnly Property ExecutionValue() As Object  
    Get  
      Return Me._fileDeleted  
    End Get  
  End Property  
  
End Class  
```  
  
## <a name="see-also"></a>参照  
 [カスタム タスクの作成](../../../integration-services/extending-packages-custom-objects/task/creating-a-custom-task.md)   
 [カスタム タスクのコーディング](../../../integration-services/extending-packages-custom-objects/task/coding-a-custom-task.md)   
 [カスタム タスク用ユーザー インターフェイスの開発](../../../integration-services/extending-packages-custom-objects/task/developing-a-user-interface-for-a-custom-task.md)  
  
  
