---
title: GenerateDatabaseUpgradeScript メソッド (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- GenerateDatabaseUpgradeScript (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- GenerateDatabaseUpgradeScript method
ms.assetid: 88534e8e-2877-41cd-b5c2-b1d33a0fd203
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5309932735310bc0e794d10766312b650b6eb934
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/11/2019
ms.locfileid: "56018973"
---
# <a name="generatedatabaseupgradescript-method-wmi-msreportserverconfigurationsetting"></a>GenerateDatabaseUpgradeScript メソッド (WMI MSReportServer_ConfigurationSetting)
  レポート サーバー データベースを [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] スキーマにアップグレードする場合に使用できるスクリプトを生成します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Public Sub GenerateDatabaseUpgradeScript(DatabaseName as String, _  
    ServerVersion as String, ByRef Script as String, _  
    ByRef HRESULT as Int32)  
```  
  
```csharp  
public void GenerateDatabaseUpgradeScript (string DatabaseName,   
    string ServerVersion, out string Script,   
    out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>パラメーター  
 *Databasename*  
 更新するレポート サーバー データベースの名前を含む文字列。  
  
 *ServerVersion*  
 レポート サーバーのバージョンを表す文字列。  
  
 *[スクリプト]*  
 [out] 生成された SQL スクリプトを含む文字列。  
  
 *HRESULT*  
 [out] 呼び出しの成功または失敗を示す値。  
  
## <a name="return-value"></a>戻り値  
 メソッド呼び出しの成功または失敗を示す *HRESULT* を返します。 値 0 は、メソッド呼び出しが成功したことを示します。 0 以外の値は、エラーが発生したことを示します。  
  
## <a name="remarks"></a>コメント  
 生成されたスクリプトは、 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、および [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]をサポートします。  
  
## <a name="requirements"></a>必要条件  
 **名前空間:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>参照  
 [MSReportServer_ConfigurationSetting メンバー](msreportserver-configurationsetting-members.md)  
  
  
