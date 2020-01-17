---
title: 主キー制約と外部キー制約 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- foreign keys [SQL Server], cascading referential integrity
- FOREIGN KEY constraints
- foreign keys [SQL Server]
- foreign keys [SQL Server], about foreign key constraints
ms.assetid: 31fbcc9f-2dc5-4bf9-aa50-ed70ec7b5bcd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 45d4cd390e0369d8289ed9e58de01b7a02f752c5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68196745"
---
# <a name="primary-and-foreign-key-constraints"></a>主キー制約と外部キー制約
  主キーと外部キーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブル内のデータに整合性を適用するために使用できる 2 種類の制約です。 これらは重要なデータベース オブジェクトです。  
  
 このトピックは次のセクションで構成されます。  
  
 [主キー制約](../tables/primary-and-foreign-key-constraints.md#PKeys)  
  
 [Foreign Key Constraints](../tables/primary-and-foreign-key-constraints.md#FKeys)  
  
 [関連タスク](../tables/primary-and-foreign-key-constraints.md#Tasks)  
  
##  <a name="PKeys"></a> 主キー制約  
 テーブルには通常、テーブルの各行を一意に識別する値が格納された単一の列または複数の列の組み合わせがあります。 この列、または列の組み合わせを、テーブルの主キー (PK) と呼び、テーブルのエンティティが整合性を持つようにします。 主キー制約は一意なデータを保証するものであるため、通常は ID 列に対して定義されます。  
  
 主キー制約をテーブルに対して指定すると、重複のないインデックスを [!INCLUDE[ssDE](../../includes/ssde-md.md)] が主キー列に対して自動的に作成し、データが一意になるようにします。 また、クエリの中で主キーが使用された場合は、このインデックスによってデータに高速にアクセスできます。 複数の列に一意キー制約が定義されている場合は、1 つの列内で値が重複してもかまいませんが、一意キー制約が定義された列に格納される値の組み合わせは一意である必要があります。  
  
 次の図に示すように、このテーブルの複合主キー制約は、 **Purchasing.ProductVendor** テーブルの **ProductID** 列と **VendorID** 列により作成されています。 そのため、**ProductID** と **VendorID** の組み合わせは、**ProductVendor** テーブル内のすべての行で一意になります。 これによって重複行の挿入が防止されます。  
  
 ![複合 PRIMARY KEY 制約](../../database-engine/media/fund04.gif "複合 PRIMARY KEY 制約")  
  
-   テーブルに含めることができる主キー制約は 1 つだけです。  
  
-   主キーは 16 列を超えることはできず、また、主キーの長さの合計が 900 バイトを超えることはできません。  
  
-   主キー制約によって生成されたインデックスが含まれていても、テーブル上のインデックスの数を、非クラスター化インデックス 999 個、クラスター化インデックス 1 個より多くすることはできません。  
  
-   主キー制約に対して clustered も nonclustered も指定されていない場合、テーブルにクラスター化インデックスが指定されていなければ、clustered が使用されます。  
  
-   主キー制約中で定義する列はすべて、not null として定義する必要があります。 NULL 値を許容するかどうかを指定しない場合、主キー制約の影響を受けるすべての列は not null に設定されます。  
  
-   CLR ユーザー定義型の列に対して主キーを定義する場合は、型の実装でバイナリ順がサポートされている必要があります。  
  
##  <a name="FKeys"></a> Foreign Key Constraints  
 外部キー (FK) は、2 つのテーブルのデータ間にリンクを確立および設定することによって外部キー テーブルに格納できるデータを制御するための単一の列または複数の列の組み合わせです。 外部キー参照では、1 つのテーブルの主キー値が格納されている列が別のテーブルの 1 つ以上の列によって参照されたときに、2 つのテーブル間にリンクが作成されます。 この列は、2 番目のテーブルの外部キーになります。  
  
 たとえば、 **Sales.SalesOrderHeader** テーブルには、 **Sales.SalesPerson** テーブルへの外部キー リンクが存在します。これは、販売注文と販売員の間に論理リレーションシップが存在するからです。 **SalesOrderHeader** テーブルの **SalesPersonID** 列は、 **SalesPerson** テーブルの主キー列と一致します。 また、 **SalesOrderHeader** テーブルの **SalesPersonID** 列は、 **SalesPerson** テーブルに対する外部キーです。 この外部キー リレーションシップを作成することによって、**SalesPerson** テーブル内に存在しない **SalesPersonID** の値を **SalesOrderHeader** テーブルに挿入することはできなくなります。  
  
### <a name="indexes-on-foreign-key-constraints"></a>外部キー制約のインデックス  
 主キー制約とは異なり、外部キー制約を作成しても対応するインデックスは自動的には作成されません。 ただし、外部キーに手動でインデックスを作成することには、通常、次のような利点があります。  
  
-   クエリ内で、一方のテーブルの外部キー制約が定義された列を、他方のテーブルの主キー列または一意なキー列と照合することによって関連テーブルのデータが結合されるとき、多くの場合、外部キー列が結合基準に使用されます。 インデックスを使用すると、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] により、外部キー テーブルの関連データがすばやく検索されます。 ただし、必ずしもこのインデックスを作成する必要はありません。 2 つのテーブル間に主キー制約または外部キー制約が定義されていなくても、関連する 2 つのテーブルのデータを結合できます。ただし、2 つのテーブル間に外部キー リレーションシップが存在するということは、それら 2 つのテーブルが、結合基準としてキーを使用するクエリ内で結合されるように最適化されていることを示します。  
  
-   主キー制約に加えた変更が、関連テーブルの外部キー制約によってチェックされます。  
  
### <a name="referential-integrity"></a>参照整合性  
 外部キー制約の主な目的は、外部キー テーブルに格納できるデータを制御することですが、主キー テーブルのデータに対する変更も制御されます。 たとえば、ある販売員の行が **Sales.SalesPerson** テーブルから削除され、その販売員の ID が **Sales.SalesOrderHeader** テーブルの販売注文に使用された場合、2 つのテーブル間の参照整合性は破棄されます。削除された販売員の販売注文は、 **SalesPerson** テーブルのデータへのリンクを持たない状態となり、 **SalesOrderHeader** テーブル内で孤立します。  
  
 外部キー制約を定義すると、このような状況が発生するのを防ぐことができます。 この制約により、外部キー テーブルのデータへのリンクが無効になるような変更を主キー テーブルのデータに加えることができなくなるため、参照整合性が保証されます。 主キー テーブルの行を削除しようとするか、または主キー値を変更しようとした場合、削除または変更する主キー値が別のテーブルの外部キー制約の値と一致していると、その操作は失敗します。 外部キー制約が定義された行を正常に変更または削除するには、まず、外部キー テーブルの外部キー データを削除または変更し、外部キーから他の主キー データへのリンクを設定する必要があります。  
  
#### <a name="cascading-referential-integrity"></a>連鎖参照整合性  
 連鎖参照整合性制約を使用することで、既存の外部キーが参照しているキーをユーザーが削除または更新するときの [!INCLUDE[ssDE](../../includes/ssde-md.md)] の動作を定義できます。 以下の連鎖動作を定義できます。  
  
 NO ACTION  
 NO ACTION を指定すると、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ではエラーが発生し、親テーブルでの行の削除操作または更新操作がロールバックされます。  
  
 CASCADE  
 親テーブルで行が更新または削除された場合に、参照元のテーブルでも対応する行が更新または削除されます。 CASCADE は、`timestamp` 型の列が外部キーまたは参照先キーの一部である場合は指定できません。 INSTEAD OF DELETE トリガーが設定されているテーブルには、ON DELETE CASCADE を指定できません。 INSTEAD OF UPDATE トリガーが設定されているテーブルには、ON UPDATE CASCADE を指定できません。  
  
 SET NULL  
 親テーブルの対応する行が更新または削除された場合、外部キーを形成するすべての値が NULL に設定されます。 この制約を実行するには、外部キー列が NULL 値を使用できる必要があります。 INSTEAD OF UPDATE トリガーが設定されているテーブルには指定できません。  
  
 SET DEFAULT  
 親テーブル内の対応する行が更新または削除されると、外部キーを構成するすべての値に既定値が設定されます。 この制約を実行するには、すべての外部キー列に既定値が定義されている必要があります。 列が NULL 値を許容し、明示的な既定値が設定されていない場合は、列の既定値として NULL が暗黙的に使用されます。 INSTEAD OF UPDATE トリガーが設定されているテーブルには指定できません。  
  
 CASCADE、SET NULL、SET DEFAULT および NO ACTION は、互いに参照関係にあるテーブルに対して組み合わせて使用することができます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] が NO ACTION を検出すると、関連する CASCADE、SET NULL および SET DEFAULT 操作が停止されロールバックされます。 DELETE ステートメントの実行によって、CASCADE、SET NULL、SET DEFAULT および NO ACTION 操作の組み合わせが適用される場合、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] が NO ACTION があるかどうかを調べる前にすべての CASCADE、SET NULL および SET DEFAULT 操作が適用されます。  
  
