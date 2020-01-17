---
title: SQL Server テーブルを作成する |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- SQL Server Native Client OLE DB provider, tables
- DBCOLUMNDESC usage
- adding tables
- CreateTable function
ms.assetid: a7b8d142-d76a-44d9-a583-86ac5109fbe8
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ab6a605e77bddbaa38ee71a0d54624c36a229f32
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73788437"
---
# <a name="creating-sql-server-tables"></a>SQL Server テーブルの作成
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、 **Itabledefinition:: CreateTable**関数を公開します。これにより、コンシューマーは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルを作成できます。 コンシューマーは**CreateTable**を使用して、コンシューマーという名前のパーマネントテーブル、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーによって生成された一意の名前を持つパーマネントテーブルまたは一時テーブルを作成します。  
  
 コンシューマーが**Itabledefinition:: CreateTable**を呼び出すと、DBPROP_TBL_TEMPTABLE プロパティの値が VARIANT_TRUE 場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーがコンシューマーの一時テーブル名を生成します。 コンシューマーは、*CreateTable* メソッドの **pTableID** パラメーターに NULL を設定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーによって生成された名前を持つ一時テーブルは、 **tables**行セットには表示されませんが、 **IOpenRowset**インターフェイスを使用してアクセスできます。  
  
 *Ptableid*パラメーターの*uName*共用体の*pwszName*メンバーにテーブル名を指定すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーによって、その名前を持つ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルが作成されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルの名前付けに関する制約が適用されるので、そのテーブル名で、パーマネント テーブル、ローカル一時テーブルまたはグローバル一時テーブルのいずれであるかを示すことができます。 詳細については、「[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)」を参照してください。 *ppTableID* パラメーターには NULL を指定できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、パーマネントテーブルまたは一時テーブルの名前を生成できます。 コンシューマーが*Ptableid*パラメーターを NULL に設定し、有効な DBID\*を指すように*pptableid*を設定した場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、 *uName*の*pwszName*メンバーに生成されたテーブルの名前を返します。*Pptableid*の値によって指された DBID の和集合。 Native Client OLE DB プロバイダー名前付きテーブルの一時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を作成するには、 *rgPropertySets*パラメーターで参照されているテーブルプロパティセットの DBPROP_TBL_TEMPTABLE OLE DB table プロパティをコンシューマーに含めます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーの名前付き一時テーブルはローカルです。  
  
 **pTableID** パラメーターの *eKind* メンバーに DBKIND_NAME を指定しないと、*CreateTable* では DB_E_BADTABLEID が返されます。  
  
## <a name="dbcolumndesc-usage"></a>DBCOLUMNDESC の使用方法  
 コンシューマーは、*pwszTypeName* メンバーまたは *wType* メンバーのいずれかを使用して、列のデータ型を指定できます。 コンシューマーが*pwszTypeName*でデータ型を指定した場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは*wtype*の値を無視します。  
  
 *pwszTypeName* メンバーを使用する場合、コンシューマーでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ型名を使用してデータ型が指定されます。 有効なデータ型名は、PROVIDER_TYPES スキーマの行セットの TYPE_NAME 列に返されるデータ型名です。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、 *Wtype*メンバー内の OLE DB 列挙型の DBTYPE 値のサブセットを認識します。 詳細については、「 [ITableDefinition でのデータ型のマッピング](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md)」を参照してください。  
  
