---
title: テーブル値パラメーターを含むコマンドの実行 | Microsoft Docs
description: テーブル値パラメーターを含むコマンドの実行
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, executing commands containing
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 320a66b84c6a5b904e98941251801c7ee5927087
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994155"
---
# <a name="executing-commands-containing-table-valued-parameters"></a>テーブル値パラメーターを含むコマンドの実行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  テーブル値パラメーターを含むコマンドを実行するには、次の 2 つのフェーズが必要になります。  
  
1.  パラメーターの型を指定する。  
  
2.  パラメーター データをバインドする。  
  
## <a name="table-valued-parameter-specification"></a>テーブル値パラメーターの指定  
 コンシューマーは、テーブル値パラメーターの型を指定できます。 この情報には、テーブル値パラメーターの型名が含まれます。 また、テーブル値パラメーターのユーザー定義テーブル型が接続の現在の既定のスキーマにない場合は、スキーマ名も含まれます。 サーバーでサポートされているかどうかに応じて、コンシューマーでは、省略可能なメタデータ情報 (列の順序など) を指定したり、特定の列のすべての行に既定値が設定されるよう指定したりすることもできます。  
  
 コンシューマーは、テーブル値パラメーターを指定するために、ISSCommandWithParameter:: SetParameterInfo を呼び出します。オプションで Isscommandwithparameter:: SetParameterProperties を呼び出すこともできます。 テーブル値パラメーターの場合、DBPARAMBINDINFO 構造体の *pwszDataSourceType* フィールドの値は DBTYPE_TABLE になります。 *ulParamSize* フィールドには ~0 が設定され、長さが不明であることを示します。 スキーマ名、型名、列の順序、既定の列など、テーブル値パラメーターの特定のプロパティは、ISSCommandWithParameters:: SetParameterProperties を使用して設定できます。  
  
## <a name="table-valued-parameter-binding"></a>テーブル値パラメーターのバインド  
 テーブル値パラメーターには、任意の行セット オブジェクトを指定できます。 プロバイダーは、実行中、このオブジェクトからテーブル値パラメーターを読み取って、サーバーに送信します。  
  
 テーブル値パラメーターをバインドするために、コンシューマーは IAccessor:: CreateAccessor を呼び出します。 テーブル値パラメーターの DBBINDING 構造体の *wType* フィールドには、DBTYPE_TABLE が設定されます。 DBBINDING 構造体の *pObject* メンバーは NULL ではなく、*pObject* の *iid* メンバーは IID_IRowset、またはその他のテーブル値パラメーターの行セット オブジェクト インターフェイスに設定されます。 DBBINDING 構造体の残りのフィールドは、ストリームされた BLOB の場合と同じように設定する必要があります。  
  
 テーブル値パラメーターと、テーブル値パラメーターに関連付けられる行セット オブジェクトのバインドでは、次の制限が適用されます。  
  
-   テーブル値パラメーターの行セット列データに許容される状態値は DBSTATUS_S_ISNULL と DBSTATUS_S_OK だけです。 DBSTATUS_S_DEFAULT ではエラーが発生し、バインド状態値が DBSTATUS_E_BADSTATUS に設定されます。  
  
-   テーブル値パラメーターは DBSTATUS_S_DEFAULT 状態でマークできます。 有効な値は DBSTATUS_S_DEFAULT と DBSTATUS_S_OK だけです。 状態が DBSTATUS_S_DEFAULT に設定された場合、テーブル値パラメーターの値は、空のテーブルに対応します。  
  
-   テーブル値パラメーターの読み取り専用列 (ID 列または計算列) は、SSPROP_PARAM_TABLE_DEFAULT_COLUMNS プロパティを使って、既定としてマークする必要があります。 既定値を持つ列も、特定のテーブル値パラメーターの列のデータ値用に既定値を使用できるように、SSPROP_PARAM_TABLE_DEFAULT_COLUMNS プロパティで、既定としてマークする必要があります。 既定としてマークされた列にバインドされたデータ値は、プロバイダーによって無視されます。  
  
-   SSPROP_PARAM_TABLE_DEFAULT も設定されない限り、データは、DBPROP_COL_AUTOINCREMENT または SSPROP_COL_COMPUTED が設定された列を想定して、サーバーに送信されます。  
  
## <a name="see-also"></a>参照  
 [テーブル値パラメーター &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [テーブル値パラメーターの使用 &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
