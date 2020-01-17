---
title: SetVirtualDirectory メソッド (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SetVirtualDirectory method
ms.assetid: 1a25cb1d-38d5-401a-970b-87b642a780e4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e68bb7c70d08fb07d3079436fafe5fd61ae104f1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66097917"
---
# <a name="setvirtualdirectory-method-wmi-msreportserverconfigurationsetting"></a>SetVirtualDirectory メソッド (WMI MSReportServer_ConfigurationSetting)
  指定したアプリケーションの仮想ディレクトリの名前を設定します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Public Sub SetVirtualDirectory(ByVal Application As String, _  
    ByVal VirtualDirectory As String, ByVal lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetVirtualDirectory(string Application, string VirtualDirectory,   
       int Lcid,out string Error, out int HRESULT);  
```  
  
## <a name="parameters"></a>パラメーター  
 *アプリケーション*  
 仮想ディレクトリを設定するアプリケーションの名前。  
  
 *VirtualDirectory*  
 仮想ディレクトリの名前。  
  
 *lcid*  
 仮想ディレクトリのロケール ID。  
  
 *[エラー]*  
 [out] 発生したエラーの説明。  
  
 *HRESULT*  
 [out] 呼び出しの成功または失敗を示す値。  
  
## <a name="return-value"></a>戻り値  
 メソッド呼び出しの成功または失敗を示す *HRESULT* を返します。 値が 0 の場合はメソッド呼び出しが正常に完了したことを示します。エラー コードの場合は呼び出しが失敗したことを示します。  
  
## <a name="remarks"></a>コメント  
 アプリケーションは、すべての URL 予約に対して仮想ディレクトリの名前を 1 つだけ持つことができます。  
  
 VirtualDirectory に指定する値は、仮想ディレクトリの名前付け規則に準拠している必要があります。 VirtualDirectory には空の文字列または空白を指定できません。  
  
 Configuration\URLReservations\Application\VirtualDirectory 要素の値を更新します。 URL 予約が作成されていない場合でも成功します。  
  
## <a name="requirements"></a>必要条件  
 **名前空間:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>関連項目  
 [MSReportServer_ConfigurationSetting メンバー](msreportserver-configurationsetting-members.md)  
  
  
