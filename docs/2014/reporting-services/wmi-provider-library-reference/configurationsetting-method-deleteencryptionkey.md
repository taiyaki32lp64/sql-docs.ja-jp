---
title: DeleteEncryptionKey メソッド (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- DeleteEncryptionKey (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- DeleteEncryptionKey method
ms.assetid: ed2f25b6-6a63-468d-9279-a577ca01b096
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cbf0eee13a113dff42a22da3703e60b3869b757f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66098528"
---
# <a name="deleteencryptionkey-method-wmi-msreportserverconfigurationsetting"></a>DeleteEncryptionKey メソッド (WMI MSReportServer_ConfigurationSetting)
  レポート サーバー データベースから暗号化キーを削除します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Public Sub DeleteEncryptionKeys(ByVal InstallationID As String, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void DeleteEncryptionKeys(string InstallationID, out Int32 HRESULT,   
    out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>パラメーター  
 *InstallationID*  
 レポート サーバー データベースのキー テーブルにあるレポート サーバーのインストール ID。  
  
 *HRESULT*  
 [out] 呼び出しの成功または失敗を示す値。  
  
 *ExtendedErrors[]*  
 [out] 呼び出しによって返されたその他のエラーを含む文字列の配列。  
  
## <a name="return-value"></a>戻り値  
 メソッド呼び出しの成功または失敗を示す HRESULT を返します。 値 0 は、メソッド呼び出しが成功したことを示します。 0 以外の値は、エラーが発生したことを示します。  
  
## <a name="remarks"></a>コメント  
 *DeleteEncryptionKey* メソッドは、レポート サーバー データベースのセキュリティで保護された情報にアクセスするレポート サーバーのキー テーブルからエントリを削除します。 指定した *InstallationID* パラメーターがデータベースのインストール ID に対応しない場合、メソッドはエラーを返します。  
  
## <a name="requirements"></a>必要条件  
 **名前空間:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>関連項目  
 [MSReportServer_ConfigurationSetting メンバー](msreportserver-configurationsetting-members.md)  
  
  
