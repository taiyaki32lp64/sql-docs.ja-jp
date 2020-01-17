---
title: MSSQLSERVER_2576 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2576 (Database Engine error)
ms.assetid: b727cc2f-c76c-46f8-bbbe-5e7a05a6eabf
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 26e5e3cbf02191edd84b26505120ee2470e65d24
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62868936"
---
# <a name="mssqlserver2576"></a>MSSQLSERVER_2576
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|2576|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC_IAM_PARENT_PAGE_WAS_NOT_SEEN|  
|メッセージ テキスト|オブジェクト ID O_ID、インデックス ID I_ID、パーティション ID PN_ID、アロケーション ユニット ID A_ID (型 TYPE) の IAM ページ P_ID2 の前のポインターは、IAM (Index Allocation Map) ページ P_ID1 を指していますが、スキャンでは見つかりませんでした。|  
  
## <a name="explanation"></a>説明  
 Index Allocation Map (IAM) ページへの参照が、IAM チェーン内の別の IAM ページに前ページ リンクとして存在しますが、この IAM ページまたはメタデータのエントリが見つかりませんでした。 *P_ID1* ページが (0:0) であれば、IAM ページ *P_ID2* が IAM チェーンの開始であり、この IAM チェーンのメタデータ エントリがありません。  
  
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
 REPAIR を実行すると、*P_ID2* ページを含んでいる IAM チェーンの再構築が試行されます。 チェーンの再構築時には、チェーンからページが削除される場合や、メタデータが破損していればチェーン全体が削除される場合があります。  
  
> [!CAUTION]  
>  この修復を実行すると、データが失われることがあります。  
  
  
