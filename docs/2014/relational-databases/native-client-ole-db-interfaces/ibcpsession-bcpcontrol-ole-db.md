---
title: Ibcpsession::bcpcontrol (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- IBCPSession::BCPControl (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPControl method
ms.assetid: d58f3fe1-45e3-4e46-8e9c-000971829d99
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6fae6e3ba4f861fa7d75ae3ee4e8825350d80c39
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046747"
---
# <a name="ibcpsessionbcpcontrol-ole-db"></a>IBCPSession::BCPControl (OLE DB)
  一括コピー操作のオプションを設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT BCPControl(   
inteOption,  
void *iValue);  
```  
  
## <a name="remarks"></a>コメント  
 **BCPControl** メソッドでは、一括コピー操作のさまざまな制御パラメーターを設定します。たとえば、一括コピーが取り消されるまでに発生してもかまわないエラーの数、データ ファイルから最初にコピーする行番号や最後にコピーする行番号、バッチ サイズなどを設定します。  
  
 また、このメソッドを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からデータを一括コピーするときに使用される SELECT ステートメントを指定することもできます。 設定することができます、`eOption`引数に bcp_option_hints を設定し、 `iValue` SELECT ステートメントを含むワイド文字の文字列へのポインターを保持する引数。  
  
 指定できる値*eOption*は。  
  
|オプション|説明|  
|------------|-----------------|  
|BCP_OPTION_ABORT|既に実行中の一括コピー操作を停止します。 別のスレッドから *eOption* 引数に BCP_OPTION_ABORT を指定して **BCPControl** メソッドを呼び出し、実行中の一括コピー操作を停止できます。 *IValue*引数は無視されます。|  
|BCP_OPTION_BATCH|バッチごとの行数を指定します。 既定値は 0 です。これは、データを抽出するときはテーブル内のすべての行が抽出されることを示し、データを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にコピーするときはユーザー データ ファイル内のすべての行がコピーされることを示します。 BCP_OPTION_BATCH に 1 未満の値を指定すると、既定値にリセットされます。|  
|BCP_OPTION_DELAYREADFMT|ブール値を設定します。true に設定した場合、[IBCPSession::BCPReadFmt](ibcpsession-bcpreadfmt-ole-db.md) により実行時に読み取りが行われます。 False (既定)、ibcpsession::bcpreadfmt はすぐに場合、フォーマット ファイルを読み取る。 シーケンス エラーが発生`BCP_OPTION_DELAYREADFMT`は true を呼び出して ibcpsession::bcpcolumns または ibcpsession::bcpcolfmt します。<br /><br /> 呼び出す場合もシーケンス エラーが発生`IBCPSession::BCPControl(BCPDELAYREADFMT, (void *)FALSE))`呼び出した後`IBCPSession::BCPControl(BCPDELAYREADFMT, (void *)TRUE)`ibcpsession::bcpwritefmt とします。<br /><br /> 詳細については、次を参照してください。[メタデータ検出](../native-client/features/metadata-discovery.md)します。|  
|BCP_OPTION_FILECP|*iValue* 引数には、データ ファイルのコード ページ番号が含まれます。 1252 や 850 などのコード ページ番号を指定するか、次のいずれかの値を指定できます。<br /><br /> -BCP_FILECP_ACP ファイル内のデータは、Microsoft Windows では [概要] タブ クライアントのコード ページです。<br />-BCP_FILECP_OEMCP ファイル内のデータは、(既定値) のクライアントの OEM コード ページです。<br />-BCP_FILECP_RAW ファイル内のデータは、コード ページの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。|  
|BCP_OPTION_FILEFMT|データ ファイル形式のバージョン番号を指定します。 80 ([!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)])、90 ([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)])、100 ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] または [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)])、110 ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)])、または 120 ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) を指定できます。 120 が既定値です。 このオプションは、以前のバージョンのサーバーでサポートされていた形式でデータをエクスポートおよびインポートする際に便利です。  たとえば、[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] サーバーのテキスト列から取得したデータを、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のサーバーの **varchar(max)** 列にインポートするには、80 を指定する必要があります。 同様に、データを **varchar(max)** 列からエクスポートするときに 80 を指定すると、データは、テキスト列が [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 形式で保存されるのと同じように保存されるので、[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] サーバーのテキスト列にインポートできます。|  
|BCP_OPTION_FIRST|ファイルまたはテーブルにコピーするデータの先頭行を指定します。 既定値は 1 です。1 未満の値を指定すると、このオプションは既定値にリセットされます。|  
|BCP_OPTION_FIRSTEX|BCP out 操作の場合は、データ ファイルにコピーするための、データベース テーブルの最初の行を指定します。<br /><br /> BCP in 操作の場合は、データベース テーブルにコピーするための、データ ファイルの最初の行を指定します。<br /><br /> *IValue*パラメーターが値を格納する、符号付き 64 ビット整数のアドレスにする必要があります。 BCPFIRSTEX に渡すことができる最大値は 2^63-1 です。|  
|BCP_OPTION_FMTXML|XML 形式でフォーマット ファイルが生成されることを指定する場合に使用します。 既定では、このオプションは無効で、フォーマット ファイルはテキスト ファイルとして保存されます。 XML フォーマット ファイルにより柔軟性が向上しますが、いくつか制約も追加されます。 たとえば、以前のフォーマット ファイルでは、1 つのフィールドにプレフィックスとターミネータを同時に指定できましたが、XML フォーマット ファイルでは指定できません。 **注:** XML フォーマット ファイルがサポートされるのは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ツールを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client と共にインストールした場合だけです。|  
|BCP_OPTION_HINTS|*iValue* 引数には、ワイド文字列ポインターが含まれます。 ポインターが指す文字列には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一括コピー処理ヒント、または結果セットを返す [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを指定します。 複数の結果セットを返す [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを指定すると、1 つ目の結果セット以外はすべて無視されます。|  
|BCP_OPTION_KEEPIDENTITY|*iValue* 引数が TRUE に設定されている場合、このオプションは、一括コピー メソッドで、ID 制約が定義された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 列用に指定したデータ値が挿入されることを示します。 入力ファイルには ID 列の値を指定する必要があります。 このオプションを設定しないと、挿入される行に対して新しい ID 値が生成されます。 ファイル内に存在する ID 列用のデータはすべて無視されます。|  
|BCP_OPTION_KEEPNULLS|ファイル内の空のデータ値を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルで NULL 値に変換するかどうかを指定します。 *iValue* 引数を TRUE に設定すると、空の値は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルで NULL に変換されます。 既定では、空の値は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブル内の列の既定値 (存在する場合) に変換されます。|  
|BCP_OPTION_LAST|コピーする最終行を指定します。 既定では、すべての行をコピーします。 1 未満の値を指定すると、このオプションは既定値にリセットされます。|  
|BCP_OPTION_LASTEX|BCP out 操作の場合は、データ ファイルにコピーするための、データベース テーブルの最後の行を指定します。<br /><br /> BCP in 操作の場合は、データベース テーブルにコピーするための、データ ファイルの最後の行を指定します。<br /><br /> *IValue*パラメーターが値を格納する、符号付き 64 ビット整数のアドレスにする必要があります。 BCPLASTEX に渡すことができる最大値は 2^63-1 です。|  
|BCP_OPTION_MAXERRS|一括コピー操作が失敗するまでに発生してもかまわないエラーの数を指定します。 既定値は 10 です。 1 未満の値を指定すると、このオプションは既定値にリセットされます。 一括コピーでは、最大 65,535 個のエラーが許容されます。 このオプションに 65,535 を超える値を設定しようとすると、65,535 が設定されます。|  
|BCP_OPTION_ROWCOUNT|現在 (または最後) の BCP 操作で処理された行数を返します。|  
|BCP_OPTION_TEXTFILE|データ ファイルは、バイナリ ファイルではなく、テキスト ファイルです。 BCP では、データ ファイルの先頭 2 バイトに含まれる Unicode バイト マーカーをチェックして、テキスト ファイルが Unicode 形式かどうかを検出します。|  
|BCP_OPTION_UNICODEFILE|このオプションに TRUE を設定して、入力ファイルが Unicode ファイル形式であることを指定します。|  
  
## <a name="arguments"></a>引数  
 *eOption*[in]  
 上記の「解説」で示したいずれかのオプションに設定します。  
  
 *iValue*[in]  
 指定された *eOption* に対する値です。 *iValue* 引数は、将来 64 ビット値に拡張できるように、void ポインターにキャストされる整数値です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 S_OK  
 メソッドが成功しました。  
  
 E_FAIL  
 プロバイダー固有のエラーが発生しました。詳細を確認するには、[ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) インターフェイスを使用してください。  
  
 E_UNEXPECTED  
 メソッドの呼び出しが予期されませんでした。 たとえば、この関数が呼び出される前に、[IBCPSession::BCPInit](ibcpsession-bcpinit-ole-db.md) メソッドが呼び出されなかった場合などです。  
  
 E_OUTOFMEMORY  
 メモリ不足エラーです。  
  
## <a name="see-also"></a>参照  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [一括コピー操作の実行](../native-client/features/performing-bulk-copy-operations.md)  
  
  
