---
title: リーフ メンバーを作成する (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- leaf members [Master Data Services], creating
- creating leaf members [Master Data Services]
- members [Master Data Services], creating leaf members
ms.assetid: 0499d3b3-d508-4d43-a740-19cf53ade9f1
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: a7204fb8183ed84390bd3eaec38b16833dd8eb2a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67906744"
---
# <a name="create-a-leaf-member-master-data-services"></a>リーフ メンバーを作成する (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で、マスター データをシステムに追加する場合は、リーフ メンバーを作成します。 データを一括で追加する場合は、ステージング テーブルを使用します。 詳細については、「[テーブルからのデータのインポート (マスター データ サービス)](../master-data-services/import-data-from-tables-master-data-services.md)」を参照してください。  
  
 データをインポートするには、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] も使用します。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 この手順を実行するには  
  
-   **[エクスプローラー]** 機能領域にアクセスする権限が必要です。  
  
-   メンバーを追加するエンティティのリーフ モデル オブジェクトに対する **作成** または **更新** 権限が最低限必要です。 作成権限では、メンバーを作成し、コードの属性のみを編集できます。 更新権限では、その他の属性を更新できます。  
  
     詳細については、「[セキュリティ (マスター データ サービス)](../master-data-services/security-master-data-services.md)」を参照してください。  
  
### <a name="to-create-a-leaf-member"></a>リーフ メンバーを作成するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] のホーム ページで、 **[モデル]** ボックスの一覧からモデルを選択します。  
  
2.  ユーザーの場合は、 **[バージョン]** ボックスの一覧から未処理のバージョンを選択します。 管理者の場合は、 **[バージョン]** ボックスの一覧から、状態が未処理またはロック済みのバージョンを選択します。  
  
3.  **[エクスプローラー]** をクリックします。  
  
4.  メニュー バーの **[エンティティ]** をポイントして、メンバーを追加するエンティティの名前をクリックします。  
  
5.  **[メンバーの追加]** をクリックします。  
  
6.  **[詳細]** ペインのフィールドに入力します。  
  
     ドメイン ベースの属性にフィルターが適用されている場合、属性値の一覧はフィルターの親属性によって制限されます。  
  
     フィルターの親属性およびドメイン ベースの属性の詳細については、「[ドメイン ベースの属性を作成する (マスター データ サービス)](../master-data-services/create-a-domain-based-attribute-master-data-services.md)」を参照してください。  
  
7.  任意。 **[注釈]** ボックスに、メンバーを追加した理由についてのコメントを入力します。 そのメンバーにアクセスできるすべてのユーザーが、その注釈を表示できます。  
  
8.  **[OK]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
 [統合メンバーを作成する (マスター データ サービス)](../master-data-services/create-a-consolidated-member-master-data-services.md)   
 [メンバー (マスター データ サービス)](../master-data-services/members-master-data-services.md)  
  
  
