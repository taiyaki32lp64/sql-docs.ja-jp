---
title: 'IBCPSession:: BCPControl (OLE DB) |Microsoft Docs'
description: IBCPSession::BCPControl (OLE DB)
ms.custom: ''
ms.date: 07/03/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- IBCPSession::BCPControl (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPControl method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 69944fc78ecfe45869ec59c37db20fdb09b2896e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015523"
---
# <a name="ibcpsessionbcpcontrol-ole-db"></a>IBCPSession::BCPControl (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  一括コピー操作のオプションを設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT BCPControl(   
      int eOption,  
      void *iValue);  
```  
  
## <a name="remarks"></a>Remarks  
 **BCPControl** メソッドでは、一括コピー操作のさまざまな制御パラメーターを設定します。たとえば、一括コピーが取り消されるまでに発生してもかまわないエラーの数、データ ファイルから最初にコピーする行番号や最後にコピーする行番号、バッチ サイズなどを設定します。  
  
 また、このメソッドを使用して、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] からデータを一括コピーするときに使用される SELECT ステートメントを指定することもできます。 **eOption** 引数を BCP_OPTION_HINTS に設定し、SELECT ステートメントを含むワイド文字列へのポインターを保持する **iValue** 引数を設定することができます。  
  
 *EOption*に指定できる値は次のとおりです。  
  
|オプション|[説明]|  
|------------|-----------------|  
|BCP_OPTION_ABORT|既に実行中の一括コピー操作を停止します。 別のスレッドから *eOption* 引数に BCP_OPTION_ABORT を指定して **BCPControl** メソッドを呼び出し、実行中の一括コピー操作を停止できます。 *Ivalue*引数は無視されます。|  
|BCP_OPTION_BATCH|バッチごとの行数を指定します。 既定値は 0 です。これは、データを抽出するときはテーブル内のすべての行が抽出されることを示し、データを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] にコピーするときはユーザー データ ファイル内のすべての行がコピーされることを示します。 BCP_OPTION_BATCH に 1 未満の値を指定すると、既定値にリセットされます。|  
|BCP_OPTION_DELAYREADFMT|ブール値を設定します。true に設定した場合、[IBCPSession::BCPReadFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md) により実行時に読み取りが行われます。 False (既定値) の場合、IBCPSession:: BCPReadFmt は、すぐにフォーマットファイルを読み取ります。 **BCP_OPTION_DELAYREADFMT**が true の場合、ibcpsession:: BCPColumns または IBCPSession:: BCPColFmt を呼び出すと、シーケンスエラーが発生します。<br /><br /> および ibcpsession:: bcpwritefmt を呼び出し`IBCPSession::BCPControl(BCPDELAYREADFMT, (void *)FALSE))` `IBCPSession::BCPControl(BCPDELAYREADFMT, (void *)TRUE)`た後にを呼び出すと、シーケンスエラーが発生します。<br /><br /> 詳細については、「[メタデータの検出](../../oledb/features/metadata-discovery.md)」を参照してください。|  
|BCP_OPTION_FILECP|*iValue* 引数には、データ ファイルのコード ページ番号が含まれます。 1252 や 850 などのコード ページ番号を指定するか、次のいずれかの値を指定できます。<br /><br /> BCP_FILECP_ACP を指定すると、ファイル内のデータには、クライアントの Microsoft Windows&#xAE; コード ページが使用されます。<br /><br /> BCP_FILECP_OEMCP を指定すると、ファイル内のデータには、クライアントの OEM コード ページ (既定) が使用されます。<br /><br /> BCP_FILECP_RAW を指定すると、ファイル内のデータには、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のコード ページが使用されます。|  
|BCP_OPTION_FILEFMT|データ ファイル形式のバージョン番号を指定します。 80 ([!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)])、90 ([!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)])、100 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] または [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)])、または 110 ([!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]) を指定できます。 110 が既定値です。 このオプションは、以前のバージョンのサーバーでサポートされていた形式でデータをエクスポートおよびインポートする際に便利です。  たとえば、[!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] サーバーのテキスト列から取得したデータを、[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降のサーバーの **varchar(max)** 列にインポートするには、80 を指定する必要があります。 同様に、データを **varchar(max)** 列からエクスポートするときに 80 を指定すると、データは、テキスト列が [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 形式で保存されるのと同じように保存されるので、[!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] サーバーのテキスト列にインポートできます。|  
|BCP_OPTION_FIRST|ファイルまたはテーブルにコピーするデータの先頭行を指定します。 既定値は 1 です。1 未満の値を指定すると、このオプションは既定値にリセットされます。|  
|BCP_OPTION_FIRSTEX|BCP out 操作の場合は、データ ファイルにコピーするための、データベース テーブルの最初の行を指定します。<br /><br /> BCP in 操作の場合は、データベース テーブルにコピーするための、データ ファイルの最初の行を指定します。<br /><br /> *Ivalue*パラメーターは、値を含む符号付き64ビット整数のアドレスである必要があります。 BCPFIRSTEX に渡すことができる最大値は 2^63-1 です。|  
|BCP_OPTION_FMTXML|XML 形式でフォーマット ファイルが生成されることを指定する場合に使用します。 既定では、このオプションは無効で、フォーマット ファイルはテキスト ファイルとして保存されます。 XML フォーマット ファイルにより柔軟性が向上しますが、いくつか制約も追加されます。 たとえば、以前のフォーマット ファイルでは、1 つのフィールドにプレフィックスとターミネータを同時に指定できましたが、XML フォーマット ファイルでは指定できません。<br /><br /> 注: XML フォーマットファイルは、ツールが[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インストールされている場合にのみサポートされ、OLE DB Driver for SQL Server です。|  
|BCP_OPTION_HINTS|*iValue* 引数には、ワイド文字列ポインターが含まれます。 ポインターが指す文字列には、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 一括コピー処理ヒント、または結果セットを返す [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを指定します。 複数の結果セットを返す [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを指定すると、1 つ目の結果セット以外はすべて無視されます。|  
|BCP_OPTION_KEEPIDENTITY|*iValue* 引数が TRUE に設定されている場合、このオプションは、一括コピー メソッドで、ID 制約が定義された [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 列用に指定したデータ値が挿入されることを示します。 入力ファイルには ID 列の値を指定する必要があります。 このオプションを設定しないと、挿入される行に対して新しい ID 値が生成されます。 ファイル内に存在する ID 列用のデータはすべて無視されます。|  
|BCP_OPTION_KEEPNULLS|ファイル内の空のデータ値を [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] テーブルで NULL 値に変換するかどうかを指定します。 *iValue* 引数を TRUE に設定すると、空の値は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] テーブルで NULL に変換されます。 既定では、空の値は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] テーブル内の列の既定値 (存在する場合) に変換されます。|  
|BCP_OPTION_LAST|コピーする最終行を指定します。 既定では、すべての行をコピーします。 1 未満の値を指定すると、このオプションは既定値にリセットされます。|  
|BCP_OPTION_LASTEX|BCP out 操作の場合は、データ ファイルにコピーするための、データベース テーブルの最後の行を指定します。<br /><br /> BCP in 操作の場合は、データベース テーブルにコピーするための、データ ファイルの最後の行を指定します。<br /><br /> *Ivalue*パラメーターは、値を含む符号付き64ビット整数のアドレスである必要があります。 BCPLASTEX に渡すことができる最大値は 2^63-1 です。|  
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
 プロバイダー固有のエラーが発生しました。詳細を確認するには、[ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) インターフェイスを使用してください。  
  
 E_UNEXPECTED  
 メソッドの呼び出しが予期されませんでした。 たとえば、この関数が呼び出される前に、[IBCPSession::BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) メソッドが呼び出されなかった場合などです。  
  
 E_OUTOFMEMORY  
 メモリ不足エラーです。  
  
## <a name="see-also"></a>参照  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [一括コピー操作の実行](../../oledb/features/performing-bulk-copy-operations.md)  
  
  
