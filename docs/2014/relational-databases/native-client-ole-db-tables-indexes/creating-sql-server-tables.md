---
title: SQL Server テーブルの作成 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: e780a04f59bacba5063ac0bd6e9b7f3c74fd211a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046388"
---
# <a name="creating-sql-server-tables"></a>SQL Server テーブルの作成
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーが公開、 **itabledefinition::createtable**関数を作成するコンシューマー[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]テーブル。 コンシューマーを使用して、 **CreateTable**によって生成された一意の名前を持つコンシューマーという名前のパーマネント テーブル、および永続的なまたは一時テーブルを作成する、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー。  
  
 コンシューマーを呼び出すと**itabledefinition::createtable**DBPROP_TBL_TEMPTABLE プロパティの値が VARIANT_TRUE の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーがコンシューマー向けに一時テーブル名を生成します。 コンシューマーは、**CreateTable** メソッドの *pTableID* パラメーターに NULL を設定します。 によって生成された名前の一時テーブル、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーには表示されません、**テーブル**行セットからアクセスできるが、 **IOpenRowset**インターフェイス。  
  
 コンシューマーが内のテーブル名を指定すると、 *pwszName*のメンバー、 *uName*共用体の*pTableID*パラメーター、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー作成、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]その名前を持つテーブル。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルの名前付けに関する制約が適用されるので、そのテーブル名で、パーマネント テーブル、ローカル一時テーブルまたはグローバル一時テーブルのいずれであるかを示すことができます。 詳細については、「[CREATE TABLE](/sql/t-sql/statements/create-table-transact-sql)」を参照してください。 *ppTableID* パラメーターには NULL を指定できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは永続的または一時的なテーブルの名前を生成できます。 コンシューマーが設定した場合、 *pTableID*パラメーターを NULL とセット*ppTableID*有効な DBID を指す\*、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでの生成された名前を返します、テーブルに、 *pwszName*のメンバー、 *uName*の値によって示される、DBID の和集合*ppTableID*します。 一時的なを作成する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB プロバイダーの名前付きのテーブルでは、コンシューマーに設定で参照されるテーブルのプロパティの OLE DB テーブル プロパティ DBPROP_TBL_TEMPTABLE が含まれています、 *rgPropertySets*パラメーター。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーの名前付き一時テーブルはローカルです。  
  
 *pTableID* パラメーターの *eKind* メンバーに DBKIND_NAME を指定しないと、**CreateTable** では DB_E_BADTABLEID が返されます。  
  
## <a name="dbcolumndesc-usage"></a>DBCOLUMNDESC の使用方法  
 コンシューマーは、*pwszTypeName* メンバーまたは *wType* メンバーのいずれかを使用して、列のデータ型を指定できます。 コンシューマーでのデータ型を指定する場合*pwszTypeName*、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーの値を無視します*wType*します。  
  
 *pwszTypeName* メンバーを使用する場合、コンシューマーでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ型名を使用してデータ型が指定されます。 有効なデータ型名は、PROVIDER_TYPES スキーマの行セットの TYPE_NAME 列に返されるデータ型名です。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでの DBTYPE の OLE DB 列挙値のサブセットの認識、 *wType*メンバー。 詳細については、次を参照してください。 [ITableDefinition でのデータ型マッピング](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md)します。  
  
> [!NOTE]  
>  列データ型を指定するためにコンシューマーが *pTypeInfo* または *pclsid* メンバーのいずれかを設定すると、**CreateTable** では DB_E_BADTYPE が返されます。  
  
 コンシューマーは、DBCOLUMNDESC *dbcid* メンバーの *uName* 共用体の *pwszName* メンバーに列名を指定します。 列名は、Unicode 文字の文字列として指定されます。 *dbcid* の *eKind* メンバーには、DBKIND_NAME を指定する必要があります。 *eKind* が無効、または *pwszName* が NULL、あるいは *pwszName* の値が有効な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ID ではない場合、**CreateTable** では DB_E_BADCOLUMNID が返されます。  
  
 列のすべてのプロパティは、テーブルに定義されたすべての列で使用できます。 プロパティ値の設定が競合していると、**CreateTable** では DB_S_ERRORSOCCURRED または DB_E_ERRORSOCCURRED が返されます。 無効な列プロパティを設定したことで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルの作成に失敗した場合、**CreateTable** ではエラーが返されます。  
  
 DBCOLUMNDESC の列プロパティは、次のように解釈されます。  
  
