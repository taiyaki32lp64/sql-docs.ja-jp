---
title: Tempdb データベース
description: 並列データウェアハウスの Tempdb データベース。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 3772e2b4cabac84c00854eba85f7a0c2a33d48bc
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400140"
---
# <a name="tempdb-database-in-parallel-data-warehouse"></a>並列データウェアハウスの tempdb データベース
**tempdb**は、ユーザーデータベースのローカル一時テーブルを格納する SQL Server PDW システムデータベースです。 一時テーブルは、多くの場合、クエリのパフォーマンスを向上させるために使用されます。 たとえば、一時テーブルを使用してスクリプトをモジュール化し、計算されたデータを再利用することができます。  
  
システムデータベースの詳細については、「[システムデータベース](system-databases.md)」を参照してください。  
  
## <a name="Basics"></a>主な用語と概念  
*ローカル一時テーブル*  
*ローカル一時テーブル*では、テーブル名の前に # プレフィックスが使用されます。これは、ローカルユーザーセッションによって作成された一時テーブルです。 各セッションは、独自のセッションのローカル一時テーブルのデータにのみアクセスできます。  
  
各セッションでは、すべてのセッションでローカル一時テーブルのメタデータを表示できます。 たとえば、すべてのセッションで、 `SELECT * FROM tempdb.sys.tables`クエリを使用してすべてのローカル一時テーブルのメタデータを表示できます。  
  
グローバル一時テーブル  
# # 構文の SQL Server でサポートされている*グローバル一時テーブル*は、このリリースの SQL Server PDW ではサポートされていません。  
  
pdwtempdb  
**pdwtempdb**は、ローカル一時テーブルを格納するデータベースです。  
  
PDW では、SQL Server**tempdb**データベースを使用した一時テーブルは実装されません。 代わりに、PDW は pdwtempdb という名前のデータベースにそれらを格納します。 このデータベースは各コンピューティングノード上に存在し、PDW インターフェイスを介してユーザーには表示されません。 管理コンソールの [ストレージ] ページには、「 **tempdb-sql**」という名前の PDW システムデータベースに含まれていることが表示されます。  
  
tempdb  
**tempdb は SQL Server** tempdb データベースです。 最小ログ記録を使用します。 SQL Server は、コンピューティングノードで tempdb を使用して、SQL Server 操作を実行する過程で必要な一時テーブルを格納します。  
  
SQL Server PDW は、次の場合に**tempdb**からテーブルを削除します。  
  
-   DROP TABLE ステートメントが実行されます。  
  
-   セッションは切断されています。 セッションの一時テーブルだけが削除されます。  
  
-   アプライアンスはシャットダウンされています。  
  
-   制御ノードには、クラスターのフェールオーバーがあります。  
  
## <a name="general-remarks"></a>全般的な解説  
SQL Server PDW は、明示的に指定されていない限り、一時テーブルとパーマネントテーブルに対して同じ操作を実行します。 たとえば、パーマネントテーブルと同様に、ローカル一時テーブル内のデータは、コンピューティングノード全体に分散されるか、レプリケートされます。  
  
## <a name="LimitationsRestrictions"></a>制限事項と制約事項  
SQL Server PDW**tempdb**データベースの制限事項と制約事項。 *次のことはできません。*  
  
-   # # で始まるグローバル一時テーブルを作成します。  
  
-   **Tempdb**のバックアップまたは復元を実行します。  
  
-   **GRANT**、 **DENY**、または**REVOKE**ステートメントを使用して、 **tempdb**に対する権限を変更します。  
  
-   **Tempdb**Tempdb の**DBCC SHRINKLOG**を実行します。  
  
-   **Tempdb**に対して DDL 操作を実行します。 これにはいくつかの例外があります。 詳細については、ローカル一時テーブルに関する制限事項と制限事項を次の一覧で参照してください。  
  
ローカル一時テーブルに関する制限事項と制約事項。 *次のことはできません。*  
  
-   一時テーブルの名前を変更する  
  
-   一時テーブルにパーティション、ビュー、または非クラスター化インデックスを作成します。 **ALTER INDEX**を使用すると、1つのを使用して作成されたテーブルのクラスター化インデックスを再構築できます。  
  
-   GRANT、DENY、または REVOKE ステートメントを使用して、一時テーブルに対する権限を変更します。  
  
-   一時テーブルに対してデータベースコンソールコマンドを実行します。  
  
-   同じバッチ内で、2つ以上の一時テーブルに同じ名前を使用します。 バッチ内で複数のローカル一時テーブルを使用する場合、各テーブルの名前は一意でなければなりません。 複数のセッションが同じバッチを実行していて、同じローカル一時テーブルを作成している場合、では、ローカル一時テーブルごとに一意の名前を維持するために、内部的にローカル一時テーブル名に数値サフィックスを追加 SQL Server PDW ます。  
  
> [!NOTE]  
> 一時テーブルの統計を作成および更新*でき*ます。**ALTER INDEX**を使用して、クラスター化インデックスを再構築できます。  
  
## <a name="permissions"></a>アクセス許可  
すべてのユーザーが tempdb 内に一時オブジェクトを作成できます。 ユーザーは追加の権限を付与されない限り、自分で作成したオブジェクトにしかアクセスできません。 ユーザーが tempdb を使用できないように tempdb への接続権限を取り消すことはできますが、一部のルーチン処理で tempdb を使用する必要があるためお勧めしません。  
  
## <a name="RelatedTasks"></a>関連タスク  
  
|タスク|説明|  
|---------|---------------|  
|**Tempdb**にテーブルを作成します。|CREATE TABLE と CREATE TABLE を SELECT ステートメントと共に使用して、ユーザーの一時テーブルを作成できます。 詳細については、「 [CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md) 」および「 [SELECT として CREATE TABLE](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)」を参照してください。|  
|**Tempdb**内の既存のテーブルの一覧を表示します。|`SELECT * FROM tempdb.sys.tables;`|  
|**Tempdb**内の既存の列の一覧を表示します。|`SELECT * FROM tempdb.sys.columns;`|  
|**Tempdb**内の既存のオブジェクトの一覧を表示します。|`SELECT * FROM tempdb.sys.objects;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
