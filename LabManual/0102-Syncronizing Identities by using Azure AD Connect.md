# ラボ 0102: Microsoft Entra Connect を使用した ID の同期



## 概要



このラボでは、Active Directory ドメイン サービスから Entra ID への同期を構成します。

### シナリオ



Contoso Corporation は現在、AD DS と Entra ID の両方でユーザーを個別のプロセスとして管理しています。これには時間がかかり、情報に一貫性がありません。Microsoft Entra Connect 同期ツールを使用して 2 つのディレクトリを接続することで、この問題に対処する任務が与えられました。

#### タスク 1: Microsoft Entra Connect とのディレクトリ同期を構成する



1. **SEA-SVR1** に、必要に応じて、**Pa55w.rd** のパスワードを使用して **Contoso\Administrator** としてサインインし、**サーバー マネージャー**を閉じます。

2. タスク バーで、[**Microsoft Edge]** を選択します。

3. アドレスバーに `https://entra.microsoft.com` と入力してアクセスします。サインインは admin@yourtenant.onmicrosoft.com として実施してください。

   アクセスして英語表記となっている場合、日本語表記に変更した方が進めやすくなります。画面右上の歯車のマーク **「Settings」** をクリックした後、左の「Language + region」をクリックし、Language と Regional format でいずれも日本語を選択し、 **[Apply] - [OK]** をクリックします。

4. 左側のナビゲーション ウィンドウの **[Entra ID**] で、 [**Entra Connect**] を選択します。

5. **Microsoft Entra Connect |[作業の開始**] ウィンドウで、[**管理]** タブを選択します。

6. [**インフラストラクチャの管理]** ページで、[**Connect 同期エージェント のダウンロード]** ボタンをクリックします。(「～のダウンロード」ボタンが２つありますが、下のものはずです。)

7. **[使用条件に同意してダウンロードする**] をクリックします。

   > **注**: Azure AD Connect は、SEA-SVR1 の **[ダウンロード]** フォルダに自動的にダウンロードされます。

8. [**ダウンロード フォルダーを開く]** を選択し、[**Downloads]** ウィンドウで **AzureAdConnect.msi** をダブルクリックします。

9. **Microsoft Entra Connect Sync**ウィザードの [**Welcome to Microsoft Entra Connect Sync**] ページで、[**I agree to the license terms and privacy notice]** チェック ボックスをオンにし、 **[Continue]** を選択します。

10. [**Express Settings**] ページで、[**Customize]** を選択します。

11. 必要な**Install required components** ページで、**Install** を選択します。

12. **[User sign-in] ** ページで、[**Password Hash Synchronization]** が選択されていることを確認し、[**Next**] を選択します。

13. [**Microsoft Entra ID への接続**] ページの **[USERNAME**] ボックスに「**[admin@yourtenant.onmicrosoft.com](mailto:admin@yourtenant.onmicrosoft.com)**」と入力し、 [**Next**] を選択します。

14. [**アカウントにサインイン]** ウィンドウで、「**[admin@yourtenant.onmicrosoft.com](mailto:admin@yourtenant.onmicrosoft.com)**」と入力し、[**Next**] を選択し、テナント パスワードを入力して、[**Sign in]** を選択します。

15. [**Connect your directories**] ページで、[**Contoso.com**] が **[FOREST]** の下に表示されていることを確認し、[**Add Directory]** を選択します。

16. [**AD フォレスト アカウント**] ウィンドウで、[**Create New AD Account]** オプションを選択し、[**ENTERPRISE ADMIN USERNAME**] フィールドに「**Contoso\Administrator**」と入力し、[**パスワード**] フィールドに「**Pa55w.rd**」と入力します。[**OK]** を選択し、[**Next**] を選択します。

17. **Microsoft Entra sign-in configuration** ページで、 **[USER PRINCIPAL NAME]** ドロップダウン リストで **userPrincipalName** 値が選択されていることを確認します。

18. **[Continue without matching all UPN suffixes to verified domains]** を選択し、[**Next**] を選択します。

19. [**Domain and OU filtering]** ページで、[**Sync selected domains and OUs]** を選択します。

20. **Contoso.com** を展開し、[**Contoso.com**] の横にあるチェック ボックスをオフにして、**IT**、 **Managers** 、**Marketing** 、 **Research** 、 および **Sales**の**チェック ボックスのみをオンとして、**[**Next**] を選択します。

21. [**次へ**] を３回クリックし、**インストール** をクリックします。

22. 構成が完了したら、 **[Exit]** を選択します。

    > 注: この時点で、ローカルの Active Directory ドメイン サービス (AD DS) と Entra ID からのオブジェクトの同期が開始されます。このプロセスが完了するまで約3〜4分待つ必要があります。または、同期サービス・アプリケーションで進行状況を確認します。

23. 開いているすべてのウィンドウを閉じます。

#### タスク2: Entra IDでの同期の確認

1. ブラウザーを起動します。

2. アドレスバーに「**[https://entra.microsoft.com](https://entra.microsoft.com/)**」と入力します。

3. サインイン プロンプトで、「**[admin@yourtenant.onmicrosoft.com](mailto:admin@yourtenant.onmicrosoft.com)**」と入力し、**次へ** を選択します。

4. [パスワードの入力] ページで、管理者アカウントのパスワードを入力し、[**サインイン]** を選択します。

   > 注: 管理者アカウントでのサインインに使用するパスワードについては、講師に確認してください。

5. [サインインしたままにする] プロンプトで、[**いいえ**] を選択します。Entra 管理センターが開きます。

7. Microsoft Entra 管理センターのナビゲーション ウィンドウで、 **[ユーザー]** を選択します。

8. ローカル AD DS のユーザーが表示されていることを確認します。これらのユーザーの [**オンプレミスの同期が有効**] 列に **[はい**] の値があることを確認します。

9. [ナビゲーション] ウィンドウで、[**グループ]** を選択し、[**すべてのグループ]** を選択します。ローカル AD DS のグループが表示されていることを確認します。これらのグループの [**ソース**] 列に **Windows Server AD** の値があることを確認します。

10. [**Managers**] グループを選択します。

11. **[Managers]** グループ ページで、[**メンバー]** を選択し、ユーザーが表示されていることを確認します。

    > このグループはローカル AD DS から提供されるため、このグループにメンバーを追加または削除することはできません。

**結果**: この演習を完了すると、Active Directory Domain Services から Entra ID に ID を同期するように Entra Connect が正常に構成されます。

**ラボの終わり**
