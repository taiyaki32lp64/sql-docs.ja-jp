---
title: ビジネス ルールの拡張機能
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 4c18be5f-a3fa-45a8-9be6-0f45f58bbc9e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 24df0fcbece66a86786550e81f3e385d6454f4b5
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728677"
---
# <a name="business-rules-extension-master-data-services"></a>ビジネス ルールの拡張機能 (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] では、ユーザー定義の SQL スクリプトを、事前に定義された条件とアクションの拡張機能として適用できます。  
  
> [!NOTE]  
>  すべてのスクリプトは、[usr] スキーマに定義する必要があります。  
  
 次の条件を満たす SQL 関数は、ビジネス ルールの条件として使用できます。  
  
-   戻り値は BIT 型である必要があります。  
  
-   次のパラメーター型のみがサポートされています。  
  
    -   NVARCHAR  
  
    -   DATETIME2  
  
    -   DECIMAL (precision, scale)  
  
         precision は 38 である必要があります。  
  
         scale は、0 ～ 7 の値である必要があります。  
  
 次の構文を使用する SQL ストアド プロシージャは、ビジネス ルールのアクションとして使用できます。  
  
```  
CREATE PROCEDURE [usr].[YourAction]  
       (         
            @MemberIdList mdm.[MemberId] READONLY,  
            @ModelName NVARCHAR(MAX),  
            @VersionName NVARCHAR(MAX),  
            @EntityName NVARCHAR(MAX),  
            @BusinessRuleName NVARCHAR(MAX)  
        )    
      AS BEGIN    
       ...     
       END  
  
```  
  
 ユーザー定義のスクリプトは、配置パッケージには追加されません。 パッケージを配置する前に、ビジネス ルールで使用されるすべてのスクリプトがターゲットのマスター データ サービス データベースに含まれていることを確認します。  
  
 スクリプト アクションは、次のアクセス許可を持つ mds_br_user として実行されます。  
  
|||  
|-|-|  
|**スキーマ**|**Permissions**|  
|mdm|SELECT|  
|stg|SELECT、UPDATE、DELETE、EXECUTE、INSERT|  
|ユーザー|FULL|  
  
## <a name="prerequisites"></a>Prerequisites  
 この手順を実行するには  
  
-   [システム管理] 機能領域にアクセスする権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「[管理者 (マスター データ サービス)](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
-   ユーザー定義のスクリプトが [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースに追加されている必要があります。  
  
## <a name="create-a-business-rule-to-take-a-user-defined-script-as-a-condition-or-as-an-action"></a>ユーザー定義のスクリプトを条件またはアクションとして実行するビジネス ルールを作成する  
  
1.  マスター データ マネージャーで、 **[システム管理]** をクリックします。  
  
2.  メニュー バーの **[管理]** をポイントし、 **[ビジネス ルール]** をクリックします。  
  
3.  **[ビジネス ルール]** ページで、 **[モデル]** ドロップダウン リストからモデルを選択します。  
  
4.  **[エンティティ]** ドロップダウン リストから、エンティティを選択します。  
  
5.  **[メンバーの種類]** ボックスの一覧から、適用するビジネス ルールのメンバーの種類を選択します。  
  
6.  **[追加]** をクリックします。  
  
7.  ユーザー定義のスクリプトを条件として作成するには、次の操作を行います。  
  
    1.  **If** ブロックの下で、 **[追加]** ボタンをクリックします。 パネルが表示されます。  
  
    2.  **[演算子]** ドロップダウン リストで、 **[ユーザー定義スクリプト]** の下にある目的のユーザー定義関数を選択します。  
  
    3.  このユーザー定義関数のすべてのパラメーターが表示されます。  
  
    4.  各パラメーターに値を割り当てます。  
  
    5.  **[保存]** をクリックします。  
  
8.  ユーザー定義のスクリプトをアクションとして作成するには、次の操作を行います。  
  
    1.  **Then** ブロックの下で、 **[追加]** ボタンをクリックします。 パネルが表示されます。  
  
    2.  **[演算子]** ドロップダウン リストで、 **[ユーザー定義スクリプト]** の下にある目的のユーザー定義関数を選択します。  
  
    3.  **[保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [ビジネス ルール (マスター データ サービス)](../master-data-services/business-rules-master-data-services.md)   
 [ビジネス ルール条件 (マスター データ サービス)](../master-data-services/business-rule-conditions-master-data-services.md)   
 [ビジネス ルール アクション (マスター データ サービス)](../master-data-services/business-rule-actions-master-data-services.md)  
  
  
