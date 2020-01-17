---
title: バックアップ タイムライン | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.SWB.POINTINTIMERESTORE.F1
- sql13.swb.backuptimeline.f1
helpviewer_keywords:
- Backup Timeline
ms.assetid: ae3565f2-ddb2-4469-a992-7531d4f9ebb8
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 30bf006998ac543b732b4aecac97280f07d36a99
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68081435"
---
# <a name="backup-timeline"></a>バックアップ タイムライン
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **[バックアップ タイムライン]** ダイアログ ボックスを使用して、特定の時点のデータベースを復元するためのバックアップを検索および指定します。 **[バックアップのタイムライン]** ダイアログ ボックスにアクセスするには、 **[データベースの復元] ([全般] ページ)** ペイン上の **[タイムライン]** をクリックします。 このダイアログ ボックスで、データベースで実行される復元操作のタイムラインを表示できます。  
  
 データベース復旧アドバイザーによって、特定の時点に復元するために必要なバックアップだけが選択されます。 これらの選択されたバックアップは、復元操作用として推奨される復元プランを示しています。 選択されたバックアップのみを使用する必要があります。 データベースの復旧アドバイザーの詳細については、「[復元と復旧の概要&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)」を参照してください。  
  
## <a name="restore-to"></a>[復元先]  
 既定では、 **[最後に作成されたバックアップ]** が選択されています。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] データベースを復元するための適切なバックアップを選択し、最後のバックアップの時点のデータベースを復元します。 **[特定の日付と時刻]** をクリックすると、手動で日時を設定できます (特定の時点を選択します)。  
  
 **[特定の日付と時刻]** では、選択した特定の日時で復元を停止できます。 タイムラインは、選択された日時の 24 時間の範囲で行われたバックアップ操作を表示します。  
  
 **日付**  
 日付を入力するか、ボックスの一覧から選択します。  
  
 **[時刻]**  
 復元を停止する特定の時点を指定する日付を入力または選択します。  
  
 **[タイムラインの間隔]**  
 タイムラインに表示される間隔の種類のオプションを表示します。  
  
## <a name="timeline-and-legend"></a>[タイムラインと凡例]  
 タイムラインの下にあるスクロール バーを使用して、タイムラインに沿ってカーソルを前後に移動させます。 バックアップをクリックすると、そのバックアップの末尾にスクロール バーが移動します。 マウス ポインターをマーカーに重ねると、選択されたバックアップ セットの情報が画面に表示されます。 バックアップの情報は、以下のマーカーによってタイムラインに表示されます。  
  
 大きい三角形  
 データベースで実行された完全バックアップを表します。これは各完全バックアップが実行された特定の時点を示します。  
  
 小さい三角形  
 データベースで実行された差分バックアップを表します。これは各差分バックアップが実行された特定の時点を示します。  
  
 緑の影の部分  
 トランザクション ログ バックアップの適用範囲を表します。  
  
 赤色の線  
 復元が可能なタイムライン上にのみ表示されます。 タイムライン上で赤色の線を動かすと、 **[日付]** および **[時刻]** ボックスに表示される日付と時刻が調整されます。  
  
## <a name="see-also"></a>参照  
 [[データベースの復元] &#40;[全般] ページ&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)  
  
  
