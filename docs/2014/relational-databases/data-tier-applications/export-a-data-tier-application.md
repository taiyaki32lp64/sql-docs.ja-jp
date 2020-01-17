---
title: データ層アプリケーションのエクスポート | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.exportdac.settings.f1
- sql12.swb. exportdac.settings.f1
- sql12.swb.exportdac.welcome.f1
- sql12.swb. exportdac.summary.f1
- sql12.swb.exportdac.progress.f1
- sql12.swb.exportdac.summary.f1
- sql12.swb.exportdac.results.f1
- sql12.swb. exportdac.results.f1
helpviewer_keywords:
- How to [DAC], export
- wizard [DAC], export
- export DAC
- data-tier application [SQL Server], export
ms.assetid: 61915bc5-0f5f-45ac-8cfe-3452bc185558
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3335c5a7fcb46b901777de0404b5206aa6a876f6
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2019
ms.locfileid: "70175977"
---
# <a name="export-a-data-tier-application"></a>データ層アプリケーションのエクスポート
  配置されているデータ層アプリケーション (DAC) またはデータベースをエクスポートすると、エクスポート ファイルが作成されます。このファイルには、データベース内のオブジェクトの定義に加え、テーブルに格納されているすべてのデータが含まれています。 さらに、このエクスポート ファイルを [!INCLUDE[ssDE](../../includes/ssde-md.md)]の別のインスタンスまたは [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]にインポートすることもできます。 エクスポートとインポートという操作を組み合わせることで、DAC をインスタンス間で移行したり論理バックアップを作成したりすることが可能です。または、[!INCLUDE[ssSDS](../../includes/sssds-md.md)] に配置されているデータベースの社内用コピーを作成することもできます。  
  
## <a name="before-you-begin"></a>作業を開始する準備  
 エクスポート プロセスでは、2 つの段階を経て DAC エクスポート ファイルが構築されます。  
  
1.  エクスポートではエクスポート ファイル (BACPAC ファイル) に DAC 定義が構築されます。DAC の抽出時には DAC パッケージ ファイルに DAC 定義が構築されますが、これと同様の処理が行われます。 エクスポートされた DAC 定義には、現在のデータベース内のすべてのオブジェクトが含まれます。 もともと DAC から配置され、その後直接変更が加えられたデータベースに対してエクスポート プロセスが実行された場合、エクスポートされる定義は、データベース内のオブジェクト セットと一致し、元の DAC に定義されている内容とは一致しません。  
  
2.  データベース内のすべてのテーブルからデータが一括コピーされて、エクスポート ファイルに組み込まれます。  
  
 エクスポート プロセスでは、DAC バージョンが 1.0.0.0 に設定され、エクスポート ファイル内の DAC の説明は空の文字列に設定されます。 データベースが DAC から配置された場合、エクスポート ファイル内の DAC 定義には、元の DAC に割り当てられた名前が格納されます。それ以外の場合、DAC 名はデータベース名に設定されます。  
  

###  <a name="LimitationsRestrictions"></a> 制限事項と制約事項  
 DAC またはデータベースをエクスポートできるのは、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]、または [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) 以降のデータベースに限られます。  
  
 DAC でサポートされていないオブジェクトまたは包含ユーザーが存在するデータベースはエクスポートできません。 DAC でサポートされるオブジェクトの種類の詳細については、「 [DAC Support For SQL Server Objects and Versions](dac-support-for-sql-server-objects-and-versions.md)」を参照してください。  
  
###  <a name="Permissions"></a> アクセス許可  
 DAC をエクスポートするには、少なくとも ALTER ANY LOGIN 権限とデータベース スコープの VIEW DEFINITION 権限、および **sys.sql_expression_dependencies**に対する SELECT 権限が必要です。 DAC をエクスポートできるのは、DAC をエクスポートするデータベースの database_owner 固定データベース ロールのメンバーでもある、securityadmin 固定サーバー ロールのメンバーです。 sysadmin 固定サーバー ロールのメンバーまたは **sa** という組み込みの SQL Server システム管理者アカウントも DAC をエクスポートできます。  
  
##  <a name="UsingDeployDACWizard"></a> データ層アプリケーションのエクスポート ウィザードの使用  
 **ウィザードを使用して DAC をエクスポートするには**  
  
1.  内部設置型または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内で、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]のインスタンスに接続します。  
  
