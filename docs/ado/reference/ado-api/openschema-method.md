---
title: OpenSchema メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::OpenSchema
- Connection15::raw_OpenSchema
helpviewer_keywords:
- OpenSchema method [ADO]
ms.assetid: 850cf3ce-f18f-4e7c-8597-96c1dc504866
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b2080145e00c658288f9d34e3fa42ed335e0c1d9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931860"
---
# <a name="openschema-method"></a>OpenSchema メソッド
プロバイダーからデータベース スキーマ情報を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Set recordset = connection.OpenSchema(QueryType, Criteria, SchemaID)  
```  
  
## <a name="return-value"></a>戻り値  
 返します、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)スキーマ情報を含むオブジェクト。 **Recordset**の静的な読み取り専用カーソルとして開かれます。 *QueryType*に表示する列を指定、 **Recordset**します。  
  
#### <a name="parameters"></a>パラメーター  
 *QueryType*  
 すべて[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)スキーマ クエリの実行の種類を表す値です。  
  
 *条件*  
 任意。 配列の各クエリの制約の*QueryType*オプション、記載されている[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)します。  
  
 *SchemaID*  
 OLE DB 仕様で定義されていないプロバイダー スキーマ クエリの GUID です。 このパラメーターは必要な場合*QueryType*に設定されている**adSchemaProviderSpecific**。 それ以外は使用されません。  
  
## <a name="remarks"></a>コメント  
 **OpenSchema**メソッドは、データ ソース、テーブル内の列内のテーブルなど、データ ソースに関する情報を返し、データ型がサポートされています。  
  
 *QueryType*引数が列 (スキーマ) が返されるかを示す GUID。 OLE DB 仕様では、スキーマの完全な一覧があります。  
  
 *条件*引数がスキーマ クエリの結果を制限します。 *条件*対応する結果の制約の列と呼ばれる列のサブセットで行う必要のある値の配列を指定します。 **Recordset**します。  
  
 定数**adSchemaProviderSpecific**の使用は、 *QueryType*引数場合は、プロバイダーは、外の独自の標準スキーマ クエリを定義します。 前の表にします。 この定数を使用する場合、 *SchemaID*引数を実行する、スキーマ クエリの GUID を渡す必要があります。 場合*QueryType*に設定されている**adSchemaProviderSpecific**が*SchemaID*が提供されていない場合、エラーが発生します。  
  
 プロバイダーは、OLE DB 標準スキーマのすべてのクエリをサポートする必要はありません。 具体的には、のみ**adSchemaTables**、 **adSchemaColumns**、および**adSchemaProviderTypes**が OLE DB 仕様で必要です。 ただし、プロバイダーは、サポートする必要はありません、*条件*これらのスキーマ クエリの制約が以前に紹介します。  
  
> [!NOTE]
>  **リモート データ サービスの使用状況**、 **OpenSchema**メソッドがクライアント側でご利用いただけません[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト。  
  
> [!NOTE]
>  Visual basic での 4 バイト符号なし整数 (DBTYPE UI4) である列、 **Recordset**から返される、 **OpenSchema**メソッドを**接続**オブジェクトことはできませんその他の変数と比較します。 OLE DB データ型の詳細については、次を参照してください[OLE DB (OLE DB) でのデータ型](https://msdn.microsoft.com/6039292f-74e0-49b2-b133-17bc117ebf6a)と[付録 a:。データ型](https://msdn.microsoft.com/e3a0533a-2196-4eb0-a31e-92fe9556ada6)Microsoft OLE DB プログラマーズ リファレンス。  
  
> [!NOTE]
>  **Visual C/C++ユーザー**クライアント側のカーソルを使用していない場合は、MDAC 2.7、MDAC 2.8、および使用される型の中に Windows Data Access Components (Windows DAC) 6.0 では、型 VT_R8 のバリアント型を返します ADO では列のスキーマの"ORDINAL_POSITION"を取得します。MDAC 2.6 VT_I4 でした。 MDAC 2.6 のバリアント型を探してそのだけに記述されたプログラムは、0 を変更しなくても、MDAC 2.7、MDAC 2.8、および Windows DAC 6.0 で実行する場合は、すべて序数を取得 VT_I4 型の返されます。 OLE DB が返すデータ型が、DBTYPE_UI4 であるために、この変更が行われ、VT_I4 の符号付きの型がないが発生していると、原因となり、データが失われる可能性がある切り捨てることがなくすべての値を格納する十分な空き領域。  
  
## <a name="applies-to"></a>適用対象  
 [Connection オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [OpenSchema メソッドの例 (VB)](../../../ado/reference/ado-api/openschema-method-example-vb.md)   
 [OpenSchema メソッドの例 (vc++)](../../../ado/reference/ado-api/openschema-method-example-vc.md)   
 [Open メソッド (ADO Connection)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open メソッド (ADO Record)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open メソッド (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open メソッド (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [付録 A: プロバイダー](../../../ado/guide/appendixes/appendix-a-providers.md)
