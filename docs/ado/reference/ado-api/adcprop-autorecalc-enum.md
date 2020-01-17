---
title: ADCPROP_AUTORECALC_ENUM |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_AUTORECALC_ENUM
helpviewer_keywords:
- ADCPROP_AUTORECALC_ENUM [ADO]
ms.assetid: ded4f087-87b9-4efa-8026-bde53d3e9e8a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 738f4cece8cf2355c12c0de4ac42314152c6370a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921440"
---
# <a name="adcpropautorecalcenum"></a>ADCPROP_AUTORECALC_ENUM
タイミングを指定します、 [MSDataShape](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)プロバイダーは、階層レコード セットの集計と計算列を再計算します。  
  
 これらの定数でのみ使用、 **MSDataShape**プロバイダーと**レコード セット**"**自動再計算**"で参照されている、動的なプロパティ、 [ADOプロパティの動的インデックス](../../../ado/reference/ado-api/ado-dynamic-property-index.md)で文書化されていると、 [OLE DB 用の Microsoft カーソル サービス](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)または[Microsoft Data Shaping Service for OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)ドキュメント。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adRecalcAlways**|1|既定値です。 再計算されるたびに、 **MSDataShape**計算列が依存する値が変更されたプロバイダーを決定します。|  
|**adRecalcUpFront**|0|最初に、階層を構築した場合にのみ**Recordset**します。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 これらの定数には、ADO と WFC 対応はありません。
