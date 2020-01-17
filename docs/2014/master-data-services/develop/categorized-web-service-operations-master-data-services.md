---
title: Web サービス操作の分類 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: e3f346b5-7e26-481d-9821-1846e2e91289
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 84339eab432194327759fbdad505cdb1af60517b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65479432"
---
# <a name="categorized-web-service-operations-master-data-services"></a>Web サービス操作の分類 (Master Data Services)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web サービスには、[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] がユーザー インターフェイスを通じて行うすべての機能をコード記述で制御できるようにするための操作が、完全なセットとして含まれています。 Web サービス操作は、<xref:Microsoft.MasterDataServices.IService> インターフェイスによって定義され、<xref:Microsoft.MasterDataServices.ServiceClient> クラスのメソッドとして実装されます。 このトピックでは、Web サービス API の使用方法を理解しやすくするために、Web サービス操作を概念ごとのカテゴリに分類します。  
  
## <a name="model-operations"></a>モデルの操作  
 これらの操作は、モデルの作成、更新、削除のほか、モデルの全コンテンツ (エンティティ、階層、バージョンなど) に対する操作に使用されます。 詳細については、「[モデル (マスター データ サービス)](../models-master-data-services.md)」を参照してください。  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.MetadataClone%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.MetadataCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.MetadataDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.MetadataGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.MetadataUpdate%2A>|  
  
## <a name="entity-operations"></a>エンティティの操作  
 これらの操作は、単一のエンティティのメンバーを作成、更新、削除するために使用されます。 詳細については、「[エンティティ &#40;マスター データ サービス&#41;](../entities-master-data-services.md)」と「[メンバー &#40;マスター データ サービス&#41;](../members-master-data-services.md)」を参照してください。  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMemberKeyLookup%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMembersCopy%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMembersCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMembersDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMembersGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMembersMerge%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMembersUpdate%2A>|  
  
## <a name="member-operations"></a>メンバーの操作  
 これらの操作は、メンバーを取得、更新、削除するために使用されます。 操作されるメンバーのセットには、複数のエンティティからのメンバーを含めることができます。 詳細については、「[バージョン (マスター データ サービス)](../members-master-data-services.md)」を参照してください。  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ModelMembersBulkDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ModelMembersBulkMerge%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ModelMembersBulkUpdate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ModelMembersGet%2A>|  
  
## <a name="attribute-and-hierarchy-operations"></a>属性と階層の操作  
 これらの操作は、属性や階層の情報を取得するために使用されます。 属性と階層は、モデル操作 (<xref:Microsoft.MasterDataServices.ServiceClient.MetadataUpdate%2A> など) を使用して変更することもできます。 詳細については、「[属性 &#40;マスター データ サービス&#41;](../attributes-master-data-services.md)」と「[階層 &#40;マスター データ サービス&#41;](../hierarchies-master-data-services.md)」を参照してください。  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMemberAttributesGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.HierarchyMembersGet%2A>|  
  
## <a name="business-rule-operations"></a>ビジネス ルールの操作  
 これらの操作は、ビジネス ルールを作成、更新、削除、パブリッシュするために使用されます。 詳細については、「[ビジネス ルール (マスター データ サービス)](../business-rules-master-data-services.md)」を参照してください。  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesClone%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesPaletteGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesPublish%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesUpdate%2A>|  
  
## <a name="annotation-operations"></a>注釈の操作  
 これらの操作は、注釈を作成、更新、削除するために使用されます。 詳細については、「[注釈 &#40;マスター データ サービス&#41;](../annotations-master-data-services.md)」を参照してください。  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.AnnotationsDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.AnnotationsUpdate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMemberAnnotationsCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMemberAnnotationsGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.TransactionAnnotationsCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.TransactionAnnotationsGet%2A>|  
  
## <a name="transaction-operations"></a>トランザクションの操作  
 これらの操作は、トランザクションを取得および破棄するために使用されます。 詳細については、「[トランザクション (マスター データ サービス)](../transactions-master-data-services.md)」を参照してください。  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.TransactionsGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.TransactionsReverse%2A>|  
  
## <a name="version-and-validation-operations"></a>バージョンと検証の操作  
 これらの操作は、バージョンをコピーおよび検証するために使用されます。 詳細については、「[バージョン &#40;マスター データ サービス&#41;](../versions-master-data-services.md)」と「[検証 &#40;マスター データ サービス&#41;](../validation-master-data-services.md)」を参照してください。  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.VersionCopy%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ValidationGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ValidationProcess%2A>|  
  
## <a name="data-quality-operations"></a>データ品質の操作  
 これらの操作は、データ品質タスクの実行と、それらの結果の確認に使用されます。  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.DataQualityCleansingOperationCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.DataQualityMatchingOperationCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.DataQualityOperationStart%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.DataQualityInstalledState%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.DataQualityKnowledgeBasesGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.DataQualityOperationResultsGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.DataQualityOperationStatus%2A>|  
  
## <a name="data-import-operations"></a>データ インポートの操作  
 これらの操作は、[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベースにデータをインポートするために使用されます。 詳細については、「[データのインポート &#40;マスター データ サービス&#41;](../overview-importing-data-from-tables-master-data-services.md)」を参照してください。  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityStagingClear%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityStagingGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityStagingLoad%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityStagingProcess%2A>|  
  
 次の操作は、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] に含まれるステージング処理を使用してデータをインポートするために使用されます。 これらの操作は、既存のデータベースをサポートする目的にのみ使用してください。 新規の開発には、先に示した操作を使用してください。  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.StagingClear%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.StagingGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.StagingNameCheck%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.StagingProcess%2A>|  
  
## <a name="data-export-operations"></a>データ エクスポートの操作  
 これらの操作は、サブスクリプション ビューを使用してデータをエクスポートするために使用されます。 詳細については、次を参照してください。[データのエクスポート&#40;Master Data Services&#41;](../overview-exporting-data-master-data-services.md)します。  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ExportViewCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ExportViewDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ExportViewListGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ExportViewUpdate%2A>|  
  
## <a name="security-operations"></a>セキュリティの操作  
 これらの操作は、[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベースへのアクセスを制御するセキュリティ設定を変更するために使用されます。 詳細については、「[セキュリティ (マスター データ サービス)](../security-master-data-services.md)」を参照してください。  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrincipalsClone%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrincipalsCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrincipalsDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrincipalsGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrincipalsUpdate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrivilegesClone%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrivilegesCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrivilegesDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrivilegesGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrivilegesUpdate%2A>|  
  
## <a name="system-operations"></a>システムの操作  
 これらの操作は、システム設定やユーザー設定を取得および更新するために使用されます。  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ServiceCheck%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ServiceVersionGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SystemDomainListGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SystemPropertiesGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SystemSettingsGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SystemSettingsUpdate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.UserPreferencesDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.UserPreferencesGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.UserPreferencesUpdate%2A>|  
  
  
