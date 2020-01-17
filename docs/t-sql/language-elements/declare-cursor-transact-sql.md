---
title: DECLARE CURSOR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DECLARE_CURSOR_TSQL
- CURSOR_TSQL
- DECLARE CURSOR
- CURSOR
dev_langs:
- TSQL
helpviewer_keywords:
- DECLARE CURSOR statement
- cursors [SQL Server], attributes
- local cursors [SQL Server]
- nesting cursors
- Transact-SQL cursors, attributes
- global cursors [SQL Server]
ms.assetid: 5a3a27aa-03e8-4c98-a27e-809282379b21
author: rothja
ms.author: jroth
ms.openlocfilehash: f0c5a07b7ff618b3857d9e67b11d50a5a29e8248
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67894787"
---
# <a name="declare-cursor-transact-sql"></a>DECLARE CURSOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] サーバー カーソルの属性を定義します。これには、スクロール動作や、カーソルが操作する結果セットを作成するクエリなどが含まれます。 `DECLARE CURSOR` は、ISO 標準に基づく構文と、[!INCLUDE[tsql](../../includes/tsql-md.md)] の拡張機能のセットを使用する構文の両方で指定できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
ISO Syntax  
DECLARE cursor_name [ INSENSITIVE ] [ SCROLL ] CURSOR   
     FOR select_statement   
     [ FOR { READ ONLY | UPDATE [ OF column_name [ ,...n ] ] } ]  
[;]  
Transact-SQL Extended Syntax  
DECLARE cursor_name CURSOR [ LOCAL | GLOBAL ]   
     [ FORWARD_ONLY | SCROLL ]   
     [ STATIC | KEYSET | DYNAMIC | FAST_FORWARD ]   
     [ READ_ONLY | SCROLL_LOCKS | OPTIMISTIC ]   
     [ TYPE_WARNING ]   
     FOR select_statement   
     [ FOR UPDATE [ OF column_name [ ,...n ] ] ]  