|プロパティ ID|説明|  
|-----------------|-----------------|  
|DBPROP_COL_AUTOINCREMENT|R/W読み取り/書き込み<br /><br /> 既定値:VARIANT_FALSE の説明:作成された列の identity プロパティを設定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ID プロパティをテーブル内の 1 つの列に設定できます。 VARIANT_TRUE に 1 つの列には、エラーが生成されます。 複数のプロパティを設定時に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、サーバーで、テーブルを作成しようとしています。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の ID プロパティは、**integer** 型、**numeric** 型、および小数点以下桁数が 0 の **decimal** 型の場合のみ有効です。 VARIANT_TRUE に他のデータ型の列にプロパティを設定でエラー発生時に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、サーバーで、テーブルを作成しようとしています。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBPROP_COL_AUTOINCREMENT と DBPROP_COL_NULLABLE 両方が VARIANT_TRUE の場合は、Native Client OLE DB プロバイダーは DB_S_ERRORSOCCURRED を返します、 *dwOption* DBPROPOPTIONS_ のない DBPROP_COL_NULLABLE の必須。 DBPROP_COL_AUTOINCREMENT と DBPROP_COL_NULLABLE の両方が VARIANT_TRUE で、DBPROP_COL_NULLABLE の *dwOption* が DBPROPOPTIONS_REQUIRED の場合、DB_E_ERRORSOCCURRED が返されます。 列は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の ID プロパティで定義され、DBPROP_COL_NULLABLE の *dwStatus* メンバーが DBPROPSTATUS_CONFLICTING に設定されます。|  
|DBPROP_COL_DEFAULT|R/W読み取り/書き込み<br /><br /> 既定値:なし<br /><br /> 説明:作成、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]列の既定の制約。<br /><br /> DBPROP の *vValue* メンバーには、さまざまなデータ型のいずれかを指定できます。 *vValue.vt* メンバーでは、列のデータ型と互換性のある型を指定する必要があります。 たとえば、DBTYPE_WSTR で定義された列の既定値として BSTR N/A を定義した場合は互換性の要件が満たされます。 DBTYPE_R8 には、エラーが生成されます。 定義された列に同じ既定値を定義するときに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、サーバーで、テーブルを作成しようとしています。|  
|DBPROP_COL_DESCRIPTION|R/W読み取り/書き込み<br /><br /> 既定値:なし<br /><br /> 説明:によって DBPROP_COL_DESCRIPTION 列プロパティが実装されていません、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー。<br /><br /> コンシューマーがこのプロパティ値の書き込みを試みた時点で、DBPROP 構造体の *dwStatus* メンバーは DBPROPSTATUS_NOTSUPPORTED を返します。<br /><br /> プロパティの設定での致命的なエラーが構成されません、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー。 他のすべてのパラメーター値が有効であれば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のテーブルが作成されます。|  
|DBPROP_COL_FIXEDLENGTH|R/W読み取り/書き込み<br /><br /> 既定値:VARIANT_FALSE<br /><br /> 説明:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは DBPROP_COL_FIXEDLENGTH を使用して、データ型のマッピングを使用して、コンシューマーが列のデータ型を定義するのかを判断、 *wType* DBCOLUMNDESC のメンバー。 詳細については、次を参照してください。 [ITableDefinition でのデータ型マッピング](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md)します。|  
|DBPROP_COL_NULLABLE|R/W読み取り/書き込み<br /><br /> 既定値:なし<br /><br /> 説明:テーブルを作成するときに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでは、プロパティが設定されている場合に、列が null 値を受け入れるかどうかを示します。 このプロパティが設定されていないときは、列が値として NULL を許容するかどうかは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定のデータベース オプション ANSI_NULLS によって決まります。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、ISO 準拠のプロバイダー。 接続されたセッションでは、ISO 準拠の動作が行われます。 DBPROP_COL_NULLABLE を設定しないと、列は NULL 値を許容します。|  
|DBPROP_COL_PRIMARYKEY|R/W読み取り/書き込み<br /><br /> 既定値:VARIANT_FALSE の説明:ときに、VARIANT_TRUE、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、PRIMARY KEY 制約で、列を作成します。<br /><br /> 列プロパティとして定義するときは、1 つの列だけが制約を判断できます。 1 つの列には、エラーが返されます。 複数のプロパティを VARIANT_TRUE を設定するときに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーが、作成しようとしています。、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]テーブル。<br /><br /> 注:コンシューマーが使用できる**iindexdefinition::createindex**を 2 つ以上の列に PRIMARY KEY 制約を作成します。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBPROP_COL_PRIMARYKEY と DBPROP_COL_UNIQUE 両方が VARIANT_TRUE の場合は、Native Client OLE DB プロバイダーは DB_S_ERRORSOCCURRED を返します、 *dwOption* DBPROPOPTIONS_REQUIRED でない DBPROP_COL_UNIQUE の。<br /><br /> DBPROP_COL_PRIMARYKEY と DBPROP_COL_UNIQUE の両方が VARIANT_TRUE で、DBPROP_COL_UNIQUE の *dwOption* が DBPROPOPTIONS_REQUIRED の場合、DB_E_ERRORSOCCURRED が返されます。 列は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の ID プロパティで定義され、DBPROP_COL_PRIMARYKEY の *dwStatus* メンバーが DBPROPSTATUS_CONFLICTING に設定されます。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、DBPROP_COL_PRIMARYKEY と DBPROP_COL_NULLABLE 両方が VARIANT_TRUE の場合にエラーを返します。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーからのエラーを返します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、コンシューマーが無効な列に PRIMARY KEY 制約を作成しようとしたときに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データ型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の **bit**、**text**、**ntext**、および **image** データ型で作成した列には、PRIMARY KEY 制約を定義できません。|  
|DBPROP_COL_UNIQUE|R/W読み取り/書き込み<br /><br /> 既定値:VARIANT_FALSE の説明:適用対象を[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]列に UNIQUE 制約。<br /><br /> 列プロパティとして定義するときは、1 つの列だけに制約が適用されます。 コンシューマーは **IIndexDefinition::CreateIndex** を使用して、2 つ以上の列の組み合わせ値に UNIQUE 制約を適用できます。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBPROP_COL_PRIMARYKEY と DBPROP_COL_UNIQUE 両方が VARIANT_TRUE の場合は、Native Client OLE DB プロバイダーは DB_S_ERRORSOCCURRED を返しますと*dwOption* DBPROPOPTIONS_REQUIRED ではありません。<br /><br /> DBPROP_COL_PRIMARYKEY と DBPROP_COL_UNIQUE の両方が VARIANT_TRUE で、*dwOption* が DBPROPOPTIONS_REQUIRED の場合、DB_E_ERRORSOCCURRED が返されます。 列は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の ID プロパティで定義され、DBPROP_COL_PRIMARYKEY の *dwStatus* メンバーが DBPROPSTATUS_CONFLICTING に設定されます。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBPROP_COL_NULLABLE と DBPROP_COL_UNIQUE 両方が VARIANT_TRUE の場合は、Native Client OLE DB プロバイダーは DB_S_ERRORSOCCURRED を返しますと*dwOption* DBPROPOPTIONS_REQUIRED ではありません。<br /><br /> DBPROP_COL_NULLABLE と DBPROP_COL_UNIQUE の両方が VARIANT_TRUE で、*dwOption* が DBPROPOPTIONS_REQUIRED の場合、DB_E_ERRORSOCCURRED が返されます。 列は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の ID プロパティで定義され、DBPROP_COL_NULLABLE の *dwStatus* メンバーが DBPROPSTATUS_CONFLICTING に設定されます。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーからのエラーを返します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、コンシューマーが無効な列に UNIQUE 制約を作成しようとしたときに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データ型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の **bit** データ型で作成された列には、UNIQUE 制約を定義できません。|  
  
 コンシューマーを呼び出すと**itabledefinition::createtable**、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、テーブルのプロパティを次のように解釈します。  
  
|プロパティ ID|説明|  
|-----------------|-----------------|  
|DBPROP_TBL_TEMPTABLE|R/W読み取り/書き込み<br /><br /> 既定値:VARIANT_FALSE の説明:既定で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーがコンシューマーによってという名前のテーブルを作成します。 ときに、VARIANT_TRUE、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーがコンシューマー向けに一時テーブル名を生成します。 コンシューマーは **CreateTable** の *pTableID* パラメーターに NULL を設定します。 *ppTableID* パラメーターには、有効なポインターを含める必要があります。|  
  
 コンシューマーが行セットが正常に作成されたテーブルで開かれることを要求した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、カーソルでサポートされている行セットを開きます。 渡されるプロパティ セットで任意の行セット プロパティを指定できます。  
  
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
  
  
