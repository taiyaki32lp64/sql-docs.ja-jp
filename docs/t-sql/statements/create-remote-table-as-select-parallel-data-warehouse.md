---
title: CREATE REMOTE TABLE AS SELECT (Parallel Data Warehouse)
ms.custom: seo-dt-2019
ms.date: 08/10/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: jrasnick
ms.topic: conceptual
ms.assetid: 16ef8191-7587-45a3-9ee9-7d99b7088de3
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1b6b024507d06149efc0bc2693b5bde2f67d482b
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401702"
---
# <a name="create-remote-table-as-select-parallel-data-warehouse"></a>CREATE REMOTE TABLE AS SELECT (Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] データベースからデータを選択し、リモート サーバー上の SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース内の新しいテーブルにデータをコピーします。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] は、MPP クエリのすべてのメリットを活用し、アプライアンスを使用して、リモート コピーのデータを選択します。 これは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能を必要とするシナリオに使用します。  
  
 リモート サーバーを構成するには、[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]の「リモート テーブルのコピー」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "|::ref1::|") [Transact-SQL 構文表記規則 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE REMOTE TABLE { database_name.schema_name.table_name | schema_name.table_name | table_name }  AT ('<connection_string>')  
    [ WITH ( BATCH_SIZE = batch_size ) ]  
    AS <select_statement>  
[;]  
  
<connection_string> ::=   
    Data Source = { IP_address | hostname } [, port ]; User ID = user_name ;Password = password;  
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT <select_criteria>  
```  
  
## <a name="arguments"></a>引数  
 *database_name*  
 リモート テーブルを作成するデータベースです。 *database_name* は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースです。 既定値は、宛先の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのユーザーのログインの既定のデータベースです。  
  
 *schema_name*  
 新しいテーブルのスキーマです。 既定値は、宛先の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのユーザーのログインの既定のスキーマです。  
  
 *table_name*  
 新しいテーブルの名前です。 使用可能なテーブル名の詳細については、[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]の「オブジェクトの名前付け規則」を参照してください。  
  
 リモート テーブルがヒープとして作成されます。 Check 制約やトリガーはありません。 リモート テーブルの列の照合順序は、ソース テーブルの列の照合順序と同じです。 これは、**char**、**nchar**、**varchar**、および **nvarchar** 型の列に適用されます。  
  
 *connection_string*  
 リモート側およびデータベースに接続するための `Data Source`、`User ID`、および `Password` パラメーターを指定する文字列です。  
  
 接続文字列は、セミコロンで区切られたキーと値のペアの一覧です。 キーワードの大文字と小文字は区別されません。 キーと値のペア間のスペースは無視されます。 ただし、データ ソースによっては、値の大文字小文字が区別されます。  
  
 *データ ソース*  
 リモートの SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の名前、IP アドレス、および TCP ポート番号を指定するパラメーターです。  
  
 *hostname* または *IP_address*  
 リモート サーバー コンピューターの名前またはリモート サーバーの IPv4 アドレスです。 IPv6 アドレスはサポートされていません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 名前付きインスタンスを、**Computer_Name\Instance_Name** または **IP_address\Instance_Name** の形式で指定することができます。 サーバーは、リモートである必要があり、(local) として指定することはできません。  
  
 TCP *port* 番号  
 接続の TCP ポート番号。 既定のポート 1433 でリッスンしていない SQL Server のインスタンスに対して、0～65535 の TCP ポート番号を指定することができます。 次に例を示します。**ServerA,1450** または **10.192.14.27,1435**  
  
> [!NOTE]  
>  IP アドレスを使用してリモート サーバーに接続することをお勧めします。 ネットワーク構成によっては、コンピューター名を使用して接続するときに、正しいサーバーの名前を解決する非アプライアンス DNS サーバーを使用するために、追加の手順が必要になることがあります。 IP アドレスで接続するときには、この手順は必要ではありません。 詳細については、[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]の「Use a DNS Forwarder to Resolve Non-Appliance DNS Names (Analytics Platform System)」(DNS フォワーダーを使用して非アプライアンス DNS 名を解決する (分析プラットフォーム システム)) を参照してください。  
  
 *user_name*  
 有効な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証ログイン名。 最大文字数は 128 文字です。  
  
 *password*  
 ログイン パスワード。 最大文字数は 128 文字です。  
  
 *batch_size*  
 バッチごとの最大行数。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] は、行をバッチで移行先サーバーに送信します。 *Batch_size* は 0 以上の正の整数です。 既定値は 0 です。  
  
 WITH *common_table_expression*  
 共通テーブル式 (CTE) と呼ばれる一時的な名前付き結果セットを指定します。 詳細については、「[WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)」を参照してください。  
  
 SELECT \<select_criteria> 新しいリモート テーブルに入力するデータを指定するクエリの述語です。 SELECT ステートメントの詳細については、「[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 必須:  
  
-   SELECT 句内の各オブジェクトの SELECT アクセス許可。  
  
-   移行先 SMP データベースに対する CREATE TABLE アクセス許可が必要です。  
  
-   移行先 SMP スキーマに対する ALTER、INSERT、および SELECT アクセス許可が必要です。  
  
## <a name="error-handling"></a>エラー処理  
 リモート データベースへのデータのコピーに失敗した場合、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] は、操作を中止し、エラーをログに記録して、リモート テーブルを削除しようとします。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 新しいテーブルの正常なクリーンアップは保証されません。  
  
## <a name="limitations-and-restrictions"></a>制限事項と制約事項  
 **リモート転送先サーバー**:  
  
-   TCP は、既定値であり、リモート サーバーへの接続でサポートされている唯一のプロトコルです。  
  
-   転送先サーバーは、非アプライアンス サーバーである必要があります。 CREATE REMOTE TABLE を使用して、1 つのアプライアンスから別のアプライアンスにデータをコピーすることはできません。  
  
-   CREATE REMOTE TABLE ステートメントは、新しいテーブルのみを作成します。 したがって、新しいテーブルが既に存在していることはありません。 リモート データベースとスキーマは既に存在している必要があります。  
  
-   リモート サーバーは、アプライアンスから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リモート データベースに転送されるデータを格納するために使用できる領域を持っている必要があります。  
  
 **SELECT ステートメント**:  
  
-   選択条件では、ORDER BY および TOP 句はサポートされていません。  
  
-   アクティブなトランザクション内、またはセッションで AUTOCOMMIT OFF 設定がアクティブなときには、CREATE REMOTE TABLE を実行できません。  
  
 [SET ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/statements/set-rowcount-transact-sql.md) は、このステートメントに効果はありません。 同様の動作を実現するには、[TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md) を使用します。  
  
## <a name="locking-behavior"></a>ロック動作  
 リモート テーブルを作成した後で、コピーを開始するまで、移行先テーブルはロックされません。 したがって、リモート テーブルが作成された後、コピーを開始する前に別のプロセスがリモート テーブルを削除する可能性があります。 これが発生した場合、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] はエラーを生成し、コピーは失敗します。  
  
## <a name="metadata"></a>メタデータ  
 選択したデータのリモート SMP サーバーへのコピーの進行状況を表示するには、[sys.dm_pdw_dms_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md) を使用します。 PARALLEL_COPY_READER 型の行に、この情報が含まれています。  
  
## <a name="security"></a>Security  
 CREATE REMOTE TABLE は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用して、リモートの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続します。Windows 認証は使用しません。  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] の外部に公開されたネットワークはファイアウォールが使用されている必要があります。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ポートおよび管理ポートは例外です。  
  
 偶発的なデータの消失または破損を防ぐために、アプライアンスから移行先データベースにコピーするために使用するユーザー アカウントは、移行先データベースに対して最低限必要なアクセス許可のみを持つようにする必要があります。  
  
 接続設定では、SSL で保護されたユーザー名とパスワードのデータを使用して SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続できますが、実際のデータはクリア テキストで暗号化されずに送信されます。 この場合、悪意のあるユーザーが、SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスにログオンするための [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザー名とパスワードが含まれている CREATE REMOTE TABLE ステートメントのテキストを傍受する可能性があります。 このリスクを避けるためには、SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスへの接続ではデータの暗号化を使用してください。  
  
##  <a name="Examples"></a> 使用例  
  
### <a name="a-creating-a-remote-table"></a>A. リモート テーブルの作成  
 この例では、`MyOrdersTable` という [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SMP のリモート テーブルをデータベース `OrderReporting` およびスキーマ `Orders` に作成します。 `OrderReporting` データベースは、既定のポート 1433 でリッスンする `SQLA` というサーバー上にあります。 サーバーへの接続では、ユーザー `David` の資格情報を使用します。ユーザーのパスワードは `e4n8@3` です。  
  
```  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
AS SELECT <select_criteria>;  
```  
  
### <a name="b-querying-the-sysdm_pdw_dms_workers-dmv-for-remote-table-copy-status"></a>B. リモート テーブルのコピーのステータスの sys.dm_pdw_dms_workers DMV のクエリを実行します。  
 このクエリは、リモート テーブルのコピーのコピー状態を表示する方法を示します。  
  
```  
SELECT * FROM sys.dm_pdw_dms_workers   
WHERE type = 'PARALLEL_COPY_READER';  
```  
  
### <a name="c-using-a-query-join-hint-with-create-remote-table"></a>C. CREATE REMOTE TABLE とクエリの結合ヒントを使用する  
 このクエリは、CREATE REMOTE TABLE を使用してクエリの結合ヒントを使用するための基本構文を示しています。 クエリが、コントロール ノードに送信された後で、コンピューティング ノード上で実行されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クエリ プランを生成するときにハッシュ結合の方法を適用します。 結合ヒントと OPTION 句の使用方法の詳細については、「[OPTION 句 &#40;Transact-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md)」を参照してください。  
  
```  
USE ssawPDW;  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
    AS SELECT T1.* FROM OrderReporting.Orders.MyOrdersTable T1   
    JOIN OrderReporting.Order.Customer T2  
    ON T1.CustomerID=T2.CustomerID OPTION (HASH JOIN);  
```  
  
  

