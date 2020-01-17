---
title: Azure Data Lake Store 接続マネージャー | Microsoft Docs
ms.custom: ''
ms.date: 06/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSCM.F1
- SQL11.DTS.DESIGNER.AFPADLSCM.F1
ms.assetid: 7f1323f9-9dc3-4378-9c70-bbc65bfeabfd
author: yualan
ms.author: janinez
manager: craigg
ms.openlocfilehash: c835f42fdbcc43309a0235f8ad862bee9c230e33
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66462699"
---
# <a name="azure-data-lake-store-connection-manager"></a>Azure Data Lake Store 接続マネージャー
  **Azure Data Lake Store 接続マネージャー** SSIS パッケージを 2 つの認証の種類を Azure Data Lake Store サービスに接続できるようにします。Azure AD のユーザー Id と Azure AD サービスの Id。  

## <a name="configure-the-azure-data-lake-store-connection-manager"></a>Azure Data Lake Store 接続マネージャーを構成する 
  
1.  **[SSIS 接続マネージャーの追加]** ダイアログ ボックスで **[AzureDataLake]** を選択し、 **[追加]** をクリックします。   
  
2.  Azure Data Lake Store 接続マネージャー エディター ダイアログ ボックスの **[ADLS ホスト]** フィールドに、Azure Data Lake Store ホストの URL を入力します。 例: https:\//test.azuredatalakestore.net または test.azuredatalakestore.net します。
  
3.  Azure Data Lake Store データにアクセスするための該当する認証の種類を選択します。

    1.  **[Azure AD のユーザー ID]** 認証オプションを選択した場合は、次の操作を行います。

        1. **[ユーザー名]** と **[パスワード]** のフィールドに値を指定します。 
    
        2. **[接続テスト]** ボタンをクリックして接続をテストします。 自分自身とテナント管理者が SSIS から Azure Data Lake Store データへのアクセスに同意していない場合は、別ウィンドウで表示されるダイアログで **[同意する]** ボタンをクリックし、SSIS から Azure Data Lake Store データへのアクセスに同意する必要があります。 この同意エクスペリエンスの詳細については、「[Azure Active Directory とアプリケーションの統合](https://docs.microsoft.com/azure/active-directory/manage-apps/plan-an-application-integration#integrating-applications-with-azure-ad)」を参照してください。
    
        > [!NOTE] 
        > Azure AD のユーザー ID 認証オプションでは、多要素認証と Microsoft アカウントはサポートされていません。
    
    2.  **[Azure AD のサービス ID]** 認証オプションを選択した場合は、次の操作を行います。
        1. Azure Data Lake リソースにアクセスできる AAD アプリケーションおよびサービス プリンシパルを作成します。
    
        2. Azure Data Lake リソースにアクセスするために適切な権限をこの AAD アプリケーションに割り当てます。 この認証オプションの詳細については、「[Use portal to create Active Directory application and service principal that can access resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)」 (ポータルを使用して、リソースにアクセスできる Active Directory アプリケーションとサービス プリンシパルを作成する) を参照してください。
    
        3. **[クライアント ID]** 、 **[シークレット キー]** および **[テナント名]** の各フィールドに値を指定します。
    
        4. **[接続テスト]** ボタンをクリックして接続をテストします。  
  
4.  **[OK]** をクリックしてダイアログ ボックスを閉じます。  
  
    作成した接続マネージャーのプロパティは、 **[プロパティ]** ウィンドウに表示されます。  
  
  
