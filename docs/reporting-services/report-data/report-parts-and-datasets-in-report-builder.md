---
title: レポート ビルダーのレポート パーツおよびデータセット | Microsoft Docs
ms.date: 09/16/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: 1fe86481-9c41-4535-a4b7-c7c4d780cab6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a06344a119dfba635a07d0050a61f561065a2984
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65571195"
---
# <a name="report-parts-and-datasets-in-report-builder"></a>レポート ビルダーのレポート パーツおよびデータセット
  レポート ビルダーでレポートにデータを含める最も簡単な方法は、レポート パーツ ギャラリーからレポート パーツを追加することです。 レポート パーツには、そのレポート パーツが依存するデータセットが含まれており、 *依存データセット*と呼ばれます。 依存データセットは共有データ ソースに基づいており、埋め込みデータセットまたは共有データセットのどちらかにすることができます。 [レポート パーツ](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)の詳細を参照してください。  
  
 レポートにデータを含めるもう 1 つの簡単な方法は、共有データセットを使用することです。 詳細については、「 [レポート埋め込みデータセットと共有データセット (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)と呼ばれます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Adding"></a> 依存データセットを持つレポート パーツのレポートへの追加  
 レポート パーツをレポートに追加すると、そのレポート パーツに含まれている依存データセットもレポートに追加されます。 レポート パーツ内の四角形に、その他の多くのレポート アイテムが含まれている場合があるため、複数の依存データセットがレポートに追加される場合もあります。 各共有データセットは独立参照であるため、依存先の共有データ ソースはレポートに追加されません。 また、各埋め込みデータセットでは、依存先の埋め込みデータ ソースまたは共有データ ソースが追加されます。  
  
 埋め込みデータ ソースの資格情報は、レポート パーツの一部として保存されません。 埋め込みデータ ソースがレポートに追加されると、レポートの実行時に資格情報が要求されます。 資格情報の指定手順を省略するには、資格情報が保存されている共有データ ソースに基づいたレポート パーツを使用します。  
  
 レポート パーツをレポートに追加した後は、追加したデータセットと作成した埋め込みデータセットまたは共有データセットに違いはありません。 追加したデータセットはレポート データ ペインに表示されます。 埋め込みデータセットは対応する共有データ ソースに表示され、共有データセットは Shared Datasets フォルダーに表示されます。  
  
##  <a name="Customizing"></a> 依存データセットのカスタマイズ  
 レポート パーツをレポートに追加した後、プレビューして、データを一部変更することができます。 変更できる内容は、操作対象のデータセットの種類によって異なります。  
  
 埋め込みデータセットのデータおよびデータ オプションを変更するには、データセットを作成した場合と同様に、クエリなどのデータセット プロパティを編集します。  
  
 共有データセットのデータおよびデータ オプションを変更する場合は、十分な権限があるレポート サーバーでのみ共有データセットの定義を変更できます。 また、レポート内の共有データセットのインスタンスについても、フィルターを追加し、計算フィールドを追加し、大文字と小文字の区別などのデータ オプションを変更して、カスタマイズできます。 詳細については、「[埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md)」を参照してください。  
  
 共有データセットの定義を変更する方法、またはレポート内の共有データセットに対する最新のデータ変更内容を表示する方法の詳細については、「[共有データセットまたは埋め込みデータセットの作成 (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)」および「[レポート データ ペインでのフィールドの追加、編集、更新 (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)」を参照してください。  
  
##  <a name="Publishing"></a> 共有データセットとしての依存データセットのパブリッシュ  
 依存データセットを持つレポート アイテムをパブリッシュする場合は、共有データセットとして、またはレポート アイテムに埋め込まれたままの埋め込みデータセットとして各データセットをパブリッシュできます。  
  
 共有データセット オプションを選択した場合、データセットは共有データセット定義としてレポート サーバーに保存されます。 レポートでは、そのデータセットを使用するすべてのレポート アイテムが、現在レポート サーバー上に存在する共有データセットを指すように更新されます。 その結果、次の 2 つの処理が行われます。  
  
1.  [パブリッシュ] ダイアログ ボックスでは、パブリッシュされた各共有データセットがパブリッシュ可能なアイテムのリストから削除されます。  
  
2.  レポート ビルダーを終了したり、新規レポートを開始したりすると、レポートを保存するように求められます。 レポートを保存しない場合、次にこのレポートを開き、レポート アイテムをパブリッシュするときに、同じデータセットの新しいコピーをパブリッシュできます。 レポート サーバーに共有データセットの複数のコピーを保存したくない場合は、レポートを保存することをお勧めします。  
  
> [!IMPORTANT]  
>  共有データセットから継続して正常にデータを使用するには、レポート アイテムのセキュリティ保護の背景にある原則を理解する必要があります。 詳細については、「 [共有データセット アイテムをセキュリティで保護する](../../reporting-services/security/secure-shared-dataset-items.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [レポート デザイン ビュー (レポート ビルダー)](../../reporting-services/report-builder/report-design-view-report-builder.md)   
 [セキュリティ (レポート ビルダー)](../../reporting-services/report-builder/security-report-builder.md)   
 [レポート パーツ &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)   
 [レポート埋め込みデータセットと共有データセット (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
