---
title: Access インベントリ (AccessToSQL) のエクスポート |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- Access databases, exporting metadata
- exporting
- exporting Access metadata
- exporting, Access metadata
- exporting, querying exported metadata
- inventories of Access databases
- querying exported metadata
ms.assetid: 7e1941fb-3d14-4265-aff6-c77a4026d0ed
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 0c05eafd1fb58b6ece15f5ad8721228d9d4beab6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006559"
---
# <a name="exporting-an-access-inventory-accesstosql"></a>Access インベントリ (AccessToSQL) のエクスポート
複数の Access データベースがあるし、に移行するものがわからない場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]プロジェクト内のすべての Access データベースのインベントリをエクスポートすることができます。 確認し、データベースと移行するには、そのデータベース内のオブジェクトを決定するインベントリのメタデータを照会します。 このインベントリすることができます簡単に、次の質問に対する回答を検索します。  
  
-   最大級のデータベースとは  
  
-   ほとんどのデータベースの所有者ですか。  
  
-   のどのデータベースでは、同じテーブルを含めるか。  
  
-   過去 6 か月間でデータベースが変更されていないか。  
  
-   どのデータベースには、個人情報が含まれてでしょうか。  
  
これらの質問回答に使用されるクエリの例は、このトピックの最後で提供されます。  
  
## <a name="exported-metadata"></a>エクスポートされたメタデータ  
SSMA は、Access データベース、テーブル、列、インデックス、外部キー、クエリ、レポート、フォーム、マクロ、およびモジュールに関するメタデータをエクスポートします。 これらの項目のカテゴリのそれぞれについてのメタデータは、別のテーブルにエクスポートされます。 これらのテーブルのスキーマは、次を参照してください。 [Access のインベントリ スキーマ](access-inventory-schemas-accesstosql.md)します。  
  
## <a name="exporting-inventory-data"></a>インベントリ データをエクスポートします。  
Access インベントリをエクスポートするに最初に開くまたは SSMA プロジェクトを作成し分析する Access データベースを追加する必要があります。 指定したそれらのデータベースに関するメタデータをエクスポートする SSMA プロジェクトにデータベースを追加した後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベースおよびスキーマです。 必要に応じて、SSMA は、メタデータを格納するテーブルを作成します。 SSMA を Access データベースに関するメタデータを追加し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース。  
  
> [!NOTE]  
> Access データベースは、複数のファイルに分割することができます。 テーブル、クエリ、フォーム、レポート、マクロ、モジュール、およびショートカットが含まれているフロント エンドのデータベースを含むバックエンド データベース。 分割データベースを移行する場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SSMA をフロント エンドのデータベースを追加します。  
  
次の手順は、プロジェクトを作成、データベース プロジェクトを追加に接続する方法をについて説明します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、し、インベントリ データをエクスポートします。  
  
**プロジェクトを作成するには**  
  
1.  アクセスするためには、SSMA を開きます。  
  
2.  **[ファイル]** メニューの **[新しいプロジェクト]** を選択します。  
  
    **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
3.  **名前**ボックスに、プロジェクトの名前を入力します。  
  
4.  **場所**ボックスで、入力するか、プロジェクトのフォルダーを選択します。  
  
5.  **移行先**コンボ ボックスに、移行、およびクリックするターゲット バージョンを選択**OK**します。  
  
プロジェクトの作成の詳細については、次を参照してください。 [Creating and Managing Projects](creating-and-managing-projects-accesstosql.md)します。  
  
**検索データベースを追加するには**  
  
1.  **ファイル** メニューのをクリックして**検索データベース**します。  
  
2.  検索データベースのウィザードで、ドライブ、ファイルのパスまたは UNC パスを検索するを入力します。 またはをクリックして**参照**ドライブまたはネットワーク フォルダーを選択します。  
  
3.  クリックして**追加**をリスト ボックスに場所を追加します。  
  
    追加の検索場所を追加する前の 2 つの手順を繰り返します。  
  
4.  必要に応じて、返されるデータベースの一覧を絞り込む検索条件を追加します。  
  
    > [!IMPORTANT]  
    > **ファイル名の全部または一部**テキスト ボックスでは、ワイルドカード文字はサポートされません。  
  
