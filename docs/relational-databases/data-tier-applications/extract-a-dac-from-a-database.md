---
title: データベースからの DAC の抽出 | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2016
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.extractdacwizard.validationandsummary.f1
- sql13.swb.extractdacwizard.introduction.f1
- sql13.swb.extractdacwizard.selectdatapage.f1
- sql13.swb.extractdacwizard.setdacproperties.f1
- sql13.swb.extractdacwizard.buildandsave.f1
helpviewer_keywords:
- extract DAC
- How to [DAC], extract
- data-tier application [SQL Server], extract
- wizard [DAC], extract
ms.assetid: ae52a723-91c4-43fd-bcc7-f8de1d1f90e5
author: stevestein
ms.author: sstein
ms.openlocfilehash: 86482b666c2ecfc5e9fcc09c1d06df14640386d0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68134794"
---
# <a name="extract-a-dac-from-a-database"></a>データベースからの DAC の抽出
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **データ層アプリケーションの抽出ウィザード** または Windows PowerShell スクリプトを使用すると、既存の SQL Server データベースからデータ層アプリケーション (DAC) パッケージを抽出できます。 抽出プロセスでは、データベース オブジェクトの定義とそれに関連するインスタンスレベルの要素を格納した DAC パッケージ ファイルが作成されます。 たとえば、DAC パッケージ ファイルには、データベース テーブル、ストアド プロシージャ、ビュー、ユーザー、およびデータベース ユーザーにマップされているログインが含まれます。  
  
 
## <a name="before-you-begin"></a>アンインストールの準備  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]、または [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 4 以降のインスタンスに存在するデータベースから DAC を抽出できます。 DAC から配置されたデータベースに対して抽出プロセスが実行された場合、データベース内のオブジェクトの定義のみが抽出されます。 プロセスは **msdb** (**の** マスター [!INCLUDE[ssSDS](../../includes/sssds-md.md)]) で登録された DAC を参照しません。 抽出プロセスは、データベース エンジンの現在のインスタンスの DAC 定義を登録しません。 DAC の登録の詳細については、「 [Register a Database As a DAC](../../relational-databases/data-tier-applications/register-a-database-as-a-dac.md)」を参照してください。  
  
##  <a name="LimitationsRestrictions"></a> 制限事項と制約事項  
 DAC を抽出できるのは、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]、または [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) 以降のデータベースに限られます。 DAC でサポートされていないオブジェクトまたは包含ユーザーがデータベースに存在する場合は、DAC を抽出できません。 DAC でサポートされるオブジェクトの種類の詳細については、「 [DAC Support For SQL Server Objects and Versions](../../relational-databases/data-tier-applications/dac-support-for-sql-server-objects-and-versions.md)」を参照してください。  
  
##  <a name="Permissions"></a> Permissions  
 DAC を抽出するには、少なくとも ALTER ANY LOGIN 権限とデータベース スコープの VIEW DEFINITION 権限、および **sys.sql_expression_dependencies**に対する SELECT 権限が必要です。 DAC を抽出できるのは、DAC を抽出するデータベースの database_owner 固定データベース ロールのメンバーでもある、securityadmin 固定サーバー ロールのメンバーです。 sysadmin 固定サーバー ロールのメンバーまたは **sa** という組み込みの SQL Server システム管理者アカウントも DAC を抽出できます。  
  
##  <a name="UsingDACExtractWizard"></a> データ層アプリケーションの抽出ウィザードの使用  
 **ウィザードを使用して DAC を抽出するには**  
  
1.  **オブジェクト エクスプローラー**で、DAC の抽出元となるデータベースを含んだインスタンスのノードを展開します。  
  
2.  **[データベース]** ノードを展開します。  
  
3.  DAC の抽出元となるデータベースのノードを右クリックし、 **[タスク]** をポイントして **[データ層アプリケーションの抽出]** を選択します。  
  
