---
title: トランザクション レプリケーションのアーティクル オプション | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], transactional replication options
- transactional replication, article options
ms.assetid: 3469b185-0ea5-4690-a71c-717230d886b6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 992b479ea0867aef1ca75e42cc865db2cc5a735f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63268651"
---
# <a name="article-options-for-transactional-replication"></a>トランザクション レプリケーションのアーティクル オプション
  トランザクション パブリケーションには、アーティクルのためのオプションがいくつかあります。 たとえば、トランザクション レプリケーションでは次のようなことが可能です。  
  
-   パブリッシャーからサブスクライバーに変更を反映する方法を指定できます。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。  
  
-   ストアド プロシージャの実行をレプリケートするように指定できます。 これは、大量のデータに影響を与えるメンテナンス用ストアド プロシージャの結果をレプリケートする場合に便利です。 詳細については、「 [Publishing Stored Procedure Execution in Transactional Replication](publishing-stored-procedure-execution-in-transactional-replication.md)」をご覧ください。  
  
-   制約やトリガーをサブスクライバーにコピーするかどうかなど、スキーマ オプションを指定します。 詳細については、「 [スキーマ オプションの指定](../publish/specify-schema-options.md)」を参照してください。  
  
-   行フィルターや列フィルターを使用できます。 テーブル アーティクルをフィルター選択すると、パブリッシュされるデータのパーティションを作成できます。 詳細については、「[パブリッシュされたデータのフィルター選択](../publish/filter-published-data.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [データとデータベース オブジェクトのパブリッシュ](../publish/publish-data-and-database-objects.md)  
  
  
