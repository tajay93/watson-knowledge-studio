---

copyright:
  years: 2015, 2018
lastupdated: "2018-04-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

此文件適用於 {{site.data.keyword.knowledgestudiofull}} on {{site.data.keyword.cloud}}。若要查看舊版 {{site.data.keyword.knowledgestudioshort}} on {{site.data.keyword.IBM_notm}} Marketplace 的文件，[請按一下此鏈結 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.bluemix.net/docs/services/knowledge-studio/troubleshooting.html){: new_window}。
{: tip}

# 疑難排解、支援與常見問題
{: #troubleshooting}

若要隔離並解決 {{site.data.keyword.IBM_notm}} 產品的問題，您可以使用疑難排解與支援資訊。此資訊包含使用隨 {{site.data.keyword.IBM_notm}} 產品（包括 {{site.data.keyword.knowledgestudiofull}}）提供的問題判斷資源的指示。
{: shortdesc}

## 疑難排解問題的技術
{: #ts_overview}

*疑難排解* 是用來解決問題的系統化方法。疑難排解的目標，在於判定某些功能不按預期運作的原因，以及如何解決該問題。某些常用技術可協助您進行疑難排解作業。

疑難排解程序的第一個步驟是完整說明問題。問題說明可協助您及 {{site.data.keyword.IBM_notm}} 技術支援代表知道從哪裡開始尋找問題的原因。此步驟包括詢問您自己一些基本問題：

- 問題的症狀為何？
- 問題發生的位置？
- 問題發生的時間？
- 問題是在哪些狀況下發生？
- 問題能否重新產生？

這些問題的答案通常會產生問題的最佳說明，從而引導您解決問題。

### 問題的症狀為何？

開始說明問題時，最常見的問題是「是什麼問題？」。這個問題看似直接明確；不過，您可以將它細分為數個更有針對性的問題，從而更詳細地說明問題。這些問題可能包括：

- 誰或哪個項目提報問題？
- 錯誤碼及訊息內容？
- 系統如何失敗？例如，是陷入迴圈、當機、損毀、效能降低，還是結果不正確？

### 問題發生的位置？

判斷問題的發生位置往往不容易，但它卻是解決問題的最重要步驟之一。報告元件與失敗元件之間可能存在許多技術層面。當您探索問題時，網路、磁碟和驅動程式只是少數幾個會考量到的元件。

下列問題可協助您專注在問題發生的位置，以隔離出問題層：

- 是否為單一平台或作業系統的特定問題，或是多個平台或作業系統的共同問題？
- 支援現行環境和配置嗎？
- 所有使用者都有這個問題嗎？
- （適用於多網站安裝。）所有網站都有這個問題嗎？

如果某一層報告問題，但問題不一定是出自該層。識別問題發生位置包括瞭解問題所在的環境。請花一些時間完整說明問題環境，其中包括作業系統和版本、所有對應的軟體和版本，以及硬體資訊。請確認您的執行環境是受支援的配置；許多問題的發生都可以追溯到不相容的軟體層次，可能未料到它們會一起執行，或尚未一起經歷完整的測試。

### 問題發生的時間？

請針對導致失敗的事件制定一份詳細的時間表，特別是那些只出現一次的情況。逆向運作可讓您輕鬆地制定時間表：從報告錯誤的時間開始（盡可能精確，甚至精細到毫秒），然後透過可用的日誌及資訊逆向運作。一般而言，只需要查看在診斷日誌中找到的第一個可疑事件即可。

若要制定事件的詳細時間表，請回答下列問題：

- 問題只發生在白天或夜晚的某個特定時段？
- 問題發生的頻率？
- 導致報告問題的事件順序？
- 問題是否發生在環境變更後（例如升級或安裝軟體或硬體）？

回應這些類型的問題可提供您調查問題的參考範圍。

### 問題是在哪些狀況下發生？

知道發生問題時有哪些系統及應用程式正在執行，是疑難排解的重要部分。這些環境相關問題可協助您識別問題的主要原因：

- 問題是否一律在您執行同一作業時發生？
- 是否需要發生一連串的特定事件之後，才會發生問題？
- 同一時間是否有任何其他應用程式失敗？

回答這類問題可協助您說明問題發生的環境，並找出所有相依關係的關聯性。請記住，只因為許多問題可能大致同時發生，並不表示這些問題彼此相關聯。

### 問題能否重新產生？

從疑難排解的角度來說，理想的問題是可以重新產生的問題。一般而言，當問題能夠重新產生時，您可以支配更多的工具與程序，以協助您進行調查。因此，可以重新產生的問題通常較容易除錯及解決。

不過，您可以重新產生的問題也可能有缺點：如果問題會產生重大業務衝擊，您不會希望它再次發生。如果可能的話，請在測試或開發環境中重建問題，這些環境通常可以在您的調查期間提供較多的彈性及控制。

- 問題能否在測試系統中重建？
- 是否有多位使用者或多個應用程式發生相同類型的問題？
- 問題能否藉由執行單一指令、一組指令或特定的應用程式重建？

## AlchemyLanguage 模型問題
{: #wks_ts_deployed_model_deleted}

### 問題

您無法部署 AlchemyLanguage 模型，或者部署成功，但模型無法使用。

### 症狀

- 您已部署模型，但狀態顯示發生錯誤。
- 您已部署模型且狀態指出模型可用，但您無法使用。
- 已順利部署模型且之前可以運作，但現在無法運作。

### 原因

下列事件可能會導致已部署的模型發生問題：

- 如果您在將金鑰新增至 REST API 呼叫的 `apikey` 參數時，打錯 {{site.data.keyword.alchemyapishort}} 金鑰，則此呼叫會失敗。對於模型 ID 也一樣。最好是複製並貼上模型 ID 及 API 金鑰，以避免打錯。
- 如果您提供無效的 {{site.data.keyword.alchemyapishort}} 金鑰，或未獲授權可部署自訂模型，則部署程序會指出已順利部署模型，但您將無法使用。
- 在 {{site.data.keyword.Bluemix}} 中使用 {{site.data.keyword.alchemylanguageshort}} 時，如果您刪除所有與 {{site.data.keyword.Bluemix_notm}} 中 {{site.data.keyword.alchemyapishort}} 金鑰相關聯的服務實例，則任何參照該金鑰的已部署模型都將從服務中移除。{{site.data.keyword.Bluemix_notm}} 會定期檢查已登錄的模型是否與有效金鑰相關聯，以及是否已刪除所有未與其相關聯的模型。如果您的模型是針對已刪除的金鑰而部署的，則模型的狀態會變更為 `error`。

### 解決問題

1. 檢查部署的狀態。

    以 {{site.data.keyword.knowledgestudioshort}} 管理者身分登入。在**模型管理** > **版本**頁面上，檢視**狀態**直欄，以檢查已部署之模型的狀態。

1. 如果模型的部署狀態是 `error` 或狀態是 `available`，但當您嘗試使用模型時，模型無法運作，請按一下**取消部署**來撤銷模型的部署。
1. 重新部署模型。

    只使用有權部署模型的有效 {{site.data.keyword.alchemyapishort}} 金鑰，並在將模型 ID 及 API 金鑰作為參數新增至 API 呼叫時，複製並貼上它們。

**相關作業**：

[將機器學習模型部署至 {{site.data.keyword.IBM_notm}} {{site.data.keyword.alchemylanguageshort}}](/docs/services/watson-knowledge-studio/publish-ml.html#wks_mabluemix)

## 無法建立免費帳戶
{: #wks_ts_free}

### 問題

您嘗試建立免費帳戶，但看到錯誤訊息：`Error 331: We are unable to process your request. Please try again later or contact the {{site.data.keyword.IBM_notm}} Helpdesk.`

### 原因

{{site.data.keyword.knowledgestudioshort}} 不允許每個組織有多個免費帳戶。

### 解決問題

建立不包括在組織中的帳戶。

如果您需要使用現行帳戶來進行免費試用，且您的使用者帳戶與付費帳戶相關聯，則可以提交支援問題單。如需相關資訊，請參閱[與 {{site.data.keyword.IBM_notm}} 支援中心聯絡](/docs/services/watson-knowledge-studio/troubleshooting.html#ts_contactingibmsupport)。

如果您需要使用現行帳戶來進行免費試用，但您的使用者帳戶未與付費帳戶相關聯，請將您的問題張貼至 [{{site.data.keyword.IBM_notm}}developerWorks Answers](https://developer.ibm.com/answers/topics/wks/)，確定將問題標記為 **WKS**。

## 無法存取應用程式
{: #wks_ts_access}

瞭解如何授權使用者存取 {{site.data.keyword.knowledgestudioshort}}，以及解決常見的存取問題。

您必須具有 {{site.data.keyword.IBM_notm}} 使用者登錄認證，才能要求 {{site.data.keyword.IBM_notm}} {{site.data.keyword.knowledgestudioshort}} 的實例。

### 管理者

每一個 {{site.data.keyword.knowledgestudioshort}} 實例都有一個與其相關聯的管理者角色。最初註冊使用此應用程式的人員會自動獲得管理者角色。管理者可以邀請其他人員。

如需如何邀請人員使用您的應用程式實例的相關資訊，請參閱[組合團隊](/docs/services/watson-knowledge-studio/team.html)。

### 註釋人員

如果您已受邀使用某人的 {{site.data.keyword.knowledgestudioshort}} 實例，以作為註釋人員，則可能會收到電子郵件邀請。首先，如果您還沒有 {{site.data.keyword.IBM_notm}} 登錄認證，則必須向 {{site.data.keyword.IBM_notm}} 登錄。在向 {{site.data.keyword.IBM_notm}} 登錄並接受邀請之後，您即獲授與實例的存取權。不過，在您獲授與存取權之後，以及在您開始註釋文件之前，管理者或實例的專案經理必須將您新增至工作區，並將註釋作業指派給您。直到您獲指派作業之後，才可在 {{site.data.keyword.knowledgestudioshort}} 實例中執行任何動作。若要註釋文件，請使用基準編輯器。使用 Google Chrome 瀏覽器以獲得最佳效能。

如需使用基準編輯器的說明，請參閱[註釋文件](/docs/services/watson-knowledge-studio/user-guide.html)。

## 實驗性服務：*實驗性* 是什麼意思？
{: #experimental}

如需實驗性服務的相關資訊，請參閱 [{{site.data.keyword.Bluemix_notm}} 文件](/docs/services/index.html#experimental_services)。如需實驗性服務的完整資料，請參閱最新版本的 [{{site.data.keyword.Bluemix_notm}} 服務說明 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/software/sla/sladb.nsf/searchsaas/?searchview&searchorder=4&searchmax=0&query=IBM+Bluemix+Service+Description){: new_window}。

## 儲存空間問題
{: #storage}

取決於您的訂閱方案，您可能達到方案指定的儲存空間限制，因而阻止您執行您要完成的作業。

### 症狀

嘗試執行下列其中一項作業時，您可能會看到關於已超出容許之儲存空間的訊息：

- 上傳文件或字典
- 部署模型或版本模型
- 對文件執行預先註釋程式

### 原因

已達到儲存空間限制，或如果要繼續執行動作，將會超出此限制。

### 解決問題

儲存空間的最大消耗者是機器學習及規則型模型。若要釋放空間，您可以採取下列動作：

- 刪除您不需要回復到的任何模型的 Snapshot 版本。
- 刪除任何您不需要的模型。
- 如果您的模型太重要而無法刪除，請考量將您的方案升級至提供更大儲存空間配置的方案。

在移除模型或模型版本之後，請先等待一小時，然後再重試導致錯誤訊息的動作。您釋放的儲存空間可能需要長達一個小時才能使用。

若要管理每月帳單，如果已將 Admin 角色指派給您，且您具有「超值」或「標準」帳戶，則您可以在 {{site.data.keyword.knowledgestudioshort}} 的「服務詳細資料」頁面上設定儲存空間限制。若要查看「服務詳細資料」頁面並設定儲存空間限制，請從 {{site.data.keyword.knowledgestudioshort}} 的頂端導覽列中，按一下**設定**圖示，按一下**檢視/修改服務詳細資料**鏈結，然後按一下**設定儲存空間限制**鏈結。
{: tip}

## 與 IBM 支援中心聯絡
{: #ts_contactingibmsupport}

「{{site.data.keyword.IBM_notm}} 支援中心」提供產品問題報告協助、回答常見問題，以及協助使用者解決產品問題。

### 開始之前

首先，請查看是否有記載您所遭遇問題的解決方案。在「[{{site.data.keyword.IBM_notm}} 支援入口網站」![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/support/home/entry/portal){: new_window} 上搜尋 {{site.data.keyword.knowledgestudioshort}}。在搜尋結果頁面上，按一下**支援**標籤，以查看來自 TechNotes、{{site.data.keyword.IBM_notm}} Redbooks 及文件的結果。按一下**適用於開發人員**標籤，以查看來自 {{site.data.keyword.IBM_notm}} developerWorks 社群的結果，例如部落格及討論區問題。

在嘗試搜尋「[{{site.data.keyword.IBM_notm}} 支援入口網站」![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/support/home/entry/portal){: new_window} 來尋找答案或解決方案之後，您可以與「{{site.data.keyword.IBM_notm}} 支援中心」聯絡。您具有的支援類型取決於您的服務類型。

- **免費方案使用者**

    藉由詢問開發人員社群的會員，來取得問題的協助及回答。如需開發人員社群的鏈結，請參閱目錄中的**開發人員社群**一節。

- **付費方案使用者**

    身為付費方案使用者，您也可以提出問題，並從其他使用者的問題中學習。討論區開放每個人使用，是一個開始的好地方。如需鏈結，請參閱目錄中的**開發人員社群**一節。

    從「[{{site.data.keyword.IBM_notm}} 雲端服務入口網站」![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://watson.service-now.com/wcp){: new_window} 提交問題單。

    > **附註：**您必須已獲授權，才能將問題提交給 {{site.data.keyword.IBM_notm}}。

### 程序

若要與「{{site.data.keyword.IBM_notm}} 支援中心」聯絡來解決問題，請執行下列動作：

1. 定義問題、收集背景資訊並判斷問題的嚴重性。
1. 收集診斷資訊（如果可能的話）。
1. 將問題提交給「{{site.data.keyword.IBM_notm}} 支援中心」。如需聯絡詳細資料，請參閱[軟體即服務 (SaaS) 支援手冊 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www-01.ibm.com/software/support/acceleratedvalue/SaaS_Handbook_V18.pdf){: new_window}。
