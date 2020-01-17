---
title: セキュリティ (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 56bc41ea-de28-4184-aa7e-99111ae55af5
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 80be0aea6705ed98fd12ea3481af59e289b94604
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65482584"
---
# <a name="security-master-data-services"></a>セキュリティ (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]では、セキュリティを使用して、仕事を行うのに必要な特定のマスター データにユーザーがアクセスできるようにすると同時に、利用を許可しないデータにはアクセスできないようにします。  
  
 また、セキュリティを使用して、任意のユーザーを特定のモデルおよび機能領域の管理者にすることも可能です (任意のユーザーに Customer モデルのバージョンの作成を許可したり、セキュリティ権限の設定資格を与えたりするなど)。  
  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] セキュリティは、ローカルまたは Active Directory のドメイン ユーザーおよびグループを基にしています。 MDS セキュリティを使用すると、ユーザーがアクセス可能なデータを判断するときに、細かいレベルの詳細を使用できます。 このレベルの細かさが原因で、セキュリティがすぐに複雑になることがあり、重複するユーザーやグループを使用する場合は注意が必要がです。 詳細については、「[ユーザー権限とグループ権限の重複 (マスター データ サービス)](overlapping-user-and-group-permissions-master-data-services.md)」を参照してください。  
  
 アクセスのセキュリティは、 **Web アプリケーションの** [ユーザー/グループの権限] [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 機能領域、または Web サービスを使用して割り当てることができます。  
  
## <a name="types-of-users"></a>ユーザーの種類  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]には、次の 2 種類のユーザーがいます。  
  
-   **[エクスプローラー]** 機能領域でデータにアクセスするユーザー。  
  
-   **[エクスプローラー]** 以外の領域で管理タスクを実行できるユーザー。 これらのユーザーは、[管理者 (マスター データ サービス)](../../2014/master-data-services/administrators-master-data-services.md) と呼ばれます。  
  
## <a name="how-to-set-security"></a>セキュリティの設定方法  
 MDS のデータまたは機能にアクセスする権限をユーザーまたはグループに付与するには、次の設定を割り当てる必要があります。  
  
-   [機能領域のアクセス権](../../2014/master-data-services/functional-area-permissions-master-data-services.md)。ユーザー インターフェイスの 5 つの機能領域のうち、ユーザーがアクセスできる領域を決定します。  
  
-   [モデル オブジェクトの権限](../../2014/master-data-services/model-object-permissions-master-data-services.md)。ユーザーがアクセスできる属性と、それらの属性に対するユーザーのアクセスの種類 (読み取りまたは更新) を決定します。  
  
-   (省略可能) [階層メンバーの権限](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)。ユーザーがアクセスできるメンバーと、それらのメンバーに対するユーザーのアクセスの種類 (読み取りまたは更新) を決定します。  
  
 属性およびメンバーに権限を割り当てる場合、権限の共通部分とルールによってどの権限が優先されるかが決まります。 詳細については、「 [権限の決定方法 (マスター データ サービス)](../../2014/master-data-services/how-permissions-are-determined-master-data-services.md)」を参照してください。  
  
 レコード レベルのセキュリティを実装するには、エンティティの階層を作成し、階層のメンバーにユーザー権限を割り当てます。 メンバーは、データ レコードです。  階層メンバーの権限は特定のメンバーに対するユーザーのアクセスを制限する場合にのみ使用します。  
  
 次の図では、スタイル エンティティの派生階層と、選択したユーザーのスタイル メンバー権限を示します。 更新権限は、M {Men's} と U {Unisex} のメンバーに割り当てられており、読み取り専用権限は女性スタイルのメンバーに割り当てられます。 つまり、ユーザーは男性とユニセックスの製品レコードを更新できますが、女性スタイルの製品レコードについては読取り専用になります。  
  
 ![スタイルの派生階層とメンバーのアクセス許可](../../2014/master-data-services/media/style-derived-hierarchy-mds.png "スタイルの派生階層とメンバーの権限")  
  
 階層を作成する方法については、次を参照してください。[明示的階層を作成&#40;Master Data Services&#41; ](../../2014/master-data-services/create-an-explicit-hierarchy-master-data-services.md)と[派生階層を作成&#40;Master Data Services&#41;](../../2014/master-data-services/create-a-derived-hierarchy-master-data-services.md)します。  
  
 メンバー権限を割り当てる方法については、次を参照してください[階層メンバーの権限を割り当てる&#40;マスター データ サービス。&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)  
  
## <a name="security-in-the-add-in-for-excel"></a>Excel 用アドインでのセキュリティ  
 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションでのセキュリティ セットは、 [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]にも適用されます。 ユーザーは、権限のあるデータのみを表示および操作できます。 管理者は、管理タスクを実行できます。  
  
 1 つ注意する必要があるのは、 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] で割り当てられたすべてのセキュリティは、Excel で有効になるまでに 20 分かかるということです。 この間隔は、web.config ファイルの設定 *MdsMaximumUserInformationCacheInterval* で定義されています。 間隔を変更するには、設定を変更して IIS を再起動します。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|モデルに対して完全な権限を持つユーザーを作成する。|[モデル管理者を作成する (マスター データ サービス)](../../2014/master-data-services/create-a-model-administrator-master-data-services.md)|  
|Active Directory グループを [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]に追加する。これは、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web アプリケーションでグループにデータへのアクセス権を付与するときの最初の手順です。|[グループを追加する (マスター データ サービス)](../../2014/master-data-services/add-a-group-master-data-services.md)|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web アプリケーションの機能領域に権限を割り当てる。|[機能領域の権限を割り当てる (マスター データ サービス)](../../2014/master-data-services/assign-functional-area-permissions-master-data-services.md)|  
|モデル オブジェクトに権限を割り当てることで、属性値に権限を割り当てる。|[モデル オブジェクト権限を割り当てる (マスター データ サービス)](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)|  
|階層ノードに権限を割り当てることで、メンバー値に権限を割り当てる。|[階層メンバーの権限を割り当てる (マスター データ サービス)](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)|  
  
## <a name="see-also"></a>参照  
 [管理者 (マスター データ サービス)](../../2014/master-data-services/administrators-master-data-services.md)   
 [ユーザーおよびグループ (マスター データ サービス)](../../2014/master-data-services/users-and-groups-master-data-services.md)   
 [機能領域権限 (マスター データ サービス)](../../2014/master-data-services/functional-area-permissions-master-data-services.md)   
 [モデル オブジェクト権限 (マスター データ サービス)](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [階層メンバーの権限 (マスター データ サービス)](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [権限の決定方法 (マスター データ サービス)](../../2014/master-data-services/how-permissions-are-determined-master-data-services.md)  
  
  
