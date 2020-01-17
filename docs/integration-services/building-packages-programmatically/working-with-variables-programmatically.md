---
title: プログラムでの変数の使用 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- System namespace
- scope [Integration Services]
- variables [Integration Services], programmatically
- configuration files [Integration Services]
- Variables collection
- User namespace
- custom variables [Integration Services]
- variables [Integration Services], customizing
ms.assetid: c4b76a3d-94ca-4a8e-bb45-cb8bd0ea3ec1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f69f0553eecb8ebe13dc23f50982ac09ef63e5a0
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71299079"
---
# <a name="working-with-variables-programmatically"></a>プログラムでの変数の使用

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  変数を使用すると、値を動的に設定し、パッケージ、コンテナー、タスク、およびイベント ハンドラーの処理を制御できます。 また、優先順位制約で変数を使用して、別のタスクへのデータ フローの方向を制御することもできます。 変数には、以下のようにさまざまな使用方法があります。  
  
-   実行時にパッケージのプロパティを更新する。  
  
-   実行時に Transact-SQL ステートメントのパラメーター値を設定する。  
  
-   Foreach ループのフローを制御する。 詳細については、「[制御フローに列挙を追加する](https://msdn.microsoft.com/library/f212b5fb-3cc4-422e-9b7c-89eb769a812a)」を参照してください。  
  
-   式で使用することにより、優先順位制約を制御する。 優先順位制約では、制約定義に変数を含めることができます。 詳細については、「 [優先順位制約に式を追加する](https://msdn.microsoft.com/library/5574d89a-a68e-4b84-80ea-da93305e5ca1)」を参照してください。  
  
-   For ループ コンテナーの条件付きの繰り返しを制御する。 詳細については、「[制御フローに繰り返しを追加する](https://msdn.microsoft.com/library/eb3a7494-88ae-4165-9d0f-58715eb1734a)」を参照してください。  
  
-   変数値が含まれる式を構築する。  
  
-   パッケージ、**Foreach ループ** コンテナー、**For ループ** コンテナー、**シーケンス** コンテナー、タスク ホスト、およびイベント ハンドラーなど、すべての種類のコンテナー用にカスタム変数を作成できます。 詳細については、「[Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)」と「[パッケージで変数を使用する](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)」をご覧ください。  
  
## <a name="scope"></a>スコープ  
 各コンテナーには、独自の <xref:Microsoft.SqlServer.Dts.Runtime.Variables> コレクションが含まれています。 新しい変数が作成されると、その親コンテナーのスコープ内に格納されます。 パッケージ コンテナーは、コンテナー階層の最上層にあるため、パッケージ スコープを持つ変数はグローバル変数と同じように機能し、パッケージ内のすべてのコンテナーで使用できます。 また、子コンテナーは、<xref:Microsoft.SqlServer.Dts.Runtime.Variables> コレクションを介して、親コンテナーの変数コレクションにアクセスできます。アクセスするには、コレクション内の変数名または変数のインデックスのどちらかを使用します。  
  
 変数は上から順にスコープされるため、パッケージ レベルで宣言された変数は、パッケージ内のすべてのコンテナーで使用できます。 したがって、コンテナーの <xref:Microsoft.SqlServer.Dts.Runtime.Variables> コレクションには、コンテナー独自の変数だけでなく、その親コンテナーに属するすべての変数が含まれます。  
  
 これに対し、タスクに含まれる変数のスコープおよび可視性は制限されているため、そのタスクのみで使用できます。  
  
 パッケージが他のパッケージを実行する場合、呼び出し元のスコープで定義された変数は、呼び出し先のパッケージで使用できます。 ただし、呼び出し先のパッケージに同じ名前の変数が存在する場合だけは例外です。 この衝突が発生すると、呼び出し先の変数値が呼び出し元のパッケージの値をオーバーライドします。 呼び出し先のパッケージのスコープで定義された変数は、呼び出し元のパッケージでは使用できません。  
  
 次のコード例では、プログラムによって、変数 `myCustomVar` をパッケージのスコープで作成し、パッケージで使用できるすべての変数を反復処理し、変数の名前、データ型、および値を出力します。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Application app = new Application();  
      // Load a sample package that contains a variable that sets the file name.  
      Package pkg = app.LoadPackage(  
        @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +  
        @"\Package Samples\CaptureDataLineage Sample\CaptureDataLineage\CaptureDataLineage.dtsx",  
        null);  
      Variables pkgVars = pkg.Variables;  
      Variable myVar = pkg.Variables.Add("myCustomVar", false, "User", "3");  
      foreach (Variable pkgVar in pkgVars)  
      {  
        Console.WriteLine("Variable: {0}, {1}, {2}", pkgVar.Name,  
          pkgVar.DataType, pkgVar.Value.ToString());  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim app As Application = New Application()  
    ' Load a sample package that contains a variable that sets the file name.  
    Dim pkg As Package = app.LoadPackage( _  
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _  
      "\Package Samples\CaptureDataLineage Sample\CaptureDataLineage\CaptureDataLineage.dtsx", _  
      Nothing)  
    Dim pkgVars As Variables = pkg.Variables  
    Dim myVar As Variable = pkg.Variables.Add("myCustomVar", False, "User", "3")  
    Dim pkgVar As Variable  
    For Each pkgVar In pkgVars  
      Console.WriteLine("Variable: {0}, {1}, {2}", pkgVar.Name, _  
        pkgVar.DataType, pkgVar.Value.ToString())  
    Next  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **サンプル出力:**  
  
 `Variable: CancelEvent, Int32, 0`  
  
 `Variable: CreationDate, DateTime, 4/18/2003 11:57:00 AM`  
  
 `Variable: CreatorComputerName, String,`  
  
 `Variable: CreatorName, String,`  
  
 `Variable: ExecutionInstanceGUID, String, {237AB5A4-7E59-4FC9-8D61-E8F20363DF25}`  
  
 `Variable: FileName, String, Junk`  
  
 `Variable: InteractiveMode, Boolean, False`  
  
 `Variable: LocaleID, Int32, 1033`  
  
 `Variable: MachineName, String, MYCOMPUTERNAME`  
  
 `Variable: myCustomVar, String, 3`  
  
 `Variable: OfflineMode, Boolean, False`  
  
 `Variable: PackageID, String, {F0D2E396-A6A5-42AE-9467-04CE946A810C}`  
  
 `Variable: PackageName, String, DTSPackage1`  
  
 `Variable: StartTime, DateTime, 1/28/2005 7:55:39 AM`  
  
 `Variable: UserName, String, <domain>\<userid>`  
  
 `Variable: VersionBuild, Int32, 198`  
  
 `Variable: VersionComments, String,`  
  
 `Variable: VersionGUID, String, {90E105B4-B4AF-4263-9CBD-C2050C2D6148}`  
  
 `Variable: VersionMajor, Int32, 1`  
  
 `Variable: VersionMinor, Int32, 0`  
  
 **System** 名前空間で有効なすべての変数は、パッケージで使用できます。 詳細については、「 [システム変数](../../integration-services/system-variables.md)」を参照してください。  
  
## <a name="namespaces"></a>名前空間  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ([!INCLUDE[ssIS](../../includes/ssis-md.md)]) では、**User** および **System** 名前空間という 2 つの既定の名前空間が提供され、変数はこれらの名前空間に属します。 既定では、開発者が作成したカスタム変数は、**User** 名前空間に追加されます。 システム変数は、**System** 名前空間に属します。 **User** 名前空間以外の名前空間を追加作成してカスタム変数を保持したり、**User** 名前空間の名前を変更することはできますが、**System** 名前空間の変数を追加したり、変更することはできません。また、システム変数を別の名前空間に割り当てることもできません。  
  
 使用できるシステム変数は、コンテナーの種類によって異なります。 パッケージ、コンテナー、タスク、およびイベント ハンドラーで使用できるシステム変数の一覧については、「[システム変数](../../integration-services/system-variables.md)」を参照してください。  
  
## <a name="value"></a>[値]  
 カスタム変数の値には、リテラルまたは式を設定できます。  
  
-   変数にリテラル値を格納する場合は、<xref:Microsoft.SqlServer.Dts.Runtime.Variable.Value%2A> プロパティの値を設定します。  
  
-   変数に式を含めて、式の結果を変数の値として使用できるようにする場合、変数の <xref:Microsoft.SqlServer.Dts.Runtime.Variable.EvaluateAsExpression%2A> プロパティを **true** に設定し、<xref:Microsoft.SqlServer.Dts.Runtime.Variable.Expression%2A> プロパティで式を指定します。 実行時に式が評価され、式の戻り値が変数の値として使用されます。 たとえば、変数の式のプロパティが `"100 * 2""100 * 2"` の場合、変数は値 200 に評価されます。  
  
 変数の <xref:Microsoft.SqlServer.Dts.Runtime.Variable.DataType%2A> に明示的に値を設定することはできません。 <xref:Microsoft.SqlServer.Dts.Runtime.Variable.DataType%2A> 値は、変数に割り当てられた初期値から推論され、その後は変更できません。 変数のデータ型の詳細については、「[Integration Services のデータ型](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
 次のコード例では、新しい変数を作成し、<xref:Microsoft.SqlServer.Dts.Runtime.Variable.EvaluateAsExpression%2A> を **true** に設定して、式 `"100 * 2"` を変数の式のプロパティに割り当てます。その後、変数の値を出力します。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package pkg = new Package();  
      Variable v100 = pkg.Variables.Add("myVar", false, "", 1);  
      v100.EvaluateAsExpression = true;  
      v100.Expression = "100 * 2";  
      Console.WriteLine("Expression for myVar: {0}",   
        v100.Properties["Expression"].GetValue(v100));  
      Console.WriteLine("Value of myVar: {0}", v100.Value.ToString());  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim pkg As Package = New Package  
    Dim v100 As Variable = pkg.Variables.Add("myVar", False, "", 1)  
    v100.EvaluateAsExpression = True  
    v100.Expression = "100 * 2"  
    Console.WriteLine("Expression for myVar: {0}", _  
      v100.Properties("Expression").GetValue(v100))  
    Console.WriteLine("Value of myVar: {0}", v100.Value.ToString)  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **サンプル出力:**  
  
 `Expression for myVar: 100 * 2`  
  
 `Value of myVar: 200`  
  
 式は、[!INCLUDE[ssIS](../../includes/ssis-md.md)] 式の構文を使用する、有効な式である必要があります。 式の構文が提供する演算子や関数のほか、リテラルも変数式で使用できますが、他の変数または列を式で参照することはできません。 詳細については、「 [Integration Services (SSIS) 式](../../integration-services/expressions/integration-services-ssis-expressions.md)に評価されるまでそのワークフローを繰り返します。  
  
## <a name="configuration-files"></a>構成ファイル  
 構成ファイルにカスタム変数を含めると、実行時に変数を更新できます。 つまり、パッケージを実行すると、パッケージにあらかじめ含まれていた変数の値は、構成ファイルの新しい値で置き換えられます。 この置き換え方法を使用すると、異なる変数値が必要な複数のサーバーにパッケージを配置するときに便利です。 たとえば、変数を使用して、**Foreach ループ** コンテナーがそのワークフローを繰り返す回数を指定したり、エラーが発生したときにイベント ハンドラーが送信する電子メールの受信者を一覧表示したり、パッケージが失敗するまでのエラーの発生回数を変更できます。 これらの変数は、各環境の構成ファイルで動的に指定できます。 したがって、構成ファイルでは読み取り/書き込み用の変数のみを使用できます。 詳細については、「 [パッケージ構成を作成する](../../integration-services/packages/create-package-configurations.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)   
 [パッケージで変数を使用する](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  
