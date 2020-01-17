---
title: OData 接続マネージャー | Microsoft Docs
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.custom: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3caa4372-aff3-4c0f-9ecd-97870948b8d0
f1_keywords:
- sql13.dts.designer.odatasource.connectionmanager.f1
- sql13.dts.designer.odataconnectionmanager.f1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 39499e36568d64f92d3608f610d64193c93389e6
ms.sourcegitcommit: 02449abde606892c060ec9e9e9a85a3f49c47c6c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74542181"
---
# <a name="odata-connection-manager"></a>OData 接続マネージャー

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


 OData 接続マネージャーを使用して、OData データ ソースに接続します。 OData ソース コンポーネントは OData 接続マネージャーを使用して OData データ ソースに接続し、サービスから取得したデータを使用します。 詳細については、「 [OData Source](../../integration-services/data-flow/odata-source.md)」を参照してください。  
  
## <a name="adding-an-odata-connection-manager-to-an-ssis-package"></a>SSIS パッケージへの OData 接続マネージャーの追加  
 次の 3 とおりの方法で、SSIS パッケージに新しい OData 接続マネージャーを追加できます。  
  
-   **[OData ソース エディター]** の **[新規]** ボタンをクリックします。  
  
-   **ソリューション エクスプローラー** で **[接続マネージャー]** を右クリックし、 **[新しい接続マネージャー]** をクリックします。 **[接続マネージャーの種類]** の **[ODATA]** をクリックします。  
  
-   パッケージ デザイナーの下部にある **[接続マネージャー]** ペインを右クリックし、 **[新しい接続]** を選択します。 **[接続マネージャーの種類]** の **[ODATA]** をクリックします。  
  
## <a name="connection-manager-authentication"></a>接続マネージャーの認証  
 OData 接続マネージャーでは、5 つの認証モードがサポートされています。  
  
-   [Windows 認証]  
  
-   基本認証 (ユーザー名とパスワードを使用)  

-   Microsoft Dynamics AX Online (ユーザー名とパスワードを使用)
  
-   Microsoft Dynamics CRM Online (ユーザー名とパスワードを使用)
  
-   Microsoft Online Services (ユーザー名とパスワードを使用)  
  
匿名アクセスを使用するには、[Windows 認証] オプションを選択します。  

Microsoft Dynamics AX Online または Microsoft Dynamics CRM Online に接続する場合、 **[Microsoft Online Services]** 認証オプションを使用することはできません。 また、多要素認証に構成されているオプションを使用することもできません。 現時点では、先進認証はサポートされていません。 
  
### <a name="specifying-and-securing-credentials"></a>資格情報の指定とセキュリティ保護  
 OData サービスで基本認証が必要とされる場合は、 [OData Connection Manager Editor](../../integration-services/connection-manager/odata-connection-manager-editor.md)でユーザー名とパスワードを指定できます。 エディターに入力した値は、パッケージ内に保存されます。 パスワードの値は、パッケージの保護レベルに応じて暗号化されます。  
  
 ユーザー名とパスワードの値をパラメーター化またはパッケージ外に保存する方法はいくつかあります。 たとえば、パラメーターを使用するか、SQL Server Management Studio からパッケージを実行するときに接続マネージャーのプロパティを直接設定できます。  
  
## <a name="odata-connection-manager-properties"></a>OData 接続マネージャーのプロパティ  
 次の一覧で、OData 接続マネージャーのプロパティについて説明します。  
  
|||  
|-|-|  
|プロパティ|[説明]|  
|url|サービス ドキュメントに対応する URL。|  
|UserName|認証に使用するユーザー名 (必要な場合)。|  
|Password|認証に使用するパスワード (必要な場合)。|  
|ConnectionString|接続マネージャーの他のプロパティが含まれます。|  
  
## <a name="odata-connection-manager-editor"></a>[OData 接続マネージャー エディター]
  **[OData 接続マネージャー エディター]** ダイアログ ボックスを使用して、OData データ ソースへの接続を追加するか、既存の接続を編集します。  
  
### <a name="options"></a>オプション  
 **接続マネージャー名**  
 接続マネージャーの名前です。  
  
 **サービス ドキュメントの場所**  
 OData サービスに対応する URL。 (例: https://services.odata.org/V3/Northwind/Northwind.svc/ )。  
  
 **認証**  
以下のオプションの 1 つを選択します。
-   **Windows 認証**。 匿名アクセスの場合は、このオプションを選択します。
-   **基本認証** 
-   **Microsoft Dynamics AX Online** (Dynamics AX Online の場合)
-   **Microsoft Dynamics CRM Online** (Dynamics CRM Online の場合)
-   **Microsoft Online Services** (Microsoft Online Services の場合)

Windows 認証以外のオプションを選択する場合は、**ユーザー名**と**パスワード**を入力します。 

Microsoft Dynamics AX Online または Microsoft Dynamics CRM Online に接続する場合、 **[Microsoft Online Services]** 認証オプションを使用することはできません。 また、多要素認証に構成されているオプションを使用することもできません。

 **[接続テスト]**  
 OData ソースへの接続をテストするには、このボタンをクリックします。  
