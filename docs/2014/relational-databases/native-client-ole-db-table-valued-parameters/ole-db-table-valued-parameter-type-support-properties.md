---
title: OLE DB テーブル値パラメーターの型のサポート (プロパティ) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (properties)
ms.assetid: b9c4e6ed-fe4f-4ef8-9bc8-784d80d44039
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5cdd19895a1cf91e1c5c8608013cb52482f946c5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046537"
---
# <a name="ole-db-table-valued-parameter-type-support-properties"></a>OLE DB テーブル値パラメーターの型のサポート (プロパティ)
  このトピックでは、テーブル値パラメーターの行セット オブジェクトに関連付けられている OLE DB プロパティおよびプロパティ セットについて説明します。  
  
## <a name="properties"></a>プロパティ  
 次に、テーブル値パラメーターの行セット オブジェクトの IRowsetInfo::GetProperties メソッドを使用して公開されるプロパティの一覧を示します。 テーブル値パラメーターの行セット プロパティはすべて読み取り専用であることに注意してください。 そのため、いずれかを設定しようと iopenrowset::openrowset または ITableDefinitionWithConstraints::CreateTableWithConstraints プロパティのメソッドが既定以外の値にエラーが発生する、オブジェクトは作成されません。  
  
 テーブル値パラメーターの行セット オブジェクトで実装されていないプロパティは、次の一覧には含まれていません。 すべてのプロパティの一覧は、Windows Data Access Components の OLE DB に関するドキュメントを参照してください。  
  
