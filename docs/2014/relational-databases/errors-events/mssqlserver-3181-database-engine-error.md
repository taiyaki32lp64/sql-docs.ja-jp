---
title: MSSQLSERVER_3181 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3181 (Database Engine error)
ms.assetid: e6d2e716-5263-477c-ad0e-7bcbfef4c1f3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a9f7332460d3dc25c756e6bd031b1a4b3a1f6743
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62868767"
---
# <a name="mssqlserver3181"></a>MSSQLSERVER_3181
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|イベント ID|3181|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|LDDB_STORAGE_VERIFY|  
|メッセージ テキスト|このバックアップの復元を試みるとストレージ領域に問題が発生する可能性があります。 詳細については、この後のメッセージを参照してください。|  
  
## <a name="explanation"></a>説明  
 RESTORE VERIFYONLY ステートメントでは、データベースの復元先ディスクの利用可能なストレージ領域がチェックされます。  
  
### <a name="possible-causes"></a>考えられる原因  
 使用可能なディスク領域が不十分なため、確認中のバックアップを復元できない可能性があります。  
  
## <a name="user-action"></a>ユーザーの操作  
 十分なディスク領域があるドライブにバックアップを復元するか、ディスク領域を増やします。  
  
## <a name="see-also"></a>関連項目  
 [データベースを新しい場所に復元する &#40;SQL Server&#41;](../backup-restore/restore-a-database-to-a-new-location-sql-server.md)   
 [新しい場所にファイルを復元&#40;SQL Server&#41;](../backup-restore/restore-files-to-a-new-location-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql)  
  
  
