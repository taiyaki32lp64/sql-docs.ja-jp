---
title: SQL Server インデックスの作成 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- CreateIndex function
- constraints [OLE DB]
- SQL Server Native Client OLE DB provider, indexes
- indexes [OLE DB]
- adding indexes
ms.assetid: 6239d440-2818-4b98-bb79-732dced41952
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bda39528b6bc04fbff6faa4c72d85a4eccd576c6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046457"
---
# <a name="creating-sql-server-indexes"></a>SQL Server インデックスの作成
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーが公開、 **iindexdefinition::createindex**関数を新しいインデックスを定義するコンシューマー[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]テーブル。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、インデックスまたは制約としてテーブルのインデックスを作成します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、制約を作成する権限がテーブルの所有者、データベースの所有者、および特定の管理ロールのメンバーに許可されます。 テーブルにインデックスを作成できるのは、既定では、テーブルの所有者だけです。 したがって、**CreateIndex** が成功するか失敗するかは、アプリケーション ユーザーのアクセス権だけでなく、作成するインデックスの種類によっても異なります。  
  
 コンシューマーは、*pTableID* パラメーターの *uName* 共用体の *pwszName* メンバーに Unicode 文字列としてテーブル名を指定します。 *pTableID* の *eKind* メンバーを DBKIND_NAME にする必要があります。  
  
 *PIndexID*パラメーターは、NULL にしてがの場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、インデックスの一意の名前を作成します。 *ppIndexID* パラメーターに DBID への有効なポインターを指定することで、インデックスの名前をキャプチャできます。  
  
 インデックス名は、*pIndexID* パラメーターの *uName* 共用体の *pwszName* メンバーに Unicode 文字列で指定できます。 *pIndexID* の *eKind* メンバーを DBKIND_NAME にする必要があります。  
  
 コンシューマーは、インデックスに参加する列または複数の列を名前で指定します。 **CreateIndex** で使用する DBINDEXCOLUMNDESC 構造体ごとに、*pColumnID* の *eKind* メンバーを DBKIND_NAME にする必要があります。 列の名前は、*pColumnID* の *uName* 共用体の *pwszName* メンバーに Unicode 文字列で指定します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インデックス内の値に基づいて昇順のサポート。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーがコンシューマーの DBINDEXCOLUMNDESC 構造体に DBINDEX_COL_ORDER_DESC を指定する場合、E_INVALIDARG を返します。  
  
 **CreateIndex** では、インデックスのプロパティが次のように解釈されます。  
  
