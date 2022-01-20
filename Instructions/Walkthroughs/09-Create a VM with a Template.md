---
wts:
    title: '09 - テンプレートを使用して VM を作成する (10 分)'
    module: 'モジュール 03: コア ソリューションおよび管理ツールに関する説明'
---
# 09 - テンプレートを使用して VM を作成する (10 分)

このチュートリアルでは、QuickStart テンプレートを使用して仮想マシンをデプロイし、監視機能を調べます。

# タスク 1: QuickStart ギャラリーを探索し、テンプレートを見つける 

このタスクでは、Azure QuickStart ギャラリーを参照し、仮想マシンを作成するテンプレートをデプロイします。 

1. ラボ環境内で、新しいブラウザーウィンドウを開き、 https://azure.microsoft.com/ja-jp/resources/templates/?azure-portal=true と入力します。ギャラリーには、人気のあるテンプレートや最近更新されたテンプレートが多数あります。これらのテンプレートを使用すると、一般的なソフトウェア パッケージのインストールを含む、Azure リソースのデプロイを自動化できます。使用できるさまざまな種類のテンプレートを参照します。

2. 「**Deploy a simple Windows VM(シンプルな Windows VM のデプロイ)**」を選択します

3. 「**Azure にデプロイ**」ボタンをクリックします。ブラウザー セッションは自動的に [Azure portal](http://portal.azure.com/) にリダイレクトされます。

    **注**: 「**Azure にデプロイ**」 ボタンを使用すると、テンプレートを Azure portal に直接デプロイできます。このようなデプロイの際は、一部の構成パラメーターについてのみプロンプトが表示されます。 

4. プロンプトが表示されたら、手順の前半で提供された資格情報を使用して、Azure サブスクライブにサインインします。

5. 「**テンプレートの編集**」をクリックします。Resource Manager テンプレート形式は、JSON 形式を使用しています。パラメーターと変数を確認します。  次に、仮想マシン名のパラメーターを見つけます。名前を **myVMTemplate** に変更します。変更を**保存**します。 

    ![VM 名が変更されたテンプレートのスクリーンショット。](../images/0901.png)

6. テンプレートにより必要とされるパラメーターを構成します (DNS ラベルのプレフィックスの ***xxxx*** をグローバルで一意になるように文字と数字で置き換えます)。その他は既定値のままにします。 

    | 設定| 値|
    |----|----|
    | サブスクリプション | **提供されている既定値を維持**|
    | リソース グループ | **新しいリソース グループの作成** |
    | リージョン | 既定を維持 |
    | 管理者ユーザー名 | **azureuser** |
    | 管理者パスワード | **Pa$$w0rd1234** |
    | DNS ラベルのプレフィックス | **myvmtemplatexxxx** |
    | OS バージョン | **2019-Datacenter** |


7. 「**確認および作成**」をクリックします。

8. デプロイを監視します。 

# タスク 2: 仮想マシンのデプロイを確認および監視する

このタスクでは、正しくデプロイされた仮想マシンを確認します。 

1. 「**すべてのサービス**」 ブレードで、「**仮想マシン**」 を検索して選択します。

2. 新しい仮想マシンが作成されたことを確認します。 

    ![仮想マシン ページのスクリーンショット。新しい VM が表示され、実行されます。](../images/0902.png)

3. 仮想マシンを選択し、「**概要**」ペインで「**監視**」タブを選択し、下にスクロールして監視データを表示します。

    **注**: 監視する時間枠は 1 時間から 30 日まで調整可能です。

4. 「**CPU (平均)**」、「**ネットワーク (合計)**」、「**ディスク バイト (合計)**」 を含むさまざまなグラフを確認します。 

    ![仮想マシンの監視グラフのスクリーンショット。](../images/0903.png)

5. 任意のグラフをクリックします。「**メトリックを追加**」 し、グラフの種類を変更できることに確認します。

6. 「**概要**」ブレードに戻ります。(トグル バーを左にスライド)
7. 「**アクティビティ ログ**」 (左側のウィンドウ) をクリックします。アクティビティ ログには、リソースの作成や変更などのイベントが記録されます。 

8. 「**フィルターの追加**」 をクリックし、さまざまなイベントの種類と操作を検索してみます。 

    ![「イベントの種類」が選択された「フィルターの追加」ページのスクリーンショット。](../images/0904.png)

お疲れさまでした! これで、テンプレートからリソースが正常に作成され、そのテンプレートが Azure にデプロイされました。

**注**: 追加コストを回避するために、オプションでこのリソース グループを削除できます。リソース グループを検索し、リソース グループをクリックして、「**リソース グループの削除**」をクリックします。リソース グループの名前を確認し、「**削除**」をクリックします。**通知**を監視して、削除の進行状況を確認します。