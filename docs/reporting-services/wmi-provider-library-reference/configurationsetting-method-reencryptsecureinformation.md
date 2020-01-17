---
title: ReencryptSecureInformation メソッド (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- ReencryptSecureInformation (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- ReencryptSecureInformation method
ms.assetid: 8a487497-c207-45b2-8c92-87c58cc68716
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 84265b1a72d93a2d8de8332e0309093a9a506ea0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65571438"
---
# <a name="configurationsetting-method---reencryptsecureinformation"></a>ConfigurationSetting メソッド - ReencryptSecureInformation
  新しい暗号化キーを生成し、この新しいキーを使用してカタログ内のセキュリティで保護されたすべての情報を再度暗号化します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Public Sub ReencryptSecureInformation(ByRef HRESULT as Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void ReencryptSecureInformation (out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>パラメーター  
 *HRESULT*  
 [out] 呼び出しの成功または失敗を示す値。  
  
 *ExtendedErrors[]*  
 [out] 呼び出しによって返されたその他のエラーを含む文字列の配列。  
  
## <a name="return-value"></a>戻り値  
 メソッド呼び出しの成功または失敗を示す *HRESULT* を返します。 値 0 は、メソッド呼び出しが成功したことを示します。 0 以外の値は、エラーが発生したことを示します。  
  
## <a name="remarks"></a>Remarks  
 ReencryptSecureInformation メソッドを使用することによって、管理者は既存の暗号化キーを新しいキーと置き換えることができます。  
  
 このメソッドを呼び出すと、レポート サーバーが新しい暗号化キーを生成し、新しい暗号化キーを使用してすべての暗号化されたコンテンツを反復処理して再度暗号化します。  
  
 配信拡張機能は、セキュリティで保護された情報を配信設定構造に格納できます。 ReencryptSecureInformation を呼び出すと、レポート サーバーが各サブスクリプションと対応する拡張機能を読み込み、関連付けられた設定に格納された情報を再度暗号化します。  
  
 スケールアウト配置のコンピューターでこのメソッドを実行する場合は、スケールアウト配置の各コンピューターを再度初期化する必要があります。  
  
## <a name="requirements"></a>必要条件  
 **名前空間:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>参照  
 [MSReportServer_ConfigurationSetting メンバー](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
