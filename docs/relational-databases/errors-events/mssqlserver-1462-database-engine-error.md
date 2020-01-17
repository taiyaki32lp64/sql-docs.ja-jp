---
title: MSSQLSERVER_1462 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1462 (Database Engine error)
ms.assetid: 680e9c1c-a9d6-4765-b601-956d0a83324c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d53f3e8a00d0f93ac9c1738479cec05d2f01a602
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67908574"
---
# <a name="mssqlserver1462"></a>MSSQLSERVER_1462
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|1462|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBM_DISABLED_DUE_TO_FAILED_REDO|  
|メッセージ テキスト|やり直し操作の失敗により、データベース ミラーリングが無効になっています。 再開できません。|  
  
## <a name="explanation"></a>説明  
データベース ミラーリングで、ミラーでのログ レコードの再実行に失敗しました。  
  
### <a name="possible-causes"></a>考えられる原因  
最も可能性が高い原因は、プリンシパル データベースでファイルの追加操作が完了しても、ファイル名またはディレクトリ構造がプリンシパル サーバーとミラー サーバーで異なるために、ミラー データベースで失敗したことです。  
  
## <a name="user-action"></a>ユーザーの操作  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログで、このエラーの原因を調べます。 原因を解決してデータベースでミラーリングを再開します。  
  
## <a name="see-also"></a>参照  
[データベース ミラーリング構成のトラブルシューティング &#40;SQL Server&#41;](~/database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  
