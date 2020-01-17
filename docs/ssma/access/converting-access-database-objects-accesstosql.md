---
title: Access データベース オブジェクト (AccessToSQL) に変換する |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- Access databases, converting schemas
- conversion
- conversion, converting schemas
- indexes, altering
- metadata
- metadata, altering
- metadata, converting
- migrating databases, one-click
- one-click migration
- schemas
- schemas, converting
- SQL
- SQL, converting
- syntax
- syntax, converting
- tables, altering
- translating Access to SQL Azure
- translating Access to SQL Server
ms.assetid: e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 56c55dbc5df61bfdb9013e505335af16fccbeecd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006630"
---
# <a name="converting-access-database-objects-accesstosql"></a>Access データベース オブジェクト (AccessToSQL) に変換します。
Access データベースを追加してに接続した後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure、SSMA は、アクセスのメタデータを表示し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure データベースのオブジェクト。 これで Access データベースのオブジェクトを選択してへのスキーマを変換し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のスキーマ。  
  
## <a name="the-conversion-process"></a>変換プロセス  
データベース オブジェクトの変換ではアクセス メタデータからオブジェクト定義が相当に変換する[!INCLUDE[tsql](../../includes/tsql-md.md)]構文、し、プロジェクトにこの情報を読み込みます。 表示することができますし、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のオブジェクトとそのプロパティを使用して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure メタデータ エクスプ ローラー。  
  
> [!IMPORTANT]  
> オブジェクトの変換でオブジェクトを作成しません[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。 のみ、オブジェクトの定義を変換し、SSMA プロジェクトで情報を格納します。  
  
変換中は、SSMA は状態を出力ウィンドウ、およびエラー、警告、およびエラー一覧ペインに情報メッセージを出力します。 この情報を使用して、Access データベースまたは必要な変換の結果を得るため、変換プロセスを変更する必要があるかどうか判断します。 内の情報を使用することもできます、 [Access データベースを移行の準備](preparing-access-databases-for-migration-accesstosql.md)トピックを確認し、変換されません。  
  
## <a name="setting-conversion-options"></a>変換オプションの設定  
オブジェクトを変換する前に、プロジェクトの変換オプションを確認して、**プロジェクト設定** ダイアログ ボックス。 このダイアログ ボックスを使用すると、SSMA がインデックス付きのメモ列、主キー、外部キー制約、タイムスタンプ、およびインデックスなしテーブルに変換する方法を設定できます。 詳細については、次を参照してください[プロジェクトの設定 (変換)。](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
## <a name="conversion-results"></a>変換結果  
次の表は、変換されますが、オブジェクトのアクセスと、その結果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure オブジェクト。  
  
|オブジェクトにアクセス|SQL Server オブジェクトの結果として得られる|  
|-----------------|-------------------------------|  
|テーブル|テーブル|  
|column|column|  
|インデックス|インデックス|  
|外部キー (foreign key)|外部キー (foreign key)|  
|クエリ (query)|ビュー<br /><br />ほとんどの SELECT クエリは、ビューに変換されます。 更新クエリなどの他のクエリは移行されません。<br /><br />SELECT クエリ パラメーターを受け取るは変換されません、およびクロス集計クエリ。|  
|レポート|変換されませんでした。|  
|フォーム|変換されませんでした。|  
|マクロ|変換されませんでした。|  
|モジュール|変換されませんでした。|  
|既定値|既定値|  
|0 個の長列のプロパティを許可します。|check 制約|  
|列の検証規則|check 制約|  
|テーブルの検証規則|check 制約|  
|主キー (primary key)|主キー (primary key)|  
  
## <a name="converting-access-objects"></a>オブジェクトへのアクセスを変換します。  
Access データベース オブジェクトを変換するには、最初に変換し、SSMA を変換するオブジェクトを選択する必要があります。 変換中に出力メッセージを表示する、**ビュー**メニューの **出力**します。  
  
**選択し、Access データベース オブジェクトを SQL Server または SQL Azure の構文に変換します。**  
  
1.  メタデータ エクスプ ローラーでのアクセス、**アクセス メタベース**、順に展開**データベース**します。  
  
2.  次の 1 つ以上の操作を行います。  
  
    -   すべてのデータベースを変換する場合は、横にチェック ボックスを選択します**データベース**します。  
  
    -   変換または個々 のデータベースの省略は、選択するか、データベース名の横にあるチェック ボックスをオフにします。  
  
    -   変換またはクエリの省略は、データベース、展開しし、オンまたはオフ、**クエリ**チェック ボックスをオンします。  
  
    -   変換または個々 のテーブルの省略は、データベースを展開し、**テーブル**、選択するか、テーブルの横にあるチェック ボックスをオフにします。  
  
3.  次のいずれかの操作を行います。  
  
    -   スキーマを変換するを右クリックして**データベース**選択**スキーマの変換**します。  
  
        個々 のオブジェクトを変換することもできます。 オブジェクトの選択に関係なく、オブジェクトに変換するには、オブジェクトを右クリックして**スキーマの変換**します。  
  
        オブジェクトが変換されると、アクセス メタデータ エクスプ ローラーで太字表示されます。  
  
    -   変換、読み込み、およびスキーマと 1 つの手順でデータを移行、データベースと選択を右クリックして**変換、読み込み、および移行**します。  
  
4.  メッセージを確認して、**出力**ウィンドウおよびエラーと警告で、**エラー一覧**ウィンドウ。  
  
## <a name="altering-tables-and-indexes"></a>テーブルとパーティション インデックスの変更  
メタデータにアクセスを変換した後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]や SQL Azure メタデータを使ってオブジェクトを読み込む前に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または変更できる SQL Azure、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure テーブルとパーティション インデックス。  
  
**テーブルまたはインデックスのプロパティを変更するには**  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure メタデータ エクスプ ローラーで、テーブルまたはインデックスを変更するを選択します。  
  
2.  **テーブル** タブで、変更をし、入力するか、新しい設定を選択するプロパティをクリックします。 たとえば、nvarchar (20)、nvarchar (15) に変更したり、テーブル列を null 許容にする チェック ボックスをオンにできます。  
  
    変更されたプロパティのセルから、カーソルを移動します。 別の行をクリックするか、Tab キーを押すと、これを行うことができます。  
  
3.  **[適用]** をクリックします。  
  
コードの変更を表示できるようになりました、 **SQL**タブ。  
  
## <a name="next-step"></a>次の手順  
移行プロセスでは、次の手順は[SQL Server に変換されたデータベース オブジェクトを読み込む](loading-converted-database-objects-into-sql-server-accesstosql.md)  
  
## <a name="see-also"></a>関連項目  
[SQL Server へのアクセス データベースの移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
