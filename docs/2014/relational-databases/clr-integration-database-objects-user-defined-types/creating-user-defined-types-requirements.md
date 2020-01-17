---
title: ユーザー定義型の要件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 63f297f1a2a3ae738e00e37acf381b830ced9e7b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62919660"
---
# <a name="user-defined-type-requirements"></a>ユーザー定義型の要件
  ユーザー定義型 (UDT) をインストールを作成するときに、いくつかの重要な設計上の決定を行う必要があります[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 ほとんどの場合は、UDT を構造体として作成することをお勧めしますが、クラスとして作成することもできます。 UDT の定義は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に登録する UDT を作成するための仕様に準拠している必要があります。  
  
## <a name="requirements-for-implementing-udts"></a>UDT の実装要件  
 UDT を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で実行するには、UDT の定義に次の要件を実装する必要があります。  
  
 UDT には、`Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` を指定する必要があります。 `System.SerializableAttribute` の使用は任意ですが、使用することをお勧めします。  
  
-   UDT のクラスまたは構造体には、public `System.Data.SqlTypes.INullable` ([!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic では `static`) `Shared` メソッドを作成して `Null` インターフェイスを実装する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、既定で NULL 値に対応します。 この作業は、UDT で実行されるコードが NULL 値を認識するために必要です。  
  
-   UDT には、オブジェクトの文字列表現からの変換をサポートする public `static` (または `Shared`) `Parse` メソッドと、オブジェクトを文字列表現に変換するための public `ToString` メソッドを含める必要があります。  
  
-   ユーザー定義シリアル化形式を指定した UDT には、`System.Data.IBinarySerialize` インターフェイスを実装して `Read` メソッドと `Write` メソッドを提供する必要があります。  
  
-   標準のシリアル化をオーバーライドする必要がある場合は、UDT に `System.Xml.Serialization.IXmlSerializable` を実装するか、すべてのパブリック フィールドとパブリック プロパティを、XML シリアル化可能な型または `XmlIgnore` で修飾された型にする必要があります。  
  
-   UDT オブジェクトのシリアル化は 1 つだけ存在する必要があります。 シリアル化ルーチンまたはシリアル化解除ルーチンでは、特定のオブジェクトの表現が複数認識されると検証が失敗します。  
  
-   データをバイト順で比較するには、`SqlUserDefinedTypeAttribute.IsByteOrdered` を `true` にする必要があります。 IComparable インターフェイスが実装されておらず、`SqlUserDefinedTypeAttribute.IsByteOrdered` が `false` の場合、バイト順での比較は失敗します。  
  
-   クラスで定義する UDT には、引数を受け取らないバプリック コンストラクターを含める必要があります。 必要に応じて、オーバーロードのクラス コンストラクターを追加作成できます。  
  
-   UDT では、データ要素をパブリック フィールドまたはプロパティ プロシージャとして公開する必要があります。  
  
-   パブリック名は、128 文字より長くすることはできずに準拠している必要があります、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で定義されている、識別子の名前付け規則[データベース識別子](../databases/database-identifiers.md)します。  
  
-   `sql_variant` 列には UDT のインスタンスを含めることはできません。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] の型システムでは UDT 間の継承階層に対応していないので、継承されたメンバーに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からアクセスすることはできません。 ただし、型のマネージド コード実装では、継承を使用してクラスを構造化したり、そのクラスのメソッドを呼び出すことができます。  
  
-   クラス コンストラクター以外のメンバーはオーバーロードできません。 オーバーロード メソッドを作成した場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にアセンブリを登録したり、型を作成するときにはエラーは発生しません。 オーバーロード メソッドが検出されるのは、型の作成時ではなく実行時です。 オーバーロード メソッドは、呼び出されない限りクラス内に存在することができます。 エラーは、オーバーロード メソッドを呼び出した時点で発生します。  
  
-   すべての `static` (または `Shared`) メンバーは定数または読み取り専用として宣言する必要があります。 静的メンバーを変更可能にすることはできません。  
  
-   `SqlUserDefinedTypeAttribute.MaxByteSize` フィールドが -1 に設定されている場合、シリアル化される UDT のサイズの上限は、ラージ オブジェクト (LOB) のサイズの上限 (現在 2 GB) と同じになります。 `MaxByteSized` フィールドに値が指定されている場合は、その値が UDT のサイズの上限になります。  
  
> [!NOTE]  
>  UDT は比較を実行するためにサーバーで使用されることはありませんが、単一のメソッド `System.IComparable` を公開する `CompareTo` インターフェイスを必要に応じて実装できます。 このインターフェイスは、クライアント側で UDT 値を正確に比較したり並べ替える場合に使用します。  
  
## <a name="native-serialization"></a>ネイティブ シリアル化  
 UDT に適したシリアル化属性は、作成する UDT の種類によって異なります。 `Native` シリアル化形式では、非常に単純な構造を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が効率的なネイティブ形式で UDT をディスクに保存できるようにします。 作成する UDT が単純で、次の型のフィールドのみを含む場合は、`Native` 形式を使用することをお勧めします。  
  
 **bool**、**バイト**、 **sbyte**、**短い**、 **ushort**、 **int**、 **uint**、**長い**、 **ulong**、 **float**、**二重**、 **SqlByte**、**SqlInt16**、 **SqlInt32**、 **SqlInt64**、 **SqlDateTime**、 **SqlSingle**、 **SqlDouble**、 **SqlMoney**、 **SqlBoolean**  
  
 上記の型のフィールドの値型で構成されているは候補として適して`Native`書式設定など`structs`Visual c# では、(または`Structures`ように Visual Basic で呼ばれています)。 たとえば、シリアル化形式に `Native` を指定した UDT には、`Native` 形式を指定した別の UDT のフィールドを含めることができます。 作成する UDT の定義が複雑で、上記の一覧にないデータ型が含まれている場合は、`UserDefined` シリアル化形式を指定する必要があります。  
  
 `Native` 形式の要件を次に示します。  
  
-   型に `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.MaxByteSize` の値を指定しないでください。  
  
-   すべてのフィールドがシリアル化可能である必要があります。  
  
-   UDT を構造体ではなくクラスで定義する場合は、`System.Runtime.InteropServices.StructLayoutAttribute` を `StructLayout.LayoutKindSequential` に指定しなければなりません。 この属性は、データ フィールドの物理レイアウトを制御し、メンバーを出現順にレイアウトするために使用します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、この属性を使用して複数の値を持つ UDT のフィールド順序を決定します。  
  
 定義された UDT の例について`Native`シリアル化、Point udt の属性を参照してください。 [Coding User-Defined 型](creating-user-defined-types-coding.md)します。  
  
## <a name="userdefined-serialization"></a>ユーザー定義シリアル化  
 `UserDefined` に `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` 形式を指定すると、開発者はバイナリ形式のフル コントロールを得ることができます。 `Format` 属性プロパティに `UserDefined` を指定するときは、コード内で次の設定を行う必要があります。  
  
-   必要に応じて `IsByteOrdered` 属性プロパティを指定します。 既定値は `false` です。  
  
-   `MaxByteSize` の `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` プロパティを指定します。  
  
-   `Read` インターフェイスを実装することによって、UDT に `Write` メソッドと `System.Data.Sql.IBinarySerialize` メソッドを実装するコードを記述します。  
  
 定義された UDT の例について`UserDefined`シリアル化、Currency UDT」を参照してください。 [Coding User-Defined 型](creating-user-defined-types-coding.md)します。  
  
> [!NOTE]  
>  UDT フィールドをインデックス化するには、ネイティブ シリアル化を使用するか、UDT フィールドを保存する必要があります。  
  
## <a name="serialization-attributes"></a>シリアル化属性  
 UDT のストレージ表現を構築し、クライアントに UDT を値として転送するためにシリアル化を使用する方法は、属性で決まります。 UDT を作成する場合、`Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` を指定する必要があります。 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` 属性では、そのクラスが UDT であることを示し、UDT のストレージを指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では必要ありませんが、必要に応じて `Serializable` 属性を指定できます。  
  
 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` には、次のプロパティがあります。  
  
 `Format`  
 シリアル化形式を指定します。UDT のデータ型に応じて `Native` または `UserDefined` を指定できます。  
  
 `IsByteOrdered`  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で実行される UDT のバイナリの比較方法を決定する `Boolean` 値。  
  
 `IsFixedLength`  
 この UDT のすべてのインスタンスの長さが同じであるかどうかを示します。  
  
 `MaxByteSize`  
 インスタンスのバイト単位の最大サイズ。 `MaxByteSize` は、`UserDefined` シリアル化形式では指定する必要があります。 UDT にユーザー定義のシリアル化を指定した場合、`MaxByteSize` は、ユーザーが定義した形式でシリアル化された UDT の合計サイズを表します。 `MaxByteSize` には、1 ～ 8000 の値を指定するか、UDT が 8000 バイトより大きいことを示す -1 (合計サイズが LOB の最大サイズを超えることはできません) に設定する必要があります。 たとえば、10 文字 (`System.Char`) の文字列プロパティを持つ UDT について考えてみましょう。 BinaryWriter を使用して UDT をシリアル化されるとき、シリアル化された文字列の合計サイズは 22 バイト数を示します。Unicode utf-16 の文字ごとに 2 バイトでは、バイトのバイナリ ストリームにシリアル化から生じるオーバーヘッド文字および 2 のコントロールの最大数を掛けます。 したがって、`MaxByteSize` の値を確認する場合、シリアル化された UDT の合計サイズは、バイナリ形式にシリアル化されたデータのサイズに、シリアル化によるオーバーヘッドを加えた値と考える必要があります。  
  
 `ValidationMethodName`  
 UDT のインスタンスの検証に使用するメソッドの名前。  
  
### <a name="setting-isbyteordered"></a>IsByteOrdered の設定  
 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.IsByteOrdered` プロパティを `true` に設定すると、シリアル化されるバイナリ データを使用して、情報の意味的な順序を保証できます。 したがって、バイト順の UDT オブジェクトの各インスタンスは、シリアル化された表現を 1 つだけ持つことができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でシリアル化されたバイト列の比較操作を行うときは、その比較結果がマネージド コードで同じ比較操作を実行した場合と同じになる必要があります。 `IsByteOrdered` を `true` に設定すると、次の機能もサポートされます。  
  
-   この型の列にインデックスを作成する機能。  
  
-   この型の列に CHECK 制約と UNIQUE 制約だけでなく主キーと外部キーを作成する機能。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] の ORDER BY 句、GROUP BY 句、および PARTITION BY 句を使用する機能。 これらの句を使用した場合、順序の決定には型のバイナリ表現が使用されます。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで比較演算子を使用する機能。  
  
-   この型の計算列を保存する機能。  
  
 `Native` を `UserDefined` に設定すると、`IsByteOrdered` と `true` のどちらのシリアル化形式でも次の比較演算子がサポートされることに注意してください。  
  
-   等しい (=)  
  
-   等しくない (!=)  
  
-   より大きい (>)  
  
-   より小さい (\<)  
  
-   以上 (> =)  
  
-   以下 (<=)  
  
### <a name="implementing-nullability"></a>NULL 値の許容属性の実装  
 アセンブリの属性を正しく指定することに加えて、クラスで NULL 値の許容属性をサポートする必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に読み込まれる UDT では NULL 値が許容されますが、その UDT に NULL 値を認識させるには、クラスに `INullable` インターフェイスを実装する必要があります。 UDT に null 値許容属性を実装する方法の例と詳細については、次を参照してください。 [Coding User-Defined 型](creating-user-defined-types-coding.md)します。  
  
### <a name="string-conversions"></a>文字列の変換  
 UDT と文字列の間の変換をサポートするには、クラスに `Parse` メソッドと `ToString` メソッドを用意する必要があります。 `Parse` メソッドでは、文字列を UDT に変換できます。 このメソッドは `static` (Visual Basic では `Shared`) メソッドとして宣言され、`System.Data.SqlTypes.SqlString` 型のパラメーターを受け取る必要があります。 実装する方法の例と詳細について、`Parse`と`ToString`メソッドを参照してください[Coding User-Defined 型](creating-user-defined-types-coding.md)します。  
  
## <a name="xml-serialization"></a>XML シリアル化  
 UDT では、XML シリアル化のコントラクトに従って `xml` データ型との間の変換をサポートする必要があります。 `System.Xml.Serialization` 名前空間には、オブジェクトを XML 形式のドキュメントまたはストリームにシリアル化するためのクラスが含まれています。 `xml` インターフェイスを使用すると、`IXmlSerializable` シリアル化を実装できます。このインターフェイスにより、XML シリアル化と XML シリアル化解除用のカスタム形式が提供されます。  
  
 UDT から `xml` 型への明示的な変換に加えて、XML シリアル化により次の操作を実行できます。  
  
-   `Xquery` データ型への変換後に、UDT インスタンスの値に `xml` を使用できます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のネイティブ XML Web サービスにより、パラメーター化クエリと Web メソッドに UDT を使用できます。  
  
-   UDT を使用して、XML データの一括読み込みを受け取ることができます。  
  
-   UDT 列を含むテーブルが格納されたデータセットをシリアル化できます。  
  
 UDT は、FOR XML クエリではシリアル化されません。 UDT の XML シリアル化を表示する FOR XML クエリを実行するには、SELECT ステートメントで、各 UDT 列を明示的に `xml` データ型に変換します。 また、これらの列を明示的に `varbinary` 型、`varchar` 型、または `nvarchar` 型に変換することもできます。  
  
## <a name="see-also"></a>参照  
 [ユーザー定義型を作成する](creating-user-defined-types.md)  
  
  