4.  ウィザードの各ダイアログの手順を実行します。  
  
    1.  [[説明] ページ](#Introduction)  
  
    2.  [[データの選択] ページ](#SelectData)  
  
    3.  [[プロパティの設定] ページ](#SetProperties)  
  
    4.  [[検証と概要] ページ](#ValidateSummary)  
  
    5.  [[パッケージのビルド] ページ](#BuildPackage)  
  
###  <a name="Introduction"></a> ウィザードの [説明] ページ  
 このページでは、データ層アプリケーションを抽出する手順について説明します。  
  
 **[次回からこのページを表示しない]** : 今後このページを表示しないようにするには、このチェック ボックスをオンにします。  
  
 **[次へ >]** : **[方法の選択]** ページに進みます。  
  
 **[キャンセル]** : データベースからデータ層アプリケーションを抽出せずにウィザードを終了します。  
  
 [&#91;抽出ウィザード&#93;](#UsingDACExtractWizard)  
  
###  <a name="SelectData"></a> Select data page  
データ層アプリケーション (DAC) パッケージ ファイルに含める参照データを選択できます。 DAC パッケージにデータを含めることは必須ではありません。 DAC パッケージには、データベースに関連するサポート対象のデータベース オブジェクトおよびインスタンス オブジェクトのスキーマがすべて、既に含まれています。  
  
 DAC パッケージ ファイルには最大 10 MB の参照データを含めることができます。 ただし、DAC に含まれるテーブルの場合、 **image** や **varchar(max)** などのバイナリ ラージ オブジェクト (BLOB) データ型を含めることはできません。 別のデータベースへ転送するためにより大量のデータを抽出するには、SQL Server Integration Services、一括コピー ユーティリティ、または他の多くのデータ移行方法のいずれかを使用します。  
  
 **[データベース テーブル]** : DAC パッケージに含めるデータが含まれたデータベース テーブルの横にあるチェック ボックスをオンにします。 10,000 行以下のテーブルを最大 10 個選択できます。  
  
 [&#91;抽出ウィザード&#93;](#UsingDACExtractWizard)  
  
###  <a name="SetProperties"></a> Set properties page  
 ウィザードのこのページでは、データ層アプリケーション (DAC) に関する情報を設定します。 これらのプロパティは、DAC を識別し、他の DAC と区別するために使用されます。  
  
 **[名前]** : この名前で、DAC を識別します。 DAC パッケージ ファイルと異なる名前を設定できますが、アプリケーションを識別できる名前である必要があります。 たとえば、データベースを財務アプリケーションで使用する場合は、"DAC Finance" などの名前を付けます。  
  
 **[バージョン (xx.xx.xx.xx という形式で、x は数字)]** : DAC のバージョンを表す数値。 DAC のバージョンは、開発者が操作している DAC のバージョンを特定するために Visual Studio で使用します。 DAC を配置すると、バージョンは **msdb** データベースに格納され、後で **の** [データ層アプリケーション] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ノードの下に表示できます。  
  
 **[説明]** - 省略可能です。 DAC の説明です。 DAC を配置すると、説明は **msdb** データベースに格納され、後で **の** [データ層アプリケーション] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]ノードの下に表示できます。  
  
 **[DAC パッケージ ファイルに保存 (.dacpac 拡張子をファイル名に含める)]** : DAC を拡張子が .dacpac の DAC パッケージ ファイルに保存します。 **[参照]** ボタンをクリックしてファイルの名前と場所を指定します。  
  
 **[既存のファイルの上書き]** : 同じ名前の DAC パッケージ ファイルが既に存在する場合にそのファイルを置き換えるには、このチェック ボックスをオンにします。  
  
###  <a name="ValidateSummary"></a> Validation and summary page  
 このページでは、すべてのデータベース オブジェクトがデータ層アプリケーション (DAC) でサポートされているかどうかを検証します。 また、データベース オブジェクト間の依存関係を確認して、DAC に正常に含めることができるオブジェクトのセットを判断します。 その後、検証レポートと、このウィザードで選択したオプションの概要を表示します。 オプションを変更するには、 **[戻る]** をクリックします。 DAC の抽出を開始するには、 **[次へ]** をクリックします。  
  
> **注!** 1 つ以上のオブジェクトが DAC でサポートされていない場合は、 **[次へ]** ボタンは無効になり、抽出プロセスを続行できません。 その場合は、サポートされていないオブジェクトを削除した後に、このウィザードを再度実行することをお勧めします。  
  
 **[概要]** : 選択したオプションの概要が **[DAC のプロパティ]** の下に表示されます。 検証の結果は **[DAC オブジェクト]** の下に表示されます。 検証の結果には、次の 3 種類があります。  
  
-   **[DAC に正常に含まれるオブジェクト]** : これらのオブジェクトとその依存関係はサポートされており、DAC に正常に含めることができます。  
  
-   **[DAC に含まれるオブジェクト (警告あり)]** : これらのオブジェクトはサポートされていますが、DAC でサポートされていない他のオブジェクトに依存しています。  
  
-   **[DAC に含まれないオブジェクト]** : これらのオブジェクトはサポートされていないため、DAC を正常に抽出する前にデータベースから削除する必要があります。  
  
 検証プロセスでは、複数レベルで依存関係の確認が行われます。 たとえば、あるストアド プロシージャがサポートされていない CLR データ型を使用するテーブルに依存している場合、そのストアド プロシージャは **[DAC に含まれるオブジェクト (警告あり)]** の下に表示されます。  
  
 1 つ以上のオブジェクトが DAC でサポートされていない場合は、 **[次へ]** ボタンは無効になり、抽出プロセスを続行できません。 その場合は、サポートされていないオブジェクトを削除した後に、このウィザードを再度実行することをお勧めします。  
  
 **[レポートの保存]** : 概要の **[DAC のオブジェクト]** ノードの下に表示されるすべてのオブジェクトの一覧を示す HTML ベースのファイルを保存できるようにします。 このレポートは、データベース オブジェクトの一部が DAC でサポートされていない場合に役立ちます。 DAC の抽出を再試行する前に、このレポートを使用してサポートされていないオブジェクトを変更または削除します。  
  
 ###  <a name="BuildPackage"></a> Build package page  
 このページでは、データ層アプリケーション (DAC) を抽出するウィザードの進行状況を監視できます。  
  
 **[アクション]** : **[DAC パッケージ ファイルの作成と保存]** では、SQL Server データベースから DAC が抽出されます。 その後、DAC パッケージがメモリ内に作成され、指定した場所に保存されます。 **[結果]** 列のリンクをクリックすると、対応する手順の結果を確認できます。  
  
 **[レポートの保存]** : クリックすると、ウィザードの進行状況の結果がファイルに保存されます。  
  
 **[完了]** : 処理が完了した後やエラーが発生した場合にクリックしてウィザードを閉じます。  
   
##  <a name="ExtractDACPowerShell"></a> PowerShell を使用して DAC を抽出する  
 **PowerShell スクリプトで Extract() メソッドを使用してデータベースから DAC を抽出するには**  
  
1.  SMO サーバー オブジェクトを作成し、それを DAC の抽出元データベースが含まれているインスタンスに設定します。  
  
2.  データベースの名前を指定する変数を追加します。  
  
3.  DAC のメタデータ (DAC 名、バージョン、説明など) を指定します。  
  
4.  抽出された DAC パッケージ ファイルのパスとファイル名を指定します。  
  
5.  上で指定した情報を使用して Extract メソッドを実行します。  
  
### <a name="example-powershell"></a>例 (PowerShell)  
 次の例では、MyDB という名前のデータベースから MyApplication という名前の DAC を抽出します。  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Specify the database to extract to a DAC.  
$dbname = "MyDB"  
  
## Specify the DAC metadata.  
$applicationname = "MyApplication"  
$version = "1.0.0.0"  
$description = "This DAC defines the database used by my application."  
  
## Specify the location and name for the extracted DAC package.  
$dacpacPath = "C:\MyDACs\MyApplication.dacpac"  
  
## Extract the DAC.  
$extractionunit = New-Object Microsoft.SqlServer.Management.Dac.DacExtractionUnit($srv, $dbname, $applicationname, $version)  
$extractionunit.Description = $description  
$extractionunit.Extract($dacpacPath)  
```  
  
## <a name="see-also"></a>参照  
 [の](../../relational-databases/data-tier-applications/data-tier-applications.md)  
  
  
