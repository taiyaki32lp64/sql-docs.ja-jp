---
title: Teradata の接続の種類 (SSRS) | Microsoft Docs
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: b02779c2-a6b9-453c-815f-adad53353952
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0c631b873ad32082dabe2fb268b7c4254b6d7551
ms.sourcegitcommit: 445842da7c7d216b94a9576e382164c67f54e19a
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2019
ms.locfileid: "71680878"
---
# <a name="teradata-connection-type-ssrs"></a>Teradata の接続の種類 (SSRS)
  Teradata のデータをレポートに含めるには、種類が Teradata のレポート データ ソースに基づいたデータセットが必要です。 このビルトイン データ ソースの種類は、.NET Managed Provider for Teradata データ処理拡張機能に基づいています。  
  
 このトピックの情報を使用して、データ ソースを構築してください。 手順については、「 [データ接続を追加および確認する (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)」を参照してください。  
  
##  <a name="Connection"></a> 接続文字列  
 データ ソースへの接続に使用する接続情報および資格情報については、データベース管理者に問い合わせてください。 次の接続文字列の例では、IP アドレスで指定したサーバー上の Teradata データ ソースを指定しています。  
  
```  
data source=<IP Address>  
```  
  
 接続文字列の例について詳しくは、「 [レポート ビルダーでのデータ接続、データ ソース、および接続文字列](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)」をご覧ください。  
  
##  <a name="Credentials"></a> [資格情報]  
 クエリの実行、ローカルでのレポートのプレビュー、およびレポート サーバーからのレポートのプレビューには、資格情報が必要です。  
  
 レポートをパブリッシュした後、レポートをレポート サーバーで実行するときに、データを取得するための権限が有効な状態になるように、データ ソースの資格情報を変更する必要が生じる場合があります。  
  
 詳細については、「[データ接続、データソース、および&#40;接続文字列レポートビルダー&#41;と SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) 」または「[レポートデータソースに関する資格情報と接続情報の指定](specify-credential-and-connection-information-for-report-data-sources.md)」を参照してください。  
  
  
##  <a name="Remarks"></a> 解説  
 Teradata データ ソースに接続するには、システム管理者が、Teradata からのデータの取得をサポートするバージョンの .NET Data Provider for Teradata をインストールしておく必要があります。 このデータ プロバイダーは、レポート ビルダーがインストールされているコンピューターとレポート サーバーにインストールされている必要があります。  
  
 このデータ プロバイダーでは使用できないレポート配信モードもあります。 このデータ処理拡張機能では、データ ドリブン サブスクリプションを使ったレポートの配信はサポートされません。 詳細については、「[サブスクライバー データに対して外部データ ソースを使用する (データ ドリブン サブスクリプション)](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)」を参照してください。  
  
  
##  <a name="Models"></a> レポート モデル  
 Teradata データ ソースに基づくレポート モデルからデータセットを作成するには、モデルを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] のモデル デザイナーでデザインし、レポート サーバーでパブリッシュする必要があります。  
  
  
##  <a name="Related"></a> 関連項目  
 次に示すセクションでは、レポート データの概念が詳細に説明されているほか、データに関連するレポートのパーツを定義し、カスタマイズし、使用する方法が説明されています。  
  
 [レポート データセット (SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)  
 レポートのデータへのアクセスの概要について説明します。  
  
 [レポート ビルダーでのデータ接続、データ ソース、および接続文字列](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
 データ接続とデータ ソースについて説明します。  
  
 [レポート埋め込みデータセットと共有データセット (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 埋め込みデータセットと共有データセットについて説明します。  
  
 [データセット フィールド コレクション (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 データセット クエリによって生成されるフィールド コレクションについて説明します。  
  
 [Reporting Services &#40;&#41; SSRS によってサポートされるデータソース](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)各データ拡張機能のプラットフォームとバージョンのサポートについて詳しく説明します。  
 
  
## <a name="see-also"></a>参照  
 [レポート パラメーター (レポート ビルダーおよびレポート デザイナー)](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [データのフィルター、グループ化、および並べ替え (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [式 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
