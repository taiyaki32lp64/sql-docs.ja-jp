---
title: 開始または PowerPivot を SharePoint サーバーの停止 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e38e6366-9f20-4db0-b2a8-da7d5adf00eb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 312afc0336405ca530f731ad4fec55a26a960e7a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071046"
---
# <a name="start-or-stop-a-powerpivot-for-sharepoint-server"></a>PowerPivot for SharePoint サーバーの開始または停止
  PowerPivot System サービスおよび[!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]インスタンスは、SharePoint ファーム内の連携要求とデータ処理をサポートするために、同じローカル アプリケーション サーバーで同時に動作します。  
  
 このトピックには、次のセクションが含まれます。  
  
 [サービスの依存関係](#dependencies)  
  
 [サービスの開始または停止](#startstop)  
  
 [PowerPivot サーバーの停止の影響](#effects)  
  
##  <a name="dependencies"></a> サービスの依存関係  
 PowerPivot System サービスには、同じ物理サーバーに一緒にインストールされているローカル Analysis Services サーバー インスタンスに対する依存関係があります。 PowerPivot System サービスを停止する場合は、ローカル Analysis Services サーバー インスタンスも手動で停止する必要があります。 一方のサービスのみが実行されている場合は、PowerPivot データの処理で要求割り当てエラーが発生します。  
  
 Analysis Services サーバーを単独で実行するのは、問題の診断またはトラブルシューティングを行う場合だけにしてください。 それ以外の場合は、同じサーバーでローカルに実行される PowerPivot System サービスが必要です。  
  
##  <a name="startstop"></a> サービスの開始または停止  
 PowerPivot System サービスまたは Analysis Services サーバー インスタンスを開始または停止するには、必ずサーバーの全体管理を使用します。 サーバーの全体管理を使用すると、同じページからサービスの開始または停止をまとめて実行できます。 また、サーバーの全体管理では、実行する必要があると思われるサービスを再起動するために、 **[1 つ以上のサービスが開始または停止されています]** というタイマー ジョブが使用されます。 SharePoint 以外のツールを使用して PowerPivot System サービスまたは Analysis Services を停止した場合は、タイマー ジョブの実行時にサービスが再起動されます。  
  
 サービスの開始および停止は、物理サービス インスタンスに適用される操作です。 ファーム内に追加の PowerPivot for SharePoint サーバーがある場合、ファーム内の他のサーバーは、PowerPivot データに対する要求の受け入れを続行します。  
  
 ファーム全体のすべての物理サービスを同時に開始または停止することはできません。 各サーバーを選択してから、特定のサービスを開始または停止する必要があります。  
  
 特定の Web アプリケーションに対する PowerPivot System サービスを開始、一時停止、または停止することはできませんが、サービスを既定の接続リストから削除して使用できない状態にすることができます。 詳細については、次を参照してください。[サーバーの全体管理で SharePoint Web アプリケーションへの PowerPivot サービス アプリケーションの接続](connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md)します。  
  
1.  サーバーの全体管理で、 **[システム設定]** の **[サーバーのサービスの管理]** をクリックします。  
  
2.  ページの上部にある [サーバー] の下矢印をクリックし、 **[サーバーの変更]** をクリックします。  
  
3.  開始または停止する PowerPivot System サービスまたは [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] インスタンスがある SharePoint サーバーを選択します。  
  
4.  サービスを選択し、アクションをクリックします。 サービスはペアで開始または停止することを忘れないでください。 PowerPivot System サービスを開始または停止する場合は、同じコンピューターで実行される Analysis Services サーバー インスタンスも開始または停止する必要があります。  
  
##  <a name="effects"></a> PowerPivot サーバーの停止の影響  
 次の表に、SharePoint サーバーでの PowerPivot System サービスおよび Analysis Services サービスの停止の影響を示します。  
  
|影響を受ける対象|説明|  
|---------------|-----------------|  
|既存のクエリ|Analysis Services サーバーで処理されているクエリは直ちに停止します。 ユーザーは、データまたはデータ ソース接続が見つからないことを示すエラーを受け取ります。|  
|現在処理中の既存のデータ更新ジョブ|現在の Analysis Services サーバーで処理されているジョブは直ちに停止します。 データ更新が失敗し、データ更新の履歴にエラーが記録されます。<br /><br /> SharePoint サーバーの全体管理の [ジョブの状態の確認] ページを使用することにより、サービスを停止する前に現在のジョブの状態を表示できます。<br /><br /> 現在処理中のジョブを確認することはできますが、キュー自体を表示して、他のジョブが開始されようとしているかどうかを確認することはできません。|  
|キュー内の既存のデータ更新要求|スケジュール設定されたデータ更新要求は、スケジュールのサイクル全体にわたって処理キューに残ります (つまり、次の開始時間までキューに残ります)。 PowerPivot System サービスがそのときまでに再起動されなかった場合、データ更新要求は削除され、エラーがログに記録されます。|  
|新しいクエリ要求またはデータ更新要求|ファーム内の PowerPivot for SharePoint サーバーのみを停止した場合、PowerPivot データに対する新しい要求は処理されません。データを要求すると、データが見つからないことを示すエラーが発生します。<br /><br /> ファーム内に追加の PowerPivot for SharePoint サーバーがある場合、要求は使用可能なサーバーのうちの 1 つに送信されます。|  
|使用状況データ|使用状況データは、サービスの停止中は収集されません。|  
  
## <a name="see-also"></a>参照  
 [PowerPivot サービス アカウントの構成](configure-power-pivot-service-accounts.md)  
  
  
