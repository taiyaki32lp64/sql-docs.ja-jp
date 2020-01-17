---
title: 許可を部分的に信頼される呼び出し元 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- AllowPartiallyTrustedCallers attribute
- security [CLR integration]
- common language runtime [SQL Server], security
- partially trusted callers [CLR integration]
ms.assetid: 20b0248f-36da-4fc3-97d2-3789fcf6e084
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bed854ba13bec4206f3ee869795af91c4da4f525
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62754200"
---
# <a name="allowing-partially-trusted-callers"></a>部分的に信頼される呼び出し元の許容
  コード ライブラリの共有は、共通言語ランタイム (CLR) 統合に関する共通のシナリオです。この場合、ユーザー定義型、ストアド プロシージャ、ユーザー定義関数、ユーザー定義集計、トリガー、またはユーティリティ クラスを含んだアセンブリは、しばしば別のアセンブリまたはアプリケーションによってアクセスされます。 複数のアプリケーションで共有されるコード ライブラリは、厳密な名前で署名する必要があります。  
  
 `System.Security.AllowPartiallyTrustedCallers` 属性で明示的にマークされていない共有マネージド コード アセンブリにアクセスできるのは、ランタイム コード アクセス セキュリティ システムによって完全に信頼されるアプリケーションだけです。 部分的に信頼されるアセンブリ ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で `SAFE` または `EXTERNAL_ACCESS` 権限セットを使用して登録されているアセンブリ) が、この属性なしに、厳密な名前で署名されたアセンブリへのアクセスを試行すると、`System.Security.SecurityException` がスローされます。 表示されるエラー メッセージは、次のような。  
  
