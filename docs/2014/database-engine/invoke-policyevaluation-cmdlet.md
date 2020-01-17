---
title: Invoke-PolicyEvaluation コマンドレット | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, Invoke-PolicyEvaluation
- Policy-Based Management, PowerShell
- Invoke-PolicyEvaluation cmdlet
- Cmdlets [SQL Server], Invoke-PolicyEvaluation
- PowerShell [SQL Server], Invoke-PolicyEvaluation
ms.assetid: 3e6d4f5a-59b7-4203-b95a-f7e692c0f131
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 17da45f3e66ed0adc68a40a776bfb8fe1126f330
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797850"
---
# <a name="invoke-policyevaluation-cmdlet"></a>Invoke-PolicyEvaluation コマンドレット
  **Invoke-PolicyEvaluation** は、SQL Server オブジェクトの対象セットが 1 つまたは複数のポリシーベースの管理ポリシーに指定された条件に準拠しているかどうかを報告する [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] コマンドレットです。  
  
## <a name="using-invoke-policyevaluation"></a>Invoke-PolicyEvaluation の使用  
 **Invoke-PolicyEvaluation** は、対象セットと呼ばれる SQL Server オブジェクトのセットに対し、1 つまたは複数のポリシーを評価します。 対象オブジェクトのセットは、ターゲット サーバーから取得されます。 それぞれのポリシーにより、対象オブジェクトに許可される状態を示す条件が定義されます。 たとえば、 **Trustworthy Database** ポリシーは、Trustworthy データベース プロパティを OFF に設定する必要があることを表します。  
  
 **-AdHocPolicyEvaluationMode** パラメーターは、実行するアクションを指定します。  
  
 [確認]  
 現在のログインの資格情報を使用して、対象オブジェクトの準拠状態を報告します。 オブジェクトの再構成は行いません。 これが既定の設定です。  
  
 CheckSqlScriptAsProxy  
 **##MS_PolicyTSQLExecutionLogin##** プロキシ ログインの資格情報を使用して、対象オブジェクトの準拠状態を報告します。 オブジェクトの再構成は行いません。  
  
 [構成]  
 現在のログインの資格情報を使用して、対象オブジェクトの準拠状態を報告します。 ポリシーに準拠していない、設定可能で決定的なオプションを再構成します。  
  
## <a name="specifying-polices"></a>ポリシーの指定  
 ポリシーを指定する方法は、ポリシーがどこに格納されているかによって異なります。 ポリシーは、次のように 2 つの形式で格納できます。  
  
-   ポリシー ストア (たとえばデータベース エンジンのインスタンス) に格納されたオブジェクト。 SQLSERVER:\SQLPolicy フォルダーを使用して、ポリシー ストア内のポリシーの場所を指定できます。 Windows PowerShell コマンドレットを使用して、入力ポリシーをそのプロパティに基づいてフィルター選択できます。たとえば、Where-Object を使用するとポリシーのカテゴリに基づいてフィルター処理でき、Get-Item を使用するとポリシー名に基づいてフィルター処理できます。  
  
-   ポリシーは、XML ファイルとしてエクスポートできます。 ファイル システム ドライブ (たとえば D:) を使用して、XML ファイルの場所を指定できます。 Where-Object などの Windows PowerShell コマンドレットを使用して、ファイル名などのファイル プロパティに基づいてポリシーをフィルター処理できます。  
  
 ポリシーがポリシー ストアに格納されている場合は、評価するポリシーを示す PSObjects のセットを渡す必要があります。 そのためには、通常、Get-Item などのコマンドレットの出力をパイプして **Invoke-PolicyEvaluation**に渡します。 **-Policy** パラメーターを指定する必要はありません。 たとえば、マイクロソフトのベスト プラクティス ポリシーがデータベース エンジンのインスタンスにインポートされている場合、次のコマンドは、 **Database Status** ポリシーを評価します。  
  
```powershell
sl "SQLSERVER:\SQLPolicy\MyComputer\DEFAULT\Policies"  
Get-Item "Database Status" | Invoke-PolicyEvaluation -TargetServerName "MYCOMPUTER"  
```  
  
 この例では、Where-Object を使用して、ポリシー ストアの複数のポリシーを、 **PolicyCategory** プロパティに基づいてフィルター処理しています。 **Invoke-PolicyEvaluation** によって、 **Where-Object**のパイプ出力からのオブジェクトが消費されます。  
  
```powershell
sl "SQLSERVER:\SQLPolicy\MyComputer\DEFAULT\Policies"  
gci | Where-Object {$_.PolicyCategory -eq "Microsoft Best Practices: Maintenance"} | Invoke-PolicyEvaluation -TargetServer "MYCOMPUTER"  
```  
  
 ポリシーが XML ファイルとして格納されている場合は、 **-Policy** パラメーターを使用して各ポリシーのパスと名前を指定する必要があります。 **-Policy** パラメーターにパスを指定しなかった場合、 **Invoke-PolicyEvaulation** は、 **sqlps** パスの現在の設定を使用します。 たとえば、次のコマンドは、SQL Server と共にインストールされたマイクロソフトのベスト プラクティス ポリシーの 1 つを、ログインの既定のデータベースに対して評価します。  
  
```powershell
Invoke-PolicyEvaluation -Policy "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033\Database Status.xml" -TargetServerName "MYCOMPUTER"  
```  
  
 次のコマンドは同じ操作を実行しますが、現在の **sqlps** パスを使用して、ポリシー XML ファイルの場所を確立します。  
  
