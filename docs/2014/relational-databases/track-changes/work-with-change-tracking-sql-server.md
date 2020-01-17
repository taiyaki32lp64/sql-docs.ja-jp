---
title: 変更の追跡のしくみ (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- change tracking [SQL Server], making changes
- change tracking [SQL Server], troubleshooting
- updating data [SQL Server]
- troubleshooting [SQL Server], change tracking
- data changes [SQL Server]
- tracking data changes [SQL Server]
- data [SQL Server], changing
- change tracking [SQL Server], data restore
- change tracking [SQL Server], ensuring consistent results
- change tracking [SQL Server], handling changes
ms.assetid: 5aec22ce-ae6f-4048-8a45-59ed05f04dc5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 5ed0a510a6b74e3c33e9cb7ed9d789ad8242a499
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270218"
---
# <a name="work-with-change-tracking-sql-server"></a>変更の追跡のしくみ (SQL Server)
  変更の追跡を使用するアプリケーションは、追跡した変更を取得し、その変更を別のデータ ストアに適用して、ソース データベースを更新できる必要があります。 このトピックでは、これらのタスクの実行方法について説明します。また、フェールオーバーが発生してデータベースをバックアップから復元する必要がある場合に、変更の追跡が果たす役割についても説明します。  
  
##  <a name="Obtain"></a> 変更追跡関数を使用した変更の取得  
 変更追跡関数を使用して、データベースに加えられた変更およびその変更に関する情報を取得する方法について説明します。  
  
### <a name="about-the-change-tracking-functions"></a>変更追跡関数について  
 アプリケーションでは、次の関数を使用して、データベースに加えられた変更およびその変更に関する情報を取得することができます。  
  
 CHANGETABLE(CHANGES …) 関数  
 変更情報のクエリには、この行セット関数を使用します。 この関数は、内部変更追跡テーブルに格納されたデータに対してクエリを実行します。 この関数は、変更された行の主キーとその他の変更情報 (該当する操作、更新された列、行のバージョンなど) を含む結果セットを返します。  
  
 CHANGETABLE(CHANGES ...) は、最終同期バージョンを引数として受け取ります。 最終同期バージョンは、 `@last_synchronization_version` 変数を使用して取得します。 最終同期バージョンのセマンティクスは次のとおりです。  
  
-   呼び出し元のクライアントは、変更を取得し、最終同期バージョン以前のすべての変更を認識しています。  
  
-   そのため、CHANGETABLE(CHANGES …) からは、最終同期バージョンより後で発生したすべての変更が返されます。  
  
     次の図は、CHANGETABLE(CHANGES …) を使用して変更を取得する方法を示しています。  
  
     ![変更の追跡のクエリ出力の例](../../database-engine/media/queryoutput.gif "変更の追跡のクエリ出力の例")  
  
 CHANGE_TRACKING_CURRENT_VERSION() 関数  
 この関数を使用すると、現在のバージョンを取得して、次回の変更クエリの際に使用できます。 このバージョンは、最後にコミットされたトランザクションのバージョンを表します。  
  
 CHANGE_TRACKING_MIN_VALID_VERSION() 関数  
 この関数を使用すると、クライアントの有効な最小バージョン (CHANGETABLE() から有効な結果を取得するために最低限必要なバージョン) を取得できます。 クライアントは、この関数から返される値に対して最終同期バージョンをチェックする必要があります。 最終同期バージョンがこの関数から返されたバージョンより小さいと、クライアントは CHANGETABLE() から有効な結果を取得できないため、再初期化が必要になります。  
  
### <a name="obtaining-initial-data"></a>初期データの取得  
 アプリケーションで初めて変更を取得する前に、クエリを送信して初期データおよび同期バージョンを取得する必要があります。 アプリケーションで適切なデータをテーブルから直接取得してから、CHANGE_TRACKING_CURRENT_VERSION() を使用して初期バージョンを取得する必要があります。 このバージョンは、初めて変更を取得するときに CHANGETABLE(CHANGES …) に渡されます。  
  
 次の例は、初期同期バージョンと初期データセットを取得する方法を示しています。  
  
```sql  
    -- Obtain the current synchronization version. This will be used next time that changes are obtained.  
    SET @synchronization_version = CHANGE_TRACKING_CURRENT_VERSION();  
  
    -- Obtain initial data set.  
    SELECT  
        P.ProductID, P.Name, P.ListPrice  
    FROM  
        SalesLT.Product AS P  
```  
  
### <a name="using-the-change-tracking-functions-to-obtain-changes"></a>変更追跡関数を使用した変更の取得  
 テーブルの変更された行およびその変更に関する情報を取得するには、CHANGETABLE(CHANGES…) を使用します。たとえば、次のクエリは、 `SalesLT.Product` テーブルの変更を取得します。  
  
```sql  
SELECT  
    CT.ProductID, CT.SYS_CHANGE_OPERATION,  
    CT.SYS_CHANGE_COLUMNS, CT.SYS_CHANGE_CONTEXT  
FROM  
    CHANGETABLE(CHANGES SalesLT.Product, @last_synchronization_version) AS CT  
  
```  
  
 通常、クライアントでは、行の主キーだけでなく、行の最新のデータを取得する必要があります。 そのため、アプリケーションで CHANGETABLE(CHANGES …) の結果をユーザー テーブルのデータと結合します。 たとえば、次のクエリでは、 `SalesLT.Product` テーブルと結合して、 `Name` 列と `ListPrice` 列の値を取得します。 `OUTER JOIN`が使用されていることに注意してください。 これは、ユーザー テーブルから削除された行の変更情報が返されるようにするために必要です。  
  
```sql  
SELECT  
    CT.ProductID, P.Name, P.ListPrice,  
    CT.SYS_CHANGE_OPERATION, CT.SYS_CHANGE_COLUMNS,  
    CT.SYS_CHANGE_CONTEXT  
FROM  
    SalesLT.Product AS P  
RIGHT OUTER JOIN  
    CHANGETABLE(CHANGES SalesLT.Product, @last_synchronization_version) AS CT  
ON  
    P.ProductID = CT.ProductID  
```  
  
 次回の変更の列挙で使用するバージョンを取得するには、次の例に示すように、CHANGE_TRACKING_CURRENT_VERSION() を使用します。  
  
```sql  
SET @synchronization_version = CHANGE_TRACKING_CURRENT_VERSION()  
```  
  
 アプリケーションで変更を取得する際は、次の例に示すように、CHANGETABLE(CHANGES…) と CHANGE_TRACKING_CURRENT_VERSION() の両方を使用する必要があります。  
  
```sql  
-- Obtain the current synchronization version. This will be used the next time CHANGETABLE(CHANGES...) is called.  
SET @synchronization_version = CHANGE_TRACKING_CURRENT_VERSION();  
  
-- Obtain incremental changes by using the synchronization version obtained the last time the data was synchronized.  
SELECT  
    CT.ProductID, P.Name, P.ListPrice,  
    CT.SYS_CHANGE_OPERATION, CT.SYS_CHANGE_COLUMNS,  
    CT.SYS_CHANGE_CONTEXT  
FROM  
    SalesLT.Product AS P  
RIGHT OUTER JOIN  
    CHANGETABLE(CHANGES SalesLT.Product, @last_synchronization_version) AS CT  
ON  
    P.ProductID = CT.ProductID  
```  
  
### <a name="version-numbers"></a>バージョン番号  
 変更の追跡が有効になっているデータベースにはバージョン カウンターがあり、変更追跡対象テーブルに変更が加えられるたびに値が増加します。 変更された各行には、バージョン番号が関連付けられています。 変更のクエリを実行する要求がアプリケーションに送信されると、バージョン番号を提供する関数が呼び出されます。 この関数により、そのバージョン以降に行われたすべての変更に関する情報が返されます。 変更追跡バージョンは、`rowversion` データ型の概念といくつかの点で似ている部分があります。  
  
### <a name="validating-the-last-synchronized-version"></a>最終同期バージョンの検証  
 変更に関する情報を保持する期間には制限があります。 期間の長さは、ALTER DATABASE の一部として指定できる CHANGE_RETENTION パラメーターで制御されます。  
  
 CHANGE_RETENTION に指定された期間によって、すべてのアプリケーションで、データベースから変更を要求する必要がある頻度が決まることに注意してください。 *last_synchronization_version* の値がテーブルの有効な最小同期バージョンより古い場合、そのアプリケーションでは有効な変更の列挙を実行できません。 これは、変更情報の一部がクリーンアップされている場合があるためです。 アプリケーションで CHANGETABLE(CHANGES …) を使用して変更を取得する前に、CHANGETABLE(CHANGES …) に渡す予定の *last_synchronization_version* の値を検証する必要があります。*last_synchronization_version* の値が有効ではない場合は、そのアプリケーションのすべてのデータを再初期化する必要があります。  
  
 次の例では、 `last_synchronization_version` の値の有効性をテーブルごとに検証する方法を示します。  
  
```sql  
-- Check individual table.  
IF (@last_synchronization_version < CHANGE_TRACKING_MIN_VALID_VERSION(  
                                   OBJECT_ID('SalesLT.Product')))  
BEGIN  
  -- Handle invalid version and do not enumerate changes.  
  -- Client must be reinitialized.  
END  
```  
  
 次の例に示すように、 `last_synchronization_version` の値の有効性は、データベースのすべてのテーブルに対してチェックできます。  
  
```sql  
-- Check all tables with change tracking enabled  
IF EXISTS (  
  SELECT COUNT(*) FROM sys.change_tracking_tables  
  WHERE min_valid_version > @last_synchronization_version )  
BEGIN  
  -- Handle invalid version & do not enumerate changes  
  -- Client must be reinitialized  
END  
```  
  
### <a name="using-column-tracking"></a>列追跡の使用  
 列追跡を使用すると、行全体ではなく、変更された列のみのデータをアプリケーションで取得できます。 たとえば、サイズは大きいが変更頻度は低い 1 つ以上の列と、頻繁に変更される他の列で構成されるテーブルのシナリオについて考えてみます。 列追跡を使用しない場合、アプリケーションでは行が変更されたことしか判断できないため、大きな列データを含むすべてのデータを同期する必要があります。 一方、列追跡を使用すると、アプリケーションでは大きな列データが変更されたかどうかを判断し、変更された場合にのみそのデータを同期できます。  
  
 列追跡情報は、CHANGETABLE(CHANGES …) 関数によって返される SYS_CHANGE_COLUMNS 列に表示されます。  
  
 列追跡を使用すると、変更されていない列に対して NULL が返されるようにすることができます。 NULL に変更できる列の場合は、別々に列を返してその列が変更されたかどうかを示す必要があります。  
  
 次の例では、 `CT_ThumbnailPhoto` 列は、変更されていない場合は `NULL` になります。 この列は `NULL` に変更された場合にも `NULL` になりますが、アプリケーションでは `CT_ThumbNailPhoto_Changed` 列を使用して、列が変更されたかどうかを判断できます。  
  
```sql  
DECLARE @PhotoColumnId int = COLUMNPROPERTY(  
    OBJECT_ID('SalesLT.Product'),'ThumbNailPhoto', 'ColumnId')  
  
SELECT  
    CT.ProductID, P.Name, P.ListPrice, -- Always obtain values.  
    CASE  
           WHEN CHANGE_TRACKING_IS_COLUMN_IN_MASK(  
                     @PhotoColumnId, CT.SYS_CHANGE_COLUMNS) = 1  
            THEN ThumbNailPhoto  
            ELSE NULL  
      END AS CT_ThumbNailPhoto,  
      CHANGE_TRACKING_IS_COLUMN_IN_MASK(  
                     @PhotoColumnId, CT.SYS_CHANGE_COLUMNS) AS  
                                   CT_ThumbNailPhoto_Changed  
     CT.SYS_CHANGE_OPERATION, CT.SYS_CHANGE_COLUMNS,  
     CT.SYS_CHANGE_CONTEXT  
FROM  
     SalesLT.Product AS P  
INNER JOIN  
     CHANGETABLE(CHANGES SalesLT.Product, @last_synchronization_version) AS CT  
ON  
     P.ProductID = CT.ProductID AND  
     CT.SYS_CHANGE_OPERATION = 'U'  
```  
  
### <a name="obtaining-consistent-and-correct-results"></a>一貫性のある正しい結果の取得  
 テーブルの変更されたデータを取得するには、複数の手順を実行する必要があります。 特定の問題について考慮して対処しないと、一貫性のない結果や正しくない結果が返される可能性があることに注意してください。  
  
 たとえば、Sales テーブルと SalesOrders テーブルに対して行われた変更を取得するには、アプリケーションで次の手順を実行します。  
  
1.  CHANGE_TRACKING_MIN_VALID_VERSION() を使用して最終同期バージョンを検証します。  
  
2.  CHANGE_TRACKING_CURRENT_VERSION() を使用して、次回の変更の取得の際に使用できるバージョンを取得します。  
  
3.  CHANGETABLE(CHANGES ...) を使用して Sales テーブルの変更を取得します。  
  
4.  CHANGETABLE(CHANGES ...) を使用して SalesOrders テーブルの変更を取得します。  
  
 データベースで実行される次の 2 つのプロセスが、上記の手順で返される結果に影響する場合があります。  
  
-   バックグラウンドでクリーンアップ プロセスが実行され、指定した保有期間より古い変更追跡情報が削除されます。  
  
     クリーンアップ プロセスは、データベースの変更の追跡を構成したときに指定した保有期間を使用する個別のバックグラウンド プロセスです。 問題になるのは、最終同期バージョンが検証されてから CHANGETABLE(CHANGES…) の呼び出しが行われるまでの間にクリーンアップ プロセスが実行された場合です。 検証の時点で有効だった最終同期バージョンが、変更の取得時には有効ではなくなっている可能性があります。 そのため、正しくない結果が返される場合があります。  
  
-   継続的な DML 操作として、Sales テーブルと SalesOrders テーブルで次のような操作が実行されます。  
  
    -   CHANGE_TRACKING_CURRENT_VERSION() を使用して次回のバージョンが取得された後に、テーブルに対して変更が行われる可能性があります。 そのため、予想よりも多くの変更が返される場合があります。  
  
    -   Sales テーブルから変更を取得する呼び出しと、SalesOrders テーブルから変更を取得する呼び出しの間に、トランザクションがコミットされる可能性があります。 そのため、SalesOrder テーブルの結果に、Sales テーブルには存在しない外部キー値が含まれる場合があります。  
  
 上記の課題を解決するには、スナップショット分離を使用することをお勧めします。 これにより、変更情報の一貫性を確保し、バックグラウンドのクリーンアップ タスクに関連する競合状態を回避することができます。 スナップショット トランザクションを使用しないと、変更の追跡を使用するアプリケーションの開発にかかる手間が大幅に増えることがあります。  
  
#### <a name="using-snapshot-isolation"></a>スナップショット分離の使用  
 変更の追跡は、スナップショット分離でも適切に機能するように設計されています。 データベースに対してスナップショット分離を有効にする必要があります。 また、変更の取得に必要なすべての手順がスナップショット トランザクション内に含まれている必要があります。 これにより、変更の取得中にデータに対して行われたすべての変更が、スナップショット トランザクション内のクエリからは認識されなくなります。  
  
 スナップショット トランザクション内でデータを取得するには、次の手順を実行します。  
  
1.  トランザクション分離レベルをスナップショットに設定し、トランザクションを開始します。  
  
2.  CHANGE_TRACKING_MIN_VALID_VERSION() を使用して最終同期バージョンを検証します。  
  
3.  CHANGE_TRACKING_CURRENT_VERSION() を使用して、次回使用するバージョンを取得します。  
  
4.  CHANGETABLE(CHANGES …) を使用して Sales テーブルの変更を取得します。  
  
5.  CHANGETABLE(CHANGES ...) を使用して SalesOrders テーブルの変更を取得します。  
  
6.  トランザクションをコミットします。  
  
 変更を取得するすべての手順がスナップショット トランザクション内で行われるため、次の点に注意してください。  
  
-   最終同期バージョンの検証後にクリーンアップが実行された場合でも、クリーンアップで実行された削除操作がトランザクション内からは認識されないため、CHANGETABLE(CHANGES ...) から有効な結果が返されます。  
  
-   次回の同期バージョンの取得後に Sales テーブルまたは SalesOrders テーブルに対して行われた変更は認識されません。そのため、CHANGETABLE(CHANGES ...) の呼び出しで、CHANGE_TRACKING_CURRENT_VERSION() によって返されたバージョンより後の変更は返されません。 また、Sales テーブルと SalesOrders テーブルの間の一貫性も保持されます。それぞれの CHANGETABLE(CHANGES …) の呼び出しの間にコミットされたトランザクションが認識されないためです。  
  
 次の例では、データベースに対してスナップショット分離を有効にする方法を示します。  
  
```sql  
-- The database must be configured to enable snapshot isolation.  
ALTER DATABASE AdventureWorksLT  
    SET ALLOW_SNAPSHOT_ISOLATION ON;  
```  
  
 スナップショット トランザクションは次のように使用します。  
  
```sql  
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
BEGIN TRAN  
  -- Verify that version of the previous synchronization is valid.  
  -- Obtain the version to use next time.  
  -- Obtain changes.  
COMMIT TRAN  
```  
  
 スナップショット トランザクションの詳細については、「[SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)」を参照してください。  
  
#### <a name="alternatives-to-using-snapshot-isolation"></a>スナップショット分離の使用に代わる方法  
 スナップショット分離の使用に代わる方法がありますが、すべてのアプリケーション要件を満たしていることを確認するための作業が必要になります。 *last_synchronization_version* が有効であり、クリーンアップ プロセスでデータが削除されていないことを変更の取得前に確認するには、次の手順を実行します。  
  
1.  CHANGETABLE() の呼び出し後に *last_synchronization_version* を確認します。  
  
2.  CHANGETABLE() を使用して変更を取得する各クエリで、その一部として *last_synchronization_version* を確認します。  
  
 次回の列挙の同期バージョンが取得された後に変更が行われる可能性があります。 この状況に対処するには、2 つの方法があります。 使用するオプションは、アプリケーションおよび各方法の副作用への対処方法によって異なります。  
  
-   新しい同期バージョンよりバージョンが大きい変更を無視します。  
  
     この方法の副作用として、新しい同期バージョンより前に行が作成または更新された場合、新しい行や更新された行がスキップされ、後で更新されます。 新しい行がある場合、作成された別のテーブルにスキップされた行を参照する行があると、参照整合性の問題が発生する可能性があります。 更新された既存の行がある場合、その行はスキップされ、次回まで同期されません。  
  
-   新しい同期バージョンよりバージョンが大きい変更も含め、すべての変更を含めます。  
  
     新しい同期バージョンよりバージョンが大きい行は、次回の同期で再度取得されます。 アプリケーションでは、このことを想定して対処する必要があります。  
  
 上記の 2 つのオプションに加え、操作に応じて両方を組み合わせた方法を検討することもできます。 たとえば、アプリケーションによっては、次回の同期バージョンより新しい変更 (行の作成または削除) は無視し、更新は無視しないようにすることが最適な場合もあります。  
  
> [!NOTE]  
>  変更の追跡 (または任意のカスタムの追跡メカニズム) を使用する場合にアプリケーションで使用する方法を選択する際には、十分な分析が必要です。 したがって、スナップショット分離を使用した方がはるかに簡単です。  
  
##  <a name="Handles"></a> 変更の追跡でデータベースへの変更が処理されるしくみ  
 変更の追跡を使用するアプリケーションの中には、別のデータ ストアとの双方向の同期を行うものもあります。 この場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースで行われた変更が他のデータ ストアで更新され、他のデータ ストアで行われた変更が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースで更新されます。  
  
 別のデータ ストアからの変更でローカル データベースを更新する際には、アプリケーションで次の操作を実行する必要があります。  
  
-   競合がないかどうかを確認します。  
  
     両方のデータ ストアで同じデータが同時に変更されると、競合が発生します。 アプリケーションで、競合がないかどうかを確認したり、競合を解決するための十分な情報を取得したりできる必要があります。  
  
-   アプリケーション コンテキスト情報を格納します。  
  
     変更追跡情報を持つデータをアプリケーションで格納します。 この情報は、変更がローカル データベースから取得されるときに他の変更追跡情報と共に取得できます。 たとえば変更のソースとなったデータ ストアの ID は、このコンテキスト情報の一例です。  
  
 同期アプリケーションでこれらの操作を実行するには、次の関数を使用できます。  
  
-   CHANGETABLE(VERSION...)  
  
     アプリケーションで変更を加える際にこの関数を使用すると、競合がないかどうかを確認できます。 この関数は、変更追跡対象テーブルの指定された行に関する最新の変更追跡情報を取得します。 この変更追跡情報には、最後に変更された行のバージョンが含まれています。 この情報をアプリケーションで使用することによって、アプリケーションの前回の同期後に行が変更されたかどうかを確認できます。  
  
-   WITH CHANGE_TRACKING_CONTEXT  
  
     アプリケーションでこの句を使用すると、コンテキスト データを格納できます。  
  
### <a name="checking-for-conflicts"></a>競合の確認  
 双方向同期のシナリオでは、前回変更を取得してから行が更新されていないかどうかをクライアント アプリケーションで確認する必要があります。  
  
 次の例は、CHANGETABLE(VERSION ...) 関数を使用して最も効率的に (別のクエリを使用せずに) 競合を確認する方法を示しています。 この例では、 `CHANGETABLE(VERSION ...)` が、 `SYS_CHANGE_VERSION` で指定される行の `@product id`を判別します。 `CHANGETABLE(CHANGES ...)` でも同じ情報を取得できますが、効率が下がります。 行の `SYS_CHANGE_VERSION` の値が `@last_sync_version`の値より大きい場合は競合があります。 競合がある場合、行は更新されません。 `ISNULL()` の確認が必要なのは、行の変更情報がない場合もあるためです。 変更の追跡を有効にしてからまだ行が更新されていない場合や、変更情報がクリーンアップされてからまだ行が更新されていない場合は、変更情報は存在しません。  
  
```sql  
-- Assumption: @last_sync_version has been validated.  
  
UPDATE  
    SalesLT.Product  
SET  
    ListPrice = @new_listprice  
FROM  
    SalesLT.Product AS P  
WHERE  
    ProductID = @product_id AND  
    @last_sync_version >= ISNULL (  
        SELECT CT.SYS_CHANGE_VERSION  
        FROM CHANGETABLE(VERSION SalesLT.Product,  
                        (ProductID), (P.ProductID)) AS CT),  
        0)  
```  
  
 次のコードでは、更新された行の数を確認して、競合に関する詳細情報を特定できます。  
  
```sql  
-- If the change cannot be made, find out more information.  
IF (@@ROWCOUNT = 0)  
BEGIN  
    -- Obtain the complete change information for the row.  
    SELECT  
        CT.SYS_CHANGE_VERSION, CT.SYS_CHANGE_CREATION_VERSION,  
        CT.SYS_CHANGE_OPERATION, CT.SYS_CHANGE_COLUMNS  
    FROM  
        CHANGETABLE(CHANGES SalesLT.Product, @last_sync_version) AS CT  
    WHERE  
        CT.ProductID = @product_id;  
  
    -- Check CT.SYS_CHANGE_VERSION to verify that it really was a conflict.  
    -- Check CT.SYS_CHANGE_OPERATION to determine the type of conflict:  
    -- update-update or update-delete.  
    -- The row that is specified by @product_id might no longer exist   
    -- if it has been deleted.  
END  
```  
  
### <a name="setting-context-information"></a>コンテキスト情報の設定  
 WITH CHANGE_TRACKING_CONTEXT 句を使用すると、アプリケーションで変更情報と一緒にコンテキスト情報を格納できます。 格納した情報は、CHANGETABLE(CHANGES ...) によって返される SYS_CHANGE_CONTEXT 列から取得できます。  
  
 コンテキスト情報は通常、変更のソースを識別するために使用されます。 変更のソースを識別できれば、その情報をデータ ストアで使用して、再び同期される際に変更が取得されないようにすることができます。  
  
```sql  
  -- Try to update the row and check for a conflict.  
  WITH CHANGE_TRACKING_CONTEXT (@source_id)  
  UPDATE  
     SalesLT.Product  
  SET  
      ListPrice = @new_listprice  
  FROM  
      SalesLT.Product AS P  
  WHERE  
     ProductID = @product_id AND  
     @last_sync_version >= ISNULL (  
         (SELECT CT.SYS_CHANGE_VERSION FROM CHANGETABLE(VERSION SalesLT.Product,  
         (ProductID), (P.ProductID)) AS CT),  
         0)  
```  
  
### <a name="ensuring-consistent-and-correct-results"></a>一貫性のある正しい結果の確保  
 アプリケーションで @last_sync_version の値を検証するときには、クリーンアップ プロセスを考慮に入れる必要があります。 これは、CHANGE_TRACKING_MIN_VALID_VERSION() が呼び出された後、更新が行われる前に、データが削除される可能性があるからです。  
  
> [!IMPORTANT]  
>  スナップショット分離を使用してスナップショット トランザクション内で変更を行うことをお勧めします。  
  
```sql  
-- Prerequisite is to ensure ALLOW_SNAPSHOT_ISOLATION is ON for the database.  
  
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
BEGIN TRAN  
    -- Verify that last_sync_version is valid.  
    IF (@last_sync_version <  
CHANGE_TRACKING_MIN_VALID_VERSION(OBJECT_ID('SalesLT.Product')))  
    BEGIN  
       RAISERROR (N'Last_sync_version too old', 16, -1);  
    END  
    ELSE  
    BEGIN  
        -- Try to update the row.  
        -- Check @@ROWCOUNT and check for a conflict.  
    END  
COMMIT TRAN  
```  
  
> [!NOTE]  
>  スナップショット トランザクション内で更新の対象になっている行は、スナップショット トランザクションの開始後に別のトランザクションで更新されている可能性があります。 この場合はスナップショット分離の更新の競合が発生し、トランザクションは終了します。 この状況が発生した場合は、更新を再試行してください。 その結果、変更の追跡の競合が検出されることになり、行は変更されません。  
  
##  <a name="DataRestore"></a> 変更の追跡とデータの復元  
 同期が必要なアプリケーションでは、変更の追跡が有効になっているデータベースが以前のバージョンのデータに戻るケースを考える必要があります。 この状況は、非同期データベース ミラーへのフェールオーバーや、ログ配布の使用時のエラーに伴い、データベースがバックアップから復元された後に発生する可能性があります。 この問題を説明するシナリオを次に示します。  
  
1.  テーブル T1 は変更の追跡の対象になっており、このテーブルの有効な最小バージョンは 50 になっています。  
  
2.  クライアント アプリケーションはバージョン 100 でデータを同期し、バージョン 50 とバージョン 100 の間で発生したすべての変更に関する情報を取得します。  
  
3.  テーブル T1 には、バージョン 100 以降もさらに変更が加えられます。  
  
4.  バージョン 120 でエラーが発生し、データベース管理者がデータベースを復元しますが、これに伴ってデータ損失が発生します。 復元操作の後、テーブルにはバージョン 70 までのデータが格納され、最小同期バージョンは 50 のままになります。  
  
     これは、プライマリ データ ストアには存在しないデータが同期データ ストアに含まれることを意味します。  
  
5.  T1 は何度も更新されます。 その結果、現在のバージョンは 130 になります。  
  
6.  クライアント アプリケーションが再び同期を実行します。このとき、クライアント アプリケーションの最終同期バージョンは 100 になっています。 100 は 50 より大きいため、この番号はクライアントの検証を通過します。  
  
     クライアントはバージョン 100 と 130 の間の変更を取得します。 この時点で、クライアントは 70 と 100 の間の変更が以前と同じではないことを認識していません。 クライアントとサーバーのデータは同期されません。  
  
 データベースがバージョン 100 より後の時点の状態に復旧された場合は、同期の問題は発生しません。 クライアントとサーバーのデータは、次の同期間隔の間に正しく同期されます。  
  
 変更の追跡では、データ損失からの復旧はサポートされていません。 ただし、この種の同期の問題を検出する方法は 2 つあります。  
  
-   データベース バージョン ID をサーバーに保存し、データベースの復旧などでデータが失われるたびに、この値を更新する方法。 この ID を各クライアント アプリケーションに保存し、各クライアントがデータを同期する際に必ず検証されるようにします。 データ損失が発生した場合は ID が一致しなくなり、クライアントが再初期化されます。 1 つの欠点は、データ損失が最後に同期された範囲に及んでいない場合に、不要な再初期化が行われる可能性があることです。  
  
-   クライアントが変更クエリを実行した時点で、最終同期バージョンの番号をクライアントごとにサーバー上に記録する方法。 データに問題がある場合は、最終同期バージョンの番号が一致しません。 これによって、再初期化が必要であることがわかります。  
  
## <a name="see-also"></a>関連項目  
 [データ変更の追跡 &#40;SQL Server&#41;](../track-changes/track-data-changes-sql-server.md)   
 [変更の追跡について &#40;SQL Server&#41;](../track-changes/about-change-tracking-sql-server.md)   
 [変更の追跡の管理 &#40;SQL Server&#41;](../track-changes/manage-change-tracking-sql-server.md)   
 [変更の追跡の有効化と無効化 &#40;SQL Server&#41;](../track-changes/enable-and-disable-change-tracking-sql-server.md)   
 [CHANGETABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/changetable-transact-sql)   
 [CHANGE_TRACKING_MIN_VALID_VERSION &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/change-tracking-min-valid-version-transact-sql)   
 [CHANGE_TRACKING_CURRENT_VERSION &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/change-tracking-current-version-transact-sql)   
 [WITH CHANGE_TRACKING_CONTEXT &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/with-change-tracking-context-transact-sql)  
  
  
