---
title: 集計関数、CALC 関数、および新しいキーワード |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], functions
- CALC function [ADO]
- NEW keyword [ADO]
- aggregate functions [ADO]
ms.assetid: 0590b466-2a36-49a2-868e-028ef5e49394
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5a7ed836b9b57ddd690dd85dd94cc12cb967c472
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926008"
---
# <a name="aggregate-functions-the-calc-function-and-the-new-keyword"></a>集計関数、CALC 関数、NEW キーワード
データ シェイプには、次の関数がサポートされています。 操作する列を含む章に割り当てられた名前は、*章エイリアス*します。  
  
 チャプター エイリアスを完全修飾名」の章を含むに先頭から成ることができます、*列名、* ピリオドで区切ってします。 たとえば、親章、chap1、子の章では、chap2 に含まれる場合 amt、amount 列を持つ、chap1.chap2.amt が修飾名になります。  
  
|集計関数|説明|  
|-------------------------|-----------------|  
|SUM (*章エイリアス*.*列名*)|指定された列のすべての値の合計を計算します。|  
|AVG (*章エイリアス*.*列名*)|指定された列のすべての値の平均を計算します。|  
|最大 (*章エイリアス*.*列名*)|指定された列の最大値を計算します。|  
|MIN (*章エイリアス*.*列名*)|指定された列の最小値を計算します。|  
|カウント (*章エイリアス*[.*列名*])|指定されたエイリアスの行の数をカウントします。 列が指定されている場合は、カウントにその列は Null 以外のみの行が含まれます。|  
|STDEV (*章エイリアス*.*列名*)|指定された列の標準偏差を計算します。|  
|ANY (*章エイリアス*.*列名*)|指定された列の値です。 予測可能な値は、列の値はチャプター内のすべての行の同じ場合にのみいずれかが存在します。<br /><br /> **注**列にチャプター内の行のすべてに対して同じ値が含まれていない場合、図形コマンド任意を返します、関数の値を指定する値のいずれか。|  
  
|計算式|説明|  
|---------------------------|-----------------|  
|CALC(*expression*)|行だけに、任意の式を計算、 **Recordset** CALC 関数を含むです。 これらを使用して任意の式[Visual Basic for Applications (VBA) 関数](../../../ado/guide/data/visual-basic-for-applications-functions.md)は許可されています。|  
  
|新しいキーワード|説明|  
|-----------------|-----------------|  
|NEW *フィールド型*[(*幅*&#124;*スケール*&#124;*精度*&#124;*エラー* [、*スケール*&#124;*エラー*])]|指定した型の空の列を追加、 **Recordset**です。|  
  
 *フィールド型*新しいキーワードと共に渡すと、次のデータ型のいずれかがあることができます。  
  
|OLE DB データ型|ADO データ型の equivalent(s)|  
|-----------------------|-----------------------------------|  
|DBTYPE_BSTR|adBSTR|  
|DBTYPE_BOOL|adBoolean|  
|DBTYPE_DECIMAL|adDecimal|  
|DBTYPE_UI1|adUnsignedTinyInt|  
|DBTYPE_I1|adTinyInt|  
|DBTYPE_UI2|adUnsignedSmallInt|  
|DBTYPE_UI4|adUnsignedInt|  
|DBTYPE_I8|adBigInt|  
|DBTYPE_UI8|adUnsignedBigInt|  
|DBTYPE_GUID|adGuid|  
|DBTYPE_BYTES|adBinary、AdVarBinary、adLongVarBinary|  
|DBTYPE_STR|adChar、adVarChar、adLongVarChar|  
|DBTYPE_WSTR|adWChar, adVarWChar, adLongVarWChar|  
|DBTYPE_NUMERIC|adNumeric|  
|DBTYPE_DBDATE|adDBDate|  
|DBTYPE_DBTIME|adDBTime|  
|DBTYPE_DBTIMESTAMP|adDBTimeStamp|  
|DBTYPE_VARNUMERIC|adVarNumeric|  
|DBTYPE_FILETIME|adFileTime|  
|DBTYPE_ERROR|adError|  
  
 (OLE DB DBTYPE_DECIMAL、または ADO、adDecimal)、decimal 型の新しいフィールドがある場合は、有効桁数と小数点の値を指定する必要があります。  
  
## <a name="see-also"></a>関連項目  
 [データ シェイプの例](../../../ado/guide/data/data-shaping-example.md)   
 [Shape の正式文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [一般的な Shape コマンド](../../../ado/guide/data/shape-commands-in-general.md)