[;]  
```  
  
## <a name="arguments"></a>引数  
 *cursor_name*  
 定義された [!INCLUDE[tsql](../../includes/tsql-md.md)] サーバー カーソルの名前です。 *cursor_name* は識別子の規則に準拠している必要があります。  
  
 INSENSITIVE  
 データの一時コピーを作成するためのカーソルを定義します。作成されるコピーは、カーソルで使用されます。 このカーソルに対する要求の応答は、すべて **tempdb** 内のこの一時テーブルから得られます。したがって、ベース テーブルへの修正は、このカーソルで取り出したデータには反映されません。また、このカーソルで修正を行うこともできません。 ISO 構文で `INSENSITIVE` を指定しない場合は、任意のユーザーによって基になるテーブルに加えられた削除および更新がコミットされると、以降のフェッチで反映されます。  
  
 SCROLL  
 すべてのフェッチ オプション (`FIRST`、`LAST`、`PRIOR`、`NEXT`、`RELATIVE`、`ABSOLUTE`) を使用可能に指定します。 ISO 形式の `DECLARE CURSOR` ステートメントに `SCROLL` を指定しない場合、`NEXT` は、サポートされている唯一のフェッチ オプションです。 `FAST_FORWARD` も指定されている場合は、`SCROLL` を指定できません。 `SCROLL` が指定されていない場合は、フェッチ オプション `NEXT` だけが使用でき、カーソルは `FORWARD_ONLY` になります。
  
 *select_statement*  
 カーソルの結果セットを定義する標準の `SELECT` ステートメントです。 カーソル宣言の *select_statement* 内で `FOR BROWSE` および `INTO` キーワードは許可されません。  
  
 *select_statement* 内の句が、要求されたカーソルの種類の機能と矛盾する場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってカーソルが別の種類に暗黙的に変換されます。  
  
 READ ONLY  
 このカーソルによる更新を禁止します。 `UPDATE` または `DELETE` ステートメントの `WHERE CURRENT OF` 句では、このカーソルを参照できません。 このオプションは、更新対象のカーソルの既定の機能をオーバーライドします。  
  
 UPDATE [OF *column_name* [ **,** ...*n*]]  
 カーソル内で更新できる列を定義します。 OF <column_name> [, <... n>] を指定した場合は、指定した列に対してのみ更新ができます。 列リストなしで `UPDATE` を指定した場合は、すべての列を更新できます。  
  
*cursor_name*  
定義された [!INCLUDE[tsql](../../includes/tsql-md.md)] サーバー カーソルの名前です。 *cursor_name* は識別子の規則に準拠している必要があります。  
  
LOCAL  
カーソルのスコープは、カーソルが作成されたバッチ、ストアド プロシージャ、またはトリガーに対してローカルです。 カーソル名は、そのスコープの中でだけ有効です。 カーソルは、バッチ、ストアド プロシージャ、またはトリガー内のローカル カーソル変数から、またはストアド プロシージャの `OUTPUT` パラメーターから参照できます。 `OUTPUT` パラメーターは、呼び出し側のバッチ、ストアド プロシージャ、トリガーにローカル カーソルを戻すのに使用されます。呼び出し側はパラメーターをカーソル変数に割り当て、ストアド プロシージャが終了した後でカーソルを参照できます。 カーソルは、`OUTPUT` パラメーターで戻された場合を除いて、バッチ、ストアド プロシージャ、またはトリガーが終了するときに暗黙的に割り当てを解除されます。 `OUTPUT` パラメーターで戻された場合は、カーソルを参照している最後の変数の割り当てが解除されるか、そのスコープが失われたときに、カーソルの割り当てが解除されます。  
  
GLOBAL  
カーソルのスコープは、接続に対してグローバルです。 カーソル名は、その接続によって実行されるストアド プロシージャやバッチの中で参照できます。 カーソルは、切断のときだけ暗黙的に割り当てを解除されます。  
  
> [!NOTE]  
>  `GLOBAL` も `LOCAL` も指定しない場合は、**default to local cursor** データベース オプションの設定によって既定の動作が決まります。  
  
FORWARD_ONLY  
カーソルは前方にだけ移動でき、先頭行から最終行までスクロールできることを指定します。 `FETCH NEXT` は、サポートされている唯一のフェッチ オプションです。 現在のユーザーが行い (または別のユーザーがコミットし)、結果セット内の行に影響を与えたすべての挿入、更新、削除ステートメントは、行がフェッチされると認識できるようになります。 ただし、カーソルは後方にスクロールできないので、データベース内の行のフェッチ後にその行に対して行われた変更内容は、カーソル内で確認できません。 順方向専用カーソルは既定では動的であり、現在の行が処理されるとすべての変更が検出されることを意味します。 これにより、カーソルを開く時間が短縮され、基になるテーブルに対して行われた更新を結果セットで表示できるようになります。 順方向専用カーソルでは後方スクロールはサポートされていませんが、アプリケーションでカーソルを閉じて開きなおすことにより、結果セットの先頭にカーソルを戻すことができます。 `STATIC`、`KEYSET`、または `DYNAMIC` キーワードなしで `FORWARD_ONLY` を指定した場合、カーソルは動的カーソルとして動作します。 `FORWARD_ONLY` と `SCROLL` のどちらも指定しない場合、既定値は `FORWARD_ONLY` になります。ただし、キーワードに `STATIC`、`KEYSET`、または `DYNAMIC` が指定されている場合を除きます。 `STATIC`、`KEYSET`、および `DYNAMIC` の各カーソルは既定で `SCROLL` になります。 ODBC と ADO のなどのデータベース API と異なり、`FORWARD_ONLY` は、`STATIC`、`KEYSET`、および `DYNAMIC`[!INCLUDE[tsql](../../includes/tsql-md.md)] の各カーソルと共にサポートされます。  
   
 STATIC  
カーソルが最初に開かれた時点での結果セットを常に表示し、カーソルによって使用されるデータの一時的なコピーを作成することを指定します。 カーソルに対するすべての要求は、**tempdb** 内のこの一時テーブルから応答されます。 したがって、ベース テーブルに対して行われた挿入、更新、削除は、このカーソルに対して行われたフェッチによって返されるデータには反映されず、カーソルが開かれた後で結果セットのメンバーシップ、順序、値に対して行われた変更は、このカーソルでは検出されません。 静的カーソルは、それ自体の更新、削除、挿入を検出してもかまいませんが、必ず行う必要はありません。 たとえば、静的カーソルが行をフェッチした後で、別のアプリケーションによってその行が更新されるものとします。 アプリケーションで静的カーソルから行を再フェッチした場合、他のアプリケーションによって変更が行われたにも関わらず、認識される値は変更されていません。 すべての種類のスクロールがサポートされています。 
  
KEYSET  
カーソルを開くときに、カーソル内の行の構成要素と順序が固定されることを指定します。 行を一意に識別するキーのセットは、**tempdb** 内の **keyset** というテーブルに組み込まれています。 このカーソルでは、変更を検出する機能において、静的カーソルと動的カーソルの中間の機能が提供されます。 静的カーソルと同様に、結果セットのメンバーシップと順序に対する変更は常に検出されません。 動的カーソルと同様に、結果セット内の行の値に対する変更は検出されます。 キーセット ドリブン カーソルは、キーセットという一意の識別子 (キー) のセットにより制御されます。 これらのキーは、結果セットの行を一意に識別する列のセットから構築されます。 キーセットは、クエリ ステートメントによって返されるすべての行からのキー値のセットです。 キーセット ドリブン カーソルでは、カーソルの行ごとにキーが作成されて保存され、クライアント ワークステーションまたはサーバーに格納されます。 各行にアクセスすると、格納されているキーを使用して、データ ソースから現在のデータ値がフェッチされます。 キーセット ドリブン カーソルでは、キーセットが完全に作成された時点で、結果セットのメンバーシップは凍結されます。 したがって、メンバーシップに影響を与える追加または更新は、開き直されるまで結果セットには反映されません。 (キーセットの所有者または他のプロセスによって行われた) データ値に対する変更は、ユーザーが結果セットをスクロールすると表示されます。
-  行が削除された場合は、削除された行は結果セット内のギャップとして認識されるので、行のフェッチを試みると -2 の `@@FETCH_STATUS` が返されます。 行に対するキーはキーセット内に存在しますが、結果セットには行は存在しなくなっています。 
-  (他のプロセスによって) カーソルの外部で行われた挿入は、カーソルを閉じて再度開いた場合にのみ表示されます。 カーソルの内部から行われた挿入は、結果セットの末尾に表示されます。
-  カーソル外部からキー値を更新すると、古い行を削除した後で新しい行を挿入した場合と同様に、 新しい値の行は表示されず、古い値の行をフェッチしようとすると `@@FETCH_STATUS` が -2 に設定されて返されます。 新しい値は、`WHERE CURRENT OF` 句を指定してカーソルから更新が行われた場合に表示されます。 

> [!NOTE]  
> クエリが一意なインデックスのないテーブルを少なくとも 1 つ参照する場合、このキーセット カーソルは静的カーソルに変換されます。  
  
DYNAMIC  
変更がカーソル内またはカーソル外の他のユーザーのどちらによって行われたのかに関係なく、カーソルをスクロールして新しいレコードをフェッチすると、結果内の行に対して行われたすべてのデータ変更が反映されるカーソルを定義します。 したがって、すべてのユーザーによって行われたすべての挿入、更新、削除ステートメントが、カーソルによって表示されます。 行のデータ値、順序、メンバーシップは、各フェッチ操作で変化する可能性があります。 `ABSOLUTE` フェッチ オプションは、動的カーソルではサポートされません。 カーソルの外部から行った更新は、(カーソルのトランザクション分離レベルが `UNCOMMITTED` に設定されている場合を除き) コミットされるまで表示されません。 たとえば、動的カーソルで 2 つの行がフェッチされた後、別のアプリケーションによって一方の行は更新され、他の行は削除されたものとします。 その後、動的カーソルでこれらの行がフェッチされた場合、削除された行は検出されませんが、更新された行は新しい値が表示されます。 
  
FAST_FORWARD  
パフォーマンスの最適化が有効に設定された `FORWARD_ONLY`、`READ_ONLY` カーソルを指定します。 `SCROLL` または `FOR_UPDATE` も指定されている場合、`FAST_FORWARD` は指定できません。 この種類のカーソルでは、カーソル内からのデータ変更は許可されません。  
  
> [!NOTE]  
> `FAST_FORWARD` と `FORWARD_ONLY` の両方を同じ `DECLARE CURSOR` ステートメントで使用できます。  
  
READ_ONLY  
このカーソルによる更新を禁止します。 `UPDATE` または `DELETE` ステートメントの `WHERE CURRENT OF` 句では、このカーソルを参照できません。 このオプションは、更新対象のカーソルの既定の機能をオーバーライドします。  
  
SCROLL_LOCKS  
カーソルによって行われる位置指定更新または位置指定削除の成功が保証されることを指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はカーソルに読み取られた行をロックし、後で変更できることを保証します。 `FAST_FORWARD` または `STATIC` も指定されている場合、`SCROLL_LOCKS` は指定できません。  
  
OPTIMISTIC  
行がカーソルに読み取られてから更新された場合に、カーソルによって行われる位置指定更新または位置指定削除が失敗することを指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、行がカーソルに読み取られるとき、その行はロックされません。 代わりに **timestamp** 列の値を比較するか、テーブルに **timestamp** 列がない場合はチェックサム値を使用して、行がカーソルに読み込まれてから変更されたかどうかが判別されます。 行が変更されている場合、位置指定更新または位置指定削除の試行は失敗します。 `FAST_FORWARD` も指定されている場合は、`OPTIMISTIC` を指定できません。  
  
 TYPE_WARNING  
 カーソルの種類が、要求されたものから別のものに暗黙的に変換された場合、クライアントに警告メッセージが送信されることを指定します。  
  
 *select_statement*  
 カーソルの結果セットを定義する標準の SELECT ステートメントです。 カーソル宣言の *select_statement* 内で `COMPUTE`、`COMPUTE BY`、`FOR BROWSE` および `INTO` キーワードは許可されません。  
  
> [!NOTE]  
> カーソル宣言内ではクエリ ヒントを使用できますが、`FOR UPDATE OF` 句も使用する場合は、`FOR UPDATE OF` の後に `OPTION (<query_hint>)` を指定する必要があります。  
  
*select_statement* 内の句が、要求されたカーソルの種類の機能と矛盾する場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってカーソルが別の種類に暗黙的に変換されます。 詳細については、「暗黙的なカーソル変換」を参照してください。  
  
FOR UPDATE [OF *column_name* [ **,** ...*n*]]  
カーソル内で更新できる列を定義します。 `OF <column_name> [, <... n>]` を指定した場合は、指定した列に対してのみ更新できます。 列リストなしで `UPDATE` を指定した場合は、すべての列を更新できます。ただし、`READ_ONLY` コンカレンシー オプションを指定した場合を除きます。  
  
## <a name="remarks"></a>Remarks  
`DECLARE CURSOR` は、[!INCLUDE[tsql](../../includes/tsql-md.md)] サーバー カーソルの属性を定義します。これには、スクロール動作や、カーソルが操作する結果セットを作成するクエリなどが含まれます。 `OPEN` ステートメントは結果セットを設定し、`FETCH` ステートメントは結果セットから行を返します。 `CLOSE` ステートメントは、カーソルに関係付けられた現在の結果セットを解放します。 `DEALLOCATE` ステートメントは、カーソルが使用するリソースを解放します。  
  
最初の形式の `DECLARE CURSOR` ステートメントは、ISO 構文を使用してカーソルの動作を宣言します。 2 番目の形式の `DECLARE CURSOR` は、[!INCLUDE[tsql](../../includes/tsql-md.md)] の拡張機能を使用します。これによって、ODBC または ADO のデータベース API カーソル関数で使用されるカーソルの種類と同じカーソルの種類を使用して、カーソルを定義できます。  
  
2 つの形式を混在することはできません。 `CURSOR` キーワードの前に `SCROLL` または `INSENSITIVE` キーワードを指定した場合、`CURSOR` キーワードと `FOR <select_statement>` キーワードの間にはキーワードを一切使用できません。 `CURSOR` と `FOR <select_statement>` の各キーワードの間にキーワードを指定した場合、`CURSOR` キーワードの前に `SCROLL` または `INSENSITIVE` を指定できません。  
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] 構文を使用した `DECLARE CURSOR` で `READ_ONLY`、`OPTIMISTIC`、または `SCROLL_LOCKS` を指定していない場合、既定値は次のようになります。  
  
-   権限が十分でなかったり、更新をサポートしないリモート テーブルにアクセスしているなどの理由で、`SELECT` ステートメントが更新をサポートしない場合、カーソルは `READ_ONLY` です。  
  
-   `STATIC` および `FAST_FORWARD` の各カーソルは既定で `READ_ONLY` になります。  
  
-   `DYNAMIC` および `KEYSET` の各カーソルは既定で `OPTIMISTIC` になります。  
  
カーソル名は、他の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントでのみ参照できます。 データベース API 関数でカーソル名を参照することはできません。 たとえば、カーソルの宣言後、OLE DB、ODBC、または ADO 関数やメソッドからカーソル名を参照することはできません。 カーソル行は、フェッチ関数や API のメソッドでフェッチすることはできません。[!INCLUDE[tsql](../../includes/tsql-md.md)] FETCH ステートメントによってのみフェッチできます。  
  
カーソルの宣言後、次に示すシステム ストアド プロシージャを使用すると、カーソルの特性を判断できます。  
  
|システム ストアド プロシージャ|[説明]|  
|------------------------------|-----------------|  
|**sp_cursor_list**|現在接続時に可視であるカーソルとその属性の一覧を返します。|  
|**sp_describe_cursor**|順方向専用カーソルか、スクロール カーソルかなど、カーソルの属性を記述します。|  
|**sp_describe_cursor_columns**|カーソル結果セット内の列の属性を記述します。|  
|**sp_describe_cursor_tables**|カーソルがアクセスするベース テーブルを記述します。|  
  
 カーソルを宣言する *select_statement* の一部として、変数を使用できます。 カーソルが宣言された後、カーソル変数の値は変更されません。  
  
## <a name="permissions"></a>アクセス許可  
 `DECLARE CURSOR` 権限は、特に指定のない限りカーソル内で使用されるビュー、テーブル、および列の `SELECT` 権限を持つユーザーに与えられます。
 
## <a name="limitations-and-restrictions"></a>制限事項と制約事項

クラスター化列ストア インデックスを使用しているテーブルでは、カーソルやトリガーは使用できません。 この制限は、非クラスター化列ストア インデックスには適用されません。非クラスター化列ストア インデックスを使用しているテーブルでは、カーソルとトリガーを使用できます。 
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-simple-cursor-and-syntax"></a>A. 単純なカーソルと構文を使用する  

このカーソルのオープン時に作成された結果セットには、テーブルに存在するすべての行と列が含まれています。 このカーソルは更新することができ、すべての更新結果および削除結果は、このカーソルに対して行ったフェッチに反映されます。 `SCROLL` オプションを指定していないため、フェッチに使用できるのは `FETCH NEXT` のみです。  
 
```sql  
DECLARE vend_cursor CURSOR  
    FOR SELECT * FROM Purchasing.Vendor  
