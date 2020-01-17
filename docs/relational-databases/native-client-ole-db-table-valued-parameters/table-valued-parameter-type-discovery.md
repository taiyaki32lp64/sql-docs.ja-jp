---
title: テーブル値パラメーターの型の検出 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, type discovery
ms.assetid: f55818c2-ebb5-4cf6-8c0c-0da41f592560
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 92bd68e69cd3127bdb2dabd6b94b1097b47e48c4
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73788570"
---
# <a name="table-valued-parameter-type-discovery"></a>テーブル値パラメーターの型の検出
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  コンシューマー (つまり、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーを使用するクライアントアプリケーション) は、コマンドテキストが OLE DB プロバイダーに与えられていれば、各コマンドパラメーターの型を検出できます。 テーブル値パラメーターの型がわかったら、コンシューマーはテーブル値パラメーターの個別の列ごとにメタデータ情報を検出できます。  
  
 プロシージャパラメーターの型情報は、ほとんどのパラメーターの型に対して ICommandWithParameters:: GetParameterInfo でサポートされています。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降では、ユーザー定義型および **xml** データ型の導入に伴い、ICommandWithParameters によりユーザー定義型の情報 (名前、スキーマ、およびカタログ) を提供することができなくなったため、GetParameterInfo メソッドは十分に目的を果たしていませんでした。 拡張型情報を提供するために、ISSCommandWithParameters という新しいインターフェイスが定義されました。  
  
 テーブル値パラメーターの場合は、ISSCommandWithParameters インターフェイスを使用して詳細情報を検出することもできます。 クライアントは、コマンドオブジェクトを準備した後で ISSCommandWithParameters:: GetParameterInfo を呼び出します。 テーブル値パラメーターでは、DBPARAMINFO 構造体の *wType* メンバーが、プロバイダーによって DBTYPE_TABLE に設定されます。 DBPARAMINFO 構造体の *ulParamSize* フィールドの値は ~0 です。  
  
 コンシューマーは、次に ISSCommandWithParameters::GetParameterProperties を使用して、追加のプロパティ (テーブル値パラメーターの型のカタログ名、テーブル値パラメーターの型のスキーマ名、テーブル値パラメーターの型名、列の順序、および既定の列) を要求します。  
  
 型名がわかったら、コンシューマーは個々の列情報を取得するために、IOpenRowset::OpenRowset を呼び出すか、テーブル値パラメーターの型名をテーブル名として指定して、DBSCHEMA_TABLE_TYPE_COLUMNS 行セットを取得する必要があります。  
  
## <a name="see-also"></a>参照  
 [テーブル値パラメーター &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [テーブル値パラメーターの使用 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
