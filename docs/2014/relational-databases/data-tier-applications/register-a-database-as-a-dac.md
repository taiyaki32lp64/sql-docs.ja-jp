---
title: データベースを DAC として登録する方法 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.registerdacwizard.registerdac.f1
- sql12.swb.registerdacwizard.summary.f1
- sql12.swb.registerdacwizard.introduction.f1
- sql12.swb.registerdacwizard.setproperties.f1
helpviewer_keywords:
- wizard [DAC], register
- How to [DAC], register
- register DAC
- data-tier application [SQL Server], register
ms.assetid: 08e52aa6-12f3-41dd-a793-14b99a083fd5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8ed991d65858d40b96013659caa2d83c479ca1d3
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782721"
---
# <a name="register-a-database-as-a-dac"></a>データベースを DAC として登録する方法
  **データ層アプリケーションの登録ウィザード**または Windows PowerShell スクリプトを使用して、既存のデータベース内のオブジェクトを表すデータ層アプリケーション (dac) 定義を作成し、その dac 定義を `msdb` システムデータベースに登録します ( [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)])。  
  
-   **作業を開始する準備:** [制限事項と制約事項](#LimitationsRestrictions)、[権限](#Permissions)  
  
-   **DAC のアップグレード:** [データ層アプリケーションの登録ウィザードの使用](#UsingRegisterDACWizard)、[PowerShell の使用](#RegisterDACPowerShell)  
  
## <a name="before-you-begin"></a>はじめに  
 登録プロセスでデータベース オブジェクトを定義する DAC 定義を作成します。 DAC の定義とデータベースを組み合わせたものが DAC インスタンスになります。 データベース エンジンのマネージド インスタンス上で DAC としてデータベースを登録した場合は、SQL Server ユーティリティ コレクション セットをこのインスタンスからユーティリティ コントロール ポイントへ次に送信するときに、登録した DAC が SQL Server ユーティリティに組み込まれます。 その後、DAC は [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **ユーティリティ エクスプローラー** の **配置されたデータ層アプリケーション** ノードに現れるようになり、**配置されたデータ層アプリケーション** の詳細ページで報告されます。  
  
###  <a name="LimitationsRestrictions"></a> 制限事項と制約事項  
 DAC は、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]または [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) 以降のデータベースでのみ登録できます。 DAC が既にデータベースに登録されている場合は、DAC の登録を実行できません。 たとえば、DAC を配置してデータベースを作成した場合、 **データ層アプリケーションの登録ウィザード**を実行できません。  
  
 DAC でサポートされていないオブジェクトまたは包含ユーザーがデータベースに存在する場合は、DAC を登録できません。 DAC でサポートされるオブジェクトの種類の詳細については、「 [DAC Support For SQL Server Objects and Versions](dac-support-for-sql-server-objects-and-versions.md)」を参照してください。  
  
###  <a name="Permissions"></a> 権限  
 DAC を [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに登録するには、少なくとも ALTER ANY LOGIN 権限とデータベース スコープの VIEW DEFINITION 権限、 **sys.sql_expression_dependencies**に対する SELECT 権限、および **dbcreator** 固定サーバー ロールのメンバーシップが必要です。 **sysadmin** 固定サーバー ロールのメンバーまたは **sa** という組み込みの SQL Server システム管理者アカウントも DAC を登録できます。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] へのログインが含まれない DAC を登録するには、 **dbmanager** ロールまたは **serveradmin** ロールのメンバーシップが必要です。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] へのログインが含まれる DAC を登録するには、 **loginmanager** ロールまたは **serveradmin** ロールのメンバーシップが必要です。  
  
##  <a name="UsingRegisterDACWizard"></a> データ層アプリケーションの登録ウィザードの使用  
 **ウィザードを使用して DAC を登録するには**  
  
1.  **オブジェクト エクスプローラー**で、DAC として登録するデータベースを含んだインスタンスのノードを展開します。  
  
2.  **[データベース]** ノードを展開します。  
  
3.  登録するデータベースを右クリックし、 **[タスク]** をポイントして **[データ層アプリケーションとして登録]** をクリックします。  
  
4.  ウィザードの各ダイアログの手順を実行します。  
  
    1.  [[説明] ページ](#Introduction)  
  
    2.  [[プロパティの設定] ページ](#Set_properties)  
  
    3.  [[検証と概要] ページ](#Summary)  
  
    4.  [[DAC の登録] ページ](#Register)  
  
##  <a name="Introduction"></a> [説明] ページ  
 このページには、データ層アプリケーションの登録手順が表示されます。  
  
 **[次回からこのページを表示しない]** : 今後このページを表示しないようにするには、このチェック ボックスをオンにします。  
  
 **[次へ >]** : **[プロパティの設定]** ページに進みます。  
  
 **[キャンセル]** : DAC を登録せずにウィザードを終了します。  
  
##  <a name="Set_properties"></a> [プロパティの設定] ページ  
 このページでは、アプリケーション名やバージョンなど DAC レベルのプロパティを指定します。  
  
 **[アプリケーション名]** : DAC 定義を識別するための名前。このフィールドには、選択したデータベースの名前が自動的に入力されます。  
  
 **[バージョン]** : DAC のバージョンを表す数値。 DAC のバージョンは、開発者が操作している DAC のバージョンを特定するために Visual Studio で使用します。 DAC を配置すると、バージョンは `msdb` データベースに格納され、後で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]の **[データ層アプリケーション]** ノードの下に表示できます。  
  
 **説明** : 省略可。 この DAC の目的についての説明。 DAC を配置すると、説明は `msdb` データベースに格納され、後で [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]の **[データ層アプリケーション]** ノードの下に表示できます。  
  
 **\< 前**へ-**概要** ページに戻ります。  
  
 **[次へ >]** : データベースのオブジェクトから DAC を作成できるかどうかを検証し、その結果を **[検証と概要]** ページに表示します。  
  
 **[キャンセル]** : DAC を登録せずにウィザードを終了します。  
  
##  <a name="Summary"></a> [検証と概要] ページ  
 このページでは、DAC の登録時にウィザードが行うアクションを確認します。 データベース内のオブジェクトから DAC を作成できるかどうかを検証する際、次の 3 つの処理が順番に実行されます。  
  
### <a name="retrieving-objects"></a>オブジェクトの取得  
 **[データベース オブジェクトとサーバー オブジェクトを取得しています。]** : データベースおよびデータベース エンジンのインスタンスから必要なすべてのオブジェクトを取得する間、進行状況バーが表示されます。  
  
 [**前\<** ]: **[プロパティの設定]** ページに戻り、エントリを変更します。  
  
 **[次へ >]** : DAC が登録され、 **[DAC の登録]** ページが表示されます。  
  
 **[キャンセル]** : DAC を登録せずにウィザードを終了します。  
  
### <a name="validating-objects"></a>オブジェクトの検証  
 **Checking**  _SchemaName_ **.** _ObjectName_ **.** : 取得したオブジェクトの依存関係を検証し、それらすべてのオブジェクトが DAC に対して有効かどうかを確認する間、進行状況バーが表示されます。 _SchemaName_ **.** _ObjectName_ は、現在検証されているオブジェクトを示します。  
  
 [**前\<** ]: **[プロパティの設定]** ページに戻り、エントリを変更します。  
  
 **[次へ >]** : DAC が登録され、 **[DAC の登録]** ページが表示されます。  
  
 **[キャンセル]** : DAC を登録せずにウィザードを終了します。  
  
### <a name="summary"></a>まとめ  
 **[次の設定を使用して DAC を登録します。]** : DAC に追加されるプロパティとオブジェクトのレポートが表示されます。  
  
 **[レポートの保存]** : 検証レポートのコピーを HTML ファイルに保存します。 既定のフォルダーは、Windows アカウントの Documents フォルダーにある **SQL Server Management Studio\DAC Packages** フォルダーです。  
  
 [**前\<** ]: **[プロパティの設定]** ページに戻り、エントリを変更します。  
  
 **[次へ >]** : DAC が登録され、 **[DAC の登録]** ページが表示されます。  
  
 **[キャンセル]** : DAC を登録せずにウィザードを終了します。  
  
##  <a name="Register"></a> [DAC の登録] ページ  
 このページには、登録の成功または失敗が表示されます。  
  
 **[DAC の登録]** : DAC を登録するために行った各アクションの成功または失敗が表示されます。 内容を確認して、各アクションの成功または失敗を判断します。 エラーが発生したアクションには、 **[結果]** 列にリンクが表示されます。 そのアクションのエラーのレポートを表示するには、リンクをクリックします。  
  
 **[レポートの保存]** : 登録レポートを HTML ファイルに保存します。 ファイルには、アクションで発生したすべてのエラーを含む、各アクションのステータスが報告されます。 既定のフォルダーは、Windows アカウントの Documents フォルダーにある **SQL Server Management Studio\DAC Packages** フォルダーです。 ファイル名の形式は、\<DACPackageName>_RegisterDACReport_yyyymmdd.html です。ここで、\<*DACPackageName*> は配置するパッケージの名前、*yyyy* は現在の年、*mm* は現在の月、*dd* は現在の日です。  
  
 **[完了]** : ウィザードを終了します。  
  
##  <a name="RegisterDACPowerShell"></a> PowerShell を使用した DAC の登録  
 **PowerShell スクリプトから Register() メソッドを使用してデータベースを DAC として登録するには**  
  
1.  SMO サーバー オブジェクトを作成し、DAC として登録するデータベースを含んだインスタンスに設定します。  
  
2.  データベースの名前を指定する変数を追加します。  
  
3.  DAC のメタデータ (DAC 名、バージョン、説明など) を指定します。  
  
4.  上記で指定した情報を使用して Register メソッドを実行します。  
  
### <a name="example-powershell"></a>例 (PowerShell)  
 次の例は、DAC として MyDB というデータベースを登録します。  
  
```powershell
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = Get-Item .  
  
## Specify the database to register as a DAC.  
$dbname = "MyDB"  
  
## Specify the DAC metadata.  
$applicationname = "MyApplication"  
$version = "1.0.0.0"  
$description = "This DAC defines the database used by my application."  
  
## Register the DAC.  
$registerunit = New-Object Microsoft.SqlServer.Management.Dac.DacExtractionUnit($srv, $dbname, $applicationname, $version)  
$registerunit.Description = $description  
$registerunit.Register()  
```  
  
## <a name="see-also"></a>関連項目  
 [データ層アプリケーション](data-tier-applications.md)  
