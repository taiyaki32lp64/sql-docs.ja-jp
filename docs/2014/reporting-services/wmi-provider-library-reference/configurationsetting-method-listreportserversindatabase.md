---
title: ListReportServersInDatabase メソッド (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- ListReportServersInDatabase (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- ListReportServersInDatabase method
ms.assetid: a4bf5968-c46f-484f-a510-65e2dde65a0d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c62e2793f11853158b7b31d1e79feb4ae59977de
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66098293"
---
# <a name="listreportserversindatabase-method-wmi-msreportserverconfigurationsetting"></a>ListReportServersInDatabase メソッド (WMI MSReportServer_ConfigurationSetting)
  セキュリティで保護された情報にアクセスできるかどうかに関係なく、レポート サーバー データベースにあるレポート サーバー インストールの一覧を返します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Public Sub ListReportServersInDatabase(ByRef MachineNames() As String, _  
    ByRef InstanceNames() As String, ByRef InstallationIDs() As String, _  
    ByRef IsInitialized() As Boolean, ByRef Length As Int32, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void ListReportServersInDatabase (out string[] MachineNames,   
    out string[] InstanceNames, out string[] InstallationIDs,   
    out Boolean[] IsInitialized,out Int32 Length, out Int32 HRESULT,    
    out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>パラメーター  
 *MachineNames[]*  
 [out] データベースのレポート サーバーのコンピューター名を含む配列。  
  
 *InstanceNames[]*  
 [out] データベースの各レポート サーバーのインスタンス名を含む配列。  
  
 *InstallationIDs[]*  
 [out] データベースの各レポート サーバーのインストール ID を含む配列。  
  
 *IsInitialized[]*  
 [out] データベースの各レポート サーバーの初期化状態を含む配列。  
  
 *Length*  
 [out] メソッドによって返される配列の長さ。 返されるすべての配列が同じ長さになります。  
  
 *HRESULT*  
 [out] 呼び出しの成功または失敗を示す値。  
  
 *ExtendedErrors[]*  
 [out] 呼び出しによって返されたその他のエラーを含む文字列の配列。  
  
## <a name="return-value"></a>戻り値  
 メソッド呼び出しの成功または失敗を示す *HRESULT* を返します。 値 0 は、メソッド呼び出しが成功したことを示します。 0 以外の値は、エラーが発生したことを示します。  
  
## <a name="remarks"></a>コメント  
 ListReportServersInDatabase は、セキュリティで保護された情報にアクセスできるかどうかに関係なく、レポート サーバー データベースにあるレポート サーバーの一覧を作成し、各レポート サーバーに関する情報を含む配列セットを返します。  
  
## <a name="requirements"></a>必要条件  
 **名前空間:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>関連項目  
 [MSReportServer_ConfigurationSetting メンバー](msreportserver-configurationsetting-members.md)  
  
  