> [!NOTE]  
>  列データ型を指定するためにコンシューマーが **pTypeInfo** または *pclsid* メンバーのいずれかを設定すると、*CreateTable* では DB_E_BADTYPE が返されます。  
  
 コンシューマーは、DBCOLUMNDESC *dbcid* メンバーの *uName* 共用体の *pwszName* メンバーに列名を指定します。 列名は、Unicode 文字列として指定されます。 *dbcid* の *eKind* メンバーには、DBKIND_NAME を指定する必要があります。 **eKind** が無効、または *pwszName* が NULL、あるいは *pwszName* の値が有効な  *ID ではない場合、* CreateTable[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では DB_E_BADCOLUMNID が返されます。  
  
 列のすべてのプロパティは、テーブルに定義されたすべての列で使用できます。 プロパティ値の設定が競合していると、**CreateTable** では DB_S_ERRORSOCCURRED または DB_E_ERRORSOCCURRED が返されます。 無効な列プロパティを設定したことで  **テーブルの作成に失敗した場合、** CreateTable[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではエラーが返されます。  
  
 DBCOLUMNDESC の列プロパティは、次のように解釈されます。  
  
|プロパティ ID|説明|  
|-----------------|-----------------|  
|DBPROP_COL_AUTOINCREMENT|R/W: 読み取り/書き込み<br /><br /> 既定値 : VARIANT_FALSE&lt;br&gt;&lt;/br&gt;説明 : 作成された列に ID プロパティを設定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ID プロパティをテーブル内の 1 つの列に設定できます。 複数の列に対してプロパティを VARIANT_TRUE に設定すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーがサーバーにテーブルを作成しようとするとエラーが発生します。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の ID プロパティは、**integer** 型、**numeric** 型、および小数点以下桁数が 0 の **decimal** 型の場合のみ有効です。 その他のデータ型の列でプロパティを VARIANT_TRUE に設定すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーがサーバーにテーブルを作成しようとするとエラーが発生します。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、DBPROP_COL_AUTOINCREMENT と DBPROP_COL_NULLABLE の両方が VARIANT_TRUE で、DBPROP_COL_NULLABLE の*Dwoption*が DBPROPOPTIONS_REQUIRED ない場合に DB_S_ERRORSOCCURRED を返します。 DBPROP_COL_AUTOINCREMENT と DBPROP_COL_NULLABLE の両方が VARIANT_TRUE で、DBPROP_COL_NULLABLE の *dwOption* が DBPROPOPTIONS_REQUIRED の場合、DB_E_ERRORSOCCURRED が返されます。 列は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の ID プロパティで定義され、DBPROP_COL_NULLABLE の *dwStatus* メンバーが DBPROPSTATUS_CONFLICTING に設定されます。|  
|DBPROP_COL_DEFAULT|R/W: 読み取り/書き込み<br /><br /> 既定値: なし<br /><br /> 説明 : 列に対して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の DEFAULT 制約を作成します。<br /><br /> DBPROP の *vValue* メンバーには、さまざまなデータ型のいずれかを指定できます。 *vValue.vt* メンバーでは、列のデータ型と互換性のある型を指定する必要があります。 たとえば、DBTYPE_WSTR で定義された列の既定値として BSTR N/A を定義した場合は互換性の要件が満たされます。 DBTYPE_R8 として定義された列で同じ既定値を定義すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーがサーバー上にテーブルを作成しようとするとエラーが発生します。|  
|DBPROP_COL_DESCRIPTION|R/W: 読み取り/書き込み<br /><br /> 既定値: なし<br /><br /> 説明: DBPROP_COL_DESCRIPTION 列プロパティは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーによって実装されていません。<br /><br /> コンシューマーがこのプロパティ値の書き込みを試みた時点で、DBPROP 構造体の *dwStatus* メンバーは DBPROPSTATUS_NOTSUPPORTED を返します。<br /><br /> プロパティを設定しても、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーにとって致命的なエラーは発生しません。 他のすべてのパラメーター値が有効であれば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のテーブルが作成されます。|  
|DBPROP_COL_FIXEDLENGTH|R/W: 読み取り/書き込み<br /><br /> 既定値 : VARIANT_FALSE<br /><br /> 説明: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、DBCOLUMNDESC の*Wtype*メンバーを使用して列のデータ型を定義するときに、DBPROP_COL_FIXEDLENGTH を使用してデータ型マッピングを決定します。 詳細については、「 [ITableDefinition でのデータ型のマッピング](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md)」を参照してください。|  
|DBPROP_COL_NULLABLE|R/W: 読み取り/書き込み<br /><br /> 既定値: なし<br /><br /> 説明: テーブルを作成するときに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、プロパティが設定されている場合に列が null 値を受け入れるかどうかを示します。 このプロパティが設定されていないときは、列が値として NULL を許容するかどうかは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定のデータベース オプション ANSI_NULLS によって決まります。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、ISO に準拠しているプロバイダーです。 接続されたセッションでは、ISO 準拠の動作が行われます。 DBPROP_COL_NULLABLE を設定しないと、列は NULL 値を許容します。|  
|DBPROP_COL_PRIMARYKEY|R/W: 読み取り/書き込み<br /><br /> 既定値: VARIANT_FALSE 説明: VARIANT_TRUE すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーによって、PRIMARY KEY 制約を持つ列が作成されます。<br /><br /> 列プロパティとして定義するときは、1 つの列だけが制約を判断できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルを作成しようとすると、複数の列に対してプロパティ VARIANT_TRUE を設定すると、エラーが返されます。<br /><br /> 注: コンシューマーは **IIndexDefinition::CreateIndex** を使用して、2 つ以上の列に PRIMARY KEY 制約を作成できます。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、DBPROP_COL_PRIMARYKEY と DBPROP_COL_UNIQUE の両方が VARIANT_TRUE で、DBPROP_COL_UNIQUE の*Dwoption*が DBPROPOPTIONS_REQUIRED ない場合に DB_S_ERRORSOCCURRED を返します。<br /><br /> DBPROP_COL_PRIMARYKEY と DBPROP_COL_UNIQUE の両方が VARIANT_TRUE で、DBPROP_COL_UNIQUE の *dwOption* が DBPROPOPTIONS_REQUIRED の場合、DB_E_ERRORSOCCURRED が返されます。 列は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の ID プロパティで定義され、DBPROP_COL_PRIMARYKEY の *dwStatus* メンバーが DBPROPSTATUS_CONFLICTING に設定されます。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、DBPROP_COL_PRIMARYKEY と DBPROP_COL_NULLABLE が両方とも VARIANT_TRUE 場合にエラーを返します。<br /><br /> コンシューマーが無効な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型の列に PRIMARY KEY 制約を作成しようとすると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からエラーを返します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の **bit**、**text**、**ntext**、および **image** データ型で作成した列には、PRIMARY KEY 制約を定義できません。|  
|DBPROP_COL_UNIQUE|R/W: 読み取り/書き込み<br /><br /> 既定値 : VARIANT_FALSE&lt;br&gt;&lt;/br&gt;説明 : 列に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の UNIQUE 制約を適用します。<br /><br /> 列プロパティとして定義するときは、1 つの列だけに制約が適用されます。 コンシューマーは **IIndexDefinition::CreateIndex** を使用して、2 つ以上の列の組み合わせ値に UNIQUE 制約を適用できます。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、DBPROP_COL_PRIMARYKEY と DBPROP_COL_UNIQUE が両方とも VARIANT_TRUE で、 *Dwoption*が DBPROPOPTIONS_REQUIRED ない場合に DB_S_ERRORSOCCURRED を返します。<br /><br /> DBPROP_COL_PRIMARYKEY と DBPROP_COL_UNIQUE の両方が VARIANT_TRUE で、*dwOption* が DBPROPOPTIONS_REQUIRED の場合、DB_E_ERRORSOCCURRED が返されます。 列は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の ID プロパティで定義され、DBPROP_COL_PRIMARYKEY の *dwStatus* メンバーが DBPROPSTATUS_CONFLICTING に設定されます。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、DBPROP_COL_NULLABLE と DBPROP_COL_UNIQUE が両方とも VARIANT_TRUE で、 *Dwoption*が DBPROPOPTIONS_REQUIRED ない場合に DB_S_ERRORSOCCURRED を返します。<br /><br /> DBPROP_COL_NULLABLE と DBPROP_COL_UNIQUE の両方が VARIANT_TRUE で、*dwOption* が DBPROPOPTIONS_REQUIRED の場合、DB_E_ERRORSOCCURRED が返されます。 列は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の ID プロパティで定義され、DBPROP_COL_NULLABLE の *dwStatus* メンバーが DBPROPSTATUS_CONFLICTING に設定されます。<br /><br /> コンシューマーが無効な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型の列に対して UNIQUE 制約を作成しようとすると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からエラーを返します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の **bit** データ型で作成された列には、UNIQUE 制約を定義できません。|  
  
 コンシューマーが**Itabledefinition:: CreateTable**を呼び出すと、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、次のようにテーブルのプロパティを解釈します。  
  
|プロパティ ID|説明|  
|-----------------|-----------------|  
|DBPROP_TBL_TEMPTABLE|R/W: 読み取り/書き込み<br /><br /> 既定値: VARIANT_FALSE 説明: 既定では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、コンシューマーによってという名前のテーブルを作成します。 VARIANT_TRUE すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーによって、コンシューマーの一時テーブル名が生成されます。 コンシューマーは *CreateTable* の **pTableID** パラメーターに NULL を設定します。 *ppTableID* パラメーターには、有効なポインターを含める必要があります。|  
  
 コンシューマーが、正常に作成されたテーブルで行セットを開くように要求すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーによって、カーソルがサポートされている行セットが開かれます。 渡されるプロパティ セットで任意の行セット プロパティを指定できます。  
  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルを作成します。  
  
```  
// This CREATE TABLE statement shows the details of the table created by   
// the following example code.  
//  
// CREATE TABLE OrderDetails  
// (  
//    OrderID      int      NOT NULL  
//    ProductID   int      NOT NULL  
//    CONSTRAINT PK_OrderDetails  
//         PRIMARY KEY CLUSTERED (OrderID, ProductID),  
//    UnitPrice   money      NOT NULL,  
//    Quantity   int      NOT NULL,  
//    Discount   decimal(2,2)   NOT NULL  
//        DEFAULT 0  
// )  
//  
// The PRIMARY KEY constraint is created in an additional example.  
HRESULT CreateTable  
    (  
    ITableDefinition* pITableDefinition  
    )  
    {  
    DBID            dbidTable;  
    const ULONG     nCols = 5;  
    ULONG           nCol;  
    ULONG           nProp;  
    DBCOLUMNDESC    dbcoldesc[nCols];  
  
    HRESULT         hr;  
  
    // Set up column descriptions. First, set default property values for  
    //  the columns.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        dbcoldesc[nCol].pwszTypeName = NULL;  
        dbcoldesc[nCol].pTypeInfo = NULL;  
        dbcoldesc[nCol].rgPropertySets = new DBPROPSET;  
        dbcoldesc[nCol].pclsid = NULL;  
        dbcoldesc[nCol].cPropertySets = 1;  
        dbcoldesc[nCol].ulColumnSize = 0;  
        dbcoldesc[nCol].dbcid.eKind = DBKIND_NAME;  
        dbcoldesc[nCol].wType = DBTYPE_I4;  
        dbcoldesc[nCol].bPrecision = 0;  
        dbcoldesc[nCol].bScale = 0;  
  
        dbcoldesc[nCol].rgPropertySets[0].rgProperties =   
            new DBPROP[NCOLPROPS_MAX];  
        dbcoldesc[nCol].rgPropertySets[0].cProperties = NCOLPROPS_MAX;  
        dbcoldesc[nCol].rgPropertySets[0].guidPropertySet =  
            DBPROPSET_COLUMN;  
  
        for (nProp = 0; nProp < NCOLPROPS_MAX; nProp++)  
            {  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                dwOptions = DBPROPOPTIONS_REQUIRED;  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].colid  
                 = DB_NULLID;  
  
            VariantInit(  
                &(dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                    vValue));  
  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                vValue.vt = VT_BOOL;  
            }  
        }  
  
    // Set the column-specific information.  
    dbcoldesc[0].dbcid.uName.pwszName = L"OrderID";  
    dbcoldesc[0].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[0].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[0].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[1].dbcid.uName.pwszName = L"ProductID";  
    dbcoldesc[1].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[1].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[1].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[2].dbcid.uName.pwszName = L"UnitPrice";  
    dbcoldesc[2].wType = DBTYPE_CY;  
    dbcoldesc[2].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[2].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[2].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[3].dbcid.uName.pwszName = L"Quantity";  
    dbcoldesc[3].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[3].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[3].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[4].dbcid.uName.pwszName = L"Discount";  
    dbcoldesc[4].wType = DBTYPE_NUMERIC;  
    dbcoldesc[4].bPrecision = 2;  
    dbcoldesc[4].bScale = 2;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].dwPropertyID =   
        DBPROP_COL_DEFAULT;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].vValue.vt = VT_BSTR;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].vValue.bstrVal =  
        SysAllocString(L"0");  
    dbcoldesc[4].rgPropertySets[0].cProperties = 2;  
  
    // Set up the dbid for OrderDetails.  
    dbidTable.eKind = DBKIND_NAME;  
    dbidTable.uName.pwszName = L"OrderDetails";  
  
    if (FAILED(hr = pITableDefinition->CreateTable(NULL, &dbidTable,  
        nCols, dbcoldesc, NULL, 0, NULL, NULL, NULL)))  
        {  
        DumpError(pITableDefinition, IID_ITableDefinition);  
        goto SAFE_EXIT;  
        }  
  
SAFE_EXIT:  
    // Clean up dynamic allocation in the property sets.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        for (nProp = 0; nProp < NCOLPROPS_MAX; nProp++)  
            {  
            if (dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                vValue.vt == VT_BSTR)  
                {  
                SysFreeString(dbcoldesc[nCol].rgPropertySets[0].  
                    rgProperties[nProp].vValue.bstrVal);  
                }  
            }  
  
        delete [] dbcoldesc[nCol].rgPropertySets[0].rgProperties;  
        delete [] dbcoldesc[nCol].rgPropertySets;  
        }  
  
    return (hr);  
    }  
```  
  
## <a name="see-also"></a>参照  
 [テーブルとインデックス](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
  
