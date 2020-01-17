---
title: CommandText プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandText
helpviewer_keywords:
- CommandText property [ADO]
ms.assetid: 4dd7e82a-8da5-4a4e-b439-11a29286fa0e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c0288dde74d2a172c9b0f8bdb865f4467fb0f637
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919727"
---
# <a name="commandtext-property-ado"></a>CommandText プロパティ (ADO)
プロバイダーに対して発行するコマンドのテキストを示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 取得または設定します、**文字列**SQL ステートメント、テーブル名、相対 URL では、ストアド プロシージャの呼び出しなど、プロバイダーのコマンドを表す値です。 既定値は空の文字列 ("")。  
  
## <a name="remarks"></a>コメント  
 使用して、 **CommandText**プロパティを設定またはで表されるコマンドのテキストを取得、[コマンド](../../../ado/reference/ado-api/command-object-ado.md)オブジェクト。 通常これは、SQL ステートメントが他の種類のコマンド ステートメントがストアド プロシージャの呼び出しなど、プロバイダーによって認識されることもできます。 特定の言語仕様またはプロバイダーのクエリ プロセッサによってサポートされているバージョンの SQL ステートメントがある必要があります。  
  
 場合、[準備](../../../ado/reference/ado-api/prepared-property-ado.md)のプロパティ、**コマンド**にオブジェクトが設定されている**True**と**コマンド**を設定すると、接続を開くオブジェクトのバインド**CommandText**プロパティ、ADO を準備します (プロバイダーが格納されているクエリのコンパイルされた形式) のクエリを呼び出すと、 [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)または[を開く](../../../ado/reference/ado-api/open-method-ado-connection.md)メソッド。  
  
 に応じて、 [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)プロパティを設定すると、ADO が alter、 **CommandText**プロパティ。 読み取ることができます、 **CommandText**実際のコマンド テキストを表示するには、いつでもプロパティを ADO は、実行中に使用されます。  
  
 使用して、 **CommandText**プロパティを設定またはファイルやディレクトリなどのリソースを指定する相対 URL を取得します。 絶対 url では、または暗黙的には、オープンで明示的に指定された場所に対する相対リソース パスです[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト。  
  
> [!NOTE]
>  Http スキームを使用して Url が自動的に呼び出さ、 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)します。 詳細については、次を参照してください。[絶対と相対 Url](../../../ado/guide/data/absolute-and-relative-urls.md)します。  
  
## <a name="applies-to"></a>適用対象  
 [Command オブジェクト (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [ActiveConnection、CommandText、CommandTimeout、CommandType、サイズ、および方向プロパティの例 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、サイズ、および方向プロパティの例 (vc++)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Requery メソッド](../../../ado/reference/ado-api/requery-method.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、サイズ、および方向プロパティの例 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