|プロパティ ID|値|  
|-----------------|-----------|  
|DBPROP_ABORTPRESERVE|VARIANT_TRUE|  
|DBPROP_ACCESSORDER|DBPROPVAL_AO_RANDOM|  
|DBPROP_BLOCKINGSTORAGEOBJECTS|VARIANT_TRUE|  
|DBPROP_BOOKMARKS<br /><br /> DBPROP_LITERALBOOKMARKS|R/W読み取り専用です。<br /><br /> 既定値:VARIANT_FALSE<br /><br /> 説明:ブックマークはテーブル値パラメーター行セット オブジェクトで許可されていません。|  
|DBPROP_BOOKMARKSKIPPED|VARIANT_FALSE|  
|DBPROP_BOOKMARKTYPE|DBPROPVAL_BMK_NUMERIC|  
|DBPROP_CANHOLDROWS|VARIANT_FALSE|  
|DBPROP_CHANGEINSERTEDROWS|VARIANT_TRUE|  
|DBPROP_COLUMNRESTRICT|VARIANT_FALSE|  
|DBPROP_COMMANDTIMEOUT|0|  
|DBPROP_COMMITPRESERVE|VARIANT_TRUE|  
|DBPROP_DEFERRED|VARIANT_FALSE|  
|DBPROP_DELAYSTORAGEOBJECTS|VARIANT_FALSE|  
|DBPROP_IAccessor<br /><br /> DBPROP_IColumnsInfo<br /><br /> DBPROP_IConvertType<br /><br /> DBPROP_IRowset<br /><br /> DBPROP_IRowsetInfo<br /><br /> DBPROP_IColumnsRowset|VARIANT_TRUE|  
|DBPROP_IConnectionPointContainer<br /><br /> DBPROP_IMultipleResults<br /><br /> DBPROP_IRowsetUpdate<br /><br /> DBPROP_IRowsetIdentity<br /><br /> DBPROP_IRowsetLocate<br /><br /> DBPROP_IRowsetScroll<br /><br /> DBPROP_IRowsetResynch|VARIANT_FALSE|  
|DBPROP_IRowsetChange|VARIANT_TRUE<br /><br /> 注:テーブル値パラメーター行セット オブジェクトには、IRowsetChange インターフェイスがサポートしています。<br /><br /> DBPROP_IRowsetChange を VARIANT_TRUE に設定して作成された行セットの動作は、即時更新モードの動作になります。<br /><br /> ただし、BLOB 列が ISequentialStream オブジェクトとしてバインドされる場合、コンシューマーでは、テーブル値パラメーターの行セット オブジェクトの有効期間中その列を保持する必要があります。|  
|DBPROP_ISupportErrorInfo|VARIANT_TRUE|  
|DBPROP_ISequentialStream|VARIANT_TRUE|  
|DBPROP_IMMOBILEROWS|VARIANT_TRUE|  
|DBPROP_LITERALIDENTITY|VARIANT_TRUE|  
|DBPROP_LOCKMODE|DBPROPVAL_LM_NONE|  
|DBPROP_MAXOPENROWS|0|  
|DBPROP_MAXPENDINGROWS|0|  
|DBPROP_MAXROWS|0|  
|DBPROP_NOTIFICATIONPHASES|0|  
|DBPROP_NOTIFYCOLUMNSET DBPROP_NOTIFYROWDELETE DBPROP_NOTIFYROWFIRSTCHANGE DBPROP_NOTIFYROWINSERT DBPROP_NOTIFYROWRESYNCH DBPROP_NOTIFYROWSETRELEASE DBPROP_NOTIFYROWSETFETCH-POSITIONCHANGE DBPROP_NOTIFYROWUNDOCHANGE DBPROP_NOTIFYROWUNDODELETE DBPROP_NOTIFYROWUNDOINSERT DBPROP_NOTIFYROWUPDATE|0|  
|DBPROP_OTHERINSERT DBPROP_OTHERUPDATEDELETE|VARIANT_FALSE|  
|DBPROP_OWNINSERT<br /><br /> DBPROP_OWNUPDATEDELETE|VARIANT_TRUE|  
|DBPROP_QUICKRESTART|VARIANT_TRUE|  
|DBPROP_REENTRANTEVENTS|VARIANT_FALSE|  
|DBPROP_REMOVEDELETED|VARIANT_TRUE|  
|DBPROP_RETURNPENDINGINSERTS|VARIANT_TRUE|  
|DBPROP_ROWRESTRICT|VARIANT_FALSE|  
|DBPROP_ROWTHREADMODEL|DBPROPVAL_RT_FREETHREAD|  
|DBPROP_SERVERCURSOR|VARIANT_FALSE|  
|DBPROP_SERVERDATAONINSERT|VARIANT_FALSE|  
|DBPROP_STRONGIDENTITY|VARIANT_TRUE|  
|DBPROP_TRANSACTEDOBJECT|VARIANT_FALSE|  
|DBPROP_UNIQUEROWS|VARIANT_FALSE|  
|DBPROP_UPDATABILITY|DBPROPVAL_UP_CHANGE &#124; DBPROPVAL_UP_DELETE &#124; DBPROPVAL_UP_INSERT|  
  
## <a name="property-sets"></a>プロパティ セット  
 次のプロパティ セットでは、テーブル値パラメーターがサポートされます。  
  
### <a name="dbpropsetsqlservercolumn"></a>DBPROPSET_SQLSERVERCOLUMN  
 このプロパティは、必要な場合、DBCOLUMNDESC 構造体から各列に対して ITableDefinitionWithConstraints::CreateTableWithConstraints を使用して、テーブル値パラメーター行セット オブジェクトを作成する過程でコンシューマーによって使用されます。  
  
|プロパティ ID|プロパティ値|  
|-----------------|--------------------|  
|SSPROP_COL_COMPUTED|R/W[読み取り/書き込み]<br /><br /> 既定値:VARIANT_FALSE<br /><br /> 型:VT_BOOL<br /><br /> 説明:VARIANT_TRUE に設定すると、列が計算列であることを示します。 VARIANT_FALSE に設定された場合は、その列が計算列ではないことを示します。|  
  
