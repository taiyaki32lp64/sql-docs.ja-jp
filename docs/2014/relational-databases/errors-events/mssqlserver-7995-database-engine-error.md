---
title: MSSQLSERVER_7995 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 7995 (Database Engine error)
ms.assetid: af6d6322-3cba-43d8-be97-e6ef15f8c933
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dc99c877374228545c575558539cad5fcac1edbe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62913247"
---
# <a name="mssqlserver7995"></a>MSSQLSERVER_7995
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|7995|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC2_SYSTEM_CATALOGS_CORRUPT|  
|メッセージ テキスト|データベース 'DBNAME' : システム カタログの一貫性エラーにより、DBCC CHECKNAME 処理を続行できません。|  
  
## <a name="explanation"></a>説明  
 DBCC CHECKDB のプロセスは、次の 3 つのステージで構成されています。  
  
1.  割り当てチェック。 これは、DBCC CHECKALLOC の実行に相当します。  
  
2.  システム テーブルの一貫性チェック。 これは、少数の不可欠なシステム ベース テーブルに対して DBCC CHECKTABLE を実行することに相当します。  
  
3.  データベース全体の一貫性チェック。  
  
 ステージ 2 で MSSQLEngine_7995 が発行されました。このメッセージは、DBCC CHECKDB コマンドで修復できないエラーが検出されたか、REPAIR が指定されていないことを示しています。 問題のシステム ベース テーブルにデータベース内のすべてのオブジェクトのメタデータが格納されているか、システム ベース テーブルが破損しているため、DBCC CHECKDB はステージ 3 に進むことができません。  
  
## <a name="user-action"></a>ユーザーの操作  
  
### <a name="look-for-hardware-failure"></a>ハードウェア障害を調査する  
 ハードウェアの診断を実行し、問題があれば修正します。 また、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows のシステム ログとアプリケーション ログ、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー ログを調査し、ハードウェア障害の結果としてエラーが発生しているかどうかを確認します。 ログに記録されているハードウェアに関する問題があれば、それを修正します。  
  
 データ破損の問題が解決しない場合は、ハードウェア コンポーネントを他のものと交換し、問題の原因を特定するようにしてください。 システムで、ディスク コントローラーの書き込みキャッシュが有効になっていないことを確認します。 書き込みキャッシュが問題と思われる場合は、ハードウェア ベンダーにお問い合わせください。  
  
 それでも問題が解決しない場合は、新しいハードウェア システムの導入をご検討ください。 導入の際には、ディスク ドライブの再フォーマットとオペレーティング システムの再インストールが必要になる場合があります。  
  
### <a name="restore-from-backup"></a>バックアップから復元する  
 問題がハードウェアに関するものではなく、また既知のクリーン バックアップがある場合は、そのバックアップを使用してデータベースを復元します。  
  
### <a name="run-dbcc-checkdb"></a>DBCC CHECKDB の実行  
 クリーン バックアップがない場合には、REPAIR 句を付けずに DBCC CHECKDB を実行して破損の程度を調べます。 DBCC CHECKDB によって使用が推奨される REPAIR 句が表示されたら、 適切な REPAIR 句を付けて DBCC CHECKDB を実行し、破損を修復します。  
  
> [!CAUTION]  
>  REPAIR 句を付けて DBCC CHECKDB を実行した場合にデータにどのような影響があるか確信がない場合は、ステートメントを実行する前に購入元にお問い合わせください。  
  
 いずれかの REPAIR 句を付けて DBCC CHECKDB を実行しても問題が解決しない場合は、購入元にお問い合わせください。  
  
### <a name="results-of-running-repair-options"></a>REPAIR オプションの実行結果  
 エラーの一覧を調べて、REPAIR によって個々のエラーに対して何が行われるかを確認してください。  
  
  
