---
title: "IsWindowsServiceEnabled プロパティ (WMI MSReportServer_ConfigurationSetting) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- IsWindowsServiceEnabled
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- IsWindowsServiceEnabled property
ms.assetid: b1b75d72-6220-43fe-abfb-f967f3972d00
caps.latest.revision: 18
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: ce08a70291bab3ae0192143658b52d939d506863
ms.contentlocale: ja-jp
ms.lasthandoff: 08/09/2017

---
# <a name="configurationsetting-property---iswindowsserviceenabled"></a>IsWindowsServiceEnabled ConfigurationSetting プロパティ
  レポート サーバー Windows サービスが有効かどうかを示します。 読み取り専用です。  
  
## <a name="syntax"></a>構文  
  
```vb  
Public Dim IsWindowsServiceEnabled As Boolean  
```  
  
```csharp  
public boolean IsWindowsServiceEnabled;  
```  
  
## <a name="property-values"></a>プロパティ値  
 読み取り専用の **ブール値** です。 **true** の値は、レポート サーバー Windows サービスが有効であることを示します。  
  
## <a name="example-code"></a>コード例  
 [MSReportServer_ConfigurationSetting クラス](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>必要条件  
 **Namespace:**[!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>参照  
 [MSReportServer_ConfigurationSetting メンバー](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  