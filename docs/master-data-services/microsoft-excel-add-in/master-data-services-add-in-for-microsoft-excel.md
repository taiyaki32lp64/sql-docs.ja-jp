---
title: Microsoft Excel 用マスター データ サービス アドイン | Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 07/25/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 33d9c8fc-9602-494d-b9ab-8f0f42785974
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ec72b2bd94d1ac7fbf68943be3081f39ed2d3e1e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68074590"
---
# <a name="master-data-services-add-in-for-microsoft-excel"></a>Microsoft Excel 用マスター データ サービス アドイン

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]では、フィルター処理したデータ リストを MDS から Excel に読み込んで、そのデータを他のデータと同様に Excel で操作することができます。 完了したら、データをパブリッシュして一元的な格納場所の MDS に戻すことができます。 セキュリティによって、表示および更新できるデータを決定します。  
  
 管理者の場合は、 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] を使用してエンティティおよび属性を作成し、それらにデータを読み込みます。 これにより、他のツールを使用してデータをモデルに読み込む必要がなくなります。  
  
 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]では、Data Quality Services (DQS) を使用して、MDS に読み込む前にデータを照合できます。 これにより、MDS 内のデータの重複を防ぐことができます。  

## <a name="downloads"></a>ダウンロード 
>*  [この Microsoft ダウンロード センター ページ](https://www.microsoft.com/download/details.aspx?id=56838)から SQL Server 2016 SP2 の Excel 用マスター データ サービス アドインをダウンロードします。 
>* [この Microsoft ダウンロード センター ページ](https://go.microsoft.com/fwlink/?linkid=836867)から SQL Server 2017 の [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] をダウンロードします。
>*  SQL Server 2019 CTP の Excel 用マスター データ サービス アドインをダウンロード[この Microsoft ダウンロード センター ページ](https://go.microsoft.com/fwlink/?linkid=2086948)します。 
 
  
## <a name="terms"></a>用語  
 アドインを使用するときに、次の用語を目にすることがあります。 詳細については、「[マスター データ サービスの概要 (MDS)](../../master-data-services/master-data-services-overview-mds.md)」を参照してください。  
  
-   *MDS repository* : すべてのマスター データが格納されている場所。 MDS データを格納するように構成されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースです。 リポジトリのデータを操作するには、そのデータを Excel に読み込みます。操作が完了したら、変更をパブリッシュしてリポジトリに戻します。 管理者は、新しいエンティティと属性をリポジトリに追加できます。  
  
-   *"MDS によって管理されるデータ"* は、MDS リポジトリに格納されているデータです。Excel に読み込むと、このデータ行は強調表示されます。 MDS によって管理されないデータをワークシートに追加できます。このようなデータは、MDS によって管理されるデータの更新時に影響を受けません。  
  
-   *model* : データのコンテナー。 複数のバージョンのコンテナーを作成することができ、通常は最後のバージョンが最新になります。 詳細については、「[モデル (マスター データ サービス)](../../master-data-services/models-master-data-services.md)」を参照してください。  
  
-   *entity* : データのリスト。 エンティティは、データベースのテーブルと考えることができます。 たとえば、 **Color** エンティティには色のリストが含まれます。 詳細については、「[エンティティ (マスター データ サービス)](../../master-data-services/entities-master-data-services.md)」を参照してください。  
  
-   *member* は 1 行のデータ (1 レコード) です。 各エンティティにはメンバーが含まれます。 たとえば、メンバーは **Blue**などです。 詳細については、「[バージョン (マスター データ サービス)](../../master-data-services/members-master-data-services.md)」を参照してください。  
  
-   *attribute* : データの列。 各メンバーには属性が含まれます。 たとえば、**Blue** メンバーの **Code** 属性は **B** です。属性の詳細については、「[属性 (マスター データ サービス)](../../master-data-services/attributes-master-data-services.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] リポジトリへの接続を作成します。|[MDS リポジトリへの接続 &#40;Excel 用 MDS アドイン&#41;](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md)|  
|MDS によって管理されるデータを Excel に読み込みます。|[マスター データ サービスから Excel へのデータのエクスポート](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)|  
|現在表示されている MDS によって管理されるデータを後で開くために使用できるショートカット クエリを保存します。|[ショートカット クエリ ファイルの保存 &#40;Excel 用 MDS アドイン&#41;](../../master-data-services/microsoft-excel-add-in/save-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|ショートカットを他のユーザーと共有します。|[ショートカット クエリ ファイルの電子メールでの送信 &#40;Excel 用 MDS アドイン&#41;](../../master-data-services/microsoft-excel-add-in/email-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|メンバーに加えられたすべての変更を表示します。|[メンバーのすべての注釈またはトランザクションの表示 &#40;Excel 用 MDS アドイン&#41;](../../master-data-services/microsoft-excel-add-in/view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)|  
|新しいデータをパブリッシュする前に、重複が存在するかどうかを調べます。|[類似データの照合 &#40;MDS Excel 用 MDS アドイン&#41;](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md)|  
|ワークシートから MDS リポジトリにデータをパブリッシュします。|[Excel からマスター データ サービスにデータをインポートする &#40;Excel 用 MDS アドイン&#41;](../../master-data-services/microsoft-excel-add-in/import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)|  
|ワークシート内のデータを含む新しいエンティティを作成します (管理者のみ)。|[エンティティの作成 &#40;Excel 用 MDS アドイン&#41;](../../master-data-services/microsoft-excel-add-in/create-an-entity-mds-add-in-for-excel.md)|  
|制約リストとも呼ばれるドメイン ベースの属性を作成します (管理者のみ)。|[ドメイン ベースの属性の作成 &#40;Excel 用 MDS アドイン&#41;](../../master-data-services/microsoft-excel-add-in/create-a-domain-based-attribute-mds-add-in-for-excel.md)|  
|Excel 用マスター データ サービス アドインで、データの読み込みとパブリッシングのプロパティを設定します。 (管理者のみ)。|[Excel 用マスター データ サービス アドインのプロパティの設定](../../master-data-services/microsoft-excel-add-in/setting-properties-for-master-data-services-add-in-for-excel.md)|  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   [接続 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/connections-mds-add-in-for-excel.md)  
  
-   [概要:Excel へのデータのエクスポート &#40;Excel 用 MDS アドイン&#41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
-   [ショートカット クエリ ファイル &#40;Excel 用 MDS アドイン&#41;](../../master-data-services/microsoft-excel-add-in/shortcut-query-files-mds-add-in-for-excel.md)  
  
-   [データの更新 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/refreshing-data-mds-add-in-for-excel.md)  
  
-   [概要:Excel からデータをインポートする&#40;MDS アドインの Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
-   [データの検証 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/validating-data-mds-add-in-for-excel.md)  
  
-   [Excel 用 MDS アドインでのデータ品質照合](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)  
  
-   [モデルの構築 &#40;Excel 用 MDS アドイン&#41;](../../master-data-services/microsoft-excel-add-in/building-a-model-mds-add-in-for-excel.md)  
  
-   [Excel 用マスター データ サービス アドインのプロパティの設定](../../master-data-services/microsoft-excel-add-in/setting-properties-for-master-data-services-add-in-for-excel.md)  
  
-   [セキュリティ &#40;マスター データ サービス&#41;](../../master-data-services/security-master-data-services.md)  
  
  
