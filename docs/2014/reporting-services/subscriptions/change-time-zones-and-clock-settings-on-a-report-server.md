---
title: レポート サーバーでタイム ゾーンと時計の設定を変更する | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- time zones [Reporting Services]
- clocks [Reporting Services]
- schedules [Reporting Services], clock settings
- schedules [Reporting Services], time zones
ms.assetid: 69a19468-baa1-40f6-b158-8afdab0f8968
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 566e421cd120010ea32f6936853e4319ec2efa11
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66100996"
---
# <a name="change-time-zones-and-clock-settings-on-a-report-server"></a>レポート サーバーでタイム ゾーンと時計の設定を変更する
  レポート サーバーでは、インストールされているコンピューターのローカル時刻が常に使用されます。 異なるタイム ゾーンを使用するように構成することはできません。 クライアント アプリケーションと、参照先のレポート サーバーのタイム ゾーンが異なる場合、スケジュールが設定された操作は、レポート サーバーのタイム ゾーンを使用して実行されます。 レポート マネージャーと SharePoint 管理ページの各スケジュール ページには、スケジュールが設定された操作が行われる正確な日時がわかるよう、タイム ゾーンが明記されます。 たとえば、カスタム スケジュールを作成するためのページには、"時間は (UTC-08:00) 太平洋標準時 (米国およびカナダ) で表されます" と表示されます。  
  
## <a name="changing-the-time-zone-native-mode"></a>タイム ゾーンの変更 (ネイティブ モード)  
 レポート サーバーをホストするコンピューターのタイム ゾーンを変更した場合、変更を有効にするにはレポート サーバー サービスを再起動する必要があります。  
  
 既存のレポート履歴スナップショットのタイムスタンプ値は、新しいタイム ゾーンの設定に同期されます。 午前 9 時にレポート履歴スナップショットを生成し、タイム ゾーンを 1 つ前のタイム ゾーンに再設定した場合、生成したスナップショットのタイムスタンプは午前 9 時から 午前 10 時に変わります。  
  
 スケジュールの既存の設定は残りますが、新しいタイム ゾーンにスライドされます。 たとえば、太平洋標準時の午前 2 時に スケジュールを実行している場合に、タイム ゾーンをオーストラリア東部標準時に変更すると、スケジュールはオーストラリア東部標準時の 午前 2 時に実行されます。  
  
 プロパティのタイムスタンプ値 (フォルダーまたはリンク レポート アイテムの作成日時など) は、新しいタイム ゾーンの設定に同期されません。 6 月 25 日の午前 9 時にアイテムを作成し、タイム ゾーンまたは時計の設定を変更しても、タイムスタンプは 6 月 25 日の午前 9 時のままです。  
  
## <a name="changing-the-time-zone-sharepoint-mode"></a>タイム ゾーンの変更 (SharePoint モード)  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モードのタイム ゾーンの構成は、SharePoint の地域設定の一部として管理されます。 詳細については、「[SharePoint Server 2010 SP1 の説明」(https://technet.microsoft.com/library/cc824907.aspx)](https://technet.microsoft.com/library/cc824907.aspx) を参照してください。  
  
## <a name="changing-the-clock-settings"></a>時計の設定の変更  
 内蔵時計を変更しても、既存のタイムスタンプ値に影響はありません。たとえば、時計を 1 時間進めても、レポート履歴スナップショットのタイムスタンプは変わりません。 スケジュールおよび配信のプロセッサの設定が新しく切り替わるまでに、10 秒の遅延が発生する場合があります。 構成ファイルのポーリング間隔の設定を変更した場合、実際の遅延時間が異なることがあります。  
  
## <a name="see-also"></a>参照  
 [Start and Stop the Report Server Service](../report-server/start-and-stop-the-report-server-service.md)   
 [スケジュール](schedules.md)  
  
  
