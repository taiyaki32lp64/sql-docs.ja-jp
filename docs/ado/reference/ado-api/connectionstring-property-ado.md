---
title: ConnectionString プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::ConnectionString
helpviewer_keywords:
- ConnectionString property [ADO]
ms.assetid: 3be75b75-4d36-4479-ab64-9a456869252a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e391ad7c61bd6c303b0558892435af344a2768fb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933498"
---
# <a name="connectionstring-property-ado"></a>ConnectionString プロパティ (ADO)
データ ソースへの接続を確立するための情報を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定または取得を**文字列**値。  
  
## <a name="remarks"></a>コメント  
 使用して、 **ConnectionString**プロパティを含む、一連の詳細な接続文字列を渡すことによって、データ ソースを指定する*引数* *値 =* で区切られたステートメントセミコロン入力します。  
  
 ADO の 5 つの引数をサポートする、 **ConnectionString**プロパティです。 ADO で処理なしのプロバイダーに直接の引数のパス。 引数の ADO サポートは、次のとおりです。  
  
|引数|説明|  
|--------------|-----------------|  
|*Provider=*|接続に使用するプロバイダーの名前を指定します。|  
|*ファイル名 =*|事前設定された接続情報を格納しているプロバイダーに固有のファイル (たとえば、永続化されたデータ ソース オブジェクト) の名前を指定します。|  
|*リモート プロバイダー =*|クライアント側の接続を開くときに使用するプロバイダーの名前を指定します。 (リモート データのサービスのみ。)|  
|*リモート サーバー =*|クライアント側の接続を開くときに使用するサーバーのパス名を指定します。 (リモート データのサービスのみ。)|  
|*URL=*|ファイルやディレクトリなどのリソースを識別する絶対 URL として、接続文字列を指定します。|  
  
 設定した後、 **ConnectionString**プロパティとオープン、[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト、プロバイダーが ADO 定義の引数名をマップすることによって、プロパティの内容をたとえば、alter 可能性があります、特定のプロバイダーに対応します。  
  
 **ConnectionString**プロパティで使用される値を自動的に継承する、 *ConnectionString*の引数、[オープン](../../../ado/reference/ado-api/open-method-ado-connection.md)現在をオーバーライドするためのメソッド**ConnectionString**中にプロパティ、**オープン**メソッドの呼び出し。  
  
 *ファイル名*引数と関連付けられているプロバイダを読み込む、ADO、両方を渡すことはできません、*プロバイダー*と*ファイル名*引数。  
  
 **ConnectionString**プロパティは、開いているときに、接続が閉じており、読み取り専用と読み取り/書き込みです。  
  
 引数の重複、 **ConnectionString**プロパティは無視されます。 いずれかの引数の最後のインスタンスが使用されます。  
  
> [!NOTE]
>  **リモート データ サービスの使用状況**クライアント側で使用すると**接続**オブジェクト、 **ConnectionString**プロパティにのみを含めることができます、*リモート プロバイダー* *リモート サーバー*パラメーター。  
  
 次の表では、各 Windows オペレーティング システムの既定の ADO プロバイダーを示します。  
  
|ADO プロバイダーは既定値|Windows オペレーティング システム|  
|--------------------------|------------------------------|  
|MSDASQL<br /><br /> (ソース コードの読みやすさを向上させるのに明示的にプロバイダー名、接続文字列で指定します。)|Windows 2000 (32 ビット)<br /><br /> Windows XP (32 ビット)<br /><br /> Windows 2003 Server (32 ビット)<br /><br /> Windows Vista (32 ビット)<br /><br /> Windows Vista Service Pack 1 またはそれ以降 (32 ビットおよび 64 ビット)<br /><br /> Windows Vista (32 ビットおよび 64 ビット) より後の Windows バージョン|  
|既定値はありません。<br /><br /> ADO アプリケーションでは、次のオペレーティング システムで実行され、プロバイダーが明示的に指定しない、ADO には、次のエラーが返されます。"ADODB します。接続: プロバイダーが指定されていないと、指定された既定のプロバイダーがありません"|Windows 2000 (64 ビット)<br /><br /> Windows XP (64 ビット)<br /><br /> Windows 2003 Server (64 ビット)<br /><br /> Windows Vista (64 ビット)|  
  
## <a name="applies-to"></a>適用対象  
 [Connection オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [ConnectionString、ConnectionTimeout、および状態のプロパティの例 (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString、ConnectionTimeout、および状態のプロパティの例 (vc++)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [付録 A: プロバイダー](../../../ado/guide/appendixes/appendix-a-providers.md)
