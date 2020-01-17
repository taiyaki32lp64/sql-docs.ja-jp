---
title: SMTPServer プロパティ (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- SMTPServer
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SMTPServer property
ms.assetid: 8bcceeba-e1a0-44ef-bda1-600c6925e1db
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b706834c80fa0ff126d35beffbfdc84ef92cefe6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66097500"
---
# <a name="smtpserver-property-wmi-msreportserverconfigurationsetting"></a>SMTPServer プロパティ (WMI MSReportServer_ConfigurationSetting)
  レポート サーバー構成ファイルから SMTP サーバー プロパティを取得します。 読み取り専用です。  
  
## <a name="syntax"></a>構文  
  
```vb  
Public Dim SMTPServer As String  
```  
  
```csharp  
public string SMTPServer;  
```  
  
## <a name="property-values"></a>プロパティ値  
 RSReportServer.config ファイルから取得した `String` プロパティ値を含む、読み取り専用の `SMTPServer` オブジェクト。  
  
## <a name="example-code"></a>コード例  
 [MSReportServer_ConfigurationSetting クラス](msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>必要条件  
 **名前空間:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>関連項目  
 [MSReportServer_ConfigurationSetting メンバー](msreportserver-configurationsetting-members.md)  
  
  
