---
title: 階層メンバーの権限
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- members [Master Data Services], permissions
- permissions [Master Data Services], members
ms.assetid: b3880eed-1bf6-4f65-ab23-b08c194cc858
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 41fe545d2a70ea1cbe3ccd05bbbd06174552d3b3
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729239"
---
# <a name="hierarchy-member-permissions-master-data-services"></a>階層メンバーの権限 (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  階層メンバーの権限はオプションであり、特定のメンバーに対するユーザーのアクセスを制限する場合にのみ使用します。 **[階層メンバー]** タブで権限を割り当てていなければ、ユーザーの権限は、 **[モデル]** タブで割り当てられた権限のみに基づいて決定されます。  
  
 階層メンバーの権限は、[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] のユーザーインターフェイス (UI) で、 **[階層メンバー]** タブの **[ユーザー/グループの権限]** 機能領域に割り当てられます。これらのアクセス許可によって、ユーザーが UI の **[エクスプローラー]** 機能領域でアクセスできるメンバーが決まります。  
  
 **[階層メンバー]** タブでは、各階層がツリー構造として表されます。 ツリー内のノードに権限を割り当てると、下位レベルで権限が明示的に割り当てられていない限り、すべての子がその権限を継承します。  
  
> [!NOTE]  
>  階層内のいずれかのノードに権限を割り当てると、同じレベル以上にある、それ以外のノード内のメンバーはすべて暗黙的に拒否されます。  
  
 **[エクスプローラー]** では、メンバーが表示されるすべての領域にメンバー権限が適用されます。 たとえば、 **Read** 権限が与えられているメンバーは、属しているすべてのエンティティ、階層、コレクションを読み取ることができます。  
  
 階層メンバーの権限は、それらを割り当てたモデル バージョンと、そのバージョンの以降のコピーに適用されます。 割り当てたバージョンよりも前のバージョンには適用されません。  
  
|権限|[説明]|  
|----------------|-----------------|  
|**読み取り**|メンバーが表示されます。<br /><br /> <br /><br /> 注: **読み取り** 権限を **ルート**に割り当てた場合、 **ルート** の下のメンバーは読み取り専用になります。ただし、明示的階層およびコレクションでは、ユーザーはメンバーを **ルート** に移動したり、新しいメンバーを **ルート**に追加したりできます。|  
|**作成**|作成権限は、階層メンバー権限では使用できません。|  
|**Update**|メンバーが表示され、ユーザーはメンバーを変更できます。 また、メンバーが属する明示的階層またはコレクションでメンバーを移動することもできます。|  
|**[削除]**|メンバーが表示され、ユーザーがそれらを削除できます。|  
|**拒否**|メンバーが表示されません。|  
  
 **[階層メンバー]** タブでは、権限を割り当ててもすぐには有効になりません。 権限が適用される頻度は、 **データベースの System Settings テーブルの** [メンバーのセキュリティ処理間隔の設定] [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] の値に応じて異なります。 メンバー権限を直ちに適用するには、「[メンバー権限を直ちに適用する方法 (マスター データ サービス)](../master-data-services/immediately-apply-member-permissions-master-data-services.md)」を参照してください。  
  
> [!NOTE]  
>  階層メンバーの権限は、再帰型階層、明示的なキャップを持つ派生階層、およびレベルを非表示にした階層に割り当てることはできません。  
  
## <a name="possible-overlapping-permissions"></a>重複の可能性がある権限  
 メンバーに権限を割り当てる際、権限の重複を解決することが必要になる場合があります。  
  
### <a name="when-a-member-belongs-to-multiple-hierarchies"></a>1 つのメンバーが複数の階層に属している場合  
 複数の階層に同じメンバーを含めることができます。  
  
-   ある階層ノードに **更新** 権限が割り当てられ、別の階層ノードに **読み取り**権限が割り当てられている場合、ノード内のメンバーの権限は **読み取り**になります。  
  
-   ある階層ノードに **更新** 権限と **作成** 権限が割り当てられ、別の階層ノードに **更新** 権限と **削除** 権限が割り当てられている場合、ノード内のメンバーを更新できます。  
  
-   ある階層ノードに **作成**/**Read**/**更新**/**削除** の各権限の組み合わせが割り当てられ、別のノードに **拒否** 権限が割り当てられている場合、ノード内のメンバーへのアクセスが拒否されます。  
  
## <a name="external-resources"></a>外部リソース  
 msdn.com のブログ投稿「 [Security Improvements (セキュリティの向上)](https://go.microsoft.com/fwlink/p/?LinkId=615376)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [階層メンバーの権限を割り当てる (マスター データ サービス)](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [権限の決定方法 (マスター データ サービス)](../master-data-services/how-permissions-are-determined-master-data-services.md)   
 [メンバー (マスター データ サービス)](../master-data-services/members-master-data-services.md)   
 [階層 (マスター データ サービス)](../master-data-services/hierarchies-master-data-services.md)   
 [メンバー権限を直ちに適用する (マスター データ サービス)](../master-data-services/immediately-apply-member-permissions-master-data-services.md)  
  
  
