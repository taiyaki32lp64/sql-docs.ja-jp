---
title: SQL Server XML 一括読み込みオブジェクトモデル (SQLXML)
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- bulk load [SQLXML], object model
- ErrorLogFile property
- SGDropTables property
- SGUseID property
- KeepNulls property
- ConnectionCommand property
- SchemaGen property
- XMLFragment property
- SQLXMLBulkLoad object
- ForceTableLock property
- CheckConstraints property
- BulkLoad property
- TempFilePath property
- IgnoreDuplicateKeys property
- Transaction property
- KeepIdentity property
- ConnectionString property
- FireTriggers property
- Execute method
- XML Bulk Load [SQLXML], object model
ms.assetid: a9efbbde-ed2b-4929-acc1-261acaaed19d
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a71a5c756953c6b70e51422b5c1032b117eb7785
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75246710"
---
# <a name="sql-server-xml-bulk-load-object-model-sqlxml-40"></a>SQL Server XML 一括読み込みオブジェクト モデル (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] XML 一括読み込みオブジェクトモデルは、SQLXMLBulkLoad オブジェクトで構成されています。 このオブジェクトでは、次のメソッドとプロパティがサポートされます。  
  
## <a name="methods"></a>メソッド  
 Execute  
 パラメーターとして渡されるスキーマ ファイルとデータ ファイル (またはストリーム) を使用して、データの一括読み込みを行います。  
  
## <a name="properties"></a>プロパティ  
 BulkLoad  
 一括読み込みを実行するかどうかを指定します。 このプロパティは、スキーマのみを生成する場合に便利です (以降の SchemaGen、SGDropTables、SGUseID の各プロパティを参照してください)。一括読み込みは実行されません。 このプロパティはブール値をとります。 このプロパティを TRUE に設定すると、XML 一括読み込みが行われます。 FALSE に設定すると、XML 一括読み込みは行われません。  
  
 既定値は TRUE です。  
  
 CheckConstraints  
 一括読み込みで列にデータを挿入するときに、列に指定されている制約 (列間の主キー/外部キーのリレーションシップによる制約など) をチェックするかどうかを指定します。 このプロパティはブール値をとります。  
  
 このプロパティを TRUE に設定すると、XML 一括読み込みで挿入される値ごとに制約がチェックされ、制約違反があるとエラーが発生します。  
  
> [!NOTE]  
>  このプロパティを FALSE のままにしておくには、対象テーブルに対する**ALTER TABLE**権限が必要です。 詳細については、「[ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)」を参照してください。  
  
 既定値は FALSE です。 FALSE に設定した場合、XML 一括読み込みでは挿入操作中、制約が無視されます。 現在の実装では、マッピング スキーマの主キーと外部キーのリレーションシップの順序でテーブルを定義する必要があります。 つまり、主キーが設定されているテーブルは、外部キーが設定されている対応テーブルよりも前に定義する必要があります。このように定義しない場合、XML 一括読み込みは失敗します。  
  
 ID 配布が実行されている場合は、このオプションは適用されず、制約チェックはオンのままになる点に注意してください。 これに該当するのは、親が ID フィールドで、その値が生成時に子に指定されるリレーションシップが定義されており、かつ `KeepIdentity=False` の場合です。  
  
 ConnectionCommand  
 XML 一括読み込みで使用する既存の接続オブジェクト (ADO や ICommand コマンドオブジェクトなど) を識別します。 ConnectionString プロパティを使用して接続文字列を指定する代わりに、ConnectionCommand プロパティを使用できます。 ConnectionCommand を使用する場合は、Transaction プロパティを TRUE に設定する必要があります。  
  
 ConnectionString プロパティと ConnectionCommand プロパティの両方を使用する場合、XML 一括読み込みでは最後に指定したプロパティが使用されます。  
  
 既定値は NULL です。  
  
 ConnectionString  
 データベース インスタンスへの接続の確立に必要な情報を提供する OLE DB 接続文字列を指定します。 ConnectionString プロパティと ConnectionCommand プロパティの両方を使用する場合、XML 一括読み込みでは最後に指定したプロパティが使用されます。  
  
 既定値は NULL です。  
  
 ErrorLogFile  
 XML 一括読み込みでエラーとメッセージを記録するログ ファイル名を指定します。 既定値は空文字列で、この場合ログは記録されません。  
  
 FireTriggers  
 一括読み込み操作中に、対象テーブルに定義されているトリガーを起動するかどうかを指定します。 既定値は FALSE です。  
  
 TRUE に設定した場合は、挿入操作中、トリガーが通常どおり起動されます。  
  