```powershell
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033"  
Invoke-PolicyEvaluation -Policy "Database Status.xml" -TargetServerName "MYCOMPUTER"  
```  
  
 次の例では、 **Get-ChildItem** コマンドレットを使用して、複数のポリシー XML ファイルを取得し、パイプを使ってオブジェクトを **Invoke-PolicyEvaluation**に渡しています。  
  
```powershell
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033"  
gci "Database Status.xml", "Trustworthy Database.xml" | Invoke-PolicyEvaluation -TargetServer "MYCOMPUTER"  
```  
  
## <a name="specifying-the-target-set"></a>対象セットの指定  
 3 つのパラメーターを使用して、対象オブジェクトのセットを指定します。  
  
-   **-TargetServerName** は、対象オブジェクトを格納している SQL Server のインスタンスを指定します。 情報は、 <xref:System.Data.SqlClient.SqlConnection> クラスの ConnectionString プロパティに定義されている形式を使用する文字列に指定できます。 <xref:System.Data.SqlClient.SqlConnectionStringBuilder> クラスを使用して、適切な形式の接続文字列を作成することができます。 また、 <xref:Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection> オブジェクトを作成し、それを **-TargetServer**のパイプ出力からのオブジェクトが消費されます。 サーバー名のみの文字列を渡した場合、 **Invoke-PolicyEvaluation** は、Windows 認証を使用してサーバーに接続します。  
  
-   **-TargetObjects** は、1 つのオブジェクト、または対象セット内の SQL Server オブジェクトを表すオブジェクトの配列を受け取ります。 たとえば、 <xref:Microsoft.SqlServer.Management.Smo.Database> クラス オブジェクトの配列を作成し、 **-TargetObjects**のパイプ出力からのオブジェクトが消費されます。  
  
-   **-TargetExpressions** は、対象セット内のオブジェクトを指定するクエリ式が含まれた文字列を受け取ります。 クエリ式には、ノードを '/' 文字で区切って指定します。 各ノードは、ObjectType[Filter] 形式で記述します。 オブジェクトの種類は、SQL Server 管理オブジェクト (SMO) オブジェクト階層内のオブジェクトの1つです。 Filter は、そのノードのオブジェクトをフィルター処理する式です。 詳細については、「 [クエリ式と Uniform Resource Name](../powershell/query-expressions-and-uniform-resource-names.md)」を参照してください。  
  
 **-TargetObjects** または **-TargetExpression**のどちらか一方だけを指定します。  
  
 次の例では、Sfc.SqlStoreConnection オブジェクトを使用して、ターゲット サーバーを指定します。  
  
```powershell
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033"  
$conn = New-Object Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection("server='MYCOMPUTER';Trusted_Connection=True")  
Invoke-PolicyEvaluation -Policy "Database Status.xml" -TargetServerName $conn  
```  
  
 次の例では、 **-TargetExpression** を使用して、評価する特定のデータベースを識別します。  
  
```powershell
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033"  
Invoke-PolicyEvaluation -Policy "Database Status.xml" -TargetServerName "MyComputer" -TargetExpression "Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012']"  
```  
  
## <a name="evaluating-analysis-services-policies"></a>Analysis Services ポリシーの評価  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]のインスタンスに対してポリシーを評価するには、アセンブリを読み込んで PowerShell に登録します。次に、Analysis Services 接続オブジェクトを含む変数を作成し、その変数を **-TargetObject** パラメーターに渡します。 次の例では、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]のベスト プラクティス セキュリティ構成ポリシーを評価します。  
  
```powershell
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\AnalysisServices\1033"  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.AnalysisServices")  
$SSASsvr = New-Object Microsoft.AnalysisServices.Server  
$SSASsvr.Connect("Data Source=Localhost")  
Invoke-PolicyEvaluation -Policy "Surface Area Configuration for Analysis Services Features.xml" -TargetObject $SSASsvr  
```  
  
## <a name="evaluating-reporting-services-policies"></a>Reporting Services ポリシーの評価  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ポリシーを評価するには、アセンブリを読み込んで PowerShell に登録します。次に、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 接続オブジェクトを含む変数を作成し、その変数を **-TargetObject** パラメーターに渡します。 次の例では、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]のベスト プラクティス セキュリティ構成ポリシーを評価します。  
  
```powershell
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\ReportingServices\1033"  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Dmf.Adapters")  
$SSRSsvr = new-object Microsoft.SqlServer.Management.Adapters.RSContainer('MyComputer')  
Invoke-PolicyEvaluation -Policy "Surface Area Configuration for Reporting Services 2008 Features.xml" -TargetObject $SSRSsvr  
```  
  
## <a name="formatting-output"></a>出力の書式設定  
 既定では、 **Invoke-PolicyEvaluation** の出力は、人間が判読できる形式の簡潔なレポートとしてコマンド プロンプト ウィンドウに表示されます。 **-OutputXML** パラメーターを使用すると、詳細なレポートを XML ファイルとして生成できます。 **Invoke-PolicyEvaluation** では、SML-IF (Systems Modeling Language Interchange Format) リーダーでファイルを読むことができるように、SML-IF スキーマが使用されます。  
  
```powershell
sl "SQLSERVER:\SQLPolicy\MyComputer\DEFAULT\Policies"  
Invoke-PolicyEvaluation -Policy "Datbase Status" -TargetServer "MYCOMPUTER" -OutputXML > C:\MyReports\DatabaseStatusReport.xml  
```  
  
## <a name="see-also"></a>「  
 [データベース エンジン コマンドレットの使用](../../2014/database-engine/use-the-database-engine-cmdlets.md)  
