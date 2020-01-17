---
title: SetServiceState メソッド (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- SetServiceState (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetServiceState method
ms.assetid: 9e1ee42d-b388-4929-89c7-8741b956c3be
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 83aa9fb906fc71b1dfb7fd3d036c119d9b4e41e2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580986"
---
# <a name="configurationsetting-method---setservicestate"></a>ConfigurationSetting メソッド - SetServiceState
  レポート サーバーの Windows サービスおよび Web サービスを開始または停止します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Public Sub SetServiceState(ByVal EnableWindowsService As Boolean, _  
    ByVal EnableWebService As Boolean, ByVal EnableReportManager As Boolean, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetServiceState(Boolean EnableWindowsService,  
    Boolean EnableWebService, Boolean EnableReportManager, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>パラメーター  
 *EnableWindowsService*  
 Windows サービスの状態を示す **Boolean** 値。 値が **true** の場合はレポート サーバー Windows サービスを開始し、 **false** の場合はレポート サーバー Windows サービスを停止します。  
  
 *EnableWebService*  
 **Web サービスの状態を示す** Boolean [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 値。 値が **true** の場合はレポート サーバー Web サービスを開始し、 **false** の場合はレポート サーバー Web サービスを停止します。  
  
 *EnableReportManager*  
 レポート マネージャーの目的の状態を示す **Boolean** 値。
 
 > [!NOTE] 
 > この設定は、SQL Server 2016 Reporting Services 累積更新プログラム 2 の時点で非推奨とされました。 Web ポータルは常に有効になります。 値は無視されます。
  
 *HRESULT*  
 [out] 呼び出しの成功または失敗を示す値。  
  
## <a name="return-value"></a>戻り値  
 メソッド呼び出しの成功または失敗を示す *HRESULT* を返します。 値 0 は、メソッド呼び出しが成功したことを示します。 0 以外の値は、エラーが発生したことを示します。  
  
## <a name="remarks"></a>Remarks  
  
## <a name="requirements"></a>必要条件  
 **名前空間:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>参照  
 [MSReportServer_ConfigurationSetting メンバー](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
