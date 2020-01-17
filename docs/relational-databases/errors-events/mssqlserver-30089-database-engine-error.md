---
title: MSSQLSERVER_30089 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9992 (Database Engine error)
ms.assetid: 188e5bde-6865-4740-a2b2-582be8f55c77
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 981d0079cb6b0ce8cf423bf44e382cca119ed477
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001945"
---
# <a name="mssqlserver30089"></a>MSSQLSERVER_30089
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|30089|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|IFTS_FDHOST_TERMINATEDABNORMAL|  
|メッセージ テキスト|フルテキスト フィルター デーモン ホスト (FDHost) プロセスが異常停止しました。 この問題は、ワード ブレーカー、ステマー、フィルターなどの言語コンポーネントの不適切な構成または誤動作が原因で、フルテキスト インデックスの作成中またはクエリの処理中に回復不可能なエラーが生じた場合に発生することがあります。 プロセスは自動的に再開されます。|  
  
## <a name="explanation"></a>説明  
何らかの問題が発生したため、フルテキスト フィルター デーモン ホストが異常停止しました。 問題の原因として、不適切な形式のドキュメント、フィルターやワード ブレーカーのバグ、フィルター デーモンの問題などが考えられます。  
  
## <a name="user-action"></a>ユーザーの操作  
通常、デーモンはエラーから回復します。 デーモンのエラーが継続する場合は、トラブルシューティングが必要になります。 問題を切り離すために、次の操作を試みてください。  
  
1.  新しい言語コンポーネントを最近インストールした場合は、そのコンポーネントをシステムから削除します。  
  
2.  クロール ログを調べて、フルテキスト インデックスの作成に失敗した新しいドキュメントがあるか確認します。該当するドキュメントがあれば、それを削除します。  
  
## <a name="see-also"></a>参照  
[sp_help_fulltext_system_components &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)  
[検索用のワード ブレーカーとステミング機能の構成と管理](~/relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)  
[検索用フィルターの構成と管理](~/relational-databases/search/configure-and-manage-filters-for-search.md)  
  
