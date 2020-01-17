---
title: '[サブスクリプションの検証オプション] (マージ サブスクリプション) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.validate.mergeoptions.f1
helpviewer_keywords:
- Subscription Validation Options dialog box
ms.assetid: 4958c4ab-2025-42ce-b836-6fb4e9e6f24d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7d7631df4a1e4c6ec37effbc06b6a141b0d41ebc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63249293"
---
# <a name="subscription-validation-options-merge-subscriptions"></a>[サブスクリプションの検証オプション]\(マージ サブスクリプション)
  **[サブスクリプションの検証オプション]** ダイアログ ボックスを使用すると、検証の際に行数だけを使用するか、行数とバイナリ チェックサムを使用するかを指定できます。  
  
## <a name="options"></a>および  
 **[行数のみを確認する]**  
 選択すると、サブスクライバー側のテーブルとパブリッシャー側のテーブルの行数が同じかどうかを確認できます。 この方法では、行の内容が一致するかどうかは確認されません。 行数の確認は、データに問題があるかどうかを調べる手軽な検証方法です。  
  
 **[行数を確認し、行データを評価するためにチェックサムを比較する (すべてのサブスクライバーは SQL Server 2000 以降を実行しているサーバー)]**  
 パブリッシャーとサブスクライバーの行数に加え、バイナリ チェックサム アルゴリズムを使用して、すべてのデータのチェックサムが計算されます。 行数の検証で失敗となった場合、チェックサムは実行されません。 このオプションは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)]では無効です。  
  
## <a name="see-also"></a>参照  
 [サブスクライバーでのデータの検証](validate-data-at-the-subscriber.md)   
 [レプリケートされたデータの検証](validate-data-at-the-subscriber.md)  
  
  
