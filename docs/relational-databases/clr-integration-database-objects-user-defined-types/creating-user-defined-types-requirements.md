---
title: ユーザー定義型の要件 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- UDTs [CLR integration], requirements
- serialization
- Native serialization format [CLR integration]
- attributes [CLR integration]
- XML serialization [CLR integration]
- user-defined types [CLR integration], requirements
- user-defined serialization [CLR integration]
- user-defined types [CLR integration], Native serialization
- UDTs [CLR integration], Native serialization
ms.assetid: bedc3372-50eb-40f2-bcf2-d6db6a63b7e6
author: rothja
ms.author: jroth
ms.openlocfilehash: 7fc3da1474546f0719af20c52f44248baa8ce5da
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028261"
---
# <a name="creating-user-defined-types---requirements"></a>ユーザー定義型の作成 - 要件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  ユーザー定義型 (UDT) をインストールを作成するときに、いくつかの重要な設計上の決定を行う必要があります[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 ほとんどの場合は、UDT を構造体として作成することをお勧めしますが、クラスとして作成することもできます。 UDT の定義は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に登録する UDT を作成するための仕様に準拠している必要があります。  
  
## <a name="requirements-for-implementing-udts"></a>UDT の実装要件  
 UDT を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で実行するには、UDT の定義に次の要件を実装する必要があります。  
  
 UDT を指定する必要があります、 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**します。 使用、 **System.SerializableAttribute**は省略可能なが推奨されます。  
  
-   UDT を実装する必要があります、 **System.Data.SqlTypes.INullable**クラスまたは構造体を作成、パブリック インターフェイス**静的**(**Shared**で[!INCLUDE[msCoName](../../includes/msconame-md.md)]VisualBasic の場合) **Null**メソッド。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、既定で NULL 値に対応します。 この作業は、UDT で実行されるコードが NULL 値を認識するために必要です。  
  
-   UDT は、パブリックなを含める必要があります**静的**(または**Shared**)**解析**、解析をサポートするメソッドとパブリック**ToString**メソッドオブジェクトの文字列形式に変換します。  
  
-   ユーザー定義のシリアル化形式を持つ UDT を実装する必要があります、 **System.Data.IBinarySerialize**インターフェイスを提供する**読み取り**と**書き込み**メソッド。  
  
-   UDT を実装する必要があります**System.Xml.Serialization.IXmlSerializable**、または xml シリアル化可能なまたはで修飾された型のすべてのパブリック フィールドおよびプロパティがあります、 **XmlIgnore**属性の場合標準のシリアル化をオーバーライドすることが必要です。  
  
-   UDT オブジェクトのシリアル化は 1 つだけ存在する必要があります。 シリアル化ルーチンまたはシリアル化解除ルーチンでは、特定のオブジェクトの表現が複数認識されると検証が失敗します。  
  
-   **SqlUserDefinedTypeAttribute.IsByteOrdered** must be **true** to compare data in byte order. IComparable インターフェイスが実装されていない場合と**SqlUserDefinedTypeAttribute.IsByteOrdered**は**false**バイト順の比較は失敗します。  
  
-   クラスで定義する UDT には、引数を受け取らないバプリック コンストラクターを含める必要があります。 必要に応じて、オーバーロードのクラス コンストラクターを追加作成できます。  
  
-   UDT では、データ要素をパブリック フィールドまたはプロパティ プロシージャとして公開する必要があります。  
  
-   パブリック名は、128 文字より長くすることはできずに準拠している必要があります、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で定義されている、識別子の名前付け規則[データベース識別子](../../relational-databases/databases/database-identifiers.md)します。  
  
-   **sql_variant**列は、UDT のインスタンスを含めることはできません。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] の型システムでは UDT 間の継承階層に対応していないので、継承されたメンバーに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からアクセスすることはできません。 ただし、型のマネージド コード実装では、継承を使用してクラスを構造化したり、そのクラスのメソッドを呼び出すことができます。  
  
-   クラス コンストラクター以外のメンバーはオーバーロードできません。 オーバーロード メソッドを作成した場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にアセンブリを登録したり、型を作成するときにはエラーは発生しません。 オーバーロード メソッドが検出されるのは、型の作成時ではなく実行時です。 オーバーロード メソッドは、呼び出されない限りクラス内に存在することができます。 エラーは、オーバーロード メソッドを呼び出した時点で発生します。  
  
-   すべて**静的**(または**Shared**) メンバーは定数として宣言されたまたは読み取り専用である必要があります。 静的メンバーを変更可能にすることはできません。  
  
-   場合、 **SqlUserDefinedTypeAttribute.MaxByteSize**フィールドが-1 に設定されている、シリアル化された UDT はラージ オブジェクト (LOB) サイズの上限 (現在 2 GB)、拡大することができます。 UDT のサイズがで指定された値を超えることはできません、 **MaxByteSized**フィールド。  
  
