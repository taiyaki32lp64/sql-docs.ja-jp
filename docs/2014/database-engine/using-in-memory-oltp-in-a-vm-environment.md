---
title: VM 環境でインメモリ OLTP の使用 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 27ec7eb3-3a24-41db-aa65-2f206514c6f9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e7f7f04b04792167fe9c4733f3e066c362f3cae4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62843065"
---
# <a name="using-in-memory-oltp-in-a-vm-environment"></a>VM 環境でのインメモリ OLTP の使用
  サーバー仮想化に伴い、各企業は IT の資本コストと運用コストを削減し、アプリケーションの準備、メンテナンス、可用性、バックアップと復旧の各プロセスを向上させることにより、IT 効率の大幅な上昇を達成しています。 最近の技術的な進歩により、仮想化を使用して、複雑なデータベース ワークロードを従来より容易に統合することができます。 ここでは、仮想化環境内での [!INCLUDE[hek_1](../includes/hek-1-md.md)] の使用に関して推奨されるベスト プラクティスについて取り扱います。  
  
##  <a name="bkmk_memoryPreAllocation"></a> メモリの事前割り当て  
 仮想化環境でのメモリに関して、パフォーマンス向上とサポート拡張は重要な考慮事項です。 仮想マシンの需要 (ピーク負荷とオフピーク負荷) に応じてメモリを迅速に仮想マシンに割り当てる能力が必須であり、メモリが浪費されていないことを確認する必要もあります。 Hyper-V 動的メモリ機能により、1 台のホスト上で実行する複数の仮想マシン間でのメモリ割り当てと管理がより迅速に行われます。  
  
 メモリ最適化テーブルを含むデータベースを仮想化する場合は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の仮想化と管理に関するいくつかのベスト プラクティスを変更する必要があります。 メモリ最適化されたテーブルが存在しない場合、次の 2 つのベスト プラクティスがあります。  
  
-   MIN_SERVER_MEMORY を使用する場合は、必要とされる量のメモリのみを割り当てる方が適切です。その結果、他のプロセス用に十分なメモリを残すことができます (その結果、ページングを回避できます)。  
  
-   メモリの事前割り当ての値を過度に大きく設定しないでください。 そうしない場合は、他のプロセスがメモリを必要とする時点で十分なメモリを取得できず、メモリのページングが発生する可能性があります。  
  
 メモリ最適化テーブルがデータベース内に含まれている場合に上記のプラクティスに従うと、データベースの復元と復旧を試みたときに、データベースを復旧するための十分なメモリが存在するにもかかわらず、データベースが "復旧の保留中" という状態にとどまる可能性があります。 その理由は、動的メモリ割り当て機能がメモリをデータベースに割り当てる場合に比べて、 [!INCLUDE[hek_2](../includes/hek-2-md.md)] は起動時により積極的にデータをメモリ内に読み込むことにあります。  
  
 **解決方法**  
  
 この問題を軽減するためには、必要に応じて追加のメモリを提供する動的メモリ機能に依存して最小限のメモリを割り当てる代わりに、データベースを復旧または再起動するために十分なメモリをデータベースに事前に割り当ててください。  
  
## <a name="see-also"></a>参照  
 [インメモリ OLTP &#40;インメモリ最適化&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
