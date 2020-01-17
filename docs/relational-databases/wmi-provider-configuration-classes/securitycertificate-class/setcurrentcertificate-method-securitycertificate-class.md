---
title: SetCurrentCertificate メソッド (SecurityCertificate)
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetCurrentCertificate Method (SecurityCertificate Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetCurrentCertificate method
ms.assetid: 04b1a76a-932d-4824-8506-e346afe7554e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 17d637c2b5b4a8f65a2d2e843cdf439d856fdd3f
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73659401"
---
# <a name="setcurrentcertificate-method-securitycertificate-class"></a>SetCurrentCertificate メソッド (SecurityCertificate クラス)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  現在のセキュリティ証明書を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.SetCurrentCertificate(SHA , SQLInstance)  
```  
  
## <a name="parts"></a>要素  
 *object*  
 セキュリティ証明書を表す [SecurityCertificate クラス](../../../relational-databases/wmi-provider-configuration-classes/securitycertificate-class/securitycertificate-class.md) オブジェクト。  
  
#### <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|---------------|-----------------|  
|*SHA*|必要なセキュリティ証明書に対応する SHA (secure hash algorithm) サムプリントを指定する文字列値。|  
|*SQLInstance*|証明書を必要とするインスタンスを指定する文字列値|  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 uint32 値。サービスが正常に変更された場合は 0、要求がサポートされていない場合は 1 になります。それ以外の数値はエラーを示します。  
  
## <a name="remarks"></a>解説  
  
## <a name="see-also"></a>参照  
 [サーバーネットワークプロトコルと Net-library の構成](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
