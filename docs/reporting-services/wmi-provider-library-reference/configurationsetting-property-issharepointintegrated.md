---
title: IsSharePointIntegrated プロパティ (WMI) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
helpviewer_keywords:
- IsSharePointIntegrated property
ms.assetid: c548fed8-5e04-4faf-8b10-b37c86178056
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0bac72cf23cfebf48f58b24bea0b50aa9033bf5d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65573735"
---
# <a name="configurationsetting-property---issharepointintegrated"></a>ConfigurationSetting プロパティ - IsSharePointIntegrated
  レポート サーバーが SharePoint 統合モードであるかどうかを示します。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]以降、このプロパティは常に **False** を返します。これは、SharePoint モードでは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インスタンスは SharePoint 共有サービスであり、WMI プロバイダーによって制御されないためです。  
  
## <a name="syntax"></a>構文  
  
```vb  
Public Dim IsSharePointIntegrated As Boolean  
```  
  
```csharp  
public Boolean IsSharePointIntegrated;  
```  
  
## <a name="property-values"></a>プロパティ値  
 レポート サーバーが SharePoint 統合モードであるかどうかを示す **Boolean** オブジェクト。  
  
## <a name="example-code"></a>コード例  
 [MSReportServer_ConfigurationSetting クラス](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>必要条件  
 **名前空間:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>参照  
 [MSReportServer_ConfigurationSetting メンバー](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
