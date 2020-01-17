---
title: DisplayName プロパティ (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- DisplayName Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- DisplayName property
ms.assetid: 49c408aa-6eb4-45cd-8d5c-60f065f24f5c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3103c9d91b8cc55c5f99f3cfa545207483e97e35
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73659714"
---
# <a name="displayname-property-sqlservice-class"></a>DisplayName プロパティ (SqlService クラス)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  サービスの表示名を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.DisplayName [= value]  
```  
  
## <a name="parts"></a>要素  
 *object*  
 サービスを表す [SqlService クラス](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) オブジェクト。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 サービスの表示名を指定する文字列値。  
  
## <a name="remarks"></a>解説  
 この文字列の長さは最大 256 文字です。 名前は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 構成マネージャーで大文字と小文字が区別されます。 ただし、表示名の比較時には、常に大文字と小文字は区別されません。  
  
## <a name="example"></a>例  
  
```  
mysqlservice.DisplayName = "Atdisk"  
```  
  
## <a name="see-also"></a>参照  
 [サービスの開始と停止](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