```  
Msg 6522, Level 16, State 1, Procedure usp_RSTest, Line 0  
A .NET Framework error occurred during execution of user defined  
routine or aggregate 'usp_RSTest':  System.Security.SecurityException: That assembly does not allow partially trusted callers.  
System.Security.SecurityException: at  
System.Security.CodeAccessSecurityEngine.ThrowSecurityException(  
Assembly asm, PermissionSet granted,PermissionSet refused,  
RuntimeMethodHandle rmh, SecurityAction action, Object demand,  
IPermission permThatFailed) at  
Microsoft.Samples.SqlServer.TestResultSet.Test()  
```  
  
 グローバル アセンブリ キャッシュに追加されるアセンブリを除き、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に登録されるすべてのアセンブリは、`AllowPartiallyTrustedCallers` 属性でマークすることをお勧めします。それにより、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって読み込まれるアセンブリが相互にアクセスできるようになります。 グローバル アセンブリ キャッシュに追加されるアセンブリは、部分的に信頼される呼び出し元から予期しないコンテキストで使用できるようになるため、`AllowPartiallyTrustedCallers` 属性を追加する前に、安全性について十分に確認する必要があります。 アセンブリは、完全に信頼されないようにする ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に `UNSAFE` 権限セットを使用して登録する) 必要があります。  
  
 詳細については、.NET Framework Software Development Kit の「部分信頼コードからのライブラリの使用」を参照してください。  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 多数のサーバー側 CLR 統合アプリケーションにとって役立つユーティリティ クラスがあるとします。 たとえば、クエリを呼び出した結果を表すクラスです。 このコンポーネントを共有できるようにするには、このユーティリティ クラスを別個のアセンブリに配置します。 それにより、このアセンブリは、CLR 統合オブジェクトを含んだ他のさまざまなアセンブリから参照されます。 このユーティリティ クラスは、さまざまなサーバー アプリケーションで使用されるため、十分に確認し、セキュリティ上のすべての問題を解決しておきます。 次に、そのユーティリティ クラスを含んだアセンブリに、`AllowPartiallyTrustedCallers` 属性を適用します。それにより、`SAFE` または `EXTERNAL_ACCESS` 権限セットでマークされたアセンブリに含まれた CLR 統合オブジェクトは、別のアセンブリに配置されている場合でも、このユーティリティ クラスおよびメソッドを使用することができます。  
  
 新しい接続を開いたりすべての結果をメモリに読み取ったりせずに、クエリの結果を確認しながらコマンドを実行することができると便利な場合があります。 ADO.NET 2.0 の複数のアクティブな結果セット (MARS) 機能は、その実行を支援するテクノロジです。 現在、MARS は、サーバー側プログラミングに使用されるインプロセス プロバイダーには実装されていません。 この制限に対処するために、サーバー側カーソルを使用することができます。 このサンプルでは、サーバー側プログラミングで MARS がサポートされないことに対処するための、サーバー側カーソルの使用方法を示します。  
  
 サーバー側カーソルの使用はサーバー リソースを多く消費するため、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のクエリ オプティマイザーがクエリのパフォーマンスを向上できなくなる場合があります。 そのため、可能な場合は必ずコードを書き直して JOIN を使用するようにしてください。  
  
 このクラスの API は、結果セット内を前後に移動できる点を除いてデータ リーダーと同じであるため、結果セットが開かれている場合でも他のコマンドを接続上で実行することができます。  
  
 この実装は非常に単純化されているため、このサンプルを簡単に理解することができます。 より効率的な実装を行うと、複数の行がフェッチされるため、データベースにかかるフェッチ行あたりの負荷を回避することができます。  
  
 このクラスを使用すると、クエリの結果すべてをデータセットに設定する場合に比べ、メモリの使用量を圧倒的に少なくすることができます。このことは、サーバー側プログラミングで非常に重要です。  
  
 また、このサンプルでは、AllowPartiallyTrustedCallers 属性を使用して、ResultSet アセンブリが他のアセンブリから安全に呼び出されるライブラリであることを指定する方法を示します。 この方法はやや複雑ですが、UNSAFE 権限を使用して呼び出し側のアセンブリを登録する方法よりはるかに安全性に優れています。 呼び出し側のアセンブリを safe として登録することで、そのアセンブリがサーバー外部のリソースに与える影響が制限されるため、サーバーの整合性が維持されます。  
  
 このサンプルのビルド手順では、ソース コード ファイルが c:\samples というディレクトリにあると仮定しています。  別のディレクトリを使用する場合は、[!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトを修正する必要があります。 [!INCLUDE[tsql](../../includes/tsql-md.md)]スクリプトでは、AdventureWorks データベースも必要です。 AdventureWorks サンプル データベースをダウンロードすることができます、 [Microsoft SQL Server のサンプルとコミュニティのプロジェクト](https://go.microsoft.com/fwlink/?LinkID=85384)ホーム ページ。  
  
 サンプルをビルドして実行するには、1 つ目のコード リストを ResultSet.cs という名前のファイルに貼り付け、csc /target:library ResultSet.cs を指定してコンパイルします。  
  
 2 つ目のコード リストを TestResultSet.cs という名前のファイルに貼り付け、csc /target:library /reference:ResultSet.dll TestResultSet.cs を指定してコンパイルします。  
  
 3 つ目のコード リストを InstallCS.sql という名前のファイルに貼り付け、sqlcmd -E -I -i InstallCS.sql を指定してコンパイルします。  
  
 4 つ目のコード リストを test.sql という名前のファイルに貼り付け、sqlcmd -E -I -i test.sql を指定してコンパイルします。  
  
 5 つ目のコード リストを Cleanup.sql というファイルに貼り付け、sqlcmd -E -I -i Cleanup.sql を指定してコンパイルします。  
  
### <a name="code"></a>コード  
  
```  
// ResultSet.cs  
using System;  
using System.Collections;  
using System.Collections.Generic;  
using System.Text;  
using System.Data;  
using System.Data.Common;  
using System.Data.Sql;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using System.IO;  
using System.Globalization;  
using Microsoft.SqlServer.Server;  
using System.Runtime.Serialization;  
  
[assembly: System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Design", "CA1020:AvoidNamespacesWithFewTypes", Scope = "namespace", Target = "Microsoft.Samples.SqlServer")]  
[assembly: System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", Scope = "member", Target = "Microsoft.Samples.SqlServer.ResultSetEnumerator.System.Collections.IEnumerator.Current", MessageId = "System.InvalidOperationException.#ctor(System.String)")]  
  
namespace Microsoft.Samples.SqlServer {  
   // This is the base class for exceptions raised in the Adventure Works Cycles Storefront application.  
   [Serializable]  
   public class ResultSetException : System.Exception {  
      public ResultSetException() {}  
      public ResultSetException(string message) : base(message) {}  
      public ResultSetException(String message, Exception innerException) : base(message, innerException) {}  
      protected ResultSetException(SerializationInfo info, StreamingContext context) : base(info, context) {}  
   }  
  
   // This exception is raised when a user tries to register an email address which has already been taken.  
   [Serializable]  
   public class InvalidStateException : ResultSetException {  
      public InvalidStateException() {}  
      public InvalidStateException(string message) : base(message) {}  
      public InvalidStateException(String message, Exception innerException) : base(message, innerException) {}  
      protected InvalidStateException(SerializationInfo info, StreamingContext context) : base(info, context) {}  
   }  
  
   // This class is used to provide an API similar to a SQL data reader except that it is possible to navigate through any   
   // part of the result set.  It is also possible to execute commands while this class is still "open" even though the   
   // CLR in-proc provider does not support MARS at this time. This implementation is highly simplified to make the   
   // sample easy to understand.  A better implementation would fetch multiple rows to avoid a database turnaround per row   
   // fetched.  Using this class can have a significantly smaller memory footprint than filling a dataset with   
   // all the results of a query which is very important for server side programming.  
   [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Design", "CA1010:CollectionsShouldImplementGenericInterface"), System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Naming", "CA1710:IdentifiersShouldHaveCorrectSuffix")]  
   public class ResultSet : IDataReader, IDataRecord, IEnumerable, IDisposable {  
      // Which database to access  
      private SqlConnection connection;  
  
      // A cache or a single row's worth of data   
      private Microsoft.SqlServer.Server.SqlDataRecord results;  
  
      //A cache of whether the columns of the current cached row are set to the default value for the column  
      private int visibleFieldCount;  
  
      private string cursorName = string.Format(CultureInfo.InvariantCulture, "[{0}]", Guid.NewGuid().ToString());  
  
      internal Microsoft.SqlServer.Server.SqlDataRecord CurrentRecord {  
         get {  
            EnsureState(StateValues.read);  
            return results;  
         }  
      }  
  
      // Which database to access.  The connection passed to the setter must be open.  
      [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", MessageId = "Microsoft.Samples.SqlServer.InvalidStateException.#ctor(System.String)")/*, System.CLSCompliant(false)*/]  
      public SqlConnection Connection {  
         get {  
            return connection;  
         }  
  
         set {  
            if (value == null)  
               throw new ArgumentNullException("value");  
            if (state != StateValues.created && state != StateValues.initialized)  
               throw new InvalidStateException("Cannot alter select command after opening the result set.");  
            if (value.State != ConnectionState.Open)  
               throw new InvalidStateException("Connection must be opened prior to setting result set connection value.");  
            connection = value;  
            if (selectCommand != null && connection != null)  
               state = StateValues.initialized;  
            else  
               state = StateValues.created;  
         }  
      }  
  
      private string selectCommand;  //What query to execute against the database  
      [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", MessageId = "Microsoft.Samples.SqlServer.InvalidStateException.#ctor(System.String)")]  
      public string SelectCommand {  
         get {  
            return selectCommand;  
         }  
  
         set {  
            if (state != StateValues.created && state != StateValues.initialized)  
               throw new InvalidStateException("Cannot alter select command after opening the result set.");  
            selectCommand = value;  
            if (selectCommand != null && connection != null)  
               state = StateValues.initialized;  
            else  
               state = StateValues.created;  
         }  
      }  
  
      private bool isScrollable = true;  
      [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", MessageId = "Microsoft.Samples.SqlServer.InvalidStateException.#ctor(System.String)")]  
      public bool IsScrollable {  
         get {  
            return isScrollable;  
         }  
  
         set {  
            if (state != StateValues.created && state != StateValues.initialized)  
               throw new InvalidStateException("Cannot alter IsScrollable property after opening the result set.");  
            isScrollable = value;  
         }  
      }  
  
      // The possible phases this object can go through from creation through termination.  
      // created:  Result set is instantiated but connection and select command are not set  
      // initialized:  Result set is instantiated and connection and select command are set  
      // opened:  The cursor has been created for browsing data  
      // read:  At least one row of data has been read and cached.  
      // closed:  Cursor is closed and deallocated, and connection is closed.  No further operations are possible.  
      private enum StateValues { created, initialized, opened, read, closed };   
  
      // What the current phase is  
      private StateValues state = StateValues.created;  
  
      // It is possible to create the result set with this constructor and then set the connection  
      // and select command using the public properties.  
      public ResultSet() {}  
  
      // Or you can create the result set all at once using this form of the constructor.  
      public ResultSet(SqlConnection connection, string selectCommand) {  
         this.Connection = connection;  
         this.SelectCommand = selectCommand;  
         state = StateValues.initialized;  
      }  
  
      // By default the result set is scrollable, but you can create a forward-only result set using this constructor   
      // and specifying false for isScrollable.  
      public ResultSet(SqlConnection connection, string selectCommand, bool isScrollable) {  
         this.Connection = connection;  
         this.SelectCommand = selectCommand;  
         this.IsScrollable = isScrollable;  
         state = StateValues.initialized;  
      }  
  
      // This method should be called just before the result set is to be used to pull data.  The open doesn't happen as   
      // part of creation as server resources are being consumed while the result set is open.  Be sure to close an open   
      // result set as soon as possible to release server side resources.  
      [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", MessageId = "Microsoft.Samples.SqlServer.InvalidStateException.#ctor(System.String)")]  
      public void Open() {  
         switch (state) {  
            case StateValues.created:  
               throw new InvalidStateException("Cannot open result set until it is properly initialized");  
            case StateValues.opened:  
            case StateValues.read:  
               throw new InvalidStateException("Result set already open.");  
            case StateValues.closed:  
               throw new InvalidStateException("Cannot reopen closed result set.");  
            default:  
               break;  
         }  
         if (state == StateValues.initialized) {  
            // There are many possible cursor options.  We only allow control of scrollability.  
            // To keep the implementation simple we only permit read operations.  
            string scrollMode = (isScrollable) ? "SCROLL" : "FORWARD_ONLY";  
  
            // Caller must ensure that any user input which is part of selectCommand is free from injection attacks.  
            SqlCommand cmd = connection.CreateCommand();  
            cmd.CommandText = string.Format(CultureInfo.InvariantCulture, "DECLARE {0} CURSOR GLOBAL {1} READ_ONLY  FOR {2}; OPEN {0};",  
                cursorName, scrollMode, selectCommand);  
            cmd.ExecuteNonQuery();  
            state = StateValues.opened;  
         }  
      }  
  
      // Free all server and client side resources being consumed for this result set.  Most operations  
      // are no longer valid after calling this method on the result set.  
      [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", MessageId = "Microsoft.Samples.SqlServer.InvalidStateException.#ctor(System.String)")]  
      public void Close() {  
         switch (state) {  
            case StateValues.created:  
            case StateValues.initialized:  
               throw new InvalidStateException("Cannot close unopened result set.");  
            case StateValues.closed:  
               throw new InvalidStateException("Result set already closed.");  
            case StateValues.opened:  
            case StateValues.read:  
               SqlCommand cmd = connection.CreateCommand();  
               cmd.CommandText =  
                   string.Format(CultureInfo.InvariantCulture, "CLOSE {0}; DEALLOCATE {0};", cursorName);  
               try {  
                  cmd.ExecuteNonQuery();  
               }  
               finally {  
                  results = null;  
                  state = StateValues.closed;  
               }  
               break;  
            default:  
               throw new InvalidStateException(  
                   string.Format(CultureInfo.InvariantCulture,  
                   "Unknown result set state {0}", state.ToString()));  
         }  
  
      }  
  
      // This implementation does not support multi-dimensional data. Always zero.  
      public int Depth {  
         get {  
            EnsureState(StateValues.read);  
            return 0;  
         }  
      }  
  
      // Normally this would return a data table with schema information about the data being returned.  
      // Unfortunately this isn't implemented in the in-proc provider, so always throw a NYI exception.  
      [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", MessageId = "System.NotImplementedException.#ctor(System.String)")]  
      public DataTable GetSchemaTable() {  
         throw new NotImplementedException("GetSchemaTable is not currently implemented.");  
      }  
  
      // Determines if there is any data to read. True if there is data to read, otherwise false.  
      [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", MessageId = "System.NotImplementedException.#ctor(System.String)")]  
      public bool HasRows {  
         get {  
            throw new NotImplementedException("HasRows is not currently implemented.");  
         }  
      }  
  
      // Determines if the result set is available for use  
      // Returns false if the result set is available for use, otherwise true.  
      public bool IsClosed {  
         get { return state == StateValues.closed; }  
      }  
  
      // Multiple result sets are not supported.  Always throws an invalid operation exception.  
      [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", MessageId = "System.InvalidOperationException.#ctor(System.String)")]  
      public bool NextResult() {  
         throw new InvalidOperationException("Multiple result sets are not support for result set class");  
      }  
  
      // Fetches the next row from the result set on the server and makes that data available to the caller.  
      // Returns True if and only if there is data to read.  
      public bool Read() {  
         return fetch(string.Format(CultureInfo.InvariantCulture, "FETCH NEXT FROM {0};", cursorName));  
      }  
  
      // Returns the number of records affected by processing this result set.  This may only be called when the result set  
      // is closed.  Since this implementation supports only read-only access, there can never be any rows affected (always -1).  
      public int RecordsAffected {  
         get {  
            EnsureState(StateValues.closed);  
            return -1;  
         }  
      }  
  
      // Move to a particular record number in the results returned by the query.  Requires a scrollable result set.  
      // Returns True if and only if there is data to read.  
      public bool ReadAbsolute(int position) {  
         EnsureScroll();  
         return fetch(string.Format(CultureInfo.InvariantCulture, "FETCH ABSOLUTE {0} FROM {1};",  
             position, cursorName));  
      }  
  
      // Move to the first result in the results returned by the query and read it.  Requires a scrollable result set.  
      // Returns True if and only if there is data to read.  
      public bool ReadFirst() {  
         EnsureScroll();  
         return fetch(string.Format(CultureInfo.InvariantCulture, "FETCH FIRST FROM {0};", cursorName));  
      }  
  
      // Move to the last result in the results returned by the query and read it.  Requires a scrollable result set.  
      // Returns True if and only if there is data to read.  
      public bool ReadLast() {  
         EnsureScroll();  
         return fetch(string.Format(CultureInfo.InvariantCulture, "FETCH LAST FROM {0};", cursorName));  
      }  
  
      // Move to the immediate prior result in the results returned by the query, and read it.  Requires a scrollable   
      // result set.  Returns True if and only if there is data to read.  
      public bool ReadPrevious() {  
         EnsureScroll();  
         return fetch(string.Format(CultureInfo.InvariantCulture, "FETCH PREVIOUS FROM {0};", cursorName));  
      }  
  
      // Move the specified number of records forward or backward from the current position  
      // in the results returned by the query and read it.  Requires a scrollable result set.  
      /// position is how many records forward or backward. Returns True if and only if there is data to read.  
      public bool ReadRelative(int position) {  
         EnsureScroll();  
         return fetch(string.Format(CultureInfo.InvariantCulture, "FETCH RELATIVE {0} FROM {1};", position, cursorName));  
      }  
  
      // Dispose is idential to closing the result set.  
      public void Dispose() {  
         Dispose(true);  
      }  
  
      protected virtual void Dispose(bool shouldClearManagedResources) {  
         Close();  
         if (shouldClearManagedResources)  
            connection = null;  
      }  
  
      // The number of columns available in the results just read  
      public int FieldCount {  
         get {  
            EnsureState(StateValues.read);  
            return results.FieldCount;  
         }  
      }  
  
      public int VisibleFieldCount {  
         get {  
            EnsureState(StateValues.read);  
            return visibleFieldCount;  
         }  
      }  
  
      [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", MessageId = "System.InvalidOperationException.#ctor(System.String)")]  
      public IDataReader GetData(int i) {  
         throw new InvalidOperationException("GetData is no longer implemented");  
      }  
  
      // What kind of data is acceptable for the specified column  
      public string GetDataTypeName(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetDataTypeName(i);  
      }  
  
      // Returns the object which represents the kind of data which is acceptable for the specified column.  
      public Type GetFieldType(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetFieldType(i);  
      }  
  
      // Returns the symbolic id of the specified column  
      public string GetName(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetName(i);  
      }  
  
      // Given a column name, returns the integer id the column.  
      public int GetOrdinal(string name) {  
         EnsureState(StateValues.read);  
         //Note: this implementation does not deal with all collation and internationalization issues.  
         return results.GetOrdinal(name);  
      }  
  
      // Places all the values contained in the current row into the supplied object array.  The elements  
      // of the array are based on the SQL type system.  
      public int GetSqlValues(object[] values) {  
         EnsureState(StateValues.read);  
         return results.GetSqlValues(values);  
      }  
  
      // Places all the values contained in the current row into the supplied object array.  The   
      // elements of the array are based on the CLR type system.  
      public int GetValues(object[] values) {  
         EnsureState(StateValues.read);  
         return results.GetValues(values);  
      }  
  
      // Accesses the data in the specified column by name  
      public object this[string name] {  
         get {  
            EnsureState(StateValues.read);  
            return results[name];  
         }  
      }  
  
      // Accesses the data in the specified column by numerical id  
      public object this[int i] {  
         get {  
            EnsureState(StateValues.read);  
            return results[i];  
         }  
      }  
  
      // The following methods provide access to column data for the current row as objects using the Sql type system.    
      // The advantage of using this type system is that you can deal very precisely with the database's concept of null.    
      // Also, some types (such as SqlXml) provide more efficient methods of data access than the CLR type system.  
  
      // Access the data in the specified column in the current row as a SqlBinary object  
      public SqlBinary GetSqlBinary(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlBinary(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlBoolean object  
      public SqlBoolean GetSqlBoolean(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlBoolean(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlByte object  
      public SqlByte GetSqlByte(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlByte(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlBytes object  
      public SqlBytes GetSqlBytes(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlBytes(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlChars object  
      public SqlChars GetSqlChars(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlChars(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlDateTime object  
      public SqlDateTime GetSqlDateTime(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlDateTime(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlDecimal object  
      public SqlDecimal GetSqlDecimal(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlDecimal(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlDouble object  
      public SqlDouble GetSqlDouble(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlDouble(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlGuid object  
      public SqlGuid GetSqlGuid(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlGuid(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlInt16 object  
      public SqlInt16 GetSqlInt16(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlInt16(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlInt32 object  
      public SqlInt32 GetSqlInt32(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlInt32(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlInt64 object  
      public SqlInt64 GetSqlInt64(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlInt64(i);  
      }  
  
      // Return schema information for the specified column  
      public Microsoft.SqlServer.Server.SqlMetaData GetSqlMetaData(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlMetaData(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlMoney object  
      public SqlMoney GetSqlMoney(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlMoney(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlSingle object  
      public SqlSingle GetSqlSingle(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlSingle(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlString object  
      public SqlString GetSqlString(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlString(i);  
      }  
  
      // Access the data in the specified column in the current row as a Sql object  
      public object GetSqlValue(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlValue(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlXml object  
      public SqlXml GetSqlXml(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlXml(i);  
      }  
  
      // The following methods provide access to column data for the current row using the CLR type system.  The advantage   
      // of using these methods is seamless integration with other CLR components.  
  
      // Access the data in the specified column in the current row as a Boolean  
      public bool GetBoolean(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetBoolean(i);  
      }  
  
      // Access the data in the specified column in the current row as a byte   
      public byte GetByte(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetByte(i);  
      }  
  
      // Copies bytes from the specified column of the current row into a buffer supplied by the caller.  
      // i is the columm, fieldOffset is where to start in the column's data, buffer is where to place the bytes,  
      // bufferOffset is where to start in the buffer, and length is how many bytes to copy.    
      // Returns how many bytes were actually copied.  
      public long GetBytes(int i, long fieldOffset, byte[] buffer, int bufferoffset, int length) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetBytes(i, fieldOffset, buffer, bufferoffset, length);  
      }  
  
      // Access the data in the specified column in the current row as a  char.  
      public char GetChar(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetChar(i);  
      }  
  
      // Copies characters from the specified column of the current row into a buffer supplied by the caller.  
      // i is the column, fieldoffset is where to start in the column's data, buffer is where to place the characters,  
      // bufferoffset is where to start in the buffer, length is how many characters to copy.  
      // Returns how many characters were actually copied.  
      public long GetChars(int i, long fieldoffset, char[] buffer, int bufferoffset, int length) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetChars(i, fieldoffset, buffer, bufferoffset, length);  
      }  
  
      // Access the data in the specified column in the current row as a DateTime   
      public DateTime GetDateTime(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetDateTime(i);  
      }  
  
      // Access the data in the specified column in the current row as a decimal.   
      public decimal GetDecimal(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetDecimal(i);  
      }  
  
      // Access the data in the specified column in the current row as a double  
      public double GetDouble(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetDouble(i);  
      }  
  
      // Access the data in the specified column in the current row as a float  
      public float GetFloat(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetFloat(i);  
      }  
  
      // Access the data in the specified column in the current row as a Guid   
      public Guid GetGuid(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetGuid(i);  
      }  
  
      // Access the data in the specified column in the current row as a short   
      public short GetInt16(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetInt16(i);  
      }  
  
      // Access the data in the specified column in the current row as an int  
      public int GetInt32(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetInt32(i);  
      }  
  
      // Access the data in the specified column in the current row as a long   
      public long GetInt64(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetInt64(i);  
      }  
  
      // Access the data in the specified column in the current row as a string   
      public string GetString(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetString(i);  
      }  
  
      // Access the data in the specified column in the current row as an object    
      public object GetValue(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetValue(i);  
      }  
  
      // Returns true if and only if the data in the specified column of the current row is null as defined by the database.    
      // Note this is different than the CLR concept of null. The parameter is the column.  
      public bool IsDBNull(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.IsDBNull(i);  
      }  
  
      // Utility method which executes a server side cursor motion command and reads the row at the current location of   
      // the cursor after the motion is complete.  Reading one row at a time can be inefficient, see comments at the start   
      // of this class. The parameter is the SQL cursor motion command to execute. Returns True if and only if there is data to read.  
      [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", MessageId = "Microsoft.Samples.SqlServer.ResultSet.EnsureState(Microsoft.Samples.SqlServer.ResultSet+StateValues,Microsoft.Samples.SqlServer.ResultSet+StateValues,System.String)")]  
      private bool fetch(string commandText) {  
         EnsureState(StateValues.read, StateValues.opened, "The result set must be open to perform the read operation.");  
         SqlCommand cmd = connection.CreateCommand();  
         cmd.CommandText = commandText;  
  
         SqlDataReader reader = null;  
         try {  
            reader = cmd.ExecuteReader();  
            // If there is no data, return false;  
            if (!reader.Read()) {  
               state = StateValues.opened;  
               return false;  
            }  
            else {  
               // Otherwise, advance the state to 'read'  
               state = StateValues.read;  
               // If we haven't cached schema information get it now  
               if (results == null) FetchMetadata(reader);  
               // Cache data values  
               object[] values = new object[FieldCount];  
               reader.GetSqlValues(values);  
               results.SetValues(values);  
               // Indicate there is data read by returning true  
               return true;  
            }  
         }  
         finally {  
            if (reader != null) {  
               reader.Close();  
               reader = null;  
            }  
         }  
      }  
  
      // Helper method for the fetch method.  Initializes the data structures which cache the schema information for the   
      // current query. The parameter is the reader from where schema information may be read.  
      private void FetchMetadata(SqlDataReader reader) {  
         int columnCount = reader.FieldCount;  
         visibleFieldCount = columnCount;  
         // Initialize the data cache  
         SqlMetaData[] metadata = new SqlMetaData[visibleFieldCount];  
  
         // Fill the schema cache for each column  
         DataTable schemaTable = reader.GetSchemaTable();  
         SqlString collationString = new SqlString(String.Empty);  
  
         for (int i = 0 ; i < metadata.Length ; i++) {  
            DataRow columnSchema = schemaTable.Rows[i];  
            metadata[i] = new SqlMetaData(  
                    reader.GetName(i),  
                    (SqlDbType)columnSchema["ProviderType"],  
                    (int)columnSchema["ColumnSize"],  
                    (byte)((short)columnSchema["NumericPrecision"]),  
                    (byte)((short)columnSchema["NumericScale"]),  
                    collationString.LCID,  
                    collationString.SqlCompareOptions,  
                    (Type)columnSchema["DataType"]  
                );  
         }  
         results = new Microsoft.SqlServer.Server.SqlDataRecord(metadata);  
      }  
  
      // Helper method which validates the state of the result set before processing a   
      // requested operation.  If the result set is in an invalid state an exception is thrown.  
      private void EnsureState(StateValues desiredState) {  
         if (state != desiredState) {  
            // Compute the default message  
            string message = string.Format(CultureInfo.InvariantCulture, "Expected result set state to be {0} but it was {1}",  
                desiredState.ToString(), state.ToString());  
            // If we have more specific information, provide a different message.  
            if (desiredState == StateValues.read)  
               message = "You must read a valid row of the result set before performing the requested operation.";  
            throw new InvalidStateException(message);  
         }  
      }  
  
      // Similar to the single argument EnsureState method except that the two specified states   
      // are both legal and a custom error message must be provided.  
      private void EnsureState(StateValues desiredState1, StateValues desiredState2, string message) {  
         if (state != desiredState1 && state != desiredState2)  
            throw new InvalidStateException(message);  
      }  
  
      // Makes certain that the requested column is valid, and throws an exception with an error message if it isn't.    
      // This would be more useful than the error message given when accessing beyond the valid boundary of an array,   
      // for example.  The parameter is the column trying to be accessed  
      private void EnsureOrdinal(int i) {  
         if (i >= results.FieldCount)  
            throw new ArgumentException(  
                string.Format(CultureInfo.InvariantCulture, "Attempt to access column {0} when only {1} columns exist",  
                i, results.FieldCount));  
      }  
  
      // Makes certain that the result set is in a proper state to read data, and that  
      // scrolling is allowed.  This method is called from methods which require scrolling capabilities.  
      [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", MessageId = "System.InvalidOperationException.#ctor(System.String)")]  
      private void EnsureScroll() {  
         if (!isScrollable)  
            throw new InvalidOperationException("Attempting to execute a scroll operation on a non-scrollable result set.");  
      }  
  
      public IEnumerator GetEnumerator() {  
         return new ResultSetEnumerator(this);  
      }  
   }  
  
   public class ResultSetEnumerator : IEnumerator {  
      private bool isRead;  
  
      private ResultSet resultSetToEnumerate;  
  
      public ResultSetEnumerator(ResultSet resultSetToEnumerate) {  
         this.resultSetToEnumerate = resultSetToEnumerate;  
      }  
  
      // Returns the current element of a result set which is represented by a SqlDataRecord  
      object IEnumerator.Current {  
         get {  
            if (!isRead)  
               throw new InvalidOperationException(  
                   "The enumerator is positioned before the first element "  
                   + "of the collection or after the last element");  
            return resultSetToEnumerate.CurrentRecord;  
  
         }  
      }  
  
      [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", MessageId = "System.InvalidOperationException.#ctor(System.String)")]  
      public SqlDataRecord Current {  
         get {  
            if (!isRead)  
               throw new InvalidOperationException(  
                   "The enumerator is positioned before the first element "  
                   + "of the collection or after the last element");  
            return resultSetToEnumerate.CurrentRecord;  
         }  
      }  
  
      // Advance to the next valid element of a result set; returns True if this position has a valid element   
      public bool MoveNext() {  
         if (!isRead) {  
            if (resultSetToEnumerate.ReadFirst()) {  
               isRead = true;  
               return true;  
            }  
            else  
               return false;  
         }  
         else {  
            return resultSetToEnumerate.Read();  
         }  
      }  
  
      // Reset the current position of the enumerator to just prior to the current element  
      public void Reset() {  
         isRead = false;  
      }  
   }  
}  
```  
  
### <a name="code"></a>コード  
  
```  
// TestResultSet.cs  
using System;  
using System.Collections.Generic;  
using System.Text;  
using System.Configuration;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
  
// Main application that increases the prices for the most popular bikes in order to demonstrate using server side cursors   
// to browser results and update in parallel.  
  
namespace Microsoft.Samples.SqlServer {  
   public sealed class TestResultSet {  
      // The factor to mulitply by the current price to get the new price for each color  
      private const String priceIncreases = "Black, 1.02, Silver, 1.01, Red, 1.05, Yellow, 1.02, Green, 1.03";  
  
      // Given the name of a color, return the price increase factor as a SqlMoney object.  
      private static readonly Dictionary<String, SqlMoney> increaseDictionary  
          = new Dictionary<String, SqlMoney>(priceIncreases.Length);  
  
      // Don't allow construction of instances since the public portion of this class is only used to contain static methods.  
      private TestResultSet() {}  
  
      // The Adventure Works Cycles corporation needs to increase the standard costs and list price for its most popular   
      // bikes due to price increases for the paint used on those bikes.  This program demonstrates browsing popular bikes   
      // and updating prices in parallel using the result set sample to implement that scenario.  Note that programmers   
      // should always consider whether using a JOIN in a server side query or update would be more efficient that using this   
      // style of programming.  
      public static void Test() {  
         // Use the priceIncreases constant to initialize entries in the increaseDictionary collection.  
         InitializeIncreaseDictionary();  
  
         SqlConnection myConnection = null;  
         bool isRSOpened = false;  
  
         // Initialize the command to get most popular bikes  
         myConnection = new SqlConnection("context connection=true");  
         ResultSet rs = null;  
         try {  
            myConnection.Open();  
            rs = new ResultSet(myConnection,  
                "SELECT TOP 10 P.ProductID, P.Name, P.Color, P.StandardCost, P.ListPrice, "  
                + "sum(SOD.OrderQty) FROM Production.Product AS P "  
                + "JOIN Sales.SalesOrderDetail AS SOD ON P.ProductID = SOD.ProductID "  
                + "JOIN Production.ProductSubcategory AS PSC "  
                + "ON P.ProductSubcategoryID = PSC.ProductSubcategoryID "  
                + "JOIN Production.ProductCategory AS PC "  
                + "ON PSC.ProductCategoryID = PC.ProductCategoryID "  
                + "WHERE PC.Name = 'Bikes' "  
                + "GROUP BY P.ProductID, P.Name, P.Color, P.StandardCost, P.ListPrice "  
                + "ORDER BY sum(SOD.OrderQty) desc;");  
  
            // Initialize the command to update the price of a product  
            SqlCommand updateCommand = myConnection.CreateCommand();  
            updateCommand.CommandText = "usp_UpdateProductPrice";  
            updateCommand.CommandType = CommandType.StoredProcedure;  
  
            SqlParameter productIDParameter = new SqlParameter("@ProductID", SqlDbType.Int);  
            updateCommand.Parameters.Add(productIDParameter);  
            SqlParameter standardCostParameter = new SqlParameter("@StandardCost", SqlDbType.Money);  
            updateCommand.Parameters.Add(standardCostParameter);  
            SqlParameter listPriceParameter = new SqlParameter("@ListPrice", SqlDbType.Money);  
            updateCommand.Parameters.Add(listPriceParameter);  
  
            rs.Open();  
            isRSOpened = true;  
  
            while (rs.Read()) {  
               // Column two in the result set contains the color of the bike  
               SqlMoney rateOfIncrease = increaseDictionary[rs.GetString(2)];  
  
               // Column zero in the result set contains the product ID  
               productIDParameter.Value = rs.GetInt32(0);  
  
               // Column three in the result set contains the current standard cost  
               standardCostParameter.Value = rs.GetSqlMoney(3) * rateOfIncrease;  
  
               // Column four in the result set contains the current list price  
               listPriceParameter.Value = rs.GetSqlMoney(4) * rateOfIncrease;  
  
               // Update the prices of one of the popular bikes based on its color and current prices.    
               updateCommand.ExecuteNonQuery();  
            }  
         }  
         finally {  
            if (myConnection != null) {  
  
               if (isRSOpened)  
                  rs.Close();  
  
               myConnection.Close();  
            }  
         }  
      }  
  
       // Helper function which fills the dictonary containing the price increases for each color  
      static void InitializeIncreaseDictionary() {  
         // Initialize a dictionary which contains the price increase factors for each color  
         String[] splitIncreases = priceIncreases.Split(new Char[] { ',' });  
  
         for ( int i = 0 ; i < splitIncreases.Length - 1 ; i += 2 ) {  
            increaseDictionary[splitIncreases[i].Trim()] = SqlMoney.Parse(splitIncreases[i + 1].Trim());  
         }  
      }  
   }  
}  
```  
  
### <a name="code"></a>コード  
  
```  
-- InstallCS.sql  
USE AdventureWorks  
GO  
  
IF EXISTS (SELECT [name] from sys.procedures WHERE [name] = N'usp_RSTest')  
DROP PROCEDURE usp_RSTest;  
GO  
  
IF EXISTS (SELECT [name] from sys.procedures WHERE [name] = N'usp_UpdateProductPrice')  
DROP PROCEDURE usp_UpdateProductPrice;  
GO  
  
IF EXISTS (SELECT [name] FROM sys.assemblies WHERE [name] = N'TestResultSet')  
DROP ASSEMBLY TestResultSet;  
GO  
  
IF EXISTS (SELECT [name] FROM sys.assemblies WHERE [name] = N'ResultSet')  
DROP ASSEMBLY ResultSet;  
GO  
  
-- Add the assembly which contains the CLR methods we want to invoke on the server.  
DECLARE @SamplesPath nvarchar(1024);  
  
CREATE ASSEMBLY [ResultSet]  
FROM 'C:\ResultSet\ResultSet.dll'  
WITH permission_set = safe;  
  
CREATE ASSEMBLY [TestResultSet]    
FROM 'C:\ResultSet\TestResultSet.dll'  
WITH permission_set = safe;  
GO  
  
CREATE PROCEDURE [usp_RSTest]  
AS EXTERNAL NAME [TestResultSet].[Microsoft.Samples.SqlServer.TestResultSet].Test  
GO  
  
CREATE PROCEDURE usp_UpdateProductPrice(  
    @ProductID int,  
    @StandardCost money,  
    @ListPrice money  
)     
AS  
SET NOCOUNT ON;  
  
UPDATE Production.Product  
SET StandardCost = @StandardCost,  
    ListPrice = @ListPrice  
WHERE ProductID = @ProductID;  
GO  
```  
  
### <a name="code"></a>コード  
  
```  
-- test.sql  
USE AdventureWorks  
GO  
  
SELECT TOP 10 P.ProductID, P.Name, P.Color, P.StandardCost, P.ListPrice, sum(SOD.OrderQty) FROM Production.Product AS P  
JOIN Sales.SalesOrderDetail AS SOD ON P.ProductID = SOD.ProductID  
JOIN Production.ProductSubcategory AS PSC ON P.ProductSubcategoryID = PSC.ProductSubcategoryID  
JOIN Production.ProductCategory AS PC ON PSC.ProductCategoryID = PC.ProductCategoryID  
WHERE PC.Name = 'Bikes'  
GROUP BY P.ProductID, P.Name, P.Color, P.StandardCost, P.ListPrice   
ORDER BY sum(SOD.OrderQty) desc;  
GO  
  
EXEC usp_RSTest  
GO  
  
SELECT TOP 10 P.ProductID, P.Name, P.Color, P.StandardCost, P.ListPrice, sum(SOD.OrderQty) FROM Production.Product AS P  
JOIN Sales.SalesOrderDetail AS SOD ON P.ProductID = SOD.ProductID  
JOIN Production.ProductSubcategory AS PSC ON P.ProductSubcategoryID = PSC.ProductSubcategoryID  
JOIN Production.ProductCategory AS PC ON PSC.ProductCategoryID = PC.ProductCategoryID  
WHERE PC.Name = 'Bikes'  
GROUP BY P.ProductID, P.Name, P.Color, P.StandardCost, P.ListPrice   
ORDER BY sum(SOD.OrderQty) desc;  
GO  
  
```  
  
### <a name="code"></a>コード  
  
```  
-- Cleanup.sql  
USE AdventureWorks  
GO  
  
IF EXISTS (SELECT [name] from sys.procedures WHERE [name] = N'usp_RSTest')  
DROP PROCEDURE usp_RSTest;  
GO  
  
IF EXISTS (SELECT [name] from sys.procedures WHERE [name] = N'usp_UpdateProductPrice')  
DROP PROCEDURE usp_UpdateProductPrice;  
GO  
  
IF EXISTS (SELECT [name] FROM sys.assemblies WHERE [name] = N'TestResultSet')  
DROP ASSEMBLY TestResultSet;  
GO  
  
IF EXISTS (SELECT [name] FROM sys.assemblies WHERE [name] = N'ResultSet')  
DROP ASSEMBLY ResultSet;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [CLR 統合のセキュリティ](../../relational-databases/clr-integration/security/clr-integration-security.md)  
  
  
