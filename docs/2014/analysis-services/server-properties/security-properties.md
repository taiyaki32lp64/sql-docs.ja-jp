---
title: セキュリティのプロパティ |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- security [Analysis Services], properties
- SecurityPackageList property
- BuiltinAdminsAreServerAdmins property
- DisableClientImpersonation property
- ErrorMessageMode property
- RequiredProtectionLevel property
- ServiceAccountIsServerAdmin property
- RequireClientAuthentication property
ms.assetid: 2fc7fe10-0cbb-49ac-aa8c-8ec3f7a7705f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9316827245adfbcf64bd798869f570dc5f0af14c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66068909"
---
# <a name="security-properties"></a>セキュリティのプロパティ
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 次の表に示すセキュリティ サーバー プロパティがサポートされています。 その他のサーバー プロパティとその設定方法の詳細については、「 [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md)」を参照してください。  
  
 **適用対象:** 多次元および表形式サーバー モード  
  
## <a name="properties"></a>プロパティ  
 `RequireClientAuthentication`  
 クライアント認証が必要かどうかを示すブール型プロパティです。  
  
 このプロパティの既定値は True で、クライアント認証が必要であることを示します。  
  
 `SecurityPackageList`  
 サーバーがクライアントの認証に使用する SSPI パッケージのコンマ区切りのリストを格納する文字列プロパティです。  
  
 `DisableClientImpersonation`  
 (たとえばストアド プロシージャからの) クライアント権限の借用が無効であるかどうかを示すブール型プロパティです。  
  
 このプロパティの既定値は False で、クライアント権限の借用が有効であることを示します。  
  
 `BuiltinAdminsAreServerAdmins`  
 ローカル コンピューターの Administrators グループのメンバーが [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管理者であるかどうかを示すブール型プロパティです。  
  
 `ServiceAccountIsServerAdmin`  
 サービス アカウントがサーバー管理者であるかどうかを示すブール型プロパティです。  
  
 このプロパティの既定値は True で、サービス アカウントがサーバー管理者であることを示します。  
  
 `ErrorMessageMode`  
 詳細プロパティです。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] サポートの指示がない限り、変更しないでください。  
  
 `DataProtection\ RequiredProtectionLevel`  
 すべてのクライアント要求に必要な保護レベルを定義する、符号付き 32 ビット整数のプロパティです。 このプロパティは、次の表に示すいずれかの値になります。  
  
|値|説明|  
|-----------|-----------------|  
|*0*|なし。クリア テキストが許可されます。|  
|*1*|(既定値) 暗号化が必要。クリア テキストのログは記録されません。|  
|*2*|クリア テキストの要求は許可されるが、署名付きのものに限る (暗号化より弱い保護)。|  
  
 `AdministrativeDataProtection\ RequiredProtectionLevel`  
 詳細プロパティです。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] サポートの指示がない限り、変更しないでください。  
  
## <a name="see-also"></a>参照  
 [Analysis services サーバーのプロパティを構成します。](server-properties-in-analysis-services.md)   
 [Analysis Services インスタンスのサーバー モードの決定](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
