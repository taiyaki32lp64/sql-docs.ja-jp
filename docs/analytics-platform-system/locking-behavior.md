---
title: ロック動作
description: 並列データウェアハウスがロックを使用してトランザクションの整合性を確保する方法と、複数のユーザーが同時にデータにアクセスする場合のデータベースの一貫性を維持する方法について説明します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: f3ecf5cf783b707b75c90dfa70d502e3c81d28c3
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401003"
---
# <a name="locking-behavior-in-parallel-data-warehouse"></a>並列データウェアハウスでのロック動作
並列データウェアハウスがロックを使用してトランザクションの整合性を確保する方法と、複数のユーザーが同時にデータにアクセスする場合のデータベースの一貫性を維持する方法について説明します。  
  
## <a name="Basics"></a>ロックの基本  
**モード**  
  
SQL Server PDW は、次の4つのロックモードをサポートします。  
  
排他的  
排他ロックは、排他ロックを保持しているトランザクションが完了するまで、ロックされたオブジェクトへの書き込みまたは読み取りを禁止します。 排他ロックが有効になっている間は、どのモードでも他のロックは許可されません。 たとえば、DROP TABLE と CREATE DATABASE は排他ロックを使用します。  
  
共有  
共有ロックでは、影響を受けるオブジェクトの排他ロックの開始は禁止されていますが、他のすべてのロックモードは許可されています。 たとえば、SELECT ステートメントを実行すると、共有ロックが開始されるため、複数のクエリで選択したデータに同時にアクセスできますが、読み取り中のレコードに対する更新は、SELECT ステートメントが完了するまで行われません。  
  
ExclusiveUpdate  
ExclusiveUpdate ロックは、ロックされたオブジェクトへの書き込みを禁止しますが、共有ロックを介した読み取りを許可します。 ExclusiveUpdate ロックが有効になっている間は、他のロックは許可されません。 たとえば、BACKUP DATABASE と RESTORE DATABASE では、排他的な更新ロックが使用されます。  
  
SharedUpdate  
SharedUpdate ロックでは、排他的ロックモードと ExclusiveUpdate ロックモードが禁止されており、オブジェクトで Shared モードと SharedUpdate lock モードが許可されています。 SharedUpdate はオブジェクトを変更しますが、変更中にオブジェクトへの読み取りアクセスは制限されません。 たとえば、INSERT および UPDATE では、SharedUpdate ロックが使用されます。  
  
**リソースクラス**  
  
ロックは、データベース、スキーマ、オブジェクト (テーブル、ビュー、またはプロシージャ)、アプリケーション (内部で使用)、EXTERNALDATASOURCE、EXTERNALFILEFORMAT、および SCHEMARESOLUTION (作成、変更、または作成中に取得されたデータベースレベルのロック) によって保持されます。スキーマオブジェクトまたはデータベースユーザーを削除しています。 これらのオブジェクトクラスは、 [dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)の object_type 列に表示されます。  
  
## <a name="Remarks"></a>一般的な解説  
ロックは、データベース、テーブル、またはビューに適用できます。  
  
SQL Server PDW は、構成可能な分離レベルを実装していません。 ANSI 規格で定義されている READ_UNCOMMITTED 分離レベルをサポートしています。 ただし、読み取り操作は READ_UNCOMMITTED で実行されるため、実際に発生するブロッキング操作はほとんどなく、システム内で競合が発生する可能性があります。  
  
SQL Server PDW は、基になる SQL Server エンジンに依存して、ロックと同時実行制御を実装します。 操作によって、基になる SQL Server が同じノード内でデッドロックが発生した場合、SQL Server PDW は SQL Server デッドロック検出機能を利用し、ブロックステートメントの1つを終了します。  
  
> [!NOTE]  
> SQL Server では、ロックが新しいロック要求によってブロックされるのを待機しているステートメントは許可されません。 SQL Server PDW がこのプロセスを完全に実装していません。 SQL Server PDW では、新しい共有ロックの継続的な要求によって、排他ロックに対する以前の (待機中の) 要求がブロックされることがあります。 たとえば、 **UPDATE**ステートメント (排他ロックを必要とする) は、一連の**SELECT**ステートメントに対して許可されている共有ロックによってブロックされることがあります。 ブロックされたプロセス ( [sys. dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md) dvm を確認することで識別) を解決するには、排他ロックが満たされるまで新しい要求の送信を停止します。  
  
## <a name="lock-definition-table"></a>定義テーブルのロック  
SQL Server では、次の種類のロックがサポートされています。 すべてのロックの種類をコントロールノードで使用できるわけではありませんが、コンピューティングノードでは発生する可能性があります。  
  
-   Sch-m (スキーマの安定性)。 スキーマ要素に対するスキーマの安定性ロックを保持しているセッションがある間、テーブルやインデックスなどのスキーマ要素が削除されないようにします。  
  
-   Sch-m-M (スキーマ変更)。 は、指定されたリソースのスキーマを変更する必要があるすべてのセッションによって保持される必要があります。 指定されたオブジェクトを参照している他のセッションがないことを確認します。  
  
-   S (共有)。 保持しているセッションに、リソースへの共有アクセスが許可されます。  
  
-   U (更新)。 リソース上で取得された更新ロックが、最終的に更新されることが許可されます。 これは、後で更新される可能性があるリソースが複数のセッションによってロックされるとき、一般的な形式のデッドロックが発生するのを防止するために使用します。  
  
-   X (排他)。 保持しているセッションで、リソースへの排他アクセスが許可されます。  
  
-   IS (インテント共有)。 ロック階層の下位のリソースに S ロックを配置することを示します。  
  
-   IU (インテント更新)。 ロック階層の下位のリソースに U ロックを設定するよう指定します。  
  
-   IX (インテント排他)。 ロック階層の下位のリソースに X ロックを設定するよう指定します。  
  
-   SIU (共有インテント更新)。 ロック階層の下位のリソースに更新ロックを設定する目的で、リソースへの共有アクセスを指定します。  
  
-   6 (共有インテント排他)。 ロック階層内の下位のリソースに排他ロックを取得する目的で、リソースへの共有アクセスを示します。  
  
-   UIX (更新インテント排他)。 ロック階層の下位のリソースに排他ロックを設定する目的で、リソースに保持する更新ロックを指定します。  
  
-   BU. 一括操作で使用されます。  
  
-   RangeS_S (共有キー範囲と共有リソースロック)。 シリアル化可能な範囲スキャンを示します。  
  
-   RangeS_U (共有キー範囲と更新リソースロック)。 シリアル化可能な更新プログラムのスキャンを示します。  
  
-   RangeI_N (挿入キー範囲と Null リソースロック)。 インデックスに新しいキーを挿入する前に範囲をテストするために使用されます。  
  
-   RangeI_S。 RangeI_N と S ロックの重なりによって作成されるキー範囲変換ロック。  
  
-   RangeI_U。 RangeI_N と U ロックの重複によって作成されるキー範囲変換ロック。  
  
-   RangeI_X。 RangeI_N と X ロックの重なりによって作成されるキー範囲変換ロック。  
  
-   RangeX_S。 RangeI_N と RangeS_S の重なりによって作成されるキー範囲変換ロック。 固定.  
  
-   RangeX_U。 RangeI_N と RangeS_U ロックの重なりによって作成されるキー範囲変換ロックです。  
  
-   RangeX_X (排他キー範囲と排他リソースロック)。 範囲内のキーを更新する場合に使用する変換ロックです。  
  
## <a name="see-also"></a>参照  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
