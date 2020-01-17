---
title: レポート実行の確認 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- auditing [Reporting Services]
- verifying report execution
- logs [Reporting Services], verifying report run
- report execution data [Reporting Services]
- status information [Reporting Services]
- report processing [Reporting Services], verifying execution
- checking report execution
ms.assetid: 18a98f2f-6b40-454e-9b37-568ed1a96458
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cd48861b53b6b7f159d4421bd86bf024838fbaf7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580074"
---
# <a name="verifying-a-report-run"></a>レポート実行の確認
  レポート処理の状態に関する情報を表示するには、ログ ファイルを使用するか、またはレポート マネージャーでレポートと共に表示される状態の情報を参照します。  
  
## <a name="sources-of-report-execution-data"></a>レポート実行のデータ ソース  
 レポート実行ログには、レポート名、レポートを実行したユーザー名、レポート実行時間、レポートの配信に使用された配信拡張機能などの、レポート実行に関する包括的な情報が提供されます。 このデータを表示または分析するには、レポート実行ログをデータベース テーブルにコピーします。データベース テーブルでは、クエリの実行やレポートの作成を簡単に行うことができます。  
  
 ログ ファイルには、レポート実行および他のサーバー操作に関する多くのエントリが含まれます。 ログ ファイルには非常に多くのデータが含まれるので、レポートの最終実行日時のみを確認する場合は、レポート マネージャーを使用することをお勧めします。 さらに情報が必要な場合は、ログ ファイルを表示する必要があります。  
  
> [!NOTE]  
>  レポート マネージャーでは、要求時に実行されるレポートの処理時間は表示されません。  
  
 次の表では、さまざまな種類のレポートでの処理日時を表示する方法を説明します。  
  
|レポートの種類|日時情報の参照先|情報の表示に必要な操作|  
|-----------------------------|-----------------------------------------------|-----------------------------------------------|  
|レポート スナップショットとして実行するレポート|[コンテンツ] ページにあります。 詳細については、「[[コンテンツ] ページ &#40;レポート マネージャー&#41;](https://msdn.microsoft.com/library/6b16869b-158a-4934-9c85-bee934b35378)」を参照してください。|1) レポートが含まれているフォルダーを見つけます。<br /><br /> 2) フォルダーを詳細表示にします。<br /><br /> 3) **[実行時]** 列の日時を記録します。|  
|レポート履歴のスナップショット|[履歴] プロパティ ページにあります。 詳細については、「[[スナップショット オプション] プロパティ ページ &#40;レポート マネージャー&#41;](https://msdn.microsoft.com/library/f6641f59-5267-4f57-8957-63b93d1a9679)」を参照してください。|1) レポートを開きます。<br /><br /> 2) **[プロパティ]** ページをクリックします。<br /><br /> 3) **[履歴]** タブをクリックします。<br /><br /> 4) **[実行時]** 列の日時を記録します。|  
|キャッシュされたレポート|キャッシュされたレポートの作成および更新に使用するスケジュールに含まれています。|1) レポートを開きます。<br /><br /> 2) **[プロパティ]** ページをクリックします。<br /><br /> 3) **[実行]** タブをクリックします。<br /><br /> 4) スケジュールを開きます。|  
  
## <a name="see-also"></a>参照  
 [Reporting Services のログ ファイルとソース](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)   
 [レポート処理プロパティの設定](../../reporting-services/report-server/set-report-processing-properties.md)   
 [レポート マネージャー &#40;SSRS ネイティブ モード&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)  
  
  
