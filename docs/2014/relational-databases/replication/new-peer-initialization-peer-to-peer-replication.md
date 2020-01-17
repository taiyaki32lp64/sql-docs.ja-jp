---
title: '[新しいピアの初期化] (ピア ツー ピア レプリケーション) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.p2pwizard.init.f1
ms.assetid: 050c00e1-78bd-4d9c-affe-40e22feb4d94
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 51e5ec3832d497f342c4fc3132a75261f6c3c154
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63022689"
---
# <a name="new-peer-initialization-peer-to-peer-replication"></a>[新しいピアの初期化] \(ピア ツー ピア レプリケーション)
  **[新しいピアの初期化]** ページを使用すると、ピア データベースを初期化する方法を指定できます (ピアはこのウィザードが完了する前に初期化する必要があります)。ピアは、手動、またはトランザクション レプリケーションが提供する " **バックアップを使用した初期化** " 機能を使用して初期化されます (ピア ツー ピア トランザクション レプリケーションは、スナップショットを使用するピアの初期化をサポートしません)。異なるピアを個別の手段で初期化する必要がある場合は、ウィザードを複数回実行してピアを個別に追加する必要があります。  
  
## <a name="options"></a>および  
 **[新しいピア データベースを初期化した方法を指定してください。]**  
 パブリッシュされたすべてのオブジェクトのスキーマとデータは、各ピアに存在する必要があります。 以下のオプションの 1 つを選択します。  
  
-   パブリッシュされたオブジェクトのスキーマを手動で作成した場合、またはバックアップを復元してから、バックアップ後の最初のパブリケーション データベースでデータを変更していない場合は、最初のオプションを選択します。 スキーマを手動で作成した場合は、すべての必要なデータが各ピアに存在することを確認してください。 このオプションは、サブスクリプションのプロパティ **sync_type** の **[レプリケーションのサポートのみ]** の値に相当します。  
  
-   バックアップを復元してから、バックアップ後の最初のパブリケーション データベースでデータを変更した場合は、2 番目のオプションを選択します。 このとき、レプリケーションは、最初のパブリケーション データベースからバックアップされていない変更を配信する必要があります。 このオプションは、サブスクリプションのプロパティ **sync_type** の **[バックアップ ファイルからの初期化を許可]** の値に相当します。  
  
     パブリケーションがピア ツー ピア レプリケーションに対して有効になっている場合は、パブリケーションの **allow_initialize_from_backup** プロパティが設定されています。 レプリケーションは、すぐに最初のパブリケーション データベースに加えた変更の追跡を開始します。 そのため、 **バックアップを使用した初期化** オプションを選択した場合は、これらの変更は 1 つまたは複数のピアにある復元されたデータベースに配信されます。 **[参照]** ボタンをクリックして使用するバックアップを選択すると、レプリケーションはバックアップからログ シーケンス番号 (LSN) を読み取ります。 より大きな LSN を持つ最初のパブリケーション データベースのすべての変更が、各ピアに配信されます。  
  
     [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]を含むトポロジを作成するか、そのようなトポロジに追加する場合は、このオプションは使用できないことがあります。 次の表に、既存のトポロジにノードを追加する場合にこのオプションを使用できるかどうかを示します。  
  
    |新しいノード|最初のノード|追加のノード|オプション|  
    |--------------|----------------|----------------------|------------|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Disabled|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|なし|Disabled|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Disabled|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|なし|有効|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|なし|有効|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|有効|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|なし|有効|  
  
## <a name="see-also"></a>関連項目  
 [ピア ツー ピア トポロジの管理 &#40;レプリケーション Transact-SQL プログラミング&#41;](administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [@loopback_detection](transactional/peer-to-peer-transactional-replication.md)  
  
  
