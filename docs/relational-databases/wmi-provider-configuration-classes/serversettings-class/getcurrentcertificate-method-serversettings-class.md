---
title: GetCurrentCertificate メソッド (ServerSettings)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- GetCurrentCertificate Method (ServerSettings Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- GetCurrentCertificate method
ms.assetid: 450e33c6-91d4-420f-ab7c-1905111f5658
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4e5d3ad1a0caf0eb2fd835d04ed80e0a2a044983
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73659319"
---
# <a name="getcurrentcertificate-method-serversettings-class"></a>GetCurrentCertificate メソッド (ServerSettings クラス)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  現在のセキュリティ証明書を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.GetCurrentCertificate(SHA)  
```  
  
## <a name="parts"></a>要素  
 *object*  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンス上のサーバー設定を表す**serversettings**オブジェクト。  
  
#### <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|---------------|-----------------|  
|*SHA*|メソッドの完了後に現在のセキュリティ証明書を指定する文字列オブジェクトの値 (出力パラメーター)|  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 **uint32** 値。サービスが正常に変更された場合は 0、要求がサポートされていない場合は 1 になります。それ以外の数値はエラーを示します。  
  
## <a name="remarks"></a>解説  
  
## <a name="see-also"></a>参照  
 [サーバーネットワークプロトコルと Net-library の構成](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
