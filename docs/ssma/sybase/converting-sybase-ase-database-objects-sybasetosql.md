---
title: Sybase ASE データベース オブジェクト (SybaseToSQL) の変換 |Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Converting Database Objects
ms.assetid: 509cb65d-2f54-427a-83d7-37919cc4e3e3
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 507ac2a61043260435a18c90fb473130988e7f35
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948511"
---
# <a name="converting-sap-ase-database-objects-sybasetosql"></a>SAP ASE データベース オブジェクト (SybaseToSQL) の変換
SAP Adaptive Server Enterprise (ASE) に接続すると後に、接続されている[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SAP Adaptive Server Enterprise (ASE) のデータベース オブジェクトを変換できる Azure SQL とプロジェクトの設定とデータ マッピング オプション、または[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL データベースオブジェクト。  
  
## <a name="the-conversion-process"></a>変換プロセス  
ASE からオブジェクトの定義は、データベース オブジェクトの変換と同様に変換して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure オブジェクト、および SSMA メタデータにこの情報を読み込みます。 インスタンスに情報は読み込まれません[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL。 使用して、オブジェクトとそのプロパティを表示することができますし、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL メタデータ エクスプ ローラー。
  
SSMA に出力ウィンドウおよびエラー メッセージを出力メッセージの出力、変換中に、**エラー一覧**ウィンドウ。 ASE のデータベースまたは必要な変換の結果を得るため、変換プロセスを変更するのにかどうかを確認するのには、出力およびエラー情報を使用します。  
  
## <a name="setting-conversion-options"></a>変換オプションの設定  
オブジェクトを変換する前に、プロジェクトの変換オプションを確認して、**プロジェクト設定** ダイアログ ボックス。 このダイアログ ボックスを使用すると、SSMA が関数とグローバル変数に変換する方法を設定できます。 詳細については、次を参照してください。[プロジェクト設定&#40;変換&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)します。  
  
## <a name="converting-ase-database-objects"></a>ASE データベース オブジェクトの変換  
ASE データベース オブジェクトを変換するには、最初に、変換するオブジェクトを選択し、SSMA 変換を実行します。 変換中に出力メッセージを表示する、**ビュー**メニューの **出力**します。  
  
**ASE のオブジェクトを SQL Server または SQL Azure の構文に変換するには**  
  
1.  Sybase メタデータ エクスプ ローラーで、ASE サーバーを展開し、展開**データベース**します。  
  
2.  変換するオブジェクトを選択します。  
  
    -   すべてのデータベースを変換する場合は、横にチェック ボックスを選択します**データベース**します。  
  
    -   変換またはデータベースの省略は、選択するか、データベース名の横にあるチェック ボックスをオフにします。  
  
    -   変換または個別のスキーマを省略は、データベースを展開し、**スキーマ**、選択するか、スキーマの横にあるチェック ボックスをオフにします。  
  
    -   変換またはオブジェクトのカテゴリの省略は、スキーマを展開し、オンまたはカテゴリの横にあるチェック ボックスをオフにします。  
  
    -   変換または個々 のオブジェクトの省略は、カテゴリ フォルダーを展開し、オンまたはオブジェクトの横にチェック ボックスをオフにします。  
  
3.  右クリックし、選択したすべてのオブジェクトを変換する**データベース**、し、**スキーマの変換**します。  
  
    オブジェクトまたは、含まれるフォルダーを右クリックして選択し、個々 のオブジェクトまたはオブジェクトのカテゴリを変換することも**スキーマの変換**します。  
  
> [!NOTE]  
> 完全に同等の SQL Server システム関数の動作では一致 SAP ASE システムの機能の一部の操作を行います。 SAP ASE の動作をエミュレートするためには、SSMA は、's2ss' と呼ばれるスキーマの変換された SQL Server データベースにユーザー定義関数を生成します。 プロジェクトの設定に応じていくつかの SQL Server のシステム関数はこれらのエミュレートされた関数で置き換えられます。 SSMA は、次のユーザー定義関数を作成します。  
  
||||  
|-|-|-|  
|**char_length_nvarchar**|**index_colorder**|**ssma_datepart**|  
|**char_length_varchar**|**inttohex**|**substring_nvarchar**|  
|**charindex_nvarchar**|**ssma_datediff**|**substring_varbinary**|  
|**charindex_varchar**|**hextoint**|**substring_varchar**|  
|**ulowsurr**|**to_unichar**|**ssma_current_time**|  
|**uhighsurr**|||  
  
## <a name="objects-not-supported-in-azure-sql"></a>Azure SQL でサポートされていないオブジェクト  
SQL Server、オンプレミスへの変換中に SAP ASE の次の T-SQL キーワードを SSMA で使用されますが、SQL Azure の T-SQL 構文では、これらのキーワードはサポートされていません。  
  
||||  
|-|-|-|  
|CHECKPOINT|CREATE/ALTER/DROP DEFAULT|CREATE/DROP RULE|  
|DBCC TRACEOFF|DBCC TRACEON|すべての許可、取り消し、拒否|  
|KILL|READTEXT|SELECT INTO|  
|SET OFFSETS|SETUSER|SHUTDOWN|  
|WRITETEXT|||  
  
## <a name="viewing-conversion-problems"></a>変換の問題を表示します。  
一部の SAP ASE オブジェクトに変換できません可能性があります。 変換の概要レポートを表示することによってコンバージョンの成功率を指定できます。  
  
**概要レポートを表示するには**  
  
1.  Sybase メタデータ エクスプ ローラーで選択**データベース**します。  
  
2.  右側のウィンドウで、選択、**レポート**タブ。  
  
    このレポートには、変換または評価されているすべてのデータベース オブジェクトの評価の概要レポートが表示されます。 個々 のオブジェクトの概要レポートを表示することもできます。  
  
    -   個々 のデータベースのレポートを表示するには、Sybase メタデータ エクスプ ローラーでデータベースを選択します。  
  
    -   個々 のデータベース オブジェクトのレポートを表示するには、Sybase メタデータ エクスプ ローラーで、オブジェクトを選択します。 変換の問題のあるオブジェクトは赤いエラー アイコンがあります。  
  
オブジェクトの変換に失敗した場合は、変換エラーを発生させた構文を表示することができます。  
  
**個々 の変換の問題を表示するには**  
  
1.  Sybase メタデータ エクスプ ローラーで、**データベース**します。  
  
2.  赤いエラー アイコンが表示されるデータベースを展開します。  
  
3.  展開、**スキーマ**フォルダー、し、赤いエラー アイコンが表示されるスキーマを展開します。  
  
4.  スキーマの下に赤いエラー アイコンが付いているフォルダーを展開します。  
  
5.  赤いエラー アイコンを含むオブジェクトを選択します。  
  
6.  右側のウィンドウで、選択、**レポート**タブ。  
  
7.  上部にある、**レポート** タブは、ドロップダウン リスト。 一覧表示されている場合**統計**、選択範囲を変更**ソース**します。  
  
    SSMA は、ソース コードとコードのすぐ上のいくつかのボタンに表示されます。  
  
8.  選択**次の問題**、右向き矢印の付いた赤いエラー アイコン。  
  
    SAP ASE の SSMA では、現在のオブジェクトで見つかった最初の問題のあるソース コードを強調表示されます。  
  
変換できなかった項目ごとにそのオブジェクトを決定する必要があります。  
  
-   プロシージャとトリガーのソース コードを編集することができます、 **SQL**タブ。  
  
-   削除または問題のあるコードを変更するには、SAP ASE オブジェクトを変更することができます。 を SSMA に更新されたコードを読み込むには、メタデータを更新する必要があります。 詳細については、次を参照してください。[への SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)します。  
  
-   オブジェクトは、移行から除外できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL のメタデータ エクスプ ローラーと Sybase メタデータ エクスプ ローラーにオブジェクトを読み込む前に、項目の横にあるチェック ボックスをオフに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL と SAP ASE からデータを移行します。  
  
## <a name="next-steps"></a>次の手順  
移行プロセスでは、次の手順は[を SQL Server に変換されたデータベース オブジェクトの読み込み/SQL Azure (SybaseToSQL)](https://msdn.microsoft.com/4c59256f-99a8-4351-9559-a455813dbd06)します。  
  
## <a name="see-also"></a>関連項目  
[SQL Server - Azure SQL Database への SAP ASE データベースの移行&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