### <a name="dbpropsetsqlserverparameter"></a>DBPROPSET_SQLSERVERPARAMETER  
 これらのプロパティが isscommandwithparameters::getparameterproperties への呼び出しでテーブル値パラメーターの型情報の検出中にコンシューマーによって読み取られ、テーブル値パラメーターに関する特定のプロパティを設定中にコンシューマーによって設定isscommandwithparameters::setparameterproperties 経由。  
  
 次の表に、これらのプロパティの詳細を示します。  
  
|プロパティ ID|プロパティ値|  
|-----------------|--------------------|  
|SSPROP_PARAM_TYPE_TYPENAME|R/W[読み取り/書き込み]<br /><br /> 既定値:VT_EMPTY<br /><br /> 型:VT_BSTR<br /><br /> 説明:コンシューマーは、取得、またはテーブル値パラメーターの型の名前を設定する、このプロパティを使用します。<br /><br /> このプロパティは、CLR ユーザー定義型と共に使用することもできます。<br /><br /> このプロパティは、テーブル値パラメーターのテーブルの型名を指定するように、必要に応じて指定できます (ODBC の呼び出し構文のコマンドの場合)。 このプロパティは、パラメーター化されたアドホック SQL クエリに必要です。|  
|SSPROP_PARAM_TYPE_SCHEMANAME|R/W[読み取り/書き込み]<br /><br /> 既定値:VT_EMPTY<br /><br /> 型:VT_BSTR<br /><br /> 説明:コンシューマーは、取得またはテーブル値パラメーターの型のスキーマ名を設定する、このプロパティを使用します。<br /><br /> このプロパティは、CLR ユーザー定義型と共に使用することもできます。|  
|SSPROP_PARAM_TYPE_CATALOGNAME|R/W読み取り専用です。<br /><br /> 既定値:VT_EMPTY<br /><br /> 型:VT_BSTR<br /><br /> 説明:コンシューマーでは、このプロパティを使用して、テーブル値パラメーターの型のカタログ名を取得します。<br /><br /> このプロパティは、CLR ユーザー定義型と共に使用することもできます。 このプロパティを設定するとエラーになります。ユーザー定義テーブル型は、それを使用するテーブル値パラメーターと同じデータベースに内にある必要があります。|  
|SSPROP_PARAM_TABLE_DEFAULT_COLUMNS|R/W[読み取り/書き込み]<br /><br /> 既定値:VT_EMPTY<br /><br /> 型:VT_UI2 &#124; VT_ARRAY<br /><br /> 説明:コンシューマーは、行セットの列のセットが既定値として扱うには指定するこのプロパティを使用します。 これらの列の値は送信されません。 プロバイダーは、コンシューマーの行セット オブジェクトからデータをフェッチしている間、このような列のバインドを必要としません。<br /><br /> 配列の各要素は、行セット オブジェクト内の列の序数である必要があります。 序数が無効な場合、コマンドの実行時にエラーが発生します。|  
|SSPROP_PARAM_TABLE_COLUMN_ORDER|R/W[読み取り/書き込み]<br /><br /> 既定値:VT_EMPTY<br /><br /> 型:VT_UI2 &#124; VT_ARRAY<br /><br /> 説明:このプロパティは、並べ替えを示すために、サーバーへのヒントを提供するコンシューマーによって使用データの列の順序付けします。 プロバイダーでは検証は行われず、提供された仕様にコンシューマーが準拠していることが想定されます。 サーバーでは、このプロパティを使用して最適化を実行します。<br /><br /> 各列の列順序情報は、配列内の要素のペアで表されます。 ペアの最初の要素は列数で、 ペアの 2 番目の要素は、昇順の場合は 1、降順の場合は 2 になります。|  
  
## <a name="see-also"></a>参照  
 [OLE DB テーブル値パラメーターの型のサポート](ole-db-table-valued-parameter-type-support.md)   
 [テーブル値パラメーターの使用 &#40;OLE DB&#41;](table-valued-parameters-ole-db.md)  
  
  
