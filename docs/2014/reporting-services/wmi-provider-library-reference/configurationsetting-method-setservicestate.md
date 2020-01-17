---
title: SetServiceState メソッド (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- SetServiceState (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetServiceState method
ms.assetid: 9e1ee42d-b388-4929-89c7-8741b956c3be
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 21c8de3e6903a28ad8358431f5e455df31d3044e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66097949"
---
# <a name="setservicestate-method-wmi-msreportserverconfigurationsetting"></a>SetServiceState メソッド (WMI MSReportServer_ConfigurationSetting)
  レポート サーバーの Windows サービスおよび Web サービスを開始または停止します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Public Sub SetServiceState(ByVal EnableWindowsService As Boolean, _  
    ByVal EnableWebService As Boolean, ByVal EnableReportManager As Boolean, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetSecureConnectionLevel(Boolean EnableWindowsService,  
    Boolean EnableWebService, Boolean EnableReportManager, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>パラメーター  
 *EnableWindowsService*  
 Windows サービスの状態を示す `Boolean` 値。 値が `true` の場合はレポート サーバー Windows サービスを開始し、`false` の場合はレポート サーバー Windows サービスを停止します。  
  
 *EnableWebService*  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web サービスの状態を示す `Boolean` 値。 値が `true` の場合はレポート サーバー Web サービスを開始し、`false` の場合はレポート サーバー Web サービスを停止します。  
  
 *EnableReportManager*  
 レポート マネージャーの目的の状態を示す `Boolean` 値。  
  
 *HRESULT*  
 [out] 呼び出しの成功または失敗を示す値。  
  
## <a name="return-value"></a>戻り値  
 メソッド呼び出しの成功または失敗を示す *HRESULT* を返します。 値 0 は、メソッド呼び出しが成功したことを示します。 0 以外の値は、エラーが発生したことを示します。  
  
## <a name="remarks"></a>コメント  
  
## <a name="requirements"></a>必要条件  
 **名前空間:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>関連項目  
 [MSReportServer_ConfigurationSetting メンバー](msreportserver-configurationsetting-members.md)  
  
  