> [!NOTE]  
>  実装できます必要に応じてそれを使用しないサーバーによって比較を実行するためですが、 **System.IComparable**インターフェイスで、1 つのメソッドを公開するには、 **CompareTo**します。 このインターフェイスは、クライアント側で UDT 値を正確に比較したり並べ替える場合に使用します。  
  
## <a name="native-serialization"></a>ネイティブ シリアル化  
 UDT に適したシリアル化属性は、作成する UDT の種類によって異なります。 **ネイティブ**シリアル化形式ができるようにする非常に単純な構造を利用して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]効率的なネイティブ形式は、UDT をディスクに保存します。 **ネイティブ**形式は、UDT は単純であり、次の種類のフィールドのみを含む場合に推奨されます。  
  
 **bool**、**バイト**、 **sbyte**、**短い**、 **ushort**、 **int**、 **uint**、**長い**、 **ulong**、 **float**、**二重**、 **SqlByte**、**SqlInt16**、 **SqlInt32**、 **SqlInt64**、 **SqlDateTime**、 **SqlSingle**、 **SqlDouble**、 **SqlMoney**、 **SqlBoolean**  
  
 上記の型のフィールドの値型で構成されているは候補として適して**ネイティブ**書式設定など**構造体**Visual C# では、(または**構造**で呼ばれています、Visual Basic の場合)。 UDT を指定するなど、**ネイティブ**シリアル化形式で指定したもう 1 つの UDT のフィールドを含めることができます、**ネイティブ**形式。 指定する必要があるかどうか、UDT の定義がより複雑な上記の一覧にないデータ型が含まれています、 **UserDefined**シリアル化形式します。  
  
 **ネイティブ**形式は、次の要件。  
  
-   型の値を指定する必要があります**Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.MaxByteSize**します。  
  
-   すべてのフィールドがシリアル化可能である必要があります。  
  
-   **された System.Runtime.InteropServices.StructLayoutAttribute**として指定する必要があります**StructLayout.LayoutKindSequential**クラスと構造体ではない、UDT が定義されている場合。 この属性は、データ フィールドの物理レイアウトを制御し、メンバーを出現順にレイアウトするために使用します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、この属性を使用して複数の値を持つ UDT のフィールド順序を決定します。  
  
 定義された UDT の例について**ネイティブ**シリアル化、Point udt の属性を参照してください。 [Coding User-Defined 型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)します。  
  
## <a name="userdefined-serialization"></a>ユーザー定義シリアル化  
 **UserDefined**形式を指定、 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**属性には、開発者の完全なバイナリ形式を制御します。 指定するときに、**形式**属性としてプロパティ**UserDefined**コードでは、次を行う必要があります。  
  
-   省略可能な指定**IsByteOrdered**属性プロパティ。 既定値は **false**です。  
  
-   指定、 **MaxByteSize**のプロパティ、 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**します。  
  
-   実装するコードを記述**読み取り**と**書き込み**メソッドの実装によって、udt、 **System.Data.Sql.IBinarySerialize**インターフェイス。  
  
 定義された UDT の例について**UserDefined**シリアル化、Currency UDT」を参照してください。 [Coding User-Defined 型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)します。  
  
> [!NOTE]  
>  UDT フィールドをインデックス化するには、ネイティブ シリアル化を使用するか、UDT フィールドを保存する必要があります。  
  
## <a name="serialization-attributes"></a>シリアル化属性  
 UDT のストレージ表現を構築し、クライアントに UDT を値として転送するためにシリアル化を使用する方法は、属性で決まります。 指定する必要があります、 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** UDT を作成するときにします。 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**属性クラスは、UDT、UDT のストレージを指定を表します。 必要に応じて指定することができます、 **Serializable**属性が[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]これは必要ありません。  
  
 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**は次のプロパティがあります。  
  
 **形式**  
 シリアル化の形式を指定します**ネイティブ**または**UserDefined**UDT のデータ型に応じて、します。  
  
 **IsByteOrdered**  
 A**ブール**を決定する値か[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]UDT のバイナリの比較を実行します。  
  
 **IsFixedLength**  
 この UDT のすべてのインスタンスの長さが同じであるかどうかを示します。  
  
 **MaxByteSize**  
 インスタンスのバイト単位の最大サイズ。 指定する必要があります**MaxByteSize**で、 **UserDefined**シリアル化形式。 ユーザー定義シリアル化が指定すると、UDT の**MaxByteSize**ユーザーが定義されている、UDT のシリアル化された形式での合計サイズを示します。 値**MaxByteSize** 1 ~ 8000 の範囲内で指定または UDT が (合計サイズは、LOB の最大サイズを超えることはできません) 8000 バイトを超えていることを示す-1 に設定する必要があります。 10 文字の文字列のプロパティを持つ UDT を検討してください (**System.Char**)。 BinaryWriter を使用して UDT をシリアル化されるとき、シリアル化された文字列の合計サイズは 22 バイト数を示します。Unicode utf-16 の文字ごとに 2 バイトでは、バイトのバイナリ ストリームにシリアル化から生じるオーバーヘッド文字および 2 のコントロールの最大数を掛けます。 そのための値を決定するときに**MaxByteSize**、シリアル化される UDT の合計サイズを考慮する必要があります: バイナリ形式でシリアル化データと、シリアル化によるオーバーヘッドのサイズ。  
  
 **ValidationMethodName**  
 UDT のインスタンスの検証に使用するメソッドの名前。  
  
