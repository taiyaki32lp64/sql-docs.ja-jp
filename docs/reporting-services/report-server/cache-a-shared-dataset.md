---
title: 共有データセットのキャッシュ | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.assetid: c2d8c81a-da1e-4a8a-9845-fff9a0903d24
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7e98e5ffd8970806e2ed92e53c8e82da21387938
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65574765"
---
# <a name="cache-a-shared-dataset"></a>共有データセットのキャッシュ
  パフォーマンスを向上させる方法の 1 つに、共有データセットのキャッシュ プロパティを構成するという方法があります。 共有データセットをキャッシュに格納した場合、クエリ結果のコピーが指定の時間、保存されます。 共有データセットを使用するレポートを要求した 1 人目のユーザーは、クエリ結果とすべての処理が完了しないとレポートを閲覧できません。 それ以降、同じレポートを要求したユーザーは、キャッシュの保持時間内であれば、クエリと処理が既に完了しているため、すぐにレポートを閲覧できます。 キャッシュ更新計画を指定してクエリを実行し、指定したキャッシュ有効期限まで結果をキャッシュしておくこともできます。  
  
 共有データセットまたはキャッシュ更新計画に基づいてレポートを実行するユーザーは、クエリ キャッシュを作成します。どちらの場合も、キャッシュ有効期限オプションに基づいてキャッシュを使用できます。  
  
 キャッシュできる共有データセットの種類には制限があります。 たとえば、データがユーザー ID によって異なる場合や、レポートを要求したユーザーのセキュリティ トークンを使ってデータが取得される場合、クエリ結果をキャッシュすることはできません。 詳細については、「[共有データセットのキャッシュ &#40;SSRS&#41;](../../reporting-services/report-server/cache-shared-datasets-ssrs.md)」と「[レポートのキャッシュ &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)」を参照してください。  
  
### <a name="to-schedule-the-expiration-of-a-cached-report"></a>キャッシュされたレポートの有効期限をスケジュールするには  
  
1.  [レポート マネージャー &#40;SSRS ネイティブ モード&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896) を開始します。  
  
2.  レポート マネージャーで、キャッシュ プロパティを設定する共有データセットに移動し、アイテムの上にマウス ポインターを移動して、下矢印をクリックします。  
  
3.  ドロップダウン メニューの **[管理]** をクリックします。  
  
4.  左フレームの **[キャッシュ]** をクリックします。  
  
    > [!NOTE]  
    >  **「共有データセットを実行するための資格情報が保存されていません」** というエラーが発生する場合は、共有データセットのキャッシュ オプションが無効になっています。 資格情報を保存するようにデータ ソースを変更するか、または資格情報が保存されている別のデータ ソースを使用するように共有データセットを変更する必要があります。  
  
5.  **[共有データセットのキャッシュ]** をクリックします。  
  
6.  30 分後にキャッシュが期限切れになるようにオプションを選択します。 キャッシュが指定のスケジュールに従って期限切れになるように選択することもできます。  
  
7.  **[適用]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [共有データセットを管理する](../../reporting-services/report-data/manage-shared-datasets.md)  
  
  