### <a name="triggers-and-cascading-referential-actions"></a>トリガーと連鎖参照動作  
 連鎖参照動作によって、AFTER UPDATE トリガーまたは AFTER DELETE トリガーは次のように起動します。  
  
-   元の DELETE または UPDATE によって直接発生するすべての連鎖参照動作が、まず実行されます。  
  
-   連鎖動作を受けたテーブルに AFTER トリガーが定義されている場合、すべての連鎖動作が実行された後でトリガーが起動します。 AFTER トリガーの起動順序は連鎖動作の逆です。 1 つのテーブル内のトリガーの起動順序は、最初または最後に起動することが決まっているトリガーがある場合を除きランダムです。 その起動順序は [sp_settriggerorder](/sql/relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql)での指定に従います。  
  
-   UPDATE 操作または DELETE 操作を直接受けたテーブルから複数の連鎖チェーンが始まる場合、それぞれのチェーンでトリガーが起動する順序は特定できません。 ただし、必ず 1 本のチェーンのトリガーがすべて起動した後で別のチェーンのトリガーが起動を開始します。  
  
-   UPDATE 操作または DELETE 操作を直接受けるテーブルの AFTER トリガーは、どの行も影響を受けないとしても起動します。 その際、他のテーブルには連鎖が波及しません。  
  
