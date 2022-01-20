---
wts:
    title: '06 - SQL Database を作成する (5 分)'
    module: 'モジュール 02 - Azure のコア サービス (ワークロード)'
---

# 06 - SQL Database を作成する (5 分)

このチュートリアルでは、Azure で SQL Database を作成し、そのデータベース内のデータをクエリします。

# タスク 1: データベースを作成する 

このタスクでは、AdventureWorksLT サンプル データベースに基づいて、SQL データベースを作成します。 

1. [Azure portal](https://portal.azure.com) にサインインします。

2. 「**すべてのサービス**」ブレードで「**SQL データベース**」を検索して選択し、**「+ 追加」、「+ 作成」、「+ 新規」** のいずれかをクリックします。 

3. 「**基本**」タブで、次の情報を入力します。  

    | 設定 | 値 | 
    | --- | --- |
    | サブスクリプション | **提供されている既定値を使用** |
    | リソース グループ | **新しいリソース グループの作成** |
    | データベース名| **db1** | 
    | サーバー | 「**新規作成**」を選択します (右側に新しいサイドバーが開きます)|
    | サーバー名 | **sqlserverxxxx** (一意である必要があります) | 
    | 場所 | **(米国) 米国東部** |
    | 認証方法 | **SQL 認証を使用する** |
    | サーバー管理者のログイン | **sqluser** |
    | パスワード | **Pa$$w0rd1234** |
    | クリック  | **OK** |

   ![「サーバー」ペインと「新しいサーバー」ペインのスクリーンショット。表に従ってフィールドが入力され、「確認および作成」と「OK」ボタンが強調表示されています。](../images/0501.png)

4. 「**ネットワーク**」タブで、次の設定を構成します (その他は既定値のままにしておきます)。 

    | 設定 | 値 | 
    | --- | --- |
    | 接続方法 | **パブリック エンドポイント** |    
    | Azure サービスとリソースのサーバーへのアクセスを許可する | **はい** |
    | 現在のクライアント IP アドレスを追加する | **いいえ** |
    
   ![「SQL Database の作成」ブレードの「ネットワーク」タブのスクリーンショット。テーブルに従って設定が選択され、「確認および作成」ボタンが強調表示されています。](../images/0501b.png)

5. **セキュリティ** タブで。 

    | 設定 | 値 | 
    | --- | --- |
    | Microsoft Defender for SQL| **後で** |
    
6. 「**追加設定**」タブに移動します。AdventureWorksLT サンプル データベースを使用します。

    | 設定 | 値 | 
    | --- | --- |
    | 既存のデータを使用する | **サンプル** |

    ![「SQL Database の作成」ブレードの「追加設定」タブのスクリーンショット。テーブルに従って設定が選択され、「確認および作成」ボタンが強調表示されています。](../images/0501c.png)

7. 「**確認および作成**」をクリックしてから「**作成**」をクリックして、リソース グループ、サーバー、データベースをデプロイおよびプロビジョニングします。デプロイには約 2 分から 5 分かかることがあります。


# タスク 2: データベースをテストする。

このタスクでは、SQL サーバーを構成し、SQL クエリを実行します。 

1. デプロイが完了したら、デプロイ ブレードで「リソースに移動」をクリックします。または、「**すべてのリソース**」ブレードから「**データベース**」を検索して選択し、**SQL データベース**で新しいデータベースが作成されたことを確認します。ページを**更新**する必要がある場合があります。

    ![先ほどデプロイされた SQL データベースとサーバーのスクリーンショット。](../images/0502.png)

2. 作成した SQL データベースを表す **db1** エントリをクリックします。db1 ブレードで、「**クエリ エディター (プレビュー)**」をクリックします。

3. ユーザー名 「**sqluser**」 でパスワード 「**Pa$$w0rd1234**」 を使用してログインします。

4. ログインすることはできません。エラーをよく読み、ファイアウォール経由で許可する必要がある IP アドレスをメモしておきます。 

    ![IP アドレス エラーを示すクエリ エディターのログイン ページのスクリーンショット。](../images/0503.png)

5. 「**db1**」ブレードに戻り、「**概要**」をクリックします。 

    ![SQL サーバー ページのスクリーンショット。](../images/0504.png)

6. db1の「**概要**」ブレードから、概要画面の上部中央にある「**サーバー ファイアウォールの設定**」をクリックします。

7. 「**+ クライアント IP の追加**」(トップ メニュー バー) をクリックし、エラーで参照されている IP アドレスを追加します。(自動入力されている可能性があります。そうでない場合は、IP アドレス フィールドに貼り付けてください)。変更を必ず**保存**してください。 

    ![新しい IP 規則が強調表示されている、SQL サーバー ファイアウォールの設定ページのスクリーンショット。](../images/0506.png)

8. SQL データベースに戻り (下部のトグル バーを左にスライドします)、「**クエリ エディター (プレビュー)**」をクリックします。ユーザー名「**sqluser**」でパスワード「**Pa$$w0rd1234**」を使用してログインします。今度は成功するはずです。新しいファイアウォール規則がデプロイされるまでに数分かかる場合があります。 

9. 正常にログインすると、クエリ ウィンドウが表示されます。エディター ウィンドウに次のクエリを入力します。 

    ```SQL
    SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
    FROM SalesLT.ProductCategory pc
    JOIN SalesLT.Product p
    ON pc.productcategoryid = p.productcategoryid;
    ```

    ![クエリ ペインとコマンドが正常に実行されたクエリ エディターのスクリーンショット。](../images/0507.png)

10. 「**実行**」 をクリックしてから、「**結果**」 ペインでクエリの結果を確認します。クエリは正常に実行されるはずです。

    ![SQL コードが正常に実行され、「結果」ペインに出力が表示されている、データベースのクエリ エディター ペインのスクリーンショット。](../images/0508.png)

お疲れさまでした。Azure で SQL Database を作成し、そのデータベース内のデータを正常にクエリしました。

**注**: 追加コストを回避するために、オプションでこのリソース グループを削除できます。リソース グループを検索し、リソース グループをクリックして、「**リソース グループの削除**」をクリックします。リソース グループの名前を確認し、「**削除**」をクリックします。**通知**を監視して、削除の進行状況を確認します。