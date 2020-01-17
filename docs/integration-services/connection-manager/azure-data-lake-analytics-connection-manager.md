---
title: Azure Data Lake Analytics 接続マネージャー | Microsoft Docs
description: SQL Server Integration Services (SSIS) パッケージでは、Azure Data Lake Analytics 接続マネージャーを使用して、Data Lake Analytics アカウントに接続できます。
ms.custom: ''
ms.date: 05/18/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: maghan
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSCM.F1
- sql14.dts.designer.afpadlscm.f1
ms.assetid: f4c44553-0f08-4731-ac47-7534990b8c8d
author: yanancai
ms.author: yanacai
ms.openlocfilehash: c2ae186aa7d7fe9ee4ef7da26ed0f5e667b8e2d9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67904811"
---
# <a name="azure-data-lake-analytics-connection-manager"></a>Azure Data Lake Analytics 接続マネージャー

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



SQL Server Integration Services (SSIS) パッケージでは、Azure Data Lake Analytics 接続マネージャーを使用して、次の 2 つの認証の種類のいずれかで Data Lake Analytics アカウントに接続できます。
-   Azure Active Directory (Azure AD) のユーザー ID
-   Azure AD のサービス ID 

Data Lake Analytics 接続マネージャー は、[SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) のコンポーネントです。
 
## <a name="configure-the-connection-manager"></a>接続マネージャーの構成

1. **[SSIS 接続マネージャーの追加]** ダイアログ ボックスで **[AzureDataLakeAnalytics]**  >  **[追加]** の順に選択します。 **[Azure Data Lake Analytics Connection Manager Editor]\(Azure Data Lake Analytics 接続マネージャー エディター\)** ダイアログ ボックスが開きます。
  
2. **[Azure Data Lake Analytics Connection Manager Editor]\(Azure Data Lake Analytics 接続マネージャー エディター\)** ダイアログ ボックスの **[ADLA Account Name]\(ADLA アカウント名\)** フィールドに、Data Lake Analytics アカウントの名前を入力します。 たとえば、「myadlaaccountname」などと入力します。
  
3. **[認証]** フィールドで、Data Lake Analytics のデータにアクセスするために適切な認証の種類を選択します。

   A. **[Azure AD のユーザー ID]** 認証オプションを選択する場合は、次の操作を行います。
   
      i. **[ユーザー名]** と **[パスワード]** のフィールドに値を指定します。    
      ii. 接続をテストするには、 **[接続テスト]** を選択します。 自分自身またはテナント管理者が SSIS から Data Lake Analytics アカウントへのアクセスに同意していない場合は、プロンプトが表示されたときに **[同意する]** を選択します。 この同意エクスペリエンスの詳細については、「 [Azure Active Directory とアプリケーションの統合](https://docs.microsoft.com/azure/active-directory/manage-apps/plan-an-application-integration#integrating-applications-with-azure-ad)」を参照してください。
    
   > [!NOTE] 
   > **[Azure AD のユーザー ID]** 認証オプションを選択する場合、多要素認証と Microsoft アカウント認証はサポートされません。
    
   B. **[Azure AD のサービス ID]** 認証オプションを選択する場合は、次の操作を行います。
   
      i. Data Lake Analytics アカウントにアクセスするための Azure AD アプリケーションおよびサービス プリンシパルを作成します。 この認証オプションの詳細については、「 [Use portal to create Active Directory application and service principal that can access resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)」 (ポータルを使用して、リソースにアクセスできる Active Directory アプリケーションとサービス プリンシパルを作成する) を参照してください。    
      ii. 適切な権限を割り当てて、この Azure AD アプリケーションが Data Lake Analytics アカウントにアクセスできるようにします。 [ユーザー追加ウィザード](https://docs.microsoft.com/azure/data-lake-analytics/data-lake-analytics-manage-use-portal#add-a-new-user)を使用して Data Lake Analytics アカウントへのアクセス許可を付与する方法を確認してください。    
      iii. **[アプリケーション ID]** 、 **[認証キー]** 、 **[テナント ID]** フィールドの値を指定します。    
      iv. 接続をテストするには、 **[接続テスト]** を選択します。  

4. **[OK]** を選択して、 **[Azure Data Lake Analytics Connection Manager Editor]\(Azure Data Lake Analytics 接続マネージャー エディター\)** ダイアログ ボックスを閉じます。  

## <a name="view-the-properties-of-the-connection-manager"></a>接続マネージャーのプロパティを表示する
作成した接続マネージャーのプロパティは、 **[プロパティ]** ウィンドウに表示されます。  
  
  
