---
title: MSSQLSERVER_2530 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
ms.assetid: 5d4be07a-38a5-4b25-819c-4dcb4636cc15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8058c7c31c49935d244726bf9e8ea0ac6cfbe750
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914573"
---
# <a name="mssqlserver2530"></a>MSSQLSERVER_2530
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|2530|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC_INDEX_IS_OFFLINE|  
|メッセージ テキスト|テーブル "%.\*ls" のインデックス "%.*ls" は無効です。|  
  
## <a name="explanation"></a>説明  
 指定されたインデックスが無効になっているため、DBCC ステートメントを実行できません。 インデックスを無効にすると、そのインデックスは再構築、または削除されて再作成されるまで無効になります。  
  
## <a name="user-action"></a>ユーザーの操作  
  
1.  次のいずれかの方法を使用して、無効になっているインデックスを有効にします。  
  
    -   REBUILD 句を指定した ALTER INDEX ステートメント  
  
    -   DROP_EXISTING 句を指定した CREATE INDEX  
  
    -   DBCC DBREINDEX  
  
2.  DBCC ステートメントを再実行します。  
  
## <a name="see-also"></a>参照  
 [インデックスと制約の有効化](../indexes/enable-indexes-and-constraints.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [DBCC DBREINDEX &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dbreindex-transact-sql)  
  
  
