---
title: 絶対と相対 Url |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- relative URLs [ADO]
- absolute URLs [ADO]
- URLs [ADO]
ms.assetid: 6a34a7ef-50cc-4c3d-82f7-106b9a8f3caf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f15c5890300687a2d587a58a586d00bf2c8d0fd8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926360"
---
# <a name="absolute-and-relative-urls"></a>絶対 URL と相対 URL
URL には、ローカルまたはネットワーク コンピューターに格納されているターゲットの場所を指定します。 ターゲットは、ファイル、ディレクトリ、HTML ページ、画像、プログラム、およびなどを使用できます。  
  
 *絶対 URL*リソースを特定するために必要なすべての情報が含まれています。  
  
 A*相対 URL*開始点として絶対 URL を使用してリソースを検索します。 実際には、ターゲットの「完全 URL」は、絶対と相対 Url を連結することによって指定されます。  
  
 *絶対 URL*は次の形式を使用: *scheme://server/path/resource*  
  
 相対 URL は通常ののみで構成されます、*パス*、し、必要に応じて、*リソース*が*スキーム*または*server*します。 次の表では、完全な URL の形式の個々 の部分を定義します。  
  
 *scheme*  
 指定する方法、*リソース*へのアクセスします。  
  
 *server*  
 コンピューターの名前を指定する場所、*リソース*が配置されています。  
  
 *path*  
 先頭のターゲット ディレクトリのシーケンスを指定します。 場合*リソース*は省略すると、ターゲットは、最後のディレクトリで*パス*します。  
  
 *resource*  
 含まれる場合、*リソース*ターゲットは、通常、ファイルの名前です。 可能性がある、*単純なファイルは、* (バイト単位) の 1 つのバイナリ ストリームを格納している、または*構造化ドキュメント、* 1 つ以上の記憶域とのバイトのバイナリ ストリームを格納しています。  
  
## <a name="url-scheme-registration"></a>URL スキームを登録します。  
 プロバイダーは、Url をサポートする場合、プロバイダーは 1 つまたは複数の URL スキームを登録します。 登録は、スキームを使用する Url の登録済みのプロバイダーを自動的に呼び出すことを意味します。 たとえば、 *http*にスキームが登録されている、 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)します。 ADO では、"http"の付いたすべての Url を表す Web フォルダーまたはインターネット発行プロバイダーで使用するファイルを前提としています。 プロバイダーが登録されているスキーマの詳細については、プロバイダーのマニュアルを参照してください。  
  
## <a name="defining-context-with-a-url"></a>URL を使用してコンテキストを定義します。  
 によって表される、開いている接続の 1 つの関数を[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト、その接続で表されるデータ ソースへの後続の操作を制限するです。 つまり、接続は、後続の操作のコンテキストを定義します。  
  
 Ado 2.7 以降では、絶対 URL をコンテキストを定義できます。 たとえばときに、[レコード](../../../ado/reference/ado-api/record-object-ado.md)、絶対 URL でオブジェクトを開く、**接続**オブジェクトは、URL で指定されたリソースを表すために暗黙的に作成します。  
  
 コンテキストを定義する絶対 URL を指定することができます、 *ActiveConnection*のパラメーター、**レコード**オブジェクト[オープン](../../../ado/reference/ado-api/open-method-ado-record.md)メソッド。 値として絶対 URL を指定することも、"URL ="キーワード、**接続**オブジェクト[オープン](../../../ado/reference/ado-api/open-method-ado-connection.md)メソッド*ConnectionString*パラメーター、および、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト[オープン](../../../ado/reference/ado-api/open-method-ado-recordset.md)メソッド*ActiveConnection*パラメーター。  
  
 開くことでコンテキストを定義することも、**レコード**または**Recordset**これらのオブジェクトが既にある、暗黙的または明示的に宣言されたため、ディレクトリを表すオブジェクトを**接続**コンテキストを指定するオブジェクト。  
  
## <a name="scoped-operations"></a>スコープの操作  
 コンテキストでは、スコープも定義します-つまり、ディレクトリとそのサブディレクトリ後続の操作に参加できます。 **レコード**オブジェクトのディレクトリを操作するいくつかのスコープを持つメソッドとそのすべてのサブディレクトリがあります。 これらのメソッドを含める[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)、 [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)、および[DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)します。  
  
## <a name="relative-urls-as-command-text"></a>コマンド テキストと相対 Url  
 内の文字列を入力して、データ ソースで実行するコマンドを指定することができます、 *CommandText*のパラメーター、**接続**オブジェクトの[Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)メソッドをおよび、 *ソース*のパラメーター、 **Recordset**オブジェクトの[オープン](../../../ado/reference/ado-api/open-method-ado-recordset.md)メソッド。  
  
 相対 URL で指定できます、 *CommandText*または*ソース*パラメーター。 相対 URL が、SQL コマンドなどのコマンドを実際に表していませんパラメーターだけを指定します。 アクティブな接続のコンテキストは、絶対 URL である必要があります、*オプション*にパラメーターを設定する必要があります**adCmdTableDirect**します。  
  
 たとえば、次のコード サンプルを開く方法を示しています。、 **Recordset**  /Winnt system32 ディレクトリの Readme25.txt ファイル。  
  
```  
recordset.Open "system32/Readme25.txt", "URL=https://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
 接続文字列で絶対 URL は、サーバーを指定します (`YourServer`) と、パス (`Winnt`)。 この URL には、コンテキストも定義します。  
  
 コマンド テキスト内の相対 URL を出発点として絶対 URL を使用し、パスの残りの部分を指定します (`system32`) と、ファイルを開く (`Readme25.txt`)。  
  
 オプション フィールド (`adCmdTableDirect`) コマンドの種類の相対 URL であることを示します。  
  
 次のコードを開く別の例として、 **Recordset**の内容に、`Winnt`ディレクトリ。  
  
```  
recordset.Open "", "URL=https://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
## <a name="ole-db-provider-supplied-url-schemes"></a>OLE DB プロバイダーが指定した URL スキーム  
 完全修飾 URL の先頭部分は、*スキーム*URL の残りの部分で識別されるリソースにアクセスするために使用されます。 例は、HTTP (ハイパー テキスト転送プロトコル) および FTP (ファイル転送プロトコル) です。  
  
 ADO では、独自の URL スキームを認識する OLE DB プロバイダーをサポートします。 たとえば、 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md) *、* 「公開」の Windows 2000 ファイルにアクセスする既存の HTTP スキームを認識します。  
  
## <a name="see-also"></a>関連項目  
 [接続オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Record オブジェクト (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
