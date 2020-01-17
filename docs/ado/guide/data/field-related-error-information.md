---
title: フィールドに関連するエラー情報 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- field-related errors [ADO]
- errors [ADO], field-related
ms.assetid: 5e7b1af4-996b-47c5-9161-c5575ad4fec9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7094c2dba004e35593f5ab11b1162efbdf3283c1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925312"
---
# <a name="field-related-error-information"></a>フィールドに関連するエラー情報
エラーは、フィールドに直接関連している場合など、データが不足している場合、または、フィールドに対して無効な型である場合を取得できます、問題の原因の詳細についてを調べることで、**フィールド**オブジェクトの**ステータス**プロパティ。 このプロパティは、問題の特定の情報を提供する拡張されています。 そのため、たとえばへの呼び出し時に**UpdateBatch**失敗した場合、問題の原因を調べることで決定できます、**状態**のプロパティ、**フィールド**影響を受ける各レコードがあります。 内の値のいずれかのプロパティには、 **FieldStatusEnum**定数。 次の表には、エラーが発生したときに特定の関心のあるこれらの値が含まれています。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adFieldCantConvertValue**|2|フィールドを取得またはデータの損失なしで保存できないことを示します。|  
|**adFieldDataOverflow**|6|プロバイダーから返されるデータが、フィールドのデータ型がオーバーフローしたことを示します。|  
|**adFieldDefault**|13|データを設定するときに、フィールドの既定値が使用されたことを示します。|  
|**adFieldIgnore**|15|ソースの値をデータを設定する場合に、このフィールドがスキップされたことを示します。 プロバイダーによって値が設定されていません。|  
|**adFieldIntegrityViolation**|10|計算された、または派生エンティティであるフィールドを変更できないことを示します。|  
|**adFieldIsNull**|3|プロバイダーが null 値を返すことを示します。|  
|**adFieldOutOfSpace**|22|プロバイダーが、移動が完了または操作をコピーするための十分な記憶域スペースを取得できないことを示します。|
