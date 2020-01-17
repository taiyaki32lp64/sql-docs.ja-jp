---
title: ストアド プロシージャ (OLE DB) の呼び出し |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- calling stored procedures
- RPC escape sequence
- OLE DB, stored procedures
- parameters [SQL Server Native Client], OLE DB
- ODBC CALL escape sequence
- stored procedures [OLE DB], calling
- SQL Server Native Client OLE DB provider, stored procedures
ms.assetid: 8e5738e5-4bbe-4f34-bd69-0c0633290bdd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7385dddea48813615a851979e526af5f03a23332
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68206586"
---
# <a name="calling-a-stored-procedure-ole-db"></a>ストアド プロシージャの呼び出し (OLE DB)
  ストアド プロシージャは、0 個以上のパラメーターを受け取ることができます。 また、値を返すこともできます。 使用する場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでは、ストアド プロシージャのパラメーターは、渡すことができます。  
  
-   データ値をハードコーディングする。  
  
-   パラメーター マーカー (?) を使用してパラメーターを指定し、プログラム変数をパラメーター マーカーにバインドしてから、データ値をプログラム変数に格納する。  
  
> [!NOTE]  
>  OLE DB で名前付きパラメーターを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ストアド プロシージャを呼び出す場合は、パラメーター名の先頭に '\@' 文字を付ける必要があります。 これは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 固有の制限です。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、この制限を MDAC よりも厳密に適用します。  
  
 パラメーターをサポートするには、コマンド オブジェクトで **ICommandWithParameters** インターフェイスを公開します。 パラメーターを使用するには、コンシューマーは、まず、**ICommandWithParameters::SetParameterInfo** メソッドを呼び出して、プロバイダーにパラメーターを示します (または、必要に応じて、**GetParameterInfo** メソッドを呼び出す呼び出し元ステートメントを準備します)。 次に、バッファーの構造を指定するアクセサーを作成し、このバッファーにパラメーター値を格納します。 最後に、アクセサーのハンドルとバッファーへのポインターを **Execute** に渡します。 その後 **Execute** を呼び出す場合、コンシューマーはバッファーに新しいパラメーター値を格納し、アクセサー ハンドルとバッファー ポインターを指定して **Execute** を呼び出します。  
  
 パラメーターを使用する一時ストアド プロシージャを呼び出すコマンドは、まず、**ICommandWithParameters::SetParameterInfo** を呼び出してパラメーター情報を定義しないと、適切に準備されません。 これは、一時ストアド プロシージャの内部名がクライアントで使用される外部名とは異なるので、SQLOLEDB がシステム テーブルをクエリして、一時ストアド プロシージャのパラメーター情報を判断できないためです。  
  
 次に、パラメーターのバインド プロセスの手順を示します。  
  
1.  DBPARAMBINDINFO 構造体の配列にパラメーター情報を格納します。パラメーター情報には、パラメーター名、パラメーターのデータ型を表すプロバイダー固有の名前、標準のデータ型名などが含まれます。 配列内の構造体 1 つが、1 つのパラメーターを表します。 その後、この配列は **SetParameterInfo** メソッドに渡されます。  
  
2.  **ICommandWithParameters::SetParameterInfo** メソッドを呼び出して、パラメーターをプロバイダーに示します。 **SetParameterInfo** では、各パラメーターのネイティブ データ型を指定します。 **SetParameterInfo** 引数は次のとおりです。  
  
    -   型情報を設定するパラメーターの数  
  
    -   型情報を設定するパラメーターの序数の配列  
  
    -   DBPARAMBINDINFO 構造体の配列  
  
3.  **IAccessor::CreateAccessor** コマンドを使用して、パラメーター アクセサーを作成します。 このアクセサーにより、バッファーの構造を指定し、パラメーター値をバッファーに格納します。 **CreateAccessor** コマンドでは、バインドのセットからアクセサーを作成します。 このバインドは、コンシューマーが DBBINDING 構造体の配列を使用して記述します。 各バインドでは、1 つのパラメーターをコンシューマーのバッファーに関連付けます。バインドには、次のような情報が含まれます。  
  
    -   バインドが適用されるパラメーターの序数  
  
    -   バインドの対象 (データ値、データ値の長さと状態)  
  
    -   これらの各情報に関するバッファー内のオフセット  
  
    -   コンシューマーのバッファー内にあるデータ値の長さと型  
  
     アクセサーは、アクセサーのハンドルにより識別されます。このハンドルは HACCESSOR 型です。 このハンドルは、**CreateAccessor** メソッドから返されます。 コンシューマーはアクセサーを使い終わるたびに、**ReleaseAccessor** メソッドを呼び出して、アクセサーが保持しているメモリを解放する必要があります。  
  
     コンシューマーが **ICommand::Execute** などのメソッドを呼び出す場合、アクセサーへのハンドルとバッファー自体へのポインターを渡します。 プロバイダーはこのアクセサーを使用して、バッファー内にあるデータを送信する方法を決定します。  
  
