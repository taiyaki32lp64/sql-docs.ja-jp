---
title: テーブル値パラメーターへのデータの挿入 |Microsoft Docs
description: OLE DB Driver for SQL Server を使用したテーブル値パラメーターへのデータの挿入
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, inserting data into
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 064dcfa74cd6471c8c279ef4b08e874097d98d64
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994131"
---
# <a name="inserting-data-into-table-valued-parameters"></a>テーブル値パラメーターへのデータの挿入
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server では、コンシューマーがテーブル値パラメーターの行にデータを指定するときのモデルとして、プッシュ モデルとプル モデルという 2 つのモデルがサポートされます。 プル モデルの使用方法を示すサンプルを利用できます。「[SQL Server データ プログラミング サンプル](https://msftdpprodsamples.codeplex.com/)」を参照してください。  
  
> [!NOTE]  
>  テーブル値パラメーターの列では、すべての行に既定値以外の値が格納されているか、すべての行に既定値が格納されているかのどちらかでなければなりません。 一部の行にだけ既定値を格納することはできません。 したがって、テーブル値パラメーターのバインドでは、テーブル値パラメーターの行セット列データに許容される状態値は DBSTATUS_S_ISNULL と DBSTATUS_S_OK だけです。 DBSTATUS_S_DEFAULT ではエラーが発生し、バインド状態値が DBSTATUS_E_BADSTATUS に設定されます。  
  
## <a name="push-model-loads-all-table-valued-paremeter-data-in-memory"></a>プッシュ モデル (メモリ内のすべてのテーブル値パラメーターのデータを読み込む)  
 プッシュ モデルは、パラメーター セットの使用方法 (ICommand::Execute の DBPARAMS パラメーター) に似ています。 プッシュ モデルが使用されるのは、IRowset インターフェイスをカスタマイズして実装せずに、テーブル値パラメーターの行セット オブジェクトを使用する場合だけです。 テーブル値パラメーターの行セット内の行数が少なく、アプリケーションに高いメモリ負荷がかからないことが見込まれる場合は、プッシュ モデルをお勧めします。 プッシュ モデルは、プル モデルよりも簡単な方法です。このモデルでは、コンシューマー アプリケーションに対し、標準的な OLE DB アプリケーションで現在一般的である以上の機能は要求されません。  
  
 コンシューマーは、コマンドを実行する前に、すべてのテーブル値パラメーターのデータをプロバイダーに提供します。 コンシューマーは、データを提供するために、各テーブル値パラメーター用にテーブル値パラメーターの行セット オブジェクトを作成します。 テーブル値パラメーターの行セット オブジェクトでは、行セットの挿入、設定、および削除の各操作が公開されます。このような操作は、コンシューマーがテーブル値パラメーターのデータを操作する際に使用します。 プロバイダーでは、実行時にこのテーブル値パラメーターの行セット オブジェクトからデータをフェッチします。  
  
 テーブル値パラメーターの行セット オブジェクトがコンシューマーに提供されると、コンシューマーはそのオブジェクトを行セット オブジェクトとして処理できます。 コンシューマーは、IColumnsInfo:: GetColumnInfo または IColumnsRowset:: GetColumnsRowset インターフェイスメソッドを使用して、各列の型情報 (型、最大長、有効桁数、および小数点以下桁数) を取得できます。 その後、コンシューマーはアクセサーを作成してデータのバインドを指定します。 次に、データ行をテーブル値パラメーターの行セットに挿入します。 これを行うには、IRowsetChange:: InsertRow を使用します。 IRowsetChange:: SetData または IRowsetChange::D eleteRows は、データを操作する必要がある場合に、テーブル値パラメーターの行セットオブジェクトでも使用できます。 テーブル値パラメーターの行セット オブジェクトは、ストリーム オブジェクトと同様に参照数がカウントされます。  
  
 IColumnsRowset:: GetColumnsRowset を使用した場合は、結果として得られる列の行セットオブジェクトに対して、次に IRowset:: GetNextRows、IRowset:: GetData、および IRowset:: ReleaseRows メソッドが呼び出されます。  
  
 OLE DB Driver for SQL Server でコマンドの実行が開始されると、テーブル値パラメーターの値は、このテーブル値パラメーターの行セット オブジェクトからフェッチされ、サーバーに送信されます。  
  
 プッシュ モデルでは、コンシューマーによる作業は必要最小限になりますが、使用するメモリはプル モデルよりも多くなります。これは、すべてのテーブル値パラメーターのデータが実行時にメモリ内に存在する必要があるためです。  
  
## <a name="pull-model-obtaining-table-valued-parameter-data-on-demand-from-the-consumer"></a>プル モデル (要求時にコンシューマーからテーブル値パラメーターのデータを取得する)  
 プル モデルは、次の 2 つのシナリオで役立ちます。  
  
-   行をストリームする場合。  
  
-   別のプロバイダーの行セットがテーブル値パラメーターの値として使用されている場合。  
  
 プル モデルでは、コンシューマーが要求時にプロバイダーにデータを提供します。 この方法は、アプリケーションでデータの挿入が何度も行われ、メモリ内のテーブル値パラメーターの行セットのデータが過度にメモリにアクセスする場合に使用します。 複数の OLE DB プロバイダーが使用される場合、プル モデルでは、コンシューマーが任意の行セット オブジェクトをテーブル値パラメーターの値として提供できます。  
  
 プル モデルを使用するには、コンシューマーが行セット オブジェクトを独自に実装する必要があります。 プルモデルをテーブル値パラメーターの行セット (CLSID_ROWSET_TVP) と共に使用する場合、コンシューマーは、プロバイダーが ITableDefinitionWithConstraints を通じて公開するテーブル値パラメーターの行セットオブジェクトを集計する必要があります。CreateTableWithConstraints メソッドまたは IOpenRowset:: OpenRowset メソッド。 コンシューマー オブジェクトに期待されるのは、IRowset インターフェイスの実装をオーバーライドすることだけです。 次の関数をオーバーライドする必要があります。  
  
-   IRowset::GetNextRows  
  
-   IRowset::AddRefRows  
  
-   IRowset:: GetData  
  
-   IRowset::ReleaseRows  
  
-   IRowset::RestartPosition  
  
 OLE DB Driver for SQL Server では、コンシューマーの行セット オブジェクトから一度に 1 つ以上の行を読み取り、テーブル値パラメーターのストリーミング動作をサポートします。 たとえば、ユーザーは、(メモリではなく) ディスクにテーブル値パラメーターの行セットのデータを保持し、OLE DB Driver for SQL Server から要求されたときにディスクからデータを読み取る機能を実装する場合があります。  
  
 コンシューマーは、テーブル値パラメーターの行セットオブジェクトで IAccessor:: CreateAccessor を使用して、データ形式を SQL Server の OLE DB ドライバーに伝えます。 プロバイダーは、データをコンシューマー バッファーから読み取る際に、既定以外の書き込み可能な列すべてを少なくとも 1 つのアクセサー ハンドルで使用できることを確認し、対応するハンドルを使用して列のデータを読み取ります。 あいまいさを排除するため、テーブル値パラメーターの行セットの列とバインドが一対一で対応するようにする必要があります。 同じ列に対するバインドが重複すると、エラーが発生します。 また、各アクセサーには、DBBindings の*Iordinal*メンバーが順番に含まれることが想定されています。 IRowset::GetData が各行のアクセサーの数と同じ回数だけ呼び出されます。呼び出しの順序は、*iOrdinal* 値の順序 (昇順) に基づきます。  
  
 プロバイダーは、テーブル値パラメーターの行セット オブジェクトで公開されるインターフェイスのほとんどを実装することが期待されています。 コンシューマーは、最小限のインターフェイス (IRowset) を使用して行セット オブジェクトを実装します。 無計画な集計があるため、残りの必須の行セット オブジェクトのインターフェイスは、テーブル値パラメーターの行セット オブジェクトによって実装されます。  
  
 任意の OLE DB プロバイダー用に取得した行セット オブジェクトなどの他の行セット オブジェクトの場合、コンシューマーが提供した行セットは、OLE DB の仕様で指定されているとおり、必須の行セット オブジェクトのインターフェイスすべてを実装する必要があります。  
  
 実行時に、OLE DB Driver for SQL Server は行セット オブジェクトにコールバックして、行をフェッチして列のデータを読み取ります。  
  
## <a name="see-also"></a>参照  
 [テーブル値パラメーター &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [テーブル値パラメーターの使用 &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
