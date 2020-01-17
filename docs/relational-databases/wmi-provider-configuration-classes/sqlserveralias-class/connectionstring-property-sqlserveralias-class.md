---
title: ConnectionString プロパティ (SqlServerAlias)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ConnectionString Property (SqlServerAlias Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
helpviewer_keywords:
- ConnectionString property
ms.assetid: 8a3692b9-3a34-42e2-b0b9-28e6bd3a7aba
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 435bb6ab0585b7f453fe035fa99be913dffbf769
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73659005"
---
# <a name="connectionstring-property-sqlserveralias-class"></a>ConnectionString プロパティ (SqlServerAlias クラス)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  サーバー接続別名に対応する接続を確立するために使用される接続文字列を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.ConnectionString [= value]  
```  
  
## <a name="parts"></a>要素  
 *object*  
 [の別名を表す](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md) SqlServerAlias クラス [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オブジェクト。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 サーバー接続別名に対応する接続を確立するために使用される接続文字列を指定する文字列。  
  
## <a name="remarks"></a>解説  
  