4.  DBPARAMS 構造体にデータを格納します。 入力パラメーター値の取得と出力パラメーター値の書き込みに使われるコンシューマーの変数が、実行時に DBPARAMS 構造体の **ICommand::Execute** に渡されます。 DBPARAMS 構造体には、次の 3 つの要素が含まれます。  
  
    -   アクセサー ハンドルで指定されているバインドに従ってプロバイダーが入力パラメーター データを取得し、出力パラメーター データを返すための、バッファーへのポインター  
  
    -   バッファー内のパラメーター セットの数  
  
    -   手順 3. で作成したアクセサー ハンドル  
  
5.  **ICommand::Execute** を使用してコマンドを実行します。  
  
## <a name="methods-of-calling-a-stored-procedure"></a>ストアド プロシージャを呼び出す方法  
 内のストアド プロシージャを実行するときに[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーをサポートします。  
  
-   ODBC CALL エスケープ シーケンス。  
  
-   リモート プロシージャ コール (RPC) エスケープ シーケンス  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)] EXECUTE ステートメント  
  
### <a name="odbc-call-escape-sequence"></a>ODBC CALL エスケープ シーケンス  
 パラメーター情報を把握している場合は、**ICommandWithParameters::SetParameterInfo** メソッドを呼び出して、パラメーターをプロバイダーに示します。 それ以外の場合は、ストアド プロシージャの呼び出しに ODBC CALL 構文を使用すると、プロバイダーはヘルパー関数を呼び出してストアド プロシージャのパラメーター情報を取得します。  
  
 パラメーター情報 (パラメーターのメタデータ) を把握していない場合は、ODBC CALL 構文の使用をお勧めします。  
  
 ODBC CALL エスケープ シーケンスを使用してプロシージャを呼び出す場合の一般的な構文は、次のとおりです。  
  
 { **[? =]** **呼び出す**_procedure_name_[ **(** [*パラメーター*] [ **、** [*パラメーター*]. **)** ]}  
  
 以下に例を示します。  
  
```  
{call SalesByCategory('Produce', '1995')}  
```  
  
### <a name="rpc-escape-sequence"></a>RPC エスケープ シーケンス  
 RPC エスケープ シーケンスは、ストアド プロシージャを呼び出す ODBC CALL 構文と似ています。 プロシージャを複数回呼び出す場合は、ストアド プロシージャを呼び出す 3 つの方法のうち、RPC エスケープ シーケンスのパフォーマンスが最も優れています。  
  
 RPC エスケープ シーケンスを使用してストアド プロシージャを実行する場合、プロバイダーはパラメーター情報の決定にヘルパー関数を呼び出しません (ODBC CALL 構文では、ヘルパー関数が呼び出されます)。 RPC 構文は ODBC CALL 構文よりも簡単です。そのためコマンドが高速に解析され、パフォーマンスが向上します。 この場合は、**ICommandWithParameters::SetParameterInfo** を実行してパラメーター情報を提供する必要があります。  
  
 RPC エスケープ シーケンスを使用する場合は、戻り値が必要です。 ストアド プロシージャが値を返さない場合、サーバーが既定で 0 を返します。 また、ストアド プロシージャ上で [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] カーソルを開くことはできません。 ストアド プロシージャは暗黙的に準備され、**ICommandPrepare::Prepare** の呼び出しは失敗します。 RPC 呼び出しを準備することができないのためにできるクエリを実行しない列のメタデータ。Icolumnsinfo::getcolumninfo と icolumnsrowset::getcolumnsrowset は DB_E_NOTPREPARED を返します。  
  
 パラメーターのメタデータを把握できている場合は、ストアド プロシージャの実行方法として RPC エスケープ シーケンスの使用をお勧めします。  
  
 次に、ストアド プロシージャを呼び出す RPC エスケープ シーケンスの例を示します。  
  
```  
{rpc SalesByCategory}  
```  
  
 RPC エスケープ シーケンスを示すサンプル アプリケーションを参照してください。[ストアド プロシージャの実行&#40;RPC 構文を使用して&#41;しプロセスのリターン コードと出力パラメーター &#40;OLE DB&#41;](../../native-client-ole-db-how-to/results/execute-stored-procedure-with-rpc-and-process-output.md)します。  
  
### <a name="transact-sql-execute-statement"></a>Transact-SQL EXECUTE ステートメント  
 ストアド プロシージャを呼び出す方法としては、[EXECUTE](/sql/t-sql/language-elements/execute-transact-sql) ステートメントよりも、ODBC CALL エスケープ シーケンスや RPC エスケープ シーケンスをお勧めします。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーの RPC メカニズムを使用して[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]コマンド処理を最適化します。 この RPC プロトコルでは、サーバー側で実行されるパラメーター処理やステートメントの解析作業の多くを排除することで、パフォーマンスを向上しています。  
  
 次に、[!INCLUDE[tsql](../../../includes/tsql-md.md)] **EXECUTE** ステートメントの例を示します。  
  
```  
EXECUTE SalesByCategory 'Produce', '1995'  
```  
  
## <a name="see-also"></a>関連項目  
 [ストアド プロシージャ](stored-procedures.md)  
  
  
