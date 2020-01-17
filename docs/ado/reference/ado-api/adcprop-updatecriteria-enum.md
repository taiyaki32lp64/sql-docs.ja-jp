---
title: ADCPROP_UPDATECRITERIA_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_UPDATECRITERIA_ENUM
helpviewer_keywords:
- ADCPROP_UPDATECRITERIA_ENUM [ADO]
ms.assetid: 33fd7b65-2ec8-4f62-91a7-630b5dab1aa2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 12d960e8fcd5e1f27ea8198ce52e080f6fddf7c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921412"
---
# <a name="adcpropupdatecriteriaenum"></a>ADCPROP_UPDATECRITERIA_ENUM
オプティミスティックを持つデータ ソースの行の更新中に競合を検出するために使用できるフィールドに指定する[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト。  
  
 これらの定数を使用して、**レコード セット**"**更新基準**"で参照されている、動的なプロパティ、 [ADO Dynamic プロパティ インデックス](../../../ado/reference/ado-api/ado-dynamic-property-index.md)に記載されていると[OLE DB 用の Microsoft カーソル サービス](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)ドキュメント。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adCriteriaAllCols**|1|データ ソースの行の任意の列が変更されている場合は、競合を検出します。|  
|**adCriteriaKey**|0|競合の場合は、キー列のデータのソース行が変更されている行が削除されていることを検出します。|  
|**adCriteriaTimeStamp**|3|競合の場合、ソース行のデータのタイムスタンプが変更されている行が後にアクセスされたことを検出、**レコード セット**が取得されます。|  
|**adCriteriaUpdCols**|2|更新されたフィールドに対応して、データ ソースの列のいずれかの行を場合に競合を検出、 **Recordset**が変更されました。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 パッケージ: **com.ms.wfc.data**  
  
|定数|  
|--------------|  
|AdoEnums.AdcPropUpdateCriteria.ALLCOLS|  
|AdoEnums.AdcPropUpdateCriteria.KEY|  
|AdoEnums.AdcPropUpdateCriteria.TIMESTAMP|  
|AdoEnums.AdcPropUpdateCriteria.UPDCOLS|
