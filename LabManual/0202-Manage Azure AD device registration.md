# ラボ 0202: Entra ID デバイス登録の管理



## 概要



このラボでは、Windows デバイスを使用して Entra 登録を実行します。

## 演習 1: Entra デバイス登録の構成



### シナリオ



何人かのユーザーが、個人の iOS、Android、Windows デバイスを使用して Contoso クラウド リソースにアクセスするように依頼しています。Contoso は Windows デバイスを所有していないため、ユーザーに Entra 参加を実行させたくありません (Entra に参加できるのは WIndows デバイスのみです)。代わりに、ユーザーが自分のデバイスを Entra に登録できるようにし、必要に応じて会社のポリシーをアプリに適用し、ユーザーが Contoso リソースにアクセスできるようにする必要があります。Windows 11 デバイスを使用して Entra デバイスの登録をテストします。

### タスク1: Entra IDデバイス登録の構成

1. ブラウザーでアドレス バーに **[「https://entra.microsoft.com](https://entra.microsoft.com/)** 」と入力して、**Enter キー**を押します。

2. ユーザーとしてサインインし、テナント管理者パスワードを使用します。[**サインインしたままにする?]** プロンプトが表示されたら、[**いいえ**] を選択します。`Admin@yourtenant.onmicrosoft.com`

   > Microsoft Entra 管理センターが開きます。

3. Microsoft Entra 管理センターのナビゲーション ウィンドウで、 **[デバイス]** を選択し、[**すべてのデバイス**] を選択します。

4. **デバイス上 |[すべてのデバイス]** ページで、[**デバイス設定**] を選択します。

5. **デバイス上|デバイス設定**ページの詳細ウィンドウで、 **[ユーザーがデバイスを Microsoft Entra に登録できる]** が [**すべて**] に設定され、淡色表示されていることを確認します。

   > このオプションは淡色表示され、テナントで Microsoft Intune が有効になっている場合、既定で **[すべて]** に設定されます。これにより、すべてのユーザーが Windows 10 以降の個人用、iOS、Android、macOS デバイスを Entra に登録できるようになります。

### タスク2: Entra登録の実行

1. **SEA-WS1** に切り替え、**Pa55w.rd** のパスワードで**管理者**としてサインインします。
2. タスク バーで、[**Start （Windowsアイコン）]** を選択し、[**Settings]** を選択します。
3. [**Settings**] ウィンドウで、[**Accounts]** を選択します。
4. [Accounts] ページで、[**Access work or school**] を選択します。
5. [**Access work or school**] ページで、[**Connect]** を選択します。
6. **[Microsoft アカウント**] ウィンドウの [メール アドレス] ボックスに「**`JoniS@yourtenant.onmicrosoft.com`**」と入力し、[**次へ**] を選択します。
7. [**Sign in**] ページで、「**[JoniS@yourtenant.onmicrosoft.com](mailto:JoniS@yourtenant.onmicrosoft.com)**」と入力し、[**次へ**] を選択します。
8. [**Enter password**] ページで、インストラクターから提供されたテナント パスワード(User password)を入力し、[**Sign in]** を選択します。
9. **Account added to this device** ページで、[**Done]** を選択します。
10. [Access work or school] ページで、「[JoniS@yourtenant.onmicrosoft.com](mailto:JoniS@yourtenant.onmicrosoft.com)」と [Work or school account] が表示されていることを確認します。
11. [Settings] ページを閉じます。

### タスク 3: Entra 登録の検証

1. [**スタート（Windowsアイコン）]** を右クリックし、[**Windows Terminal (Admin)]** を選択します。

2. **Windows PowerShell** ウィンドウで、次のコマンドを入力し、**Enter キー**を押します。

   ```
   dsregcmd /status
   ```

   

3. [**User State]** の下の出力で、 [**WorkplaceJoined: YES]** が表示されていることを確認します。これは、ユーザーが Entra ID でデバイス登録を実行したことを示します。

4. PowerShell を閉じてから、SEA-WS1 からサインアウトします。

5. ブラウザー の Microsoft Entra 管理センターで、[**Entra ID**] を展開します。

6. **[デバイス]** を選択し、[**すべてのデバイス**] を選択します。[デバイス(Devices)] ペインに、SEA-WS1 がリストされていることに注意してください。

7. [**参加の種類]** が **[Microsoft Entra 登録済み**] として一覧表示され、所有者が **Joni Sherman** であることを確認します。

   > デバイスは Microsoft Entra に登録されており、Microsoft Entra に参加しているわけではありません。Entra 登録済みデバイスは、通常、Entra に参加できないデバイス、またはユーザーが個人的に所有するデバイスです。デバイスを登録すると、クラウドベースのリソースにアクセスできるようになります。

8. Microsoft Edge を閉じます。

### タスク4: Windowsにサインインし、組織から切断する



1. **SEA-WS1** に切り替えると、Entra Joined デバイスや Entra Hybrid Joined デバイスとは異なり、Entra 登録済みデバイスではローカル アカウントのみを選択できることに気付きます。

2. SEA-WS1 で、**パスワード Pa55w.rd** を使用して**admin**としてサインインします。

3. タスク バーで、[**Start （Windowsアイコン）]** を選択し、[**Settings]** を選択します。

4. [**Settings**] ウィンドウで、[**Accounts]** を選択します。

5. [Accounts] ページで、[**Access work or school**] を選択します。

6. [**Access work or school**] ページで、[**Connect]** を選択します。

7. [**Access work or school**] ページで、**JoniS** 職場または学校アカウントを選択します。

8. [Disconnect this account] の横にある [**Disconnect **] を選択し、[**Yes**] を選択します。

   > 登録済みデバイスを Azure AD から切断するために再起動する必要はありません。

9. 今後のラボの準備のため、SEA-WS1を再起動します。

**結果**: この演習を完了すると、Entra デバイスの登録が構成されます。

**ラボの終わり**