### <a name="setting-isbyteordered"></a>IsByteOrdered の設定  
 ときに、 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.IsByteOrdered**プロパティに設定されて**true**、実際にシリアル化されたバイナリ データを使用できることを保証するセマンティック情報の順序付けします。 したがって、バイト順の UDT オブジェクトの各インスタンスは、シリアル化された表現を 1 つだけ持つことができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でシリアル化されたバイト列の比較操作を行うときは、その比較結果がマネージド コードで同じ比較操作を実行した場合と同じになる必要があります。 次の機能もサポートされているときに**IsByteOrdered**に設定されている**true**:  
  
-   この型の列にインデックスを作成する機能。  
  
-   この型の列に CHECK 制約と UNIQUE 制約だけでなく主キーと外部キーを作成する機能。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] の ORDER BY 句、GROUP BY 句、および PARTITION BY 句を使用する機能。 これらの句を使用した場合、順序の決定には型のバイナリ表現が使用されます。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで比較演算子を使用する機能。  
  
-   この型の計算列を保存する機能。  
  
 なお両方、**ネイティブ**と**UserDefined**シリアル化形式は次の比較演算子をサポートと**IsByteOrdered**に設定されている**は true。** :  
  
-   等しい (=)  
  
-   等しくない (!=)  
  
-   より大きい (>)  
  
-   より小さい (\<)  
  
-   以上 (> =)  
  
-   以下 (<=)  
  
### <a name="implementing-nullability"></a>NULL 値の許容属性の実装  
 アセンブリの属性を正しく指定することに加えて、クラスで NULL 値の許容属性をサポートする必要があります。 読み込まれる Udt[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]は null に対応して、UDT に null 値を認識させるためには、クラスを実装する必要がありますが、 **INullable**インターフェイス。 UDT に null 値許容属性を実装する方法の例と詳細については、次を参照してください。 [Coding User-Defined 型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)します。  
  
### <a name="string-conversions"></a>文字列の変換  
 文字列変換との間の UDT をサポートするために指定する必要があります、**解析**メソッドと**ToString**クラスのメソッド。 **解析**メソッドにより UDT に変換する文字列。 として宣言する必要がある必要があります**静的**(または**Shared** Visual basic)、型のパラメーターを受け取ると**System.Data.SqlTypes.SqlString**します。 実装する方法の例と詳細について、**解析**と**ToString**メソッドを参照してください[Coding User-Defined 型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)します。  
  
## <a name="xml-serialization"></a>XML シリアル化  
 Udt との間の変換をサポートする必要があります、 **xml** XML シリアル化のコントラクトに準拠することで、データ型。 **System.Xml.Serialization**名前空間には XML 形式のドキュメントまたはストリームにオブジェクトをシリアル化に使用されるクラスが含まれています。 実装することもできます**xml**を使用してシリアル化、 **IXmlSerializable**インターフェイスで、XML シリアル化および逆シリアル化のカスタム書式を提供します。  
  
 UDT からの明示的な変換を実行するだけでなく**xml**、XML シリアル化では、することができます。  
  
-   使用**Xquery** UDT のインスタンスへの変換後の値を**xml**データ型。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のネイティブ XML Web サービスにより、パラメーター化クエリと Web メソッドに UDT を使用できます。  
  
-   UDT を使用して、XML データの一括読み込みを受け取ることができます。  
  
-   UDT 列を含むテーブルが格納されたデータセットをシリアル化できます。  
  
 UDT は、FOR XML クエリではシリアル化されません。 Udt の XML シリアル化を表示する FOR XML クエリを実行する各 UDT 列を明示的に変換、 **xml** SELECT ステートメントでのデータ型。 列を明示的に変換できます**varbinary**、 **varchar**、または**nvarchar**します。  
  
## <a name="see-also"></a>参照  
 [ユーザー定義型を作成する](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
