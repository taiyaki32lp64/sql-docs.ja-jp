---
title: ディスク入出力サブシステム読み取り再試行の問題の確認 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: cedf4097-5b73-4964-9935-74a101847019
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 68c8cdb91f4c850618d19b26f0125205bfd045b9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63158772"
---
# <a name="check-disk-input-output-subsystem-for-read-retry-problems"></a>ディスク I/O サブシステムの読み取り再試行の問題の確認
  このルールでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のイベント ログにエラー メッセージ 825 があるどうかを確認します。 このメッセージは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が最初の試行ではディスクからデータを読み取れなかったことを示します。 このメッセージは、ディスク I/O サブシステムに大きな問題があることを示しています。 このメッセージは、現時点では [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の問題を示していませんが、 ディスクの問題を解決しないと、データの損失やデータベースの破損につながる可能性があります。  
  
## <a name="best-practices-recommendations"></a>ベスト プラクティスと推奨事項  
 次の操作を行って、原因となっているハードウェアの問題を特定し、解決してください。  
  
-   このメッセージのエラー ログと変数テキストを確認し、問題の原因を明らかにする手掛かりを見つける。  
  
-   ディスク システムを確認する。 この問題は、ディスク、ディスク コントローラー、アレイ カード、またはディスク ドライバーに関連している可能性があります。  
  
-   ディスク システムの状態を調べる最新のユーティリティがあるかどうか、ディスクの製造元に問い合わせる。  
  
-   ドライバーの最新の更新があるかどうか、ディスクの製造元に問い合わせる。  
  
## <a name="for-more-information"></a>詳細情報  
 [MSSQLSERVER_825](../errors-events/mssqlserver-825-database-engine-error.md)  
  
 [SQL Server I/O Basics, Chapter 2](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10))  
  
  
