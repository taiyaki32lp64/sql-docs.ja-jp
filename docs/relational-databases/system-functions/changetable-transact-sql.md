---
title: CHANGETABLE (TRANSACT-SQL) |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CHANGETABLE_TSQL
- CHANGETABLE
dev_langs:
- TSQL
helpviewer_keywords:
- CHANGETABLE
- change tracking [SQL Server], CHANGETABLE
ms.assetid: d405fb8d-3b02-4327-8d45-f643df7f501a
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 11295f953e2f3e4e237838dfdb158fd01c9fa645
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68042902"
---
# <a name="changetable-transact-sql"></a>CHANGETABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  テーブルに対する変更の追跡情報を返します。このステートメントを使用すると、テーブルに対するすべての変更または特定の行に関する変更の追跡情報を取得できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql
CHANGETABLE (  
    { CHANGES table , last_sync_version  
    | VERSION table , <primary_key_values> } )  
[AS] table_alias [ ( column_alias [ ,...n ] )  
  
<primary_key_values> ::=  
( column_name [ , ...n ] ) , ( value [ , ...n ] )  
```  
  
## <a name="arguments"></a>引数  
 変更*テーブル*、 *last_sync_version*  
 指定したバージョン以降に発生したすべての変更についての情報をテーブルに追跡を返します*last_sync_version*します。  
  
 *テーブル*  
 変更箇所を取得するユーザー定義テーブルを指定します。 テーブルで変更の追跡が有効になっている必要があります。 1 つ、2 つ、3 つ、または 4 つの部分で構成されるテーブル名を使用できます。 テーブルのシノニムを使用することもできます。  
  
 *last_sync_version*  
 変更を取得する際に、呼び出し元アプリケーションによって、変更が必要な時点を指定する必要があります。 last_sync_version は、その時点を指定します。 この関数により、そのバージョン以降に変更されたすべての行に関する情報が返されます。 アプリケーションは、last_sync_version よりも大きいバージョンの変更を受信するようにクエリを実行します。  
  
 通常、変更を取得する前に、アプリケーションが呼び出す**CHANGE_TRACKING_CURRENT_VERSION()** 使用されるバージョンを取得する次の時刻の変更が必要です。 したがって、アプリケーションで実際の値を解釈または理解する必要はありません。  
  
 last_sync_version は呼び出し元アプリケーションによって取得されるため、アプリケーションで値を保存する必要があります。 アプリケーションでこの値が失われた場合は、データを再初期化する必要があります。  
  
 *last_sync_version*は**bigint**します。 スカラー値を指定する必要があります。 式を指定すると構文エラーが発生します。  
  
 NULL を指定すると、すべての変更箇所が返されます。  
  
 *last_sync_version*いることを確認しない古すぎるため、データベース用に構成された保有期間に従って、変更情報の一部またはすべてがクリーンアップされている可能性がありますを検証する必要があります。 詳細については、次を参照してください。 [CHANGE_TRACKING_MIN_VALID_VERSION &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)と[ALTER DATABASE SET Options &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)します。  
  
 VERSION *table*, { <primary_key_values> }  
 指定した行に関する最新の変更追跡情報を返します。 行は主キー値によって識別される必要があります。 <主キー値> で主キー列を識別し、値を指定します。 主キー列の名前は任意の順序で指定できます。  
  
 *Table*  
 変更追跡情報を取得するユーザー定義テーブルを指定します。 テーブルで変更の追跡が有効になっている必要があります。 1 つ、2 つ、3 つ、または 4 つの部分で構成されるテーブル名を使用できます。 テーブルのシノニムを使用することもできます。  
  
 *column_name*  
 主キー列の名前を指定します。 複数の列名を任意の順序で指定できます。  
  
 *[値]*  
 主キーの値を指定します。 同じ順序で値を指定する必要があります複数の主キー列がある場合、列の表示と、 *column_name*一覧。  
  
 [AS]*table_alias* [(*column_alias* [,...*n* ])]  
 CHANGETABLE によって返される結果の名前を指定します。  
  
 *table_alias*  
 CHANGETABLE によって返されるテーブルの別名を指定します。 *table_alias*は必須であり、有効なである必要があります[識別子](../../relational-databases/databases/database-identifiers.md)します。  
  
 *column_alias*  
 CHANGETABLE によって返される列の別名を指定します (省略可能)。 これにより、重複する名前が結果に含まれていた場合に列名をカスタマイズできるようになります。  
  
## <a name="return-types"></a>戻り値の型  
 **テーブル**  
  
## <a name="return-values"></a>戻り値  
  
### <a name="changetable-changes"></a>CHANGETABLE CHANGES  
 CHANGES を指定すると、次の列を含む 0 以上の行が返されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|SYS_CHANGE_VERSION|**bigint**|行の最後の変更に関連付けられているバージョンの値です。|  
|SYS_CHANGE_CREATION_VERSION|**bigint**|最後の挿入操作に関連付けられているバージョンの値です。|  
|SYS_CHANGE_OPERATION|**nchar(1)**|変更の種類を示します。<br /><br /> **U** = Update<br /><br /> **I** = 挿入<br /><br /> **D** = Delete|  
|SYS_CHANGE_COLUMNS|**varbinary(4100)**|last_sync_version (ベースライン) 以降に変更された列の一覧です。 計算列が変更済みとしてを決して表示されることに注意してください。<br /><br /> 以下の場合は値が NULL になります。<br /><br /> 列の変更の追跡が有効になっていない場合。<br /><br /> 操作が挿入操作または削除操作の場合。<br /><br /> すべての非主キー列が 1 回の操作で更新された場合。 このバイナリ値を直接解釈しないでください。 代わりに、その解釈は、次のように使用します。 [CHANGE_TRACKING_IS_COLUMN_IN_MASK()](../../relational-databases/system-functions/change-tracking-is-column-in-mask-transact-sql.md)します。|  
|SYS_CHANGE_CONTEXT|**varbinary (128)**|変更のコンテキスト情報を使用して必要に応じて指定できる、 [WITH](../../relational-databases/system-functions/with-change-tracking-context-transact-sql.md) INSERT、UPDATE、または DELETE ステートメントの一部としての句。|  
|\<主キー列の値 >|ユーザー テーブルの列と同じ|追跡対象テーブルの主キーの値です。 これらの値により、ユーザー テーブルの各行が一意に識別されます。|  
  
### <a name="changetable-version"></a>CHANGETABLE VERSION  
 VERSION を指定すると、次の列を含む 1 つの行が返されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|SYS_CHANGE_VERSION|**bigint**|行に関連付けられている現在の変更バージョンの値です。<br /><br /> 変更追跡情報の保有期間より長い期間にわたって変更が行われていない場合や、変更の追跡を有効にしてからまだ行が変更されていない場合は、値が NULL になります。|  
|SYS_CHANGE_CONTEXT|**varbinary (128)**|INSERT、UPDATE、DELETE の各ステートメントの一部として WITH 句を使用することによってオプションで指定できる変更のコンテキスト情報です。|  
|\<主キー列の値 >|ユーザー テーブルの列と同じ|追跡対象テーブルの主キーの値です。 これらの値により、ユーザー テーブルの各行が一意に識別されます。|  
  
## <a name="remarks"></a>コメント  
 CHANGETABLE 関数は、クエリの FROM 句の中でテーブルとして使用されるのが一般的です。  
  
## <a name="changetablechanges"></a>CHANGETABLE(CHANGES...)  
 新しい行や変更された行の行データを取得するには、主キー列を使用して結果セットをユーザー テーブルに結合します。 以降の同じ行に複数の変更があった場合でも、変更されたユーザー テーブルの各行の 1 行のみが返されます、 *last_sync_version*値。  
  
 主キー列の変更は更新としてマークされません。 主キーの値が変更された場合は、古い値が削除されて新しい値が挿入されたと見なされます。  
  
 行を削除した後、その古い主キーを持つ行を挿入した場合、その変更は、行のすべての列に対する更新と見なされます。  
  
 SYS_CHANGE_OPERATION と SYS_CHANGE_COLUMNS 列に対して返される値は、指定したベースライン (last_sync_version) を基準とは。 たとえば、バージョン 10 とバージョン 15 で更新操作、挿入操作が行われた場合、ベースライン*last_sync_version*が 12 の場合、更新プログラムが報告されます。 場合、 *last_sync_version*値が 8 の挿入が報告されます場合、。 SYS_CHANGE_COLUMNS では、計算列は更新された列として報告されません。  
  
 一般に、ユーザー テーブルに対するデータの挿入、更新、または削除の操作は、MERGE ステートメントも含め、すべて追跡されます。  
  
 ユーザー テーブルのデータに影響する操作のうち、追跡されない操作は次のとおりです。  
  
-   UPDATETEXT ステートメントの実行  
  
     このステートメントは将来のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では削除される予定であり、非推奨とされます。 ただし、UPDATE ステートメントの .WRITE 句によって加えられた変更は追跡されます。  
  
-   TRUNCATE TABLE の使用による行の削除  
  
     テーブルが切り捨てられると、テーブルに関連付けられている変更追跡バージョン情報はリセットされ、変更の追跡を有効にした直後と同じ状態になります。 クライアント アプリケーションは必ず最終同期バージョンを検証する必要があります。 テーブルが切り捨てられていると、検証が失敗します。  
  
## <a name="changetableversion"></a>CHANGETABLE(VERSION...)  
 存在しない主キーが指定された場合は、空の結果セットが返されます。  
  
 保有期間より長い期間にわたって変更が行われていない場合 (クリーンアップによって変更情報が削除されている場合など) や、テーブルに対して変更の追跡を有効にしてからまだ行が変更されていない場合、SYS_CHANGE_VERSION の値は NULL になります。  
  
## <a name="permissions"></a>アクセス許可  
 指定されているテーブルで次のアクセス許可が必要です、*テーブル*変更追跡情報を取得する値。  
  
-   主キー列に対する SELECT 権限  
  
-   VIEW CHANGE TRACKING  
  
## <a name="examples"></a>使用例  
  
### <a name="a-returning-rows-for-an-initial-synchronization-of-data"></a>A. データの初期同期のための行を返す  
 次の例は、テーブル データを初期同期するためにデータを取得する方法を示しています。 このクエリは、すべての行データと、それらに関連付けられているバージョンを返します。 返されたデータをシステムに挿入または追加すると、同期されたデータがシステムに含まれるようになります。  
  
```sql  
-- Get all current rows with associated version  
SELECT e.[Emp ID], e.SSN, e.FirstName, e.LastName,  
    c.SYS_CHANGE_VERSION, c.SYS_CHANGE_CONTEXT  
FROM Employees AS e  
CROSS APPLY CHANGETABLE   
    (VERSION Employees, ([Emp ID], SSN), (e.[Emp ID], e.SSN)) AS c;  
```  
  
### <a name="b-listing-all-changes-that-were-made-since-a-specific-version"></a>B. 特定のバージョン以降に行われたすべての変更を一覧表示する  
 次の例では、指定したバージョン (`@last_sync_version)` 以降にテーブルで行われたすべての変更を一覧表示します。 [Emp ID] および SSN は複合主キーの列です。  
  
```sql  
DECLARE @last_sync_version bigint;  
SET @last_sync_version = <value obtained from query>;  
SELECT [Emp ID], SSN,  
    SYS_CHANGE_VERSION, SYS_CHANGE_OPERATION,  
    SYS_CHANGE_COLUMNS, SYS_CHANGE_CONTEXT   
