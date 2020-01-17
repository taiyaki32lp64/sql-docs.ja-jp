---
title: ADO MD と ADO の併用 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, using with ADO MD
ms.assetid: cfae435e-2ac3-4312-8c1e-9ca4a74cd875
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d3c634ec056d42e97dcbea3422a0e19a33596d54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923146"
---
# <a name="using-ado-with-ado-md"></a>ADO MD と ADO の併用
ADO および ADO MD は、関連するが、別のオブジェクト モデルです。 ADO では、データ ソースへの接続、コマンドを実行する、表形式のデータと表形式のスキーマのメタデータの取得、およびプロバイダーのエラー情報を表示するためのオブジェクトを提供します。 ADO MD では、多次元データを取得し、マルチ ディメンション スキーマのメタデータを表示するためのオブジェクトを提供します。  
  
 MDP を使用する場合は、ADO、ADO MD で、またはその両方で、アプリケーションを使用できます。 プロジェクト内で両方のライブラリを参照する、MDP によって提供される機能へのフル アクセスが必要です。  
  
 多次元データセットのフラット化された、表形式ビューを取得するコンシューマー向けの多くの場合に便利です。 ADO を使用してこれを行う[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト。 ソースを指定、[セルセット](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)として、***ソース***のパラメーター、[オープン](../../../ado/reference/ado-api/open-method-ado-recordset.md)のメソッド、**レコード セット**のソースとしてではなくADO MD**セルセット**します。  
  
 オブジェクトの階層ではなく表形式ビューで、スキーマ メタデータを確認するためにもあります。 ADO [OpenSchema](../../../ado/reference/ado-api/openschema-method.md)メソッドを[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトを開くユーザーを使用できます、**レコード セット**スキーマ情報を格納します。 ***QueryType***のパラメーター、 **OpenSchema**メソッドがいくつか[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md) MDPs に特に関連する値。 これらの値は次のとおりです。  
  
-   **adSchemaCubes**  
  
-   **adSchemaDimensions**  
  
-   **adSchemaHierarchies**  
  
-   **adSchemaLevels**  
  
-   **adSchemaMeasures**  
  
-   **adSchemaMembers**  
  
 ADO の列挙値の ADO MD のプロパティまたはメソッドを使用するには、プロジェクトは、ADO MD と ADO ライブラリを参照する必要があります。 たとえば、ADO を使用することができます**adState** ADO md の列挙値[状態](../../../ado/reference/ado-md-api/state-property-ado-md.md)プロパティ。 ライブラリへの参照を確立する方法の詳細については、開発ツールのドキュメントを参照してください。  
  
 ADO オブジェクトやメソッドの詳細については、次を参照してください。、 [ADO の API リファレンス](../../../ado/reference/ado-api/ado-api-reference.md)します。  
  
## <a name="see-also"></a>参照  
 [ADO MD オブジェクト モデル](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (多次元) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [多次元スキーマとデータの概要](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [ADO MD を使用したプログラミング](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [多次元データの操作](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
