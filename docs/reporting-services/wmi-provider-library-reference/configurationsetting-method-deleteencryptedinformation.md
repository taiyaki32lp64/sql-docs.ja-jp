---
title: DeleteEncryptedInformation メソッド (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- DeleteEncryptedInformation (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- DeleteEncryptedInformation method
ms.assetid: c14ed187-bdd9-4304-88e3-72072f03c21b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9e86c1964a4ece26115116b8e21c763caaab797b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65572226"
---
# <a name="configurationsetting-method---deleteencryptedinformation"></a>ConfigurationSetting メソッド - DeleteEncryptedInformation
  レポート サーバー データベースから暗号化された情報を削除します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Public Sub DeleteEncryptedInformation(ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void DeleteEncryptedInformation(out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>パラメーター  
 *HRESULT*  
 [out] 呼び出しの成功または失敗を示す値。  
  
 *ExtendedErrors[]*  
 [out] 呼び出しによって返されたその他のエラーを含む文字列の配列。  
  
## <a name="return-value"></a>戻り値  
 メソッド呼び出しの成功または失敗を示す *HRESULT* を返します。 値 0 は、メソッド呼び出しが成功したことを示します。 0 以外の値は、エラーが発生したことを示します。  
  
## <a name="remarks"></a>Remarks  
 このメソッドを呼び出すと、次のデータが削除されます。  
  
-   ユーザー名とパスワードを含む、暗号化されたデータ ソース情報  
  
-   配信拡張機能インターフェイスを使用して暗号化されたサブスクリプション データ  
  
-   レポート サーバー データベースのキー テーブルからのすべての情報  
  
 このメソッドを呼び出した後は、ユーザーがレポート サーバー データベースを使用する各コンピューターを初期化する必要があります。  
  
 DeleteEncryptedInformation メソッドを呼び出しても、レポート サーバー構成ファイルには影響しません。  
  
## <a name="requirements"></a>必要条件  
 **名前空間:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>参照  
 [MSReportServer_ConfigurationSetting メンバー](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