FROM CHANGETABLE (CHANGES Employees, @last_sync_version) AS C;  
```  
  
### <a name="c-obtaining-all-changed-data-for-a-synchronization"></a>C. 変更されたすべてのデータを同期のために取得する  
 次の例は、変更されたデータをすべて取得する方法を示しています。 このクエリでは、変更追跡情報をユーザー テーブルと結合して、ユーザー テーブルの情報が返されるようにしています。 A`LEFT OUTER JOIN`削除された行の行が返されるようにに使用されます。  
  
```sql  
-- Get all changes (inserts, updates, deletes)  
DECLARE @last_sync_version bigint;  
SET @last_sync_version = <value obtained from query>;  
SELECT e.FirstName, e.LastName, c.[Emp ID], c.SSN,  
    c.SYS_CHANGE_VERSION, c.SYS_CHANGE_OPERATION,  
    c.SYS_CHANGE_COLUMNS, c.SYS_CHANGE_CONTEXT   
FROM CHANGETABLE (CHANGES Employees, @last_sync_version) AS c  
    LEFT OUTER JOIN Employees AS e  
        ON e.[Emp ID] = c.[Emp ID] AND e.SSN = c.SSN;  
```  
  
### <a name="d-detecting-conflicts-by-using-changetableversion"></a>D. CHANGETABLE(VERSION...) を使用して競合を検出する  
 次の例は、前回の同期以降に変更されていない場合にのみ行を更新する方法を示しています。 `CHANGETABLE` を使用して、特定の行のバージョン番号を取得しています。 行が更新されていた場合は変更は行われず、その行に対する最新の変更に関する情報が返されます。  
  
```sql  
-- @last_sync_version must be set to a valid value  
UPDATE  
    SalesLT.Product  
SET  
    ListPrice = @new_listprice  
FROM  
    SalesLT.Product AS P  
WHERE  
    ProductID = @product_id AND  
    @last_sync_version >= ISNULL (  
        (SELECT CT.SYS_CHANGE_VERSION FROM   
            CHANGETABLE(VERSION SalesLT.Product,  
            (ProductID), (P.ProductID)) AS CT),  
        0);  
```  
  
## <a name="see-also"></a>参照  
 [変更追跡関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [データ変更の追跡 &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [CHANGE_TRACKING_IS_COLUMN_IN_MASK &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/change-tracking-is-column-in-mask-transact-sql.md)   
 [CHANGE_TRACKING_CURRENT_VERSION &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-current-version-transact-sql.md)   
 [CHANGE_TRACKING_MIN_VALID_VERSION &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)  
  
  
