---
title: '[新しい共有スケジュール] (Management Studio) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.newschedule.f1
ms.assetid: b2c69586-d98e-4933-827d-f5e6c15c5203
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 083fa7998e347b3aa3abe7aacbf9585a18047b20
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66100226"
---
# <a name="new-shared-schedule-management-studio"></a>[新しい共有スケジュール] (Management Studio)
  このページを使用すると、パブリッシュされたレポートおよびサブスクリプションを実行するための共有スケジュールを作成できます。 共有スケジュールは、レポート固有のスケジュールやサブスクリプション固有のスケジュールの代わりに使用できます。 集中管理されるスケジュール情報と、スケジュールされた操作を一時停止して再開する機能は、アイテム固有のスケジュールと共有スケジュールを区別する 2 つの重要な機能です。  
  
 1 つのスケジュールの中で、複数の頻度を組み合わせて使用することができない場合があります。 たとえば、毎週金曜日の正午と 午後 4 時 00 分まで レポートを実行する場合、実行日を金曜日に指定した日単位のスケジュールを 2 つ作成し、1 つは開始時刻を正午に、 もう 1 つは開始時刻を午後 4 時に設定する必要があります。  
  
 スケジュールは、そのスケジュールをホストおよび処理するレポート サーバーのローカル時間に基づいて処理されます。  
  
 このページを開くには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を起動してレポート サーバーに接続し、 **[共有スケジュール]** を右クリックして **[新しいスケジュール]** をクリックします。 スケジュールを保存するには、SQL Server エージェント サービスが実行されている必要があります。  
  
> [!NOTE]  
>  この機能は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各エディションでサポートされる機能の一覧については、「[SQL Server 2012 の各エディションがサポートする機能](https://go.microsoft.com/fwlink/?linkid=232473)」(https://go.microsoft.com/fwlink/?linkid=232473) を参照してください。  
  
## <a name="options"></a>および  
 **名前**  
 共有スケジュールの名前を入力します。 この名前は、ユーザーがレポートおよびサブスクリプションの共有スケジュールを選択するときにドロップダウン リストに表示されます。 リスト内に納まり、共有スケジュールと別のスケジュールとを簡単に区別できるわかりやすい名前を付けてください。 名前には、少なくとも 1 つの英数字が含まれている必要があります。 また、スペースおよびいくつかの記号を含めることもできます。 名前を指定するときに使用できない記号は次のとおりです。  
  
 ; ? : \@ & = + , $ / * \< >  
  
 " /  
  
 **[このスケジュールの実行開始日]**  
 このスケジュールの開始日を指定します。  
  
 **[このスケジュールの終了日]**  
 このスケジュールの有効期限を指定します。  
  
 **型**  
 定期的なパターンが主に時間、日、週、または月のどれに基づくかを指定します。  
  
 **[時間] ([定期的なパターン])**  
 スケジュール設定した操作を一定時間ごとに実行する (たとえば 6 時間ごとにレポートを実行する) ためのオプションを選択します。 間隔は時間と分で指定できます。  
  
 **[日]\([定期的なパターン])**  
 スケジュール設定した操作を数日間隔で実行する (たとえば 2 日ごとにレポートを実行する) ためのオプションを選択します。 間隔は日数で指定し、スケジュールを実行する時と分を指定できます。  
  
 **[週]\([定期的なパターン])**  
 スケジュール設定した操作を毎週実行するか、繰り返しのパターンが週単位 (たとえば隔週でレポートを実行する) の場合のオプションを選択します。 週間スケジュールについて、スケジュールを実行する日、時、分を指定できます。  
  
 **[月]\([定期的なパターン])**  
 スケジュール設定した操作を毎月実行するか、繰り返しのパターンが月単位の場合のオプションを選択します。 月間スケジュールについて、スケジュールを実行する日、時、分を指定できます。 スケジュールでは特定の月を指定しなくてもかまいません。  
  
 **1 回。**  
 特定の日時に 1 回のみスケジュールを実行する場合にこのオプションを選択します。  
  
## <a name="see-also"></a>関連項目  
 [Management Studio のレポート サーバーの F1 ヘルプ](report-server-in-management-studio-f1-help.md)   
 [Management Studio でレポート サーバーに接続する](connect-to-a-report-server-in-management-studio.md)   
 [Create, Modify, and Delete Schedules](../subscriptions/create-modify-and-delete-schedules.md)   
 [[スケジュール]](../subscriptions/schedules.md)   
 [Management Studio のレポート サーバーの F1 ヘルプ](report-server-in-management-studio-f1-help.md)  
  
  