5.  クリックして**スキャン**します。  
  
    スキャン ページが表示されます。 これには、検出されたデータベースと検索の進行状況が表示されます。 検索を停止する をクリックして**停止**します。  
  
6.  ファイルの選択 ページで、プロジェクトに追加する各データベースを選択します。  
  
    使用することができます、**すべて選択**と**すべてクリア**を選択するか、すべてのデータベースをクリアするリストの上部にあるボタン。 CTRL キーを押しながら複数の行を選択したり、行の範囲を選択するように、SHIFT キーを保持できます。  
  
7.  **[次へ]** をクリックします。  
  
8.  確認してください ページで、次のようにクリックします。**完了**します。  
  
データベースをプロジェクトに追加する方法の詳細については、次を参照してください。[の追加と削除の Access データベース ファイル](adding-and-removing-access-database-files-accesstosql.md)します。  
  
**SQL Server に接続するには**  
  
1.  **ファイル**メニューの  **SQL サーバーへの接続**します。  
  
2.  接続ダイアログ ボックスで入力するかのインスタンスの名前を選択[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
    -   ローカル コンピューターの既定のインスタンスに接続する場合は、入力**localhost**またはドット ( **.** )。  
  
    -   別のコンピューターで既定のインスタンスに接続する場合は、コンピューターの名前を入力します。  
  
    -   名前付きインスタンスに接続する場合は、コンピューター名、バック スラッシュ、およびインスタンス名を入力します。 以下に例を示します。\Myinstance します。  
  
3.  **データベース**ボックスに、エクスポートされたメタデータのターゲット データベースの名前を入力します。  
  
4.  場合、インスタンスの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]既定以外のポートで接続を受け入れる、使用されるポート番号を入力するように構成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内の接続、**サーバー ポート**ボックス。 既定のインスタンスの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]既定のポート番号は 1433 です。 名前付きインスタンスは、SSMA の試行からポート番号を取得する、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービス。  
  
5.  **認証**ドロップダウン メニューで、接続に使用する、認証の種類を選択します。 現在の Windows アカウントを使用する**Windows 認証**します。 使用する、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログインで、 **SQL Server 認証**、およびユーザー名とパスワードを入力します。  
  
