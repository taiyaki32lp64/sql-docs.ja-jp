---
title: MSSQLSERVER_3961 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3961 (Database Engine error)
ms.assetid: 3bbc6965-6445-400c-940a-2d85b037513f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f12e70423905a78eddecb93a8b4623c96a6f0322
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914084"
---
# <a name="mssqlserver3961"></a>MSSQLSERVER_3961
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|3961|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|XACT_METADATA_INVALID|  
|メッセージ テキスト|データベース '%.*ls' でスナップショット分離トランザクションが失敗しました。ステートメントからアクセスされるオブジェクトが、このトランザクションの開始後に別の同時トランザクションの DDL ステートメントで変更されました。  メタデータはバージョン管理されないため、この操作は許可されません。 メタデータに対する同時更新は、スナップショット分離と組み合わせると一貫性を損なう結果になる可能性があります。|  
  
## <a name="explanation"></a>説明  
 このエラーは、スナップショット分離下でメタデータに対してクエリを実行している場合に、スナップショット分離下でアクセスされているメタデータを更新する同時実行 DDL ステートメントが存在すると発生する可能性があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、メタデータのバージョン管理はサポートされません。 そのため、スナップショット分離下で実行されている明示的なトランザクションでは、実行できる DDL 操作に制限があります。 暗黙的なトランザクションとは、原則的に、DDL ステートメントでもスナップショット分離のセマンティックを適用することのできる単一のステートメントをいいます。 スナップショット分離下では、BEGIN TRANSACTION ステートメントの後に、ALTER TABLE、CREATE INDEX、CREATE XML INDEX、ALTER INDEX、DROP INDEX、DBCC REINDEX、ALTER PARTITION FUNCTION、ALTER PARTITION SCHEME などの DDL ステートメントを実行することはできません。共通言語ランタイム (CLR) の DDL ステートメントも同様です。 暗黙的なトランザクション内でスナップショット分離を使用している場合は、これらのステートメントが許可されます。 暗黙的なトランザクションとは、原則的に、DDL ステートメントでもスナップショット分離のセマンティックを適用することのできる単一のステートメントをいいます。  
  
## <a name="user-action"></a>ユーザーの操作  
 スナップショット分離レベルをスナップショット以外の分離レベル (メタデータに対してクエリを実行する前の READ COMMITTED など) に変更します。  
  
  
