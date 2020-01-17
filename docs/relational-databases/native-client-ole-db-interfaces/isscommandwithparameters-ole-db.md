---
title: ISSCommandWithParameters (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSCommandWithParameters (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSCommandWithParameters interface
ms.assetid: 3419b7f3-36a3-4863-816e-e641e4e90496
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 08291b998c0f540b56cad59d29433135993487c8
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761962"
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **Isscommandwithparameters**は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML とユーザー定義型 (UDT) のサポートを公開します。 これは、コア OLE DB インターフェイス**ICommandWithParameters**から継承する省略可能なインターフェイスです。 **ICommandWithParameters**から継承された3つのメソッドに加えて、**Getparameterinfo**、 **Mapparameternames**、および**setparameterinfo**;**Isscommandwithparameters**には、サーバー固有のデータ型を処理するために使用される2つの新しいメソッドが用意されています。  
  
> [!NOTE]  
>  **Isscommandwithparameters**インターフェイスは、サービスコンポーネントが使用されている場合に使用できますが、サービスコンポーネント自体はこのインターフェイスを使用しません。  
  
|メソッド|[説明]|  
|------------|-----------------|  
|[ISSCommandWithParameters:: GetParameterProperties &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md)|コマンドに渡された各 UDT パラメーターまたは XML パラメーターごとに、1 つの **SSPARAMPROPS** プロパティ セット構造体を返します。他の型のパラメーターの場合、戻り値はありません。|  
|[ISSCommandWithParameters:: SetParameterProperties &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)|序数順に各パラメーターのパラメーター プロパティを設定するか、**SSPARAMPROPS** 構造体の配列を指定して、一括でパラメーター プロパティを設定します。|  
  
## <a name="see-also"></a>参照  
 [インターフェイス&#40;OLE DB&#41; ](https://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)   
 [XML データ型の使用](../../relational-databases/native-client/features/using-xml-data-types.md)   
 [ユーザー定義型の使用](../../relational-databases/native-client/features/using-user-defined-types.md)  
  
  
