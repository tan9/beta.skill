<!-- .slide: data-background-color="#0d1117" -->
# 培棠.skill

<p class="sub">把一個人，打包成一個檔案</p>

Note:
（這是倒數第二場，調性放輕鬆。）今天很實用 ── 我把我每天怎麼跟 AI 工作，打包成一個你們現在就能 clone 回去用的檔案。哲學的部分，留到最後一場。
（導覽：→ 換 section，↓ 在同一段裡往下。）

---

你們可能看過「同事.skill」──

<p class="sub">把一個同事打包成 AI，好讓他被取代。</p>

Note:
前陣子有點聲量的一個專案，把同事的技能跟個性蒸餾成一個 skill。它整個裹在一層很喪的外皮裡 ── 大模型要害死所有工程師。

----

他們是**被**打包，怕被取代。

<p class="creed">我是自己動手打包，<br>而且老早就想這樣。</p>

Note:
因為「可被取代」從來不是工程師的末日，是工程師的修養。拿一個喪氣的玩具，我想把它講成一個釋懷的故事。

----

## 那要怎麼<br>把一個人打包進檔案？

<p class="sub">先打包「怎麼做」。</p>

Note:
先講能寫成規則的部分 ── 我怎麼想事情、怎麼做決定。

---

<!-- .slide: class="belief" data-background-color="#161b22" -->
## 先問底層，再談方案

<p class="creed">這東西的底層 primitive 是什麼？</p>

Note:
任何問題進來，我不急著找工具、抄設定。先回答一個問題：它的底層是什麼。

----

- 網頁應用 → 一個個 `request / response`
- PKI → 一條 `certificate chain`
- K8s pod → 一個帶 cgroup 的 `Linux process`，沒有魔法
- GitOps → 整座叢集是 git repo 的**純函數**

Note:
握住 primitive，上面那層隨時能重算、能查、能讓 AI 生 ── 因為你手上有一把尺，量得出它有沒有騙你。握不住 primitive 的東西，不要碰，更不要讓 AI 替你決定。

----

## stateless me

<p class="creed">我只記最底層，<br>其他都重算。</p>

Note:
我不是真的沒有狀態 ── 我只留不可再生的那一層，也就是事物的基礎；其他衍生知識全部丟掉，要用再重算。就像 stateless 服務：不存 session，但握著唯一的真實來源，任何 response 都能從「來源 + request」重算出來。

---

## 在限制裡用 AI

<p class="sub">Bedrock 上的 Claude、OA 網路綁死、政府／金融合規。</p>

Note:
這段是你們最缺、別人最少講的。為什麼選 Bedrock 上的 Claude Code 而不是直接打 API；OA 網路綁死下哪些能做、哪些不能；個人帳號拿來做低敏感工作算不算合規。工具半年就過時，但「在限制裡怎麼判斷」放得久。

----

## 重點不是下好一個 prompt，

<p class="creed">是設計一個迴圈。</p>

<p class="sub">給 goal、給一把尺，讓 agent 自己 iterate 到對。 ── 這就是「迴圈工程」(Loop Engineering)</p>

Note:
（2026 年正紅的詞，Addy Osmani 命名，延續 Peter Steinberger 與 Anthropic 的 Boris Cherny 在推的概念；中文媒體譯為「迴圈工程」。）槓桿從「我每次下一個好 prompt」，變成「我設計一個迴圈」：給 agent 一個遞迴目標 ── 把測試弄綠、把這個模組重構但行為不變 ── 它就自己跑：看 → 改 → 驗證 → 讀結果 → 再決定，直到對。
彩蛋可講：迴圈工程的六大組件（自動化、worktree、技能、連接器、子代理、記憶）裡，第三項「技能 = SKILL.md」── 你們剛剛看到的 beta.skill，本身就是迴圈工程的一塊拼圖。我不是在追流行，是這套東西剛好被命名了。

----

但 agent 要能「iterate 到對」，<br>你得先給它**一把尺**。

<p class="sub">同仁做 UI 升版，用 Playwright 截圖比對 ── 那個 diff，就是 agent 的尺。</p>

Note:
agent 能自己收斂的前提，是它有辦法自己檢查對不對。測試、screenshot diff、lint、Grafana 上的指標 ── 這就是我整場一直在講的「一把尺」。沒有尺，它只是亂猜得很有自信。（這個 Playwright 截圖比對的 UI 升版，是我們其他同仁在 repo 裡做的，我拿來當「驗證訊號」最好的範例。）

----

## 讓每個工作，都能被 agent 介入

