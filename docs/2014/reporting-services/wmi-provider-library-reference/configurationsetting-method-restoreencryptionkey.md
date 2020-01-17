---
title: RestoreEncryptionKey メソッド (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- RestoreEncryptionKey (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- RestoreEncryptionKey method
ms.assetid: 37e949f5-15af-4858-848a-f482ee94fcd9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d4cb556e127fa23f5b16506abdcc8e04ed433878
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66098124"
---
# <a name="restoreencryptionkey-method-wmi-msreportserverconfigurationsetting"></a>RestoreEncryptionKey メソッド (WMI MSReportServer_ConfigurationSetting)
  指定した暗号化キーをレポート サーバー データベースに再適用します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Public Sub RestoreEncryptionKey(ByRef KeyFile() As Integer, _  
    ByRef Length As Int32, ByVal Password As String, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void RestoreEncryptionKey(out Byte[] KeyFile, out Int32 Length,   
            string Password, out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>パラメーター  
 *KeyFile[]*  
 [out] 暗号化された暗号化キーを含む配列。  
  
 *Length*  
 [out] メソッドによって返される配列の長さ。  
  
 *Password*  
 暗号化キーの暗号化に使用される文字列。  
  
 *HRESULT*  
 [out] 呼び出しの成功または失敗を示す値。  
  
 *ExtendedErrors[]*  
 [out] 呼び出しによって返されたその他のエラーを含む文字列の配列。  
  
## <a name="return-value"></a>戻り値  
 メソッド呼び出しの成功または失敗を示す *HRESULT* を返します。 値 0 は、メソッド呼び出しが成功したことを示します。 0 以外の値は、エラーが発生したことを示します。  
  
## <a name="remarks"></a>コメント  
 レポート サーバー データベースのレポート サーバーに既にエントリが存在する場合、そのエントリは削除されます。 その後、指定した暗号化キーとレポート サーバーの公開キーを使用して、新しいエントリが作成されます。  
  
 このメソッドが最も効果的なのは、暗号化キーの一覧を消去する [DeleteEncryptionKey](configurationsetting-method-deleteencryptionkey.md) メソッドの後に呼び出した場合です。  
  
## <a name="requirements"></a>必要条件  
 **名前空間:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>参照  
 [MSReportServer_ConfigurationSetting メンバー](msreportserver-configurationsetting-members.md)  
  
  