> [!NOTE]  
>  このプロパティを FALSE のままにしておくには、対象テーブルに対する**ALTER TABLE**権限が必要です。 詳細については、「[ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)」を参照してください。  
  
 ID 配布が実行されている場合は、このオプションは適用されず、トリガーはオンのままになる点に注意してください。 これに該当するのは、親が ID フィールドで、その値が生成時に子に指定されるリレーションシップが定義されており、かつ `KeepIdentity=False` の場合です。  
  
 ForceTableLock  
 XML 一括読み込みでデータをコピーするテーブルを、一括読み込み中にロックするかどうかを指定します。 このプロパティはブール値をとります。 このプロパティを TRUE に設定すると、XML 一括読み込み中、テーブルはロックされます。 FALSE に設定すると、XML 一括読み込みでテーブルにレコードが挿入されるときに、毎回テーブルがロックされます。  
  
 既定値は FALSE です。  
  
 IgnoreDuplicateKeys  
 キー列に挿入される値が重複している場合の動作を指定します。 このプロパティが TRUE に設定されている状態で、キー列に挿入されるレコードの値が重複している場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ではそのレコードは挿入されません。 しかし、その後に続くレコードは挿入されるので、一括読み込み操作は失敗しません。 このプロパティを FALSE に設定すると、キー列に挿入される値が重複している場合、一括読み込みは失敗します。  
  
 IgnoreDuplicateKeys プロパティが TRUE に設定されている場合、テーブルに挿入されたすべてのレコードに対して COMMIT ステートメントが発行されます。 このため、パフォーマンスが低下します。 トランザクションの動作はファイルを使用して実装されるので、プロパティは、Transaction プロパティが FALSE に設定されている場合にのみ TRUE に設定できます。  
  
 既定値は FALSE です。  
  
 KeepIdentity  
 ソース ファイルにある ID 型列値の取り扱い方法を指定します。 このプロパティはブール値をとります。 このプロパティを TRUE に設定すると、XML 一括読み込みでは、ソース ファイルで指定されている値が ID 列に割り当てられます。 このプロパティを FALSE に設定すると、一括読み込み操作では、ソースで指定されている ID 列値は無視されます。 この場合、ID 列値は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] によって割り当てられます。  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で生成される値が ID 列に格納される場合に、一括読み込みでこの列を参照する外部キー列も読み込まれる場合、一括読み込みではこれらの ID 値が外部キー列に適切に割り当てられます。  
  
 このプロパティの値は、一括読み込みの対象となるすべての列に適用されます。 既定値は TRUE です。  
  
