---
title: ServerName プロパティ (SqlServerAlias)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ServerName Property (SqlServerAlias Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ServerName property
ms.assetid: 58c82b19-b548-42fa-9c5a-059b606da097
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 979b738b046bb53168bbbbbef4d3d64563f2add0
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73659688"
---
# <a name="servername-property-sqlserveralias-class"></a>ServerName プロパティ (SqlServerAlias クラス)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  サーバー接続別名によって指定された [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスの名前を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.ServerName [= value]  
```  
  
## <a name="parts"></a>要素  
 *object*  
 [の別名を表す](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md) SqlServerAlias クラス [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オブジェクト。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 サーバー接続別名によって参照された [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスの名前を指定する文字列値。  
  
## <a name="remarks"></a>解説  
  
