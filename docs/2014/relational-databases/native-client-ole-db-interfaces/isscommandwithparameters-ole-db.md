---
title: ISSCommandWithParameters (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSCommandWithParameters (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- ISSCommandWithParameters interface
ms.assetid: 3419b7f3-36a3-4863-816e-e641e4e90496
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4de7c6a99afcbd7db7c6e233fb737f129b536b8b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63209767"
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
  **ISSCommandWithParameters**のサポートが公開されます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]XML およびユーザー定義型 (UDT)。 これは、主要な OLE DB インターフェイスから継承される省略可能なインターフェイス**ICommandWithParameters**します。 継承した次の 3 つのメソッドだけでなく**ICommandWithParameters**;**GetParameterInfo**、 **MapParameterNames**、および**SetParameterInfo**;**ISSCommandWithParameters**サーバー固有のデータ型を処理するために使用される 2 つの新しいメソッドを提供します。  
  
> [!NOTE]  
>  **ISSCommandWithParameters**サービス コンポーネントが使用されますが、サービス コンポーネント自体はこのインターフェイスを使用していない場合は、インターフェイスを使用することができます。  
  
|方法|説明|  
|------------|-----------------|  
|[Isscommandwithparameters::getparameterproperties &#40;OLE DB&#41;](isscommandwithparameters-getparameterproperties-ole-db.md)|コマンドに渡された各 UDT パラメーターまたは XML パラメーターごとに、1 つの **SSPARAMPROPS** プロパティ セット構造体を返します。他の型のパラメーターの場合、戻り値はありません。|  
|[Isscommandwithparameters::setparameterproperties &#40;OLE DB&#41;](isscommandwithparameters-setparameterproperties-ole-db.md)|序数順に各パラメーターのパラメーター プロパティを設定するか、**SSPARAMPROPS** 構造体の配列を指定して、一括でパラメーター プロパティを設定します。|  
  
## <a name="see-also"></a>関連項目  
 [インターフェイス&#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [XML データ型の使用](../native-client/features/using-xml-data-types.md)   
 [ユーザー定義型の使用](../native-client/features/using-user-defined-types.md)  
  
  