接続の詳細については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を参照してください[SQL Server に接続する&#40;AccessToSQL&#41;](../../ssma/access/connecting-to-sql-server-accesstosql.md)します。  
  
**インベントリ情報をエクスポートするには**  
  
1.  メタデータ エクスプ ローラーでのアクセス、**アクセス メタベース**します。  
  
2.  次のチェック ボックスをオン**データベース**します。  
  
    個々 のデータベースまたはデータベース オブジェクトを省略するには展開、**データベース**フォルダー、およびデータベースまたはデータベース オブジェクトの横にあるチェック ボックスをオフにします。  
  
3.  右クリック**データベース**選択**スキーマのエクスポート**します。  
  
4.  **[スキーマのエクスポートの**] ダイアログ ボックスでは、エクスポートのメタデータのターゲット スキーマを選択し、順にクリックします**OK**します。  
  
メタデータをエクスポートするたびに SSMA は、インベントリ データを追加します。 既存のインベントリ データが更新または削除されません。  
  
## <a name="querying-the-exported-metadata"></a>エクスポートされたメタデータのクエリを実行します。  
Access データベースに関するメタデータをエクスポートした後は、メタデータを照会できます。 クエリ エディター ウィンドウを使用する、次の手順について説明する[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]クエリを実行します。  
  
**メタデータを照会するには**  
  
1.  **開始**メニューで、**すべてのプログラム**、 をポイント**Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005**または**Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008**または**Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012**、 をクリックし、 **SQL Server Management Studio**します。  
  
2.  **サーバーへの接続** ダイアログ ボックスでは、設定を確認し、順にクリックします**Connect**します。  
  
3.  Management Studio ツールバーで、次のようにクリックします。**新しいクエリ**クエリ エディターを開きます。  
  
4.  クエリ エディター ウィンドウで、クエリを入力します。 いくつかの例は、次のセクションに表示されます。  
  
5.  クエリを実行する F5 キーを押します。  
  
## <a name="query-examples"></a>クエリの例  
次のクエリを実行する前にを使用してを実行する必要があります*database_name*エクスポートされたメタデータを含むデータベースに対してクエリを実行することを確認するクエリ。 たとえば、MyAccessMetadata という名前のデータベースにメタデータをエクスポートする場合は追加する、次の先頭に、[!INCLUDE[tsql](../../includes/tsql-md.md)]コード。  
  
```  
USE MyAccessMetadata;  
GO  
```  
すべての次の例を使用して、 **dbo**スキーマ。 別のスキーマにメタデータをエクスポートした場合は、これらのクエリを実行すると、スキーマを変更することを確認してください。  
  
### <a name="what-tables-and-columns-are-in-these-databases"></a>どのようなテーブルと列は、これらのデータベースではでしょうか。  
次のクエリでは、列、テーブル、およびデータベースのメタデータが含まれているテーブルを結合し、すべてのデータベース、テーブル、および列名で並べ替えられた列の名前を返します。  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D.DatabaseId  
ORDER BY ColumnName;  
```  
  
### <a name="what-are-the-largest-databases"></a>最大級のデータベースとは  
次のクエリは、ファイルのサイズに基づいて並べ替えられて、各 Access データベースにデータベース名、ファイルのサイズ、およびテーブルの数を返します。  
  
```  
SELECT DatabaseName, FileSize, TablesCount  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileSize DESC;  
```  
  
### <a name="who-is-the-owner-of-most-of-the-databases"></a>ほとんどのデータベースの所有者は誰ですか。  
次のクエリでは、所有者に並べ替えて、各アクセス データベースの所有者とデータベースの名前を返します。  
  
```  
SELECT DatabaseName, FileOwner  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileOwner;  
```  
  
### <a name="which-databases-contain-the-same-tables"></a>のどのデータベースでは、同じテーブルを含めるか。  
次のクエリでは、サブクエリを使用して、テーブルの一覧で 1 回以上表示されるすべてのテーブル名を検索しますし、このテーブルの一覧を使用して、データベース名を取得します。 結果は、データベース名とし、テーブル名としてが返され、テーブル名で並べ替えられます。  
  
```  
SELECT DatabaseName, TableName   
FROM dbo.SSMA_Access_InventoryTables T  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON D.DatabaseId = T.DatabaseId  
WHERE TableName IN (  
SELECT TableName   
FROM dbo.SSMA_Access_InventoryTables  
GROUP BY TableName   
HAVING count(*)>1  
)  
ORDER BY TableName;  
```  
  
### <a name="which-databases-were-not-modified-in-the-last-six-months"></a>過去 6 か月間には、データベースは変更されていないか。  
次のクエリは、現在の日付を取得、6 か月前に、月の値を取得し、し、6 か月前よりも大きい値の変更された日付を含むデータベースの一覧を返します。  
  
```  
SELECT DatabaseName, DateModified  
FROM dbo.SSMA_Access_InventoryDatabases  
WHERE DATEDIFF(month, DateModified, GETDATE()) > 6  
ORDER BY DateModified;  
```  
  
### <a name="which-databases-contain-private-information"></a>どのデータベースには、個人情報が含まれてでしょうか。  
Access データベースには、機密情報や個人情報が含まれます。 これらのデータベースを移動する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のセキュリティ機能を活用するためにします。 機密データを含む列は、特定の名前、または、特定の文字を含めることがわかっている場合は、その情報が含まれているすべての列を検索するクエリを使用できます。 たとえば、「給与」、文字列が含まれるすべての列を見つけることができます。  クエリは、データベース名、テーブル名、および列名を返します。  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D. DatabaseId  
WHERE ColumnName LIKE '%salary%';  
```  
列名がわからない場合は、すべての列を返すクエリを記述できます。 これを行うには、前のクエリから WHERE 句を削除します。  
  
## <a name="see-also"></a>参照  
[Access データベースの移行の準備](preparing-access-databases-for-migration-accesstosql.md)  
  