> [!NOTE]  
>  このプロパティを TRUE のままにするには、対象テーブルに対する**ALTER TABLE**権限が必要です。 この権限がない場合は、値を FALSE に設定する必要があります。 詳細については、「[ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)」を参照してください。  
  
 KeepNulls  
 列に対応する属性または子要素が XML ドキュメントに見つからない場合に、その列に使用する値を指定します。 このプロパティはブール値をとります。 このプロパティを TRUE に設定すると、XML 一括読み込みでは列に NULL 値が割り当てられます。 サーバーで列の既定値が設定されている場合でも、その既定値は割り当てられません。 このプロパティの値は、一括読み込みの対象となるすべての列に適用されます。  
  
 既定値は FALSE です。  
  
 SchemaGen  
 一括読み込み操作の前に、必要なテーブルを作成するかどうかを指定します。 このプロパティはブール値をとります。 このプロパティを TRUE に設定すると、マッピング スキーマで指定されているテーブルが作成されます (データベースは存在している必要があります)。 データベース内に1つ以上のテーブルが既に存在する場合、SGDropTables プロパティは、これらの既存のテーブルを削除して再作成するかどうかを決定します。  
  
 SchemaGen プロパティの既定値は FALSE です。 SchemaGen では、新しく作成されたテーブルに PRIMARY KEY 制約は作成されません。 ただし、SchemaGen では、マッピングスキーマで**sql: relationship**と**sql: キーフィールド**の注釈が一致しているかどうか、およびキーフィールドが1つの列で構成されている場合に、データベースに外部キー制約が作成されます。  
  
 SchemaGen プロパティを TRUE に設定すると、XML 一括読み込みでは次のことが行われることに注意してください。  
  
-   要素名と属性名から、必要なテーブルを作成します。 このため、スキーマでは要素と属性に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の予約語を使用しないでください。  
  
-   [Xml データ型](../../../t-sql/xml/xml-transact-sql.md)の形式で、 [sql: overflow フィールド](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md)を使用して指定された任意の列のオーバーフローデータを返します。  
  
 SGDropTables  
 既存のテーブルを削除し、再作成するかどうかを指定します。 このプロパティは、SchemaGen プロパティが TRUE に設定されている場合に使用します。 SGDropTables が FALSE の場合は、既存のテーブルが保持されます。 このプロパティが TRUE の場合、既存のテーブルは削除され再作成されます。  
  
 既定値は FALSE です。  
  
 SGUseID  
 テーブルの作成時に PRIMARY KEY 制約を作成するときに、 **id**型として識別されるマッピングスキーマの属性を使用できるかどうかを指定します。 このプロパティは、SchemaGen プロパティが TRUE に設定されている場合に使用します。 SGUseID が TRUE の場合、SchemaGen ユーティリティは、 **dt: type = "id"** が主キー列として指定されている属性を使用し、テーブルの作成時に適切な primary key 制約を追加します。  
  
 既定値は FALSE です。  
  
 TempFilePath  
 XML 一括読み込みで、読み込んだデータ用の一時ファイルを作成するファイル パスを指定します。 (このプロパティは、Transaction プロパティが TRUE に設定されている場合にのみ役立ちます)。XML 一括読み込みに使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]するアカウントにこのパスへのアクセス権があることを確認する必要があります。 このプロパティを設定しない場合、XML 一括読み込みでは、TEMP 環境変数で指定された場所に一時ファイルが格納されます。  
  
 トランザクション  
 一括読み込みをトランザクションとして実行するよう指定します。この場合、一括読み込みが失敗するとロールバックが実行されます。 このプロパティはブール値をとります。 このプロパティを TRUE に設定すると、一括読み込みはトランザクション コンテキストで実行されます。 TempFilePath プロパティは、Transaction が TRUE に設定されている場合にのみ役立ちます。  
  
> [!NOTE]  
>  バイナリデータ (たとえば、bin. hex, bin. base64 XML データ型) をバイナリ、image [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データ型に読み込んでいる場合は、Transaction プロパティを FALSE に設定する必要があります。  
  
 既定値は FALSE です。  
  
 XMLFragment  
 ソース データが XML フラグメントであるかどうかを指定します。 XML フラグメントとは、最上位 (ルート) 要素のない、単一の XML ドキュメントです。 このプロパティはブール値をとります。 ソース ファイルに XML フラグメントが含まれている場合は、このプロパティを TRUE に設定する必要があります。  
  
 既定値は FALSE です。  
  
  