|プロパティ ID|説明|  
|-----------------|-----------------|  
|DBPROP_INDEX_AUTOUPDATE|R/W読み取り/書き込み<br /><br /> 既定値:なし<br /><br /> 説明:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーがこのプロパティをサポートしていません。 **CreateIndex** でこのプロパティの設定を試みると、戻り値として DB_S_ERRORSOCCURRED が返されます。 プロパティ構造体の *dwStatus* メンバーには、DBPROPSTATUS_BADVALUE が示されます。|  
|DBPROP_INDEX_CLUSTERED|R/W読み取り/書き込み<br /><br /> 既定値:VARIANT_FALSE<br /><br /> 説明:クラスタ リングのコントロールのインデックス。<br /><br /> VARIANT_TRUE:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーが、クラスター化インデックスを作成しようとしています。、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]テーブル。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、どのテーブルでもクラスター化インデックスは 1 つしかサポートされません。<br /><br /> VARIANT_FALSE:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーが、非クラスター化インデックスを作成しようとしています。、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]テーブル。|  
|DBPROP_INDEX_FILLFACTOR|R/W読み取り/書き込み<br /><br /> 既定値:0<br /><br /> 説明:ストレージに使用されるインデックス ページの割合を指定します。 詳細については、「[CREATE INDEX](/sql/t-sql/statements/create-index-transact-sql)」を参照してください。<br /><br /> バリアントの型は VT_I4 です。 値は 1 ～ 100 にする必要があります。|  
|DBPROP_INDEX_INITIALIZE|R/W読み取り/書き込み<br /><br /> 既定値:なし<br /><br /> 説明:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーがこのプロパティをサポートしていません。 **CreateIndex** でこのプロパティの設定を試みると、戻り値として DB_S_ERRORSOCCURRED が返されます。 プロパティ構造体の *dwStatus* メンバーには、DBPROPSTATUS_BADVALUE が示されます。|  
|DBPROP_INDEX_NULLCOLLATION|R/W読み取り/書き込み<br /><br /> 既定値:なし<br /><br /> 説明:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーがこのプロパティをサポートしていません。 **CreateIndex** でこのプロパティの設定を試みると、戻り値として DB_S_ERRORSOCCURRED が返されます。 プロパティ構造体の *dwStatus* メンバーには、DBPROPSTATUS_BADVALUE が示されます。|  
|DBPROP_INDEX_NULLS|R/W読み取り/書き込み<br /><br /> 既定値:なし<br /><br /> 説明:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーがこのプロパティをサポートしていません。 **CreateIndex** でこのプロパティの設定を試みると、戻り値として DB_S_ERRORSOCCURRED が返されます。 プロパティ構造体の *dwStatus* メンバーには、DBPROPSTATUS_BADVALUE が示されます。|  
|DBPROP_INDEX_PRIMARYKEY|R/W読み取り/書き込み<br /><br /> 既定値:VARIANT_FALSE の説明:参照の整合性を主キー制約としてインデックスを作成します。<br /><br /> VARIANT_TRUE:テーブルの PRIMARY KEY 制約をサポートするために、インデックスが作成されます。 列には NULL 値を許容しないでください。<br /><br /> VARIANT_FALSE:インデックスは、テーブル内の行値の PRIMARY KEY 制約として使用されません。|  
|DBPROP_INDEX_SORTBOOKMARKS|R/W読み取り/書き込み<br /><br /> 既定値:なし<br /><br /> 説明:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーがこのプロパティをサポートしていません。 **CreateIndex** でこのプロパティの設定を試みると、戻り値として DB_S_ERRORSOCCURRED が返されます。 プロパティ構造体の *dwStatus* メンバーには、DBPROPSTATUS_BADVALUE が示されます。|  
|DBPROP_INDEX_TEMPINDEX|R/W読み取り/書き込み<br /><br /> 既定値:なし<br /><br /> 説明:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーがこのプロパティをサポートしていません。 **CreateIndex** でこのプロパティの設定を試みると、戻り値として DB_S_ERRORSOCCURRED が返されます。 プロパティ構造体の *dwStatus* メンバーには、DBPROPSTATUS_BADVALUE が示されます。|  
|DBPROP_INDEX_TYPE|R/W読み取り/書き込み<br /><br /> 既定値:なし<br /><br /> 説明:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーがこのプロパティをサポートしていません。 **CreateIndex** でこのプロパティの設定を試みると、戻り値として DB_S_ERRORSOCCURRED が返されます。 プロパティ構造体の *dwStatus* メンバーには、DBPROPSTATUS_BADVALUE が示されます。|  
|DBPROP_INDEX_UNIQUE|R/W読み取り/書き込み<br /><br /> 既定値:VARIANT_FALSE<br /><br /> 説明:参加している列または列に UNIQUE 制約としてインデックスを作成します。<br /><br /> VARIANT_TRUE:インデックスを使用して、テーブルの行の値を一意に制限します。<br /><br /> VARIANT_FALSE:インデックスは、行の値を一意に制約されません。|  
  
 プロバイダー固有のプロパティ セット DBPROPSET_SQLSERVERINDEX、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、次のデータ ソース情報のプロパティを定義します。  
  
