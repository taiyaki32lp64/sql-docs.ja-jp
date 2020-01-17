---
title: 0 (整数) メソッド (java. Timestamp, int) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 114f55af-62ab-4c60-8724-0affbbbbbcdc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c13438851fdc543a3567abdc001af5b5b9e726fc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001552"
---
# <a name="valueof-method-javasqltimestamp-int"></a>valueOf (java.sql.Timestamp, int) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  引数に java.sql.Timestamp 値とオフセット (分) を示す値を受け取って、GMT からの特定のオフセットで特定の時点を表す **DateTimeOffset** オブジェクトを作成します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public static DateTimeOffset valueOf(java.sql.Timestamp timestamp, int minutesOffset)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *timestamp*  
  
 java.sql.Timestamp値です。  
  
 *minutesOffset*  
  
 分単位のオフセットです。  
  
## <a name="return-value"></a>戻り値  
 GMT から指定されたオフセット (分単位) で、java. Timestamp オブジェクトによって指定された特定の時点を表す DateTimeOffset オブジェクトを返します。  
  
## <a name="see-also"></a>参照  
 [DateTimeOffset クラス](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset のメンバー](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
