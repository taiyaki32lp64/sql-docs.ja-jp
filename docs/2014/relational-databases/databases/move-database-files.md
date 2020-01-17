---
title: データベース ファイルの移動 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- disaster recovery [SQL Server], moving database files
- files [SQL Server], moving
- data files [SQL Server], moving
- file moving [SQL Server]
- moving full-text catalogs
- moving databases
- full-text catalogs [SQL Server], moving
- moving database files
- scheduled disk maintenance [SQL Server]
- moving files
- relocating database files
- planned database relocations [SQL Server]
- databases [SQL Server], moving
ms.assetid: 89f01b10-5fae-4ed8-b0fb-a4b9f540fd28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9544d2d2b2c505e3557d9cd0ae348b41bec5e821
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62871701"
---
# <a name="move-database-files"></a>データベース ファイルの移動
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) ステートメントの FILENAME 句で新しいファイルの場所を指定して、システムおよびユーザー データベースを移動することができます。 データ ファイル、ログ ファイル、およびフルテキスト カタログ ファイルもこの方法で移動できます。 データベース ファイルの移動は、次の状況で便利な場合があります。  
  
-   障害復旧。 たとえば、ハードウェア障害により、データベースが問題のあるモードになっている場合や、シャットダウンされた場合など。  
  
-   計画に従った再配置。  
  
-   スケジュールされたディスク メンテナンスとしての再配置。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[ユーザー データベースの移動](move-user-databases.md)|ユーザー データベース ファイルおよびフルテキスト カタログ ファイルを新しい場所に移動する手順について説明します。|  
|[システム データベースの移動](system-databases.md)|システム データベース ファイルを新しい場所に移動する手順について説明します。|  
  
## <a name="see-also"></a>参照  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [データベースのデタッチとアタッチ &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)  
  
  
