---
title: 'ISSCommandWithParameters:: SetParameterProperties (OLE DB) |Microsoft Docs'
description: ISSCommandWithParameters::SetParameterProperties (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSCommandWithParameters::SetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- SetParameterProperties method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: b9f5a3251b05453d01b2ef984c6a9ea7bde1c115
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015392"
---
# <a name="isscommandwithparameterssetparameterproperties-ole-db"></a>ISSCommandWithParameters::SetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  序数順に各パラメーターのパラメーター プロパティを設定するか、SSPARAMPROPS 構造体の配列を指定して、一括でパラメーター プロパティを設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT SetParameterProperties(  
      DB_UPARAMS cParams,   
      SSPARAMPROPS rgParamProperties[]);  
```  
  
## <a name="arguments"></a>引数  
 *cParams*[in]  
 *rgParamProperties* 配列内の SSPARAMPROPS 構造体の数。 この数が 0 の場合、**ISSCommandWithParameters::SetParameterProperties** では、コマンドのパラメーターに指定されているすべてのプロパティを削除します。  
  
 *rgParamProperties*[in]  
 設定する SSPARAMPROPS 構造体の配列。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **ISSCommandWithParameters::SetParameterProperties** メソッドでは、主要な OLE DB **ICommandProperties::SetProperties** メソッドと同じエラー コードを返します。  
  
## <a name="remarks"></a>Remarks  
 このメソッドを使用したパラメーター プロパティの設定は、各パラメーターに対して序数順に行うか、プロパティ配列から SSPARAMPROPS が構築されるたびに **ISSCommandWithParameters::SetParameterProperties** を 1 回呼び出すことによって行うことができます。  
  
 **ISSCommandWithParameters::SetParameterProperties** メソッドを呼び出す前に、**SetParameterInfo** メソッドを呼び出す必要があります。 `SetParameterProperties(0, NULL)` を呼び出すと、指定したパラメーター プロパティがすべて消去されます。また、`SetParameterInfo(0,NULL,NULL)` を呼び出すと、パラメーターに関連付けられているすべてのプロパティを含めて、パラメーターに関するすべての情報が消去されます。  
  
 **ISSCommandWithParameters::SetParameterProperties** を呼び出すときに DBTYPE_XML 型または DBTYPE_UDT 型以外のパラメーターのプロパティを指定すると、DB_E_ERRORSOCCURRED または DB_S_ERRORSOCCURRED が返され、そのパラメーターの SSPARAMPROPS に含まれているすべての DBPROP の *dwStatus* フィールドに DBPROPSTATUS_NOTSET が設定されます。 DB_E_ERRORSOCCURRED または DB_S_ERRORSOCCURRED が指しているパラメーターを検出するには、SSPARAMPROPS に含まれている各 DBPROPSET の DBPROP 配列をすべて調べる必要があります。  
  
 **ISSCommandWithParameters::SetParameterProperties** を呼び出すときに、**SetParameterInfo** によって情報が設定されていないパラメーターのプロパティを指定すると、プロバイダーは次のエラー メッセージと共に E_UNEXPECTED を返します。  
  
 パラメーターを指定して SetParameterProperties メソッドを呼び出す場合は、最初に SetParameterInfo メソッドを呼び出す必要があります。 パラメーターのプロパティを設定する前に、パラメーター情報を設定する必要があります。  
  
 **ISSCommandWithParameters::SetParameterProperties** を呼び出すときに、情報が設定されているパラメーターと設定されていないパラメーターが含まれている場合、SSPARAMPROPS プロパティ セットの DBPROPSET 内の dwStatus プロパティに DBSTATUS_NOTSET が設定されて返されます。  
  
 SSPARAMPROPS 構造体は、次のように定義されています。  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
 で始まるデータベースエンジンの機能強化[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] isscommandwithparameters:: setparameterproperties を使用すると、予期される結果についてより正確な説明を取得できます。 これらのより正確な結果は、以前のバージョンの[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]で ISSCommandWithParameters:: setparameterproperties によって返される値とは異なる場合があります。 詳細については、「[メタデータの検出](../../oledb/features/metadata-discovery.md)」を参照してください。  
  
|メンバー|[説明]|  
|------------|-----------------|  
|*iOrdinal*|渡されるパラメーターの序数|  
|*cPropertySets*|*rgPropertySets* 内の DBPROPSET 構造体の数|  
|*rgPropertySets*|DBPROPSET 構造体の配列を返すメモリへのポインター|  
  
## <a name="see-also"></a>参照  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