|プロパティ ID|説明|  
|-----------------|-----------------|  
|SSPROP_INDEX_XML|型:VT_BOOL (R/W)<br /><br /> 既定値:VARIANT_FALSE<br /><br /> 説明:このプロパティを指定するには、値 VARIANT_TRUE を iindexdefinition::createindex のインデックスが作成される列に対応して作成されているプライマリ xml インデックスが発生します。 このプロパティが VARIANT_TRUE の場合、cIndexColumnDescs を 1 にする必要があります。それ以外の値を指定するとエラーが発生します。|  
  
 次の例では、主キー インデックスを作成します。  
  
```  
// This CREATE TABLE statement shows the referential integrity and   
// PRIMARY KEY constraint on the OrderDetails table that will be created   
// by the following example code.  
//  
// CREATE TABLE OrderDetails  
// (  
//    OrderID      int      NOT NULL  
//    ProductID   int      NOT NULL  
//        CONSTRAINT PK_OrderDetails  
//        PRIMARY KEY CLUSTERED (OrderID, ProductID),  
//    UnitPrice   money      NOT NULL,  
//    Quantity   int      NOT NULL,  
//    Discount   decimal(2,2)   NOT NULL  
//        DEFAULT 0  
// )  
//  
HRESULT CreatePrimaryKey  
    (  
    IIndexDefinition* pIIndexDefinition  
    )  
    {  
    HRESULT             hr = S_OK;  
  
    DBID                dbidTable;  
    DBID                dbidIndex;  
    const ULONG         nCols = 2;  
    ULONG               nCol;  
    const ULONG         nProps = 2;  
    ULONG               nProp;  
  
    DBINDEXCOLUMNDESC   dbidxcoldesc[nCols];  
    DBPROP              dbpropIndex[nProps];  
    DBPROPSET           dbpropset;  
  
    DBID*               pdbidIndexOut = NULL;  
  
    // Set up identifiers for the table and index.  
    dbidTable.eKind = DBKIND_NAME;  
    dbidTable.uName.pwszName = L"OrderDetails";  
  
    dbidIndex.eKind = DBKIND_NAME;  
    dbidIndex.uName.pwszName = L"PK_OrderDetails";  
  
    // Set up column identifiers.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        dbidxcoldesc[nCol].pColumnID = new DBID;  
        dbidxcoldesc[nCol].pColumnID->eKind = DBKIND_NAME;  
  
        dbidxcoldesc[nCol].eIndexColOrder = DBINDEX_COL_ORDER_ASC;  
        }  
    dbidxcoldesc[0].pColumnID->uName.pwszName = L"OrderID";  
    dbidxcoldesc[1].pColumnID->uName.pwszName = L"ProductID";  
  
    // Set properties for the index. The index is clustered,  
    // PRIMARY KEY.  
    for (nProp = 0; nProp < nProps; nProp++)  
        {  
        dbpropIndex[nProp].dwOptions = DBPROPOPTIONS_REQUIRED;  
        dbpropIndex[nProp].colid = DB_NULLID;  
  
        VariantInit(&(dbpropIndex[nProp].vValue));  
  
        dbpropIndex[nProp].vValue.vt = VT_BOOL;  
        }  
    dbpropIndex[0].dwPropertyID = DBPROP_INDEX_CLUSTERED;  
    dbpropIndex[0].vValue.boolVal = VARIANT_TRUE;  
  
    dbpropIndex[1].dwPropertyID = DBPROP_INDEX_PRIMARYKEY;  
    dbpropIndex[1].vValue.boolVal = VARIANT_TRUE;  
  
    dbpropset.rgProperties = dbpropIndex;  
    dbpropset.cProperties = nProps;  
    dbpropset.guidPropertySet = DBPROPSET_INDEX;  
  
    hr = pIIndexDefinition->CreateIndex(&dbidTable, &dbidIndex, nCols,  
        dbidxcoldesc, 1, &dbpropset, &pdbidIndexOut);  
  
    // Clean up dynamically allocated DBIDs.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        delete dbidxcoldesc[nCol].pColumnID;  
        }  
  
    return (hr);  
    }  
```  
  
## <a name="see-also"></a>参照  
 [テーブルとインデックス](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
  
