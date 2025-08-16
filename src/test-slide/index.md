---
marp: true
theme: hanaseleb
paginate: true
footer: 'proofpoint'
style: |
  /* タイトルのはみ出し防止と全体バランス */
  section h1 { font-size: 1.8em; line-height: 1.2; }
  section h2 { font-size: 1.2em; }
  p.small { font-size: 0.9em; color: #555; }
---

# <!-- fit --> FIDO認証のダウングレード攻撃  
2025年8月12日  
proofpoint  
_出典: proofpoint.com_

---

![w:1000](https://www.proofpoint.com/sites/default/files/styles/metatag/public/blog%20banners/Blog-bannar_building.png.webp?itok=QrCHR7yR)  
*FIDO認証の重要性*  
_source: proofpoint.com_

---

### Key takeaways  
- FIDOベースのパスキーは、一般的な認証情報フィッシングやアカウント乗っ取りに対する推奨認証方法です。  
- FIDOベースの認証がダウングレード攻撃により回避される可能性があります。  
- 攻撃者は専用のフィッシュレットを使用し、FIDO認証をより安全でない方法にダウングレードさせることができます。  
- 現在、FIDO認証ダウングレード攻撃は観測されていません。  
- ダウングレード攻撃は「フィッシング耐性」認証方法に対する重要な手法です。  

---

### Overview  
組織が進化する脅威に対応しようとする中で、FIDO認証の採用がオンラインセキュリティを大きく向上させています。しかし、最近の研究でFIDOベースの認証メカニズムをダウングレードする脅威ベクターが発見されました。

---

### Modern phishing, AiTM style  
FIDO標準以前、現代の認証情報窃盗手法はフィッシング技術に依存していました。AiTM攻撃は、フィッシングメッセージから始まり、偽のログインページに誘導します。

---

### FIDO  
FIDOはオンライン認証を強化するために開発されたオープンスタンダードのセットです。FIDOは従来の認証情報の必要性を排除し、フィッシングの脅威を軽減します。

---

### The proof is in the phishlet  
フィッシング攻撃はFIDO-securedアカウントに対して失敗することが多いです。フィッシュレットは、正当なウェブサイトを模倣し、ユーザーの認証情報を傍受するためのテンプレートです。

---

![w:500](https://www.proofpoint.com/sites/default/files/inline-images/Screenshot%202025-08-11%20at%202.25.30%E2%80%AFPM.png)  
*フィッシュレットのエラー表示*  
_source: proofpoint.com_

---

### FIDO downgrade attack execution  
特定のFIDOベースの認証実装は、ダウングレード攻撃に対して脆弱です。この攻撃は、ユーザーをより安全でない認証方法に戻すことを強制します。

---

#### User agent spoofing  
一部のブラウザはFIDO2認証をサポートしていません。攻撃者はこれを利用して、ユーザーをより安全でない方法で認証させることができます。

![w:1000](https://www.proofpoint.com/sites/default/files/inline-images/Screenshot%202025-08-11%20at%202.26.47%E2%80%AFPM.png)  
*FIDO2認証のサポート状況*  
_source: proofpoint.com_

---

#### Authentication downgrade flow  
Proofpointの研究者は、Evilginx AiTM攻撃フレームワーク用の特別なフィッシュレットを作成しました。攻撃の流れは以下の通りです。  
- **初期インタラクション**: フィッシングリンクがターゲットに送信されます。  
- **認証ダウングレード**: ターゲットがフィッシングリンクをクリックすると、認証エラーメッセージが表示され、代替のサインイン方法を選択するよう促されます。  

---

![w:600](https://www.proofpoint.com/sites/default/files/inline-images/Screenshot%202025-08-11%20at%202.28.43%E2%80%AFPM.png)  
*サインインエラーメッセージ*  
_source: proofpoint.com_

---

- **認証情報とMFAトークンの盗難**: ターゲットが偽のインターフェースを使用して認証すると、攻撃者は認証情報を傍受できます。  
- **セッションハイジャックとアカウント乗っ取り**: 攻撃者は、盗まれたセッションクッキーを自分のブラウザにインポートし、アカウントにアクセスします。  

--- 


![w:1200](https://www.proofpoint.com/sites/default/files/inline-images/Screenshot%202025-08-11%20at%202.29.14%E2%80%AFPM.png)  
*Evilginxのセッションリスト*  
_source: proofpoint.com_

---

### User accounts remain at risk  
ダウングレード攻撃は、攻撃者がより安全でない方法で認証させることを可能にします。これにより、認証情報やセッションクッキーが盗まれ、アカウント乗っ取りにつながる可能性があります。

---

- **低い努力の代替手段**: 多くの攻撃者は、よりシンプルな攻撃パスを選んでいます。  
- **技術的なスキル**: ダウングレード攻撃を実行するためには、専門的な知識が必要です。  

---

### 参考  
[Proofpoint Blog](https://www.proofpoint.com/us/blog/threat-insight/dont-phish-let-me-down-fido-authentication-downgrade)  
[Credential Phishing](https://www.proofpoint.com/us/threat-reference/phishing)  
[Account Takeover (ATO)](https://www.proofpoint.com/us/threat-reference/account-takeover-fraud)  
[FIDO-based authentication](https://fidoalliance.org/passkeys/)  
[Multi-Factor Authentication (MFA)](https://www.proofpoint.com/us/threat-reference/multifactor-authentication)  
[FIDO Alliance](https://fidoalliance.org/)  
[Evilginx AiTM attack framework](https://github.com/kgretzky/evilginx2)  
[Microsoft Entra ID FIDO2 Compatibility](https://learn.microsoft.com/en-us/entra/identity/authentication/concept-fido2-compatibility?tabs=web#web-browser-support)  