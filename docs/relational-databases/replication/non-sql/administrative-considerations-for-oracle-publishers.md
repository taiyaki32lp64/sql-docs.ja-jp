---
title: "Oracle パブリッシャーの管理上の注意点 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Oracle publishing [SQL Server replication], administrative considerations
- administering replication, Oracle publishing
ms.assetid: cfd81fb5-419b-4a1b-97c4-be7c9d4ee289
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 058c10375ed15b5375f814199a57d032c5291018
ms.contentlocale: ja-jp
ms.lasthandoff: 06/22/2017

---
# <a name="administrative-considerations-for-oracle-publishers"></a>Oracle パブリッシャーの管理上の注意点
  Oracle データベース システムの管理者は、Oracle パブリッシャーを構成して、レプリケーションの変更追跡のメカニズムを設定した後でも、標準の Oracle データベース ユーティリティを使用したり、通常のシステム管理作業を実行したりすることができます。 しかし、特定の管理作業を実行してパブリッシュされたデータへの影響については注意する必要があります。  
  
 レプリケーション用にパブリッシュされた列の削除や変更、またはレプリケーション オブジェクトの削除や変更の場合を除いて、これらの注意点はスナップショット パブリケーションには当てはまりません。  
  
## <a name="importing-and-loading-data"></a>データのインポートと読み込み  
 Oracle 上のトランザクション パブリケーションでは、トリガーを使用して変更を追跡します。 パブリッシュされたテーブルに対する変更がサブスクライバーにレプリケートされるのは、更新、挿入、削除の際にレプリケーション トリガーが起動されたときだけです。 Oracle ユーティリティの Oracle インポートおよび SQL*Loader には、レプリケートされたテーブルにこれらのユーティリティから行を挿入したときにトリガーを起動するかどうかを指定するオプションがあります。  
  
### <a name="oracle-import"></a>Oracle インポート  
 Oracle インポートでは、 **ignore** オプションを「y」または「n」に設定できます (既定値は「n」です)。 **ignore** を「n」に設定すると、インポート時にテーブルが削除されて再作成されます。 このときレプリケーション トリガーが削除され、レプリケーションが無効になります。 **ignore** を「y」に設定すると、既存のテーブルに行が読み込まれ、レプリケーション トリガーが起動されます。 したがって、レプリケートされるテーブルに Import ツールでインポートする際には、 **ignore** を「y」に設定してください。  
  
### <a name="sqlloader"></a>SQL*Loader  
 SQL\*Loader では、**direct** オプションを「true」または「false」に設定できます (既定値は「false」です)。 **direct** を「false」に設定すると、通常の INSERT ステートメントを使用して行が挿入され、レプリケーション トリガーが起動されます。 **direct** を「true」に設定すると、読み込みが最適化され、トリガーは起動されません。 したがって、SQL*Loader ツールでレプリケートされるテーブルへの読み込みを行う際には、 **direct** を「false」に設定してください。  
  
## <a name="making-changes-to-published-objects"></a>パブリッシュされたオブジェクトに対する変更  
 以下の操作には、特別な注意は必要ありません。  
  
-   パブリッシュされたテーブルでのインデックスの再構築  
  
-   パブリッシュされたテーブルへのユーザー トリガーの追加  
  
 以下の操作では、パブリッシュされたテーブルに対するすべての操作を停止する必要があります。  
  
-   パブリッシュされたテーブルの移動  
  
 以下の操作では、パブリケーションを削除し、各操作を実行した後でパブリケーションを作成し直す必要があります。  
  
-   パブリッシュされたテーブルの切り捨て  
  
-   パブリッシュされたテーブル名の変更  
  
-   パブリッシュされたテーブルへの列の追加  
  
-   レプリケーション用にパブリッシュされた列の削除または変更  
  
-   ログに記録されない操作の実行  
  
## <a name="dropping-or-modifying-replication-objects"></a>レプリケーション オブジェクトの削除と変更  
 パブリッシャー レベルの追跡テーブル、トリガー、シーケンス、ストアド プロシージャを削除または変更するには、パブリッシャーを削除して再構成する必要があります。 これらのオブジェクトの一部の一覧については、「[Objects Created on the Oracle Publisher](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md)」 (Oracle パブリッシャーで作成されたオブジェクト) を参照してください。  
  
 パブリッシャーの削除と再構成の詳細については、「 [Troubleshooting Oracle Publishers](../../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)」の「パブリッシャーの再構成が必要になる変更」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Oracle パブリッシャーの構成](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Oracle パブリッシャーの設計上の注意点および制限](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)   
 [Oracle Publishing Overview](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  