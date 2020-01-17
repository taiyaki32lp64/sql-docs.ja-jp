---
title: モデル配置オプション
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: cf1b17b4-47d5-4eba-83f9-fb0555806867
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 692b207767dfc3d1ae4a032722e4cca6b2972ea0
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727968"
---
# <a name="model-deployment-options-master-data-services"></a>モデル配置オプション (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] でモデル パッケージ ファイルを配置するとき、新しいモデルまたは複製モデルを配置するのか、以前に複製したモデルを更新するのかを決定する必要があります。  
  
## <a name="workflows"></a>ワークフロー  
 モデル パッケージを操作する場合、2 つの主要なワークフローがあります。  
  
-   テスト環境でモデルのパッケージを作成し、そのモデルの複製を運用環境に配置します。 後で、テスト環境から運用環境に更新を配置します。  
  
-   モデルのパッケージを作成し、同じ環境に新しいモデルとして配置します。 この場合、モデルに新しい名前を付ける必要があります。  
  
## <a name="options"></a>および  
 MDS データベースでは、各モデル オブジェクトに一意の識別子 (ID) があります。 これらの ID は、モデルの配置パッケージに含まれます。 パッケージを配置する際、これらの ID をどのように処理するかを選択する必要があります。  
  
 次の表は、システム管理のモデル配置ウィザードまたは MDSModelDeploy ツールのいずれかを使用してモデルを配置する際に何を選択すればよいかを決定するのに役立ちます。  
  
|オプション|[説明]|注|  
|------------|-----------------|-----------|  
|[新規作成]|一意の名前を持つ新しいモデルを作成します。 すべてのモデル オブジェクトに新しい識別子が作成されます。|新しい識別子を持つ新しいモデルを作成した場合、後でモデル配置ツールを使用してモデルに更新を適用することはできません。 Web アプリケーションのウィザードを使用してモデル パッケージを配置ときに、同じ名前または ID を持つモデルが既に存在している場合、選択できるのは新しいモデルの作成のみです。|  
|複製|パッケージ内のモデルの正確な複製である新しいモデルを作成します。 このオプションは、名前または識別子が同じモデルがターゲット環境内に存在しない場合にのみ機能します。 複数の環境に同じモデルがあり、複製したモデルを後で更新する場合は、"複製" を使用します。|これは、Web アプリケーションのウィザードの既定の動作です。 同じ名前または ID を持つモデルが既に存在する場合は、代わりに新しいモデルを作成するよう求められます。|  
|Update|パッケージ内のモデルを使用して、既存のモデルを更新します。 両方のモデルの識別子が同じである必要があります。 このオプションは、以前に複製したモデルを更新するために使用します。|以前に複製したモデルのみを更新できます (名前と ID が一致する必要があります)。|  
  
## <a name="see-also"></a>参照  
 [MDSModelDeploy を使用したモデルの配置パッケージの配置](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)   
 [ウィザードを使用したモデルの配置パッケージの展開](../master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md)   
 [モデルの配置 (マスター データ サービス)](../master-data-services/deploying-models-master-data-services.md)  
  
  