2.  **オブジェクト エクスプローラー**で、DAC のエクスポート元のインスタンスのノードを展開します。  
  
3.  データベース名を右クリックします。  
  
4.  **[タスク]** をクリックし、 **[データ層アプリケーションのエクスポート]** を選択します。  
  
5.  ウィザードの各ダイアログの手順を実行します。  
  
    -   [[説明] ページ](#Introduction)  
  
    -   [[エクスポートの設定] ページ](#Export_settings)  
  
    -   [[検証] ページ](#Validation)  
  
    -   [[概要] ページ](#Summary)  
  
    -   [[進行状況] ページ](#Progress)  
  
    -   [[結果] ページ](#Results)  
  
##  <a name="Introduction"></a> [説明] ページ  
 このページには、データ層アプリケーションのエクスポート ウィザードの手順が表示されます。  
  
 **オプション**  
  
 **[次回からこのページを表示しない]** : 今後 [説明] ページを表示しないようにするには、このチェック ボックスをオンにします。  
  
 **[次へ]** : **[DAC パッケージの選択]** ページに進みます。  
  
 **[キャンセル]** : 操作を取り消し、ウィザードを閉じます。  
  
##  <a name="Export_settings"></a> [エクスポートの設定] ページ  
 このページを使用して、BACPAC ファイルを作成する場所を指定します。  
  
-   **[ローカル ディスクに保存]** : BACPAC ファイルをローカル コンピューター上のディレクトリに作成します。 **[参照]** をクリックしてローカル コンピューター内を参照するか、用意されている領域にパスを指定します。 パス名には、ファイル名および .bacpac 拡張子を含める必要があります。  
  
-   **[Save to Azure]\(Azure に保存\)** : BACPAC ファイルを Azure コンテナーに作成します。 このオプションを検証するためには、Azure コンテナーに接続する必要があります。 このオプションでは、一時ファイル用のローカル ディレクトリを指定する必要もあります。 一時ファイルは、指定した場所に作成され、操作の完了後も残ります。  
  
 エクスポートするテーブルのサブセットを指定するには、 **[詳細]** オプションを使用します。  
  
##  <a name="Validation"></a> [検証] ページ  
 [検証] ページを使用して、操作の妨げとなる問題を確認します。 続行するには、妨げとなる問題を解決し、 **[検証の再実行]** をクリックして、検証が成功したことを確認します。  
  
 続行するには、 **[次へ]** をクリックします。  
  
##  <a name="Summary"></a> [概要] ページ  
 このページを使用すると、操作の指定ソースとターゲットの設定を確認できます。 指定した設定でエクスポート操作を実行するには、 **[完了]** をクリックします。 エクスポート操作をキャンセルしてウィザードを終了するには、 **[キャンセル]** をクリックします。  
  
##  <a name="Progress"></a> [進行状況] ページ  
 このページには、操作の進行状況を示す進行状況バーが表示されます。 詳細な状態を表示するには、 **[詳細表示]** をクリックします。  
  
##  <a name="Results"></a> [結果] ページ  
 このページでは、エクスポート操作の成功と失敗が報告され、各アクションの結果が示されます。 エラーが発生したアクションには、 **[結果]** 列にリンクが表示されます。 そのアクションのエラーのレポートを表示するには、リンクをクリックします。  
  
 **[完了]** をクリックして、ウィザードを終了します。  
  
##  <a name="NetApp"></a> .Net Framework アプリケーションの使用  
 **.Net Framework アプリケーションで Export() メソッドを使用して DAC をエクスポートするには**  
  
 コード例を参照するには、 [Codeplex](https://go.microsoft.com/fwlink/?LinkId=219575)上の DAC サンプル アプリケーションをダウンロードしてください。  
  
1.  SMO サーバー オブジェクトを作成し、エクスポートする DAC が含まれたインスタンスにそれを設定します。  
  
2.  `ServerConnection` オブジェクトを開いて、同じインスタンスに接続します。  
  
3.  `Export` 型の `Microsoft.SqlServer.Management.Dac.DacStore` メソッドを使用して、DAC をエクスポートします。 エクスポートする DAC の名前と、エクスポート ファイルの出力先となるフォルダーのパスを指定します。  
  
## <a name="see-also"></a>参照  
 [データ層アプリケーション](data-tier-applications.md)   
 [データベースからの DAC の抽出](extract-a-dac-from-a-database.md)  
  
  
