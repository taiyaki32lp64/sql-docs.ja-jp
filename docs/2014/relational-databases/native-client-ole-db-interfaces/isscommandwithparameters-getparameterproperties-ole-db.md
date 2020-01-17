---
title: Isscommandwithparameters::getparameterproperties (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- GetParameterProperties method
ms.assetid: 7f4cc5ea-d028-4fe5-9192-bd153ab3c26c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d492a64b6d8a4e8ddf7de27067f1f0bcfef205e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62638084"
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties (OLE DB)
  SSPARAMPROPS プロパティ セット構造体の配列を返します。各 UDT または XML パラメーターごとに 1 つの SSPARAMPROPS プロパティ セットが返されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT GetParameterProperties(  
DB_UPARAMS *pcParams,  
SSPARAMPROPS **prgParamProperties);  
```  
  
## <a name="arguments"></a>引数  
 *pcParams*[out][in]  
 *prgParamProperties* に返された SSPARAMPROPS 構造体の数を保持するメモリへのポインター。  
  
 *prgParamProperties*[out]  
 SSPARAMPROPS 構造体の配列が返されるメモリへのポインター。 プロバイダーは、構造体のメモリを割り当てます、このメモリをアドレスを返しますコンシューマーでこのメモリを解放する**imalloc::free**場合必要はありません、構造体。 呼び出しの前に**imalloc::free**の*prgParamProperties*、コンシューマーは呼び出す必要がありますも**VariantClear**の*vValue*プロパティバリアントがの参照が含まれている場合、メモリ リークを防ぐために各 DBPROP 構造体のタイプ (たとえば、BSTR です。)場合*pcParams*の出力が 0 個または DB_E_ERRORSOCCURRED 以外のエラーが発生する、プロバイダーのメモリを割り当てられません、確実に*prgParamProperties*出力に null ポインターです。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **GetParameterProperties**メソッドは、主要な OLE DB と同じエラー コードを返します**icommandproperties::getproperties**その DB_S_ERRORSOCCURRED と db_e_errorsoccured は返す以外のメソッドにすることはできません発生します。  
  
## <a name="remarks"></a>コメント  
 **Isscommandwithparameters::getparameterproperties**を一貫して動作**GetParameterInfo**します。 場合[isscommandwithparameters::setparameterproperties](isscommandwithparameters-setparameterproperties-ole-db.md)または**SetParameterInfo**が呼び出されなかったり、cParams に 0 をというまたは**GetParameterInfo**パラメーター情報を派生し、これを返します。 場合**isscommandwithparameters::setparameterproperties**または**SetParameterInfo**の少なくとも 1 つのパラメーターが呼び出された**isscommandwithparameters::getparameterproperties**をこれらのパラメーターに対してのみプロパティを返します**isscommandwithparameters::setparameterproperties**が呼び出されました。 場合**isscommandwithparameters::setparameterproperties**が呼び出された後**isscommandwithparameters::getparameterproperties**または**GetParameterInfo**、後続の呼び出し**isscommandwithparameters::getparameterproperties**をこれらのパラメーターのオーバーライドされた値を返す**isscommandwithparameters::setparameterproperties**が呼び出されました。  
  
 SSPARAMPROPS 構造体は、次のように定義されています。  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
|Member|説明|  
|------------|-----------------|  
|*iOrdinal*|渡されるパラメーターの序数|  
|*cPropertySets*|*rgPropertySets* 内の DBPROPSET 構造体の数|  
|*rgPropertySets*|DBPROPSET 構造体の配列を返すメモリへのポインター|  
  
## <a name="see-also"></a>参照  
 [ISSCommandWithParameters &#40;OLE DB&#41;](isscommandwithparameters-ole-db.md)  
  
  
