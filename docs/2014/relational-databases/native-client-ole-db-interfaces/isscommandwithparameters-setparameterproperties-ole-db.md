---
title: Isscommandwithparameters::setparameterproperties (OLE DB) |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSCommandWithParameters::SetParameterProperties (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- SetParameterProperties method
ms.assetid: 4cd0281a-a2a0-43df-8e46-eb478b64cb4b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 778021ce007f0c1eac68197e0c07e2cb7b0bb001
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62638770"
---
# <a name="isscommandwithparameterssetparameterproperties-ole-db"></a>ISSCommandWithParameters::SetParameterProperties (OLE DB)
  序数順に各パラメーターのパラメーター プロパティを設定するか、SSPARAMPROPS 構造体の配列を指定して、一括でパラメーター プロパティを設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT SetParameterProperties(  
DB_UPARAMS cParams,   
SSPARAMPROPS rgParamProperties[]);  
```  
  
## <a name="arguments"></a>引数  
 *cParams*[in]  
 *rgParamProperties* 配列内の SSPARAMPROPS 構造体の数。 この番号が 0 の場合`ISSCommandWithParameters::SetParameterProperties`コマンドのパラメーターに指定されているすべてのプロパティが削除されます。  
  
 *rgParamProperties*[in]  
 設定する SSPARAMPROPS 構造体の配列。  
  
## <a name="return-code-values"></a>リターン コードの値  
 `ISSCommandWithParameters::SetParameterProperties`メソッドは、主要な OLE DB と同じエラー コードを返します**icommandproperties::setproperties**メソッド。  
  
## <a name="remarks"></a>コメント  
 このメソッドを使用してパラメーターのプロパティを設定または許可されて各パラメーターの序数を 1 つの`ISSCommandWithParameters::SetParameterProperties`プロパティ配列から SSPARAMPROPS が構築された 1 回呼び出します。  
  
 **SetParameterInfo**メソッドを呼び出す前に呼び出す必要があります、`ISSCommandWithParameters::SetParameterProperties`メソッド。 `SetParameterProperties(0, NULL)` を呼び出すと、指定したパラメーター プロパティがすべて消去されます。また、`SetParameterInfo(0,NULL,NULL)` を呼び出すと、パラメーターに関連付けられているすべてのプロパティを含めて、パラメーターに関するすべての情報が消去されます。  
  
 呼び出す`ISSCommandWithParameters::SetParameterProperties`のない型のパラメーター プロパティを指定する dbtype_xml 型または DBTYPE_UDT 返します DB_E_ERRORSOCCURRED または DB_S_ERRORSOCCURRED とマーク、 *dwStatus* SSPARAMPROPS に含まれているすべてのときのフィールドdbpropstatus_notset パラメーター。 DB_E_ERRORSOCCURRED または DB_S_ERRORSOCCURRED が指しているパラメーターを検出するには、SSPARAMPROPS に含まれている各 DBPROPSET の DBPROP 配列をすべて調べる必要があります。  
  
 場合`ISSCommandWithParameters::SetParameterProperties`がパラメーター情報がまだ設定されていないパラメーターのプロパティを指定するために呼び出される**SetParameterInfo**プロバイダーは、次のエラー メッセージと共に E_UNEXPECTED を返します。  
  
 パラメーターを指定して SetParameterProperties メソッドを呼び出す場合は、最初に SetParameterInfo メソッドを呼び出す必要があります。 パラメーターのプロパティを設定する前に、パラメーター情報を設定する必要があります。  
  
 場合に呼び出し`ISSCommandWithParameters::SetParameterProperties`いくつかのパラメーター、パラメーター ヒントが設定されているし、いくつかのパラメーター、パラメーター ヒントが設定されていない、SSPARAMPROPS プロパティ セットの DBPROPSET 内の dwStatus プロパティに DBSTATUS_NOTSET が返さが含まれています。  
  
 SSPARAMPROPS 構造体は、次のように定義されています。  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
 以降では、データベース エンジンの機能強化[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]isscommandwithparameters::setparameterproperties 期待どおりの結果のより正確な記述を取得できるようにします。 これらのより正確な結果の以前のバージョンの isscommandwithparameters::setparameterproperties によって返される値が異なる場合があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 詳細については、次を参照してください。[メタデータ検出](../native-client/features/metadata-discovery.md)します。  
  
|Member|説明|  
|------------|-----------------|  
|*iOrdinal*|渡されるパラメーターの序数|  
|*cPropertySets*|*rgPropertySets* 内の DBPROPSET 構造体の数|  
|*rgPropertySets*|DBPROPSET 構造体の配列を返すメモリへのポインター|  
  
## <a name="see-also"></a>参照  
 [ISSCommandWithParameters &#40;OLE DB&#41;](isscommandwithparameters-ole-db.md)  
  
  