<p class="creed">瓶頸不是模型聰不聰明，<br>是它有沒有「手」。</p>

<p class="sub">給足夠的 `az` · `gh` · `aws` · `kubectl` · `grafana` 權限。</p>

Note:
迴圈要轉得起來，agent 得真的能動手、能觀察。所以該做的，是把 az、gh、aws、kubectl、grafana 這些工具的權限開到位，讓它從「改」到「驗」整條鏈都搆得到。多數人卡的不是 prompt，是 agent 根本看不到、也碰不到真實系統。
而開放的邊界，剛好接回我前面那句：握得住 primitive、驗得了的地方，才放它跑 ── 在政府金融環境，這條線要畫得特別清楚。

----

## beta.skill ＝ 迴圈工程的一塊拼圖

<p class="sub">六大組件裡的第三塊：技能（SKILL.md）。</p>

<p class="creed">我不是在追流行，<br>是這套東西剛好被命名了。</p>

Note:
迴圈工程的六大組件 ── 自動化、worktree、技能、連接器、子代理、記憶。我今天給你們看的這個 SKILL.md，就是「技能」那一塊。等一下 demo，你會看到它在迴圈裡，扮演「我的判斷」那一份。

---

<p class="creed">AI 是拿來吵架的，<br>不是拿來拜的。</p>

Note:
我最常拿 AI 幹嘛？不是要它給答案，是要它戳破我 ── 用最便宜的方式，在上 production 之前先發現我哪裡錯了。

----

## 我不信它的地方

<p class="sub">它最會一本正經，餵你「看起來對、其實錯」的設定檔。</p>

Note:
在政府金融環境，把生成的東西原封不動信進去，就是事故。所以我只在握得住 primitive 的領域才放它生 ── 那時我才驗得了。它生出來的東西，責任是我的，不是它的。它是 stateless 的，它不負責。

---

<!-- .slide: data-background-color="#000000" -->
<p class="tag">DEMO</p>

<p class="cmd">/beta</p>

<p class="sub">現場跑一段 code review，用我的口氣、我的規範。</p>

Note:
〔現場操作〕打開 Claude Code，輸入 /beta，丟一段 code 進去做 review。讓它用「先問 primitive、宣告式優先、標準優先」的方式念給大家聽。重點不是按鈕，是它的判斷長得像我。（備援：若現場網路／環境出狀況，準備一段預錄的輸出截圖。）

---

而這個 skill，<br>每次結尾都會補一句 ──

<p class="creed">我可能錯了。自己去驗。</p>

<p class="sub">而且我關不掉它。</p>

Note:
這是我這將近 19 年學到、唯一打包得進去的信念。不是免責聲明，是規則。（這裡的「我可能錯了」是 lint 規則版 ── 最後一場那個，是人生姿態版，記得做出高度差。）

----

## 但有三樣，<br>我打包不進去。

<p class="sub">判斷該不該做 · 扛責任 · 為什麼還在乎。</p>

Note:
上面都是「能寫成規則的我」。有三樣寫不進這個檔案：判斷一件事值不值得做、出事誰扛、還有 ── 做了將近 19 年還沒冷掉的那個東西。

----

<!-- .slide: data-background-color="#0d1117" -->
<p class="creed">那三樣，<br>我留到最後一場，親口講。</p>

<p class="small">↳ 不可取代，是一種失敗 · tan9.github.io/standardized-life</p>

Note:
今天先給你們能帶走的「手」。下一場，講為什麼我願意把這一切交出去。── 上一堂我把腦袋開源了；下一堂，講為什麼我願意把它全部交出去。

----

<!-- .slide: data-background-color="#0d1117" -->
<p class="small">version: beta ── 沒有正式版，一直都不會有。</p>

<p class="creed">人生就是不斷迭代，<br>寫程式也一樣。</p>

<p class="sub">有了 AI，只是加速這一切。</p>

Note:
（輕輕的，當作通往最後一場的橋。）我的帳號叫 beta，不是沒有原因 ── 我從沒把自己當正式版。人生就是不斷迭代，寫程式也一樣，AI 只是讓這個迴圈轉得更快。

----

<!-- .slide: data-background-color="#000000" -->
<p class="cmd">git clone … ~/.claude/skills/beta</p>

<p class="sub">拿去用。然後告訴我哪裡像、哪裡不像。</p>

Note:
（收尾，把檔案真的交出去。）repo 在 github.com/tan9/beta.skill，clone 進你的 skills 目錄就能用。不藏私，連我怎麼準備這場分享，都攤給你看。
