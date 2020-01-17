---
title: MSSQLSERVER_2577 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2577 (Database Engine error)
ms.assetid: f53256a2-2fb0-47fd-9ed9-c45389104145
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7fb2c67a1d2e0ea80f0fb54c0136831109a9c3f3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023066"
---
# <a name="mssqlserver2577"></a>MSSQLSERVER_2577
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|2577|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC_IAM_CHAIN_SEQUENCE_OUT_OF_ORDER|  
|メッセージ テキスト|オブジェクト ID O_ID、インデックス ID I_ID、パーティション ID PN_ID、アロケーション ユニット ID A_ID (型 TYPE) の IAM (Index Allocation Map) チェーン内のチェーン シーケンス番号が間違っています。 シーケンス番号 SEQUENCE1 のページ P_ID1 がシーケンス番号 SEQUENCE2 のページ P_ID2 を指しています。|  
  
## <a name="explanation"></a>説明  
個々の IAM (Index Allocation Map) ページにはすべて、シーケンス番号が付けられています。 シーケンス番号は、IAM チェーン内における IAM ページの位置を表します。 シーケンス番号には、IAM ページごとに値が 1 ずつ増加するという規則があります。 IAM ページ *P_ID2* には、この規則に従わないシーケンス番号が付けられています。  
  
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
REPAIR を実行すると、IAM チェーンが再構築されます。 REPAIR はまず、既存の IAM チェーンを半分ずつに分割します。 チェーンの前半は IAM ページ *P_ID1* で終わります。 *P_ID1* ページの次ページ ポインターは、(0:0) に設定されます。 チェーンの後半は IAM ページ *P_ID2* から始まります。 *P_ID2* ページの前ページ ポインターは、(0:0) に設定されます。  
  
次に REPAIR は、この 2 つのチェーンを接続し、IAM チェーンのシーケンス番号を再生成します。 修復できない IAM ページがあれば、その割り当ては解除されます。  
  
> [!CAUTION]  
> この修復を実行すると、データが失われることがあります。  
  