OPEN vend_cursor  
FETCH NEXT FROM vend_cursor;  
```  
  
### <a name="b-using-nested-cursors-to-produce-report-output"></a>B. 入れ子になったカーソルを使用してレポート出力を作成する  
 次の例では、カーソルを入れ子にして複雑なレポートを作成する方法を示します。 内部のカーソルは、各製造元に対して宣言されます。  
  
```sql  
SET NOCOUNT ON;  
  
DECLARE @vendor_id int, @vendor_name nvarchar(50),  
    @message varchar(80), @product nvarchar(50);  
  
PRINT '-------- Vendor Products Report --------';  
  
DECLARE vendor_cursor CURSOR FOR   
SELECT VendorID, Name  
FROM Purchasing.Vendor  
WHERE PreferredVendorStatus = 1  
ORDER BY VendorID;  
  
OPEN vendor_cursor  
  
FETCH NEXT FROM vendor_cursor   
INTO @vendor_id, @vendor_name  
  
WHILE @@FETCH_STATUS = 0  
BEGIN  
    PRINT ' '  
    SELECT @message = '----- Products From Vendor: ' +   
        @vendor_name  
  
    PRINT @message  
  
    -- Declare an inner cursor based     
    -- on vendor_id from the outer cursor.  
  
    DECLARE product_cursor CURSOR FOR   
    SELECT v.Name  
    FROM Purchasing.ProductVendor pv, Production.Product v  
    WHERE pv.ProductID = v.ProductID AND  
    pv.VendorID = @vendor_id  -- Variable value from the outer cursor  
  
    OPEN product_cursor  
    FETCH NEXT FROM product_cursor INTO @product  
  
    IF @@FETCH_STATUS <> 0   
        PRINT '         <<None>>'       
  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
  
        SELECT @message = '         ' + @product  
        PRINT @message  
        FETCH NEXT FROM product_cursor INTO @product  
        END  
  
    CLOSE product_cursor  
    DEALLOCATE product_cursor  
        -- Get the next vendor.  
    FETCH NEXT FROM vendor_cursor   
    INTO @vendor_id, @vendor_name  
END   
CLOSE vendor_cursor;  
DEALLOCATE vendor_cursor;  
```  
  
## <a name="see-also"></a>参照  
 [@@FETCH_STATUS &#40;Transact-SQL&#41;](../../t-sql/functions/fetch-status-transact-sql.md)   
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [カーソル &#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