-   あるトリガーで他のテーブルに対し UPDATE 操作または DELETE 操作が行われた場合、操作の後に 2 次的な連鎖チェーンが開始される場合があります。 この 2 次的なチェーンは、最初に発生したチェーンのすべてのトリガーが起動した後でそれぞれの UPDATE 操作または DELETE 操作ごとに処理されます。 その後の UPDATE 操作または DELETE 操作についても、この処理が再帰的に繰り返されます。  
  
-   CREATE、ALTER、DELETE、またはその他の DDL (データ定義言語) 操作をトリガー内で実行すると、DDL トリガーが起動する場合があります。 その結果、新たな連鎖チェーンを開始したりトリガーを起動したりする DELETE 操作または UPDATE 操作が実行されることもあります。  
  
-   特定の連鎖参照動作のチェーン内でエラーが発生した場合、エラーが表示され、そのチェーンの AFTER トリガーは起動されずに、チェーンを開始した DELETE 操作または UPDATE 操作がロールバックされます。  
  
-   INSTEAD OF トリガーを含んだテーブルに、連鎖動作を指定する REFERENCES 句を同時に指定することはできません。 ただし、連鎖動作の対象になるテーブルの AFTER トリガーは、別のテーブルやビューに対して INSERT、UPDATE、または DELETE ステートメントを実行し、そのオブジェクトに定義されている INSTEAD OF トリガーを起動できます。  
  
##  <a name="Tasks"></a> 関連タスク  
 次の表は、主キー制約および外部キー制約に関連した一般的なタスクの一覧です。  
  
|タスク|トピック|  
|----------|-----------|  
|主キーを作成する方法について説明します。|[主キーの作成](../tables/create-primary-keys.md)|  
|主キーを削除する方法について説明します。|[主キーの削除](../tables/delete-primary-keys.md)|  
|主キーを変更する方法について説明します。|[主キーの変更](../tables/modify-primary-keys.md)|  
|外部キー リレーションシップを作成する方法について説明します。|[外部キーのリレーションシップの作成](../tables/create-foreign-key-relationships.md)|  
|外部キー リレーションシップを変更する方法について説明します。|[外部キー リレーションシップの変更](../tables/modify-foreign-key-relationships.md)|  
|外部キー リレーションシップを削除する方法について説明します。|[外部キーのリレーションシップの削除](../tables/delete-foreign-key-relationships.md)|  
|外部キーのプロパティを表示する方法について説明します。|[外部キーのプロパティの表示](../tables/view-foreign-key-properties.md)|  
|レプリケーションに対して外部キー制約を無効にする方法を説明します。|[レプリケーションに対して外部キー制約を無効にする方法](../tables/disable-foreign-key-constraints-for-replication.md)|  
|INSERT または UPDATE ステートメント時に外部キー制約を無効にする方法について説明します。|[INSERT ステートメントまたは UPDATE ステートメントに対して外部キー制約を無効にする方法](../tables/disable-foreign-key-constraints-with-insert-and-update-statements.md)|  
  
  
