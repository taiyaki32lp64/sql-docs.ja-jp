---
title: OLE DB Driver for SQL Server の UTF-8 のサポート | Microsoft Docs
description: OLE DB Driver for SQL Server の UTF-8 のサポート
ms.custom: ''
ms.date: 04/23/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: v-kaywon
ms.author: v-kaywon
ms.openlocfilehash: fb596365f284a141b5e57bfc8601427fe603d73d
ms.sourcegitcommit: 49f3d12c0a46d98b82513697a77a461340f345e1
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70392016"
---
# <a name="utf-8-support-in-ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server の UTF-8 のサポート
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Microsoft OLE DB Driver for SQL Server (version 18.2.1) によって、UTF-8 サーバーのエンコードのサポートが追加されます。 SQL Server の UTF-8 のサポートについては、以下を参照してください。
- [照合順序と Unicode のサポート](../../../relational-databases/collations/collation-and-unicode-support.md)
- [UTF-8 のサポート](#ctp23)

> [!IMPORTANT]
> Microsoft OLE DB Driver for SQL Server は[Getacp](https://docs.microsoft.com/windows/win32/api/winnls/nf-winnls-getacp)関数を使用して、DBTYPE_STR 入力バッファーのエンコーディングを決定します。 GetACP が UTF-8 エンコードを返すシナリオはサポートされていません。 バッファーで Unicode データを格納する必要がある場合は、バッファーデータ型を DBTYPE_WSTR (UTF-16 エンコード) に設定する必要があります。

## <a name="data-insertion-into-a-utf-8-encoded-char-or-varchar-column"></a>UTF-8 でエンコードされた CHAR または VARCHAR 列へのデータの挿入
挿入用の入力パラメーター バッファーが作成されるとき、そのバッファーは、[DBBINDING 構造体](https://go.microsoft.com/fwlink/?linkid=2071182)の配列を使用して記述されます。 各 DBBINDING 構造体では単一のパラメーターがコンシューマーのバッファーに関連付けられ、データ値の長さや型などの情報が含まれます。 CHAR 型の入力パラメーター バッファーでは、DBBINDING 構造体の *wType* を DBTYPE_STR に設定する必要があります。 WCHAR 型の入力パラメーター バッファーでは、DBBINDING 構造体の *wType* を DBTYPE_WSTR に設定する必要があります。

パラメーターを指定してコマンドを実行するとき、ドライバーによってパラメーターのデータ型情報が作成されます。 入力バッファーの型とパラメーターのデータ型が一致している場合、ドライバーで変換は行われません。 それ以外の場合は、ドライバーによって、入力パラメーター バッファーがパラメーターのデータ型に変換されます。 パラメーターのデータ型は、[icommandwithparameters::setparameterinfo](https://go.microsoft.com/fwlink/?linkid=2071577) を呼び出すことでユーザーが明示的に設定できます。 情報が提供されていない場合、ドライバーでは、(a) ステートメントが準備されたときにサーバーから列のメタデータを取得するか、(b) 入力パラメーターのデータ型から既定の変換を試みることによって、パラメーターのデータ型情報を取得します。

入力パラメーター バッファーは、入力バッファーのデータ型とパラメーターのデータ型に応じて、ドライバーまたはサーバーによって、サーバーの列の照合順序に変換される場合があります。 この変換時に、入力バッファー内のすべての文字をクライアントのコード ページまたはデータベースの照合順序のコード ページで表現できない場合は、データ損失が発生する可能性があります。 次の表に、UTF-8 対応列にデータを挿入する際の変換プロセスを示します。

|バッファーのデータ型|パラメーター データ型|変換|ユーザーの予防措置|
|---             |---                |---       |---            |
|DBTYPE_STR|DBTYPE_STR|クライアントのコード ページからデータベースの照合順序のコード ページへのサーバーの変換; データベースの照合順序のコード ページから列の照合順序のコード ページへのサーバーの変換。|入力データのすべての文字を、クライアントのコード ページとデータベースの照合順序のコード ページで表現できることを確認します。 たとえば、ポーランド語の文字を挿入するには、クライアントのコード ページを 1250 (ANSI 中央ヨーロッパ) に設定し、データベースの照合順序で、照合順序指定子として Polish を使用する (例: Polish_100_CI_AS_SC) か、UTF-8 対応にすることができます。|
|DBTYPE_STR|DBTYPE_WSTR|クライアントのコード ページから UTF-16 エンコードへのドライバーの変換; UTF-16 エンコードから列の照合順序のコード ページへのサーバーの変換。|入力データのすべての文字を、クライアントのコード ページで表現できることを確認します。 たとえば、ポーランド語の文字を挿入するには、クライアントのコード ページを 1250 (ANSI 中央ヨーロッパ) に設定できます。|
|DBTYPE_WSTR|DBTYPE_STR|UTF-16 エンコードからデータベースの照合順序のコード ページへのドライバーの変換; データベースの照合順序のコード ページから列の照合順序のコード ページへのサーバーの変換。|入力データのすべての文字を、データベースの照合順序のコード ページで表現できることを確認します。 たとえば、ポーランド語の文字を挿入するには、データベースの照合順序のコード ページで、照合順序指定子として Polish を使用する (例: Polish_100_CI_AS_SC) か、UTF-8 対応にすることができます。|
|DBTYPE_WSTR|DBTYPE_WSTR|UTF-16 から列の照合順序のコード ページへのサーバーの変換。|[なし] :|

## <a name="data-retrieval-from-a-utf-8-encoded-char-or-varchar-column"></a>UTF-8 でエンコードされた CHAR または VARCHAR 列からのデータ取得
データ取得用のバッファーが作成されるとき、そのバッファーは、[DBBINDING 構造体](https://go.microsoft.com/fwlink/?linkid=2071182)の配列を使用して記述されます。 各 DBBINDING 構造体には、取得された行の単一の列が関連付けられます。 列データを CHAR として取得するには、DBBINDING 構造体の*wType* を DBTYPE_STR に設定します。 列データを WCHAR として取得するには、DBBINDING 構造体の*wType* を DBTYPE_WSTR に設定します。

結果のバッファーの型インジケーターが DBTYPE_STR の場合は、ドライバーによって UTF-8 エンコード データがクライアントのエンコードに変換されます。 ユーザーは、UTF-8 列からのデータをクライアントのエンコードで表現できることを確認する必要があります。そうでない場合は、データ損失が発生する可能性があります。

結果のバッファーの型インジケーターが DBTYPE_WSTR の場合は、ドライバーによって UTF-8 エンコード データが UTF-16 エンコードに変換されます。

<a name="ctp23"></a>

### <a name="utf-8-support-sql-server-2019-ctp-23"></a>UTF-8 のサポート (SQL Server 2019 CTP 2.3)

[!INCLUDE[ss2019](../../../includes/sssqlv15-md.md)] では、インポートまたはエクスポートのエンコードとして、あるいはテキスト データのデータベース レベルまたは列レベルの照合順序として、広く使用されている UTF-8 文字エンコードの完全なサポートが導入されています。 UTF-8 は、`CHAR` および `VARCHAR` データ型で許可されており、`UTF8` サフィックスを持つようにオブジェクトの照合順序を作成するか変更すると有効になります。

たとえば、`LATIN1_GENERAL_100_CI_AS_SC` を `LATIN1_GENERAL_100_CI_AS_SC_UTF8` に変更するような場合です。 UTF-8 は、[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] で導入された補助文字をサポートする Windows 照合順序にのみ使用できます。 `NCHAR` および `NVARCHAR` では UTF-16 エンコードのみが許可され、変更されていません。

使用されている文字セットによっては、この機能によりストレージを大幅に節約できます。 たとえば、ASCII (ラテン) 文字列の既存の列データ型を、UTF-8 対応の照合順序を使用して `NCHAR(10)` から `CHAR(10)` に変更すると、必要なストレージが 50% 削減されます。 このように減るのは、`NCHAR(10)` を保存するには 20 バイト必要であるのに対し、`CHAR(10)` では同じ Unicode 文字列に 10 バイトしか必要ないためです。

詳細については、「 [Collation and Unicode Support](../../../relational-databases/collations/collation-and-unicode-support.md)」を参照してください。

**CTP 2.1** 既定で [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] の設定中に UTF-8 照合順序を選択するためのサポートが追加されました。

**CTP 2.2** SQL Server レプリケーションで UTF-8 文字エンコードを使用するためのサポートが追加されました。

**CTP 2.3** BIN2 照合順序 (UTF8_BIN2) で UTF-8 文字エンコードを使用するためのサポートが追加されました。

## <a name="see-also"></a>参照  
[OLE DB Driver for SQL Server の機能](../../oledb/features/oledb-driver-for-sql-server-features.md) 

[OLE DB Driver for SQL Server の UTF-16 のサポート](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)    
  
  
