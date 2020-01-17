---
title: InitializeReportServer メソッド (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- InitializeReportServer (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- InitializeReportServer method
ms.assetid: 0304acc2-1fd7-437b-94d9-1c1073dd3ca4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e5612bc9326a359a287501aedc5227436cc576eb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65570865"
---
# <a name="configurationsetting-method---initializereportserver"></a>ConfigurationSetting メソッド - InitializeReportServer
  指定されたレポート サービス インスタンスを初期化します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Public Sub InitializeReportServer(ByVal InstallationID As String, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void InitializeReportServer(string InstallationID,   
    out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>パラメーター  
 *InstallationID*  
 暗号化キーを暗号化するための文字列。暗号化キーを返す前に、この文字列を使用して暗号化されます。  
  
 *HRESULT*  
 [out] 呼び出しの成功または失敗を示す値。  
  
 *ExtendedErrors[]*  
 [out] 呼び出しによって返されたその他のエラーを含む文字列の配列。  
  
## <a name="return-value"></a>戻り値  
 メソッド呼び出しの成功または失敗を示す *HRESULT* を返します。 値 0 は、メソッド呼び出しが成功したことを示します。 0 以外の値は、エラーが発生したことを示します。  
  
## <a name="remarks"></a>Remarks  
 このメソッドを呼び出すと、レポート サーバー データベースのセキュリティで保護された情報にアクセスする暗号化キーが、 *InstallationID*で特定されるレポート サーバーの公開キーを使用して暗号化されます。  
  
 指定したレポート サーバーの公開キーは、レポート サーバー データベースに書き込んでおく必要があります。  
  
 セキュリティで保護された情報に既にアクセスしたレポート サーバーに対して、 *InitializeReportServer* メソッドを呼び出して、暗号化キーの暗号を解除する必要があります。 次に、暗号化された暗号化キーがレポート サーバー データベースに格納されます。  
  
 レポート サーバーの [IsInitialized](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-isinitialized.md) プロパティが **true** に設定されている場合に InitializeReportServer メソッドを呼び出すと、メソッドは暗号化キーの暗号化を試みないで成功を返します。  
  
## <a name="requirements"></a>必要条件  
 **名前空間:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>参照  
 [MSReportServer_ConfigurationSetting メンバー](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
