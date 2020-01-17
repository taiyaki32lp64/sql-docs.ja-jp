---
title: 拡張イベントへの PowerShell プロバイダーの使用
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
helpviewer_keywords:
- PowerShell [SQL Server], xevent
- extended events [SQL Server], PowerShell
- PowerShell [SQL Server], extended events
ms.assetid: 0b10016f-a479-4444-a484-46cb4677cf64
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c7fba3c0ad9ab6f004d001b1a8e04d86e27d1818
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75242888"
---
# <a name="use-the-powershell-provider-for-extended-events"></a>拡張イベントへの PowerShell プロバイダーの使用

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell プロバイダーを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拡張イベントを管理できます。 XEvent サブフォルダーは、SQLSERVER ドライブで利用可能です。 このフォルダーには、次のいずれかの方法でアクセスできます。  
  
-   コマンド プロンプトで「 **sqlps**」と入力し、Enter キーを押します。 「 **cd xevent**」と入力して Enter キーを押します。 そこから、 **cd** コマンドと **dir** コマンド (または **Set-Location** コマンドレットと **Get-Childitem** コマンドレット) を使用して、サーバー名とインスタンス名に移動できます。  
  
-   オブジェクト エクスプローラーで、インスタンス名、 **[管理]** の順に展開し、 **[拡張イベント]** を右クリックして、 **[PowerShell の起動]** をクリックします。 これにより、次のパスで PowerShell が起動します。  
  
     PS SQLSERVER:\XEvent\\*ServerName*\\*InstanceName*>  
  
    > [!NOTE]  
    >  PowerShell は、 **[拡張イベント]** の下の任意のノードから起動できます。 たとえば、 **[Sessions]** を右クリックし、 **[PowerShell の起動]** をクリックできます。 これにより、1 レベル深い Sessions フォルダーで PowerShell が起動します。  
  
 XEvent フォルダー ツリーを参照して、既存の拡張イベント セッションと、関連するイベント、ターゲット、および述語を表示できます。 たとえば、PS SQLSERVER:\XEvent\\*ServerName*\\*InstanceName*> パスから、「**cd sessions**」と入力し、Enter キーを押し、「**dir**」と入力して、Enter キーを押すと、そのインスタンスに格納されているセッションの一覧を表示できます。 また、セッションが実行中かどうか (および実行中の場合は実行時間)、およびセッションがインスタンスの起動時に開始されるように構成されているかどうかも表示されます。  
  
 セッションに関連付けられているイベント、述語、およびターゲットを表示するには、ディレクトリをセッション名に変更してから、events フォルダーまたは targets フォルダーを表示します。 たとえば、既定のシステム正常性セッションに関連付けられているイベントおよび述語を表示するには、PS SQLSERVER:\XEvent\\*ServerName*\\*InstanceName*\Sessions> パスから、「**cd system_health\events**」と入力し、Enter キーを押し、「**dir**」と入力して、Enter キーを押します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell プロバイダーは、拡張イベント セッションの作成、変更、および管理に使用できる強力なツールです。 次のセクションでは、拡張イベントに PowerShell スクリプトを使用する基本的な例をいくつか紹介します。  
  
## <a name="examples"></a>例  
 以下の例では、次の点に注意してください。  
  
-   スクリプトは、PS SQLSERVER:\\> プロンプト (コマンド プロンプトで「**sqlps**」と入力すると利用可能になります) から実行する必要があります。  
  
-   スクリプトでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の既定のインスタンスを使用します。  
  
-   スクリプトは、.ps1 拡張子を付けて保存してください。  
  
-   PowerShell 実行ポリシーで、スクリプトを実行できるようにする必要があります。 実行ポリシーを設定するには、 **Set-Executionpolicy** コマンドレットを使用します (詳細については、「 **get-help set-executionpolicy -detailed**」と入力し、Enter キーを押してください)。  
  
 次のスクリプトでは、"TestSession" という名前の新しいセッションが作成されます。  
  
```  
#Script for creating a session.  
cd XEvent  
$h = hostname  
cd $h  
  
#Use the default instance.  
$store = dir | where {$_.DisplayName -ieq 'default'}  
$session = new-object Microsoft.SqlServer.Management.XEvent.Session -argumentlist $store, "TestSession"  
$event = $session.AddEvent("sqlserver.file_written")  
$event.AddAction("package0.callstack")  
$session.Create()  
```  
  
 次のスクリプトでは、前の例で作成したセッションにリング バッファー ターゲットが追加されます (この例では、 **Alter** メソッドの使用方法を示しています。 ターゲットは、最初にセッションを作成するときに追加できます)。  
  
```  
#Script to alter a session.  
cd XEvent  
$h = hostname  
cd $h  
cd DEFAULT\Sessions  
  
#Used to find the specified session.  
$session = dir|where {$_.Name -eq 'TestSession'}  
  
#Add the ring buffer target and call the Alter method.  
$session.AddTarget("package0.ring_buffer")  
$session.Alter()  
```  
  
 次のスクリプトでは、述語式を使用する新しいセッションが作成されます。 この例では、sqlserver.file_written イベントを利用して、c:\temp.log ファイルに書き込まれたときの情報を収集します。  
  
```  
#Script for creating a session.  
cd XEvent  
$h = hostname  
cd $h  
  
#Use the default instance.  
$store = dir | where {$_.DisplayName -ieq 'default'}  
$session = new-object Microsoft.SqlServer.Management.XEvent.Session -argumentlist $store, "TestSession2"  
$event = $session.AddEvent("sqlserver.file_written")  
  
#Construct a predicate "equal_i_unicode_string(path, N'c:\temp.log')".  
$column = $store.SqlServerPackage.EventInfoSet["file_written"].DataEventColumnInfoSet["path"]  
$operand = new-object Microsoft.SqlServer.Management.XEvent.PredOperand -argumentlist $column  
$value = new-object Microsoft.SqlServer.Management.XEvent.PredValue -argumentlist "c:\temp.log"  
$compare = $store.Package0Package.PredCompareInfoSet["equal_i_unicode_string"]  
$predicate = new-object Microsoft.SqlServer.Management.XEvent.PredFunctionExpr -argumentlist $compare, $operand, $value  
$event.SetPredicate($predicate)  
$session.Create()  
```  
  
## <a name="security"></a>Security  
 拡張イベント セッションを作成、変更、または削除するには、ALTER ANY EVENT SESSION 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)   
 [system_health セッションの使用](../../relational-databases/extended-events/use-the-system-health-session.md)   
 [拡張イベントのツール](../../relational-databases/extended-events/extended-events-tools.md)  
  
  
