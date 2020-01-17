---
title: CreateSSLCertificateBinding メソッド (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- CreateSSLCertificateBinding
ms.assetid: 407d50e4-0a55-43cb-8ddf-2d82714071b1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f16b86b1343d83c44819427b8ba6c43726798e93
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66098539"
---
# <a name="createsslcertificatebinding-method-wmi-msreportserverconfigurationsetting"></a>CreateSSLCertificateBinding メソッド (WMI MSReportServer_ConfigurationSetting)
  SSL 証明書のバインドを作成します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Public Sub CreateSSLCertificateBinding(ByVal Application As String, _  
    ByVal CertificateHash As String, ByVal IPAddress As String, _  
    ByVal Port As Int32, ByVal lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void CreateSSLCertificateBinding(string application,   
    string certificateHash, string IPAddress, int Port,   
    int lcid, out string error, out int HRESULT);  
```  
  
## <a name="parameters"></a>パラメーター  
 *アプリケーション*  
 証明書のバインドを作成する必要があるアプリケーションの名前。  
  
 *CertificateHash*  
 証明書のハッシュ。  
  
 *IPAddress*  
 アプリケーションの IP アドレス。  
  
 *ポート*  
 バインドに関連付けられた SSL ポート。  
  
 *Lcid*  
 返されるエラー メッセージに使用するロケール。  
  
 *Error*  
 [out] 発生したエラーの説明。  
  
 *HRESULT*  
 [out] 呼び出しの成功または失敗を示す値。  
  
## <a name="return-value"></a>戻り値  
 メソッド呼び出しの成功または失敗を示す *HRESULT* を返します。 値が 0 の場合はメソッド呼び出しが正常に完了したことを示します。エラー コードの場合は呼び出しが失敗したことを示します。  
  
## <a name="remarks"></a>コメント  
 このメソッドは、アプリケーションの rsreportserver.config にバインドを追加します。 バインドが HTTP.SYS に存在しない場合は作成されます。  
  
 バインドを作成する前に、メソッドの呼び出しによって、指定されたアプリケーションの URL 予約が調査され、SSL 証明書のバインドが有効かどうかが確認されます。  
  
 次の条件が検証されて、その結果エラーが発生する場合があります。  
  
1.  証明書が存在しない。  
  
2.  指定された IP アドレスがこのコンピューターの IP アドレスと一致しない。  
  
3.  指定された IP アドレスが DHCP の IP アドレス (定期的に変更される) であるため、代わりにワイルドカードの IP アドレス (0.0.0.0) が使用されている。  
  
4.  指定された IP アドレスが URL 予約の IP アドレスと一致せず、ワイルドカードまたはホスト名の URL 予約も存在しない。  
  
5.  ホスト名を指定する URL 予約は存在するが、ホスト名が証明書のホスト名と一致しない。  
  
## <a name="requirements"></a>必要条件  
 **名前空間:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>参照  
 [MSReportServer_ConfigurationSetting メンバー](msreportserver-configurationsetting-members.md)  
  
  
