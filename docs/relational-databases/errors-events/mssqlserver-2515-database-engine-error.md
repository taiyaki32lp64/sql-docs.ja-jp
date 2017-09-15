---
title: MSSQLSERVER_2515 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 2515 (Database Engine error)
ms.assetid: af93aa29-70c9-4923-90af-aafadb20c1c6
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: eaf2bd523ded029d2692472cc712ba4211a2eb53
ms.contentlocale: ja-jp
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver2515"></a>MSSQLSERVER_2515
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|2515|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC_DIFF_MAP_OUT_OF_SYNC|  
|メッセージ テキスト|ページ P_ID、オブジェクト ID O_ID、インデックス ID I_ID、パーティション ID PN_ID、アロケーション ユニット ID A_ID (型 TYPE) は変更されていますが、差分バックアップ ビットマップでは変更が設定されていません。|  
  
## <a name="explanation"></a>説明  
指定のページにあるログ シーケンス番号 (LSN) の値が、データベースの BackupManager 内の差分参照 LSN か、ファイルのファイル制御ブロック内の差分ベース LSN のうち、新しい方の値より大きくなっています。 ところが、差分バックアップ ビットマップでは、このページに変更が行われたことが記録されていません。  
  
このチェックは、差分ビットマップにエラーがないとわかっている場合にのみ実行されるので、報告されるのは各データベースにつき 1 ページのみです。  
  
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
> REPAIR 句を付けて DBCC CHECKDB を実行した場合にデータにどのような影響があるか確信がない場合は、ステートメントを実行する前に購入元にお問い合わせください。  
  
いずれかの REPAIR 句を付けて DBCC CHECKDB を実行しても問題が解決しない場合は、購入元にお問い合わせください。  
  
### <a name="results-of-running-repair-options"></a>REPAIR オプションの実行結果  
REPAIR を実行すると、差分ビットマップが無効になります。 データベースの完全バックアップを作成するまで、差分バックアップは実行できません。 データベースの完全バックアップにより、差分ビットマップを再構築するためのベースラインが提供されます。  
  
## <a name="see-also"></a>参照  
[データベースの完全バックアップの作成 &#40;SQL Server&#41;](~/relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
[MSSQLSERVER_2516](~/relational-databases/errors-events/mssqlserver-2516-database-engine-error.md)  
  
