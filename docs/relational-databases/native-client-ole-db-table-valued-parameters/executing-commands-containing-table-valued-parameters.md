---
title: テーブル値パラメーターを持つコマンド
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, executing commands containing
ms.assetid: 7ecba6f6-fe7a-462a-9aa3-d5115b6d4529
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a41e0e4993bc9a742f4b116ec2434fd3d8c09b76
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75242750"
---
# <a name="executing-commands-containing-table-valued-parameters"></a>テーブル値パラメーターを含むコマンドの実行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  テーブル値パラメーターを含むコマンドを実行するには、次の 2 つのフェーズが必要になります。  
  
1.  パラメーターの型を指定する。  
  
2.  パラメーター データをバインドする。  

## <a name="table-valued-parameter-specification"></a>テーブル値パラメーターの指定  
 コンシューマーは、テーブル値パラメーターの型を指定できます。 この情報には、テーブル値パラメーターの型名が含まれます。 また、テーブル値パラメーターのユーザー定義テーブル型が接続の現在の既定のスキーマにない場合は、スキーマ名も含まれます。 サーバーでサポートされているかどうかに応じて、コンシューマーでは、省略可能なメタデータ情報 (列の順序など) を指定したり、特定の列のすべての行に既定値が設定されるよう指定したりすることもできます。  
  
 コンシューマーは、テーブル値パラメーターを指定するために、ISSCommandWithParameter:: SetParameterInfo を呼び出します。オプションで Isscommandwithparameter:: SetParameterProperties を呼び出すこともできます。 テーブル値パラメーターの場合、DBPARAMBINDINFO 構造体の *pwszDataSourceType* フィールドの値は DBTYPE_TABLE になります。 
  *ulParamSize* フィールドには ~0 が設定され、長さが不明であることを示します。 スキーマ名、型名、列の順序、既定の列など、テーブル値パラメーターの特定のプロパティは、ISSCommandWithParameters:: SetParameterProperties を使用して設定できます。  
  
## <a name="table-valued-parameter-binding"></a>テーブル値パラメーターのバインド  
 テーブル値パラメーターには、任意の行セット オブジェクトを指定できます。 プロバイダーは、実行中、このオブジェクトからテーブル値パラメーターを読み取って、サーバーに送信します。  
  
 テーブル値パラメーターをバインドするために、コンシューマーは IAccessor:: CreateAccessor を呼び出します。 テーブル値パラメーターの DBBINDING 構造体の *wType* フィールドには、DBTYPE_TABLE が設定されます。 DBBINDING 構造体の *pObject* メンバーは NULL ではなく、*pObject* の *iid* メンバーは IID_IRowset、またはその他のテーブル値パラメーターの行セット オブジェクト インターフェイスに設定されます。 DBBINDING 構造体の残りのフィールドは、ストリームされた BLOB の場合と同じように設定する必要があります。  
  
 テーブル値パラメーターと、テーブル値パラメーターに関連付けられる行セット オブジェクトのバインドでは、次の制限が適用されます。  
  
-   テーブル値パラメーターの行セット列データに許容される状態値は DBSTATUS_S_ISNULL と DBSTATUS_S_OK だけです。 DBSTATUS_S_DEFAULT ではエラーが発生し、バインド状態値が DBSTATUS_E_BADSTATUS に設定されます。  
  
-   テーブル値パラメーターは DBSTATUS_S_DEFAULT 状態でマークできます。 有効な値は DBSTATUS_S_DEFAULT と DBSTATUS_S_OK だけです。 状態が DBSTATUS_S_DEFAULT に設定された場合、テーブル値パラメーターの値は、空のテーブルに対応します。  
  
-   テーブル値パラメーターの読み取り専用列 (ID 列または計算列) は、SSPROP_PARAM_TABLE_DEFAULT_COLUMNS プロパティを使って、既定としてマークする必要があります。 既定値を持つ列も、特定のテーブル値パラメーターの列のデータ値用に既定値を使用できるように、SSPROP_PARAM_TABLE_DEFAULT_COLUMNS プロパティで、既定としてマークする必要があります。 既定としてマークされた列にバインドされたデータ値は、プロバイダーによって無視されます。  
  
-   SSPROP_PARAM_TABLE_DEFAULT も設定されない限り、データは、DBPROP_COL_AUTOINCREMENT または SSPROP_COL_COMPUTED が設定された列を想定して、サーバーに送信されます。  
  
## <a name="see-also"></a>参照  
 [テーブル値パラメーター &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [テーブル値パラメーターを使用する &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
