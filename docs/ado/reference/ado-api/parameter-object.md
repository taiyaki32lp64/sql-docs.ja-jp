---
title: パラメーター オブジェクト |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Parameter
helpviewer_keywords:
- Parameter object [ADO]
ms.assetid: e010e794-7f0f-4026-8b5b-37328e437d63
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 15df27e3dc48decf743a78dd4d147a22dc7cf276
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931661"
---
# <a name="parameter-object"></a>Parameter オブジェクト
パラメーターまたはに関連付けられている引数を表します、[コマンド](../../../ado/reference/ado-api/command-object-ado.md)オブジェクトがパラメーター化クエリまたはストアド プロシージャに基づいています。  
  
## <a name="remarks"></a>コメント  
 プロバイダーの多くは、パラメーター化コマンドをサポートします。 これらは、目的のアクションが 1 回に定義されているコマンドが、変数 (またはパラメーター) は、コマンドのいくつかの詳細を変更するために使用します。 たとえば、SQL SELECT ステートメントは WHERE 句、および並べ替え句の列名を定義するのに別の一致条件を定義するのにパラメーターを使用できます。  
  
 **パラメーター**オブジェクトに関連付けられたパラメーター化クエリは、パラメーターを表しますまたは入力/出力引数と戻り値のストアド プロシージャ。 プロバイダー、いくつかのコレクション、メソッド、またはのプロパティの機能に応じて、**パラメーター**オブジェクトを使用できない可能性があります。  
  
 コレクション、メソッド、およびプロパティの使用、**パラメーター**オブジェクトを次を行うことができます。  
  
-   設定または使用して、パラメーターの名前を取得、[名前](../../../ado/reference/ado-api/name-property-ado.md)プロパティ。  
  
-   設定または使用して、パラメーターの値を返す、[値](../../../ado/reference/ado-api/value-property-ado.md)プロパティ。 **値**の既定のプロパティ、**パラメーター**オブジェクト。  
  
-   設定またはパラメーターの特性を取得、[属性](../../../ado/reference/ado-api/attributes-property-ado.md)、[方向](../../../ado/reference/ado-api/direction-property.md)、[精度](../../../ado/reference/ado-api/precision-property-ado.md)、 [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md)、 [サイズ](../../../ado/reference/ado-api/size-property-ado-parameter.md)、および[型](../../../ado/reference/ado-api/type-property-ado.md)プロパティ。  
  
-   時間の長いバイナリまたは文字データを持つパラメーターを渡す、 [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)メソッド。  
  
-   使用してプロバイダーに固有の属性へのアクセス、[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)コレクション。  
  
 名前がわかっており、パラメーターのプロパティに関連付けられている場合は、呼び出したいストアド プロシージャまたはパラメーター化クエリを使用できます、 [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)メソッドを作成する**パラメーター**オブジェクト使用して適切なプロパティの設定、 [Append](../../../ado/reference/ado-api/append-method-ado.md)メソッドに追加する、[パラメーター](../../../ado/reference/ado-api/parameters-collection-ado.md)コレクション。 これにより、設定およびに電話しなくてもパラメーターの値を取得できます、[更新](../../../ado/reference/ado-api/refresh-method-ado.md)メソッドを**パラメーター**プロバイダーからパラメーター情報を取得するコレクション、可能性がありますリソースを消費する操作です。  
  
 **パラメーター**オブジェクトは、スクリプトを実行することはありません。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [パラメーター オブジェクトのプロパティ、メソッド、およびイベント](../../../ado/reference/ado-api/parameter-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [コマンド オブジェクト (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [CreateParameter メソッド (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Parameters コレクション (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Properties コレクション (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
