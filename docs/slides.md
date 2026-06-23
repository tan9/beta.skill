<!-- .slide: data-background-color="#0d1117" -->
# 培棠.skill

<p class="sub">把一個人，打包成一個檔案</p>

Note:
（這是倒數第二場，調性放輕鬆。）今天很實用 ── 我把我每天怎麼跟 AI 工作，打包成一個你們現在就能 clone 回去用的檔案。哲學的部分，留到最後一場。
（導覽：→ 換 section，↓ 在同一段裡往下。）

---

有個工具叫 dot-skill ──

<p class="sub">把一個人（同事、家人、偶像）蒸餾成一個 skill。<br>它的標語：把冷冰冰的告別，變成溫暖的 skill。</p>

Note:
（這就是我用來做 beta.skill 的工具 ── colleague-skill / dot-skill，github.com/titanwings/colleague-skill。）它主打的不是取代誰，是把一個人想事情、講話的方式保存下來 ── 標語直接寫「Transforming cold farewells into warm skills」。對一個要走的人來說，這個切入點剛剛好。

----

我就用它，<br>把**我自己**打包了。

<p class="creed">而且我老早就想被打包 ──<br>可被取代，不是末日，是修養。</p>

Note:
別人也許怕被一個檔案取代；我剛好相反 ── 我這快 19 年一直在做的，就是讓自己變得可被取代。所以把自己打包成一個誰都能 clone 的檔案，對我不是威脅，是交付完成的證明。

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

- 網頁應用 → 一對對 `request/response`
- PKI → 一條 `certificate chain`
- git → 一張 commit 的 `graph`，branch / merge / rebase 都在動它
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

<p class="sub">公司給了 Copilot，但多數人還停在「跟它 chat」。</p>

Note:
這段是你們最缺、別人最少講的。其實工具早就在手上了 ── 公司有提供 GitHub Copilot 訂閱（token 有限）。但現況是：很多人還不太熟怎麼用，或停在「開個對話框問它」的 chat 階段；就算有在用的，多半也還沒透過 CLI agent 把效益拉到最大。
所以重點不是「要不要用 AI」，是「在 OA 網路綁死、政府／金融合規、token 有限這些框框裡，怎麼從 chat 往『真正讓 agent 幹活』走」── 這也正是下一段「迴圈工程」要回答的。
（我自己私下還養了 Claude Code、Codex、Antigravity 幾家當試驗場，但那是個人摸索，公司環境裡的主力是 Copilot。）

----

## 重點不是下好一個 prompt，

<p class="creed">是設計一個迴圈。</p>

<p class="sub">給 goal、給一把尺，讓 agent 自己 iterate 到對。 ── 這就是「迴圈工程」(Loop Engineering)</p>

Note:
（2026 年由 Google 的 Addy Osmani 命名，延續 Peter Steinberger（OpenClaw）與 Anthropic 的 Boris Cherny 的概念；中文媒體譯為「迴圈工程」。出處：addyosmani.com/blog/loop-engineering/。）槓桿從「我每次下一個好 prompt」，變成「我設計一個迴圈」：給 agent 一個遞迴目標 ── 把測試弄綠、把這個模組重構但行為不變 ── 它就自己跑：看 → 改 → 驗證 → 讀結果 → 再決定，直到對。（beta.skill 跟這套東西的關係，下一張講。）

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

## beta.skill 是哪一塊？

automations · worktrees · **skills** · connectors · sub-agents · memory

<p class="sub">Loop Engineering 的積木（Addy Osmani）。他對 skill 的定義，就是<br>「一個放著 `SKILL.md` 的資料夾」── 你手上這個，就是這一塊。</p>

<p class="creed">我不是在追流行，<br>是這套東西剛好被命名了。</p>

Note:
Osmani 把 loop engineering 拆成這幾塊積木，其中「skill」他講得很白：把專案知識（這裡是「我的判斷」）寫進 SKILL.md，讓 agent 每一輪不用重講一遍 ──「A skill is how you stop re-explaining the same project context every session like a goldfish.」他還特別點名 Codex 跟 Claude Code 用的就是同一個 SKILL.md 格式。所以我今天給你們的這個 beta.skill，不是趕流行硬湊的，它本來就是 loop engineering 裡那塊 skill。（出處：addyosmani.com/blog/loop-engineering/）

----

## 誠實盤點：六塊，我踩到五塊

- **skills** ✅　beta.skill
- **connectors** ✅　az / gh / aws / kubectl / grafana
- **sub-agents** ✅　那把尺（測試 / 驗證）
- **worktrees** ✅　多版本平行維護　← 靠 git 基本功
- **memory** ✅　agent 自動處理（CLAUDE.md / 記憶檔）
- **automations** ✕　養過龍蝦（OpenClaw），訂閱禁程式介接後牠就死了

Note:
六塊踩到五塊 ── 而且 memory 這塊坦白說不是我厲害，是現在的 agent 自動幫你做了。Osmani 對 memory 的原話就是「一個活在對話之外的 markdown 檔」── 那不就是 CLAUDE.md / 記憶檔嗎？Claude Code 的 CLAUDE.md+記憶、Codex 的 AGENTS.md、Copilot 的 instructions 檔，各家都內建了，你連想都不用想。
真正還沒走到的，只剩 automations（自主排程的迴圈）。不是沒試 ── 我養過一隻龍蝦（OpenClaw ── github.com/openclaw/openclaw 🦞「The lobster way」，作者 Peter Steinberger 正是前面迴圈工程的奠基者之一），結果消費級訂閱禁止程式介接，牠就死了，這剛好是「在限制裡用 AI」最生動的反例。承認做不到，比假裝全能可信 ── 也呼應後面那句「我可能錯了」。

----

## worktree 玩得動，<br>是因為 git 基本功夠

<p class="creed">你敢讓 agent 在分支上亂搞，<br>是因為 rebase / reflog / worktree<br>你都收得回來。</p>

<p class="sub">git 就是你的 primitive ── 握得住它，才敢放 agent 跑。</p>

Note:
worktree、rebase、reflog、cherry-pick 這些基本功，不是老派，是你敢放手讓 agent 在程式碼上動刀的底氣。agent 搞砸了，你 reflog 找得回來、reset 收得掉 ── 這就是「握得住 primitive 才放它生」用在 git 上。基本指令練熟，比學任何花俏工具都值得。

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
〔現場操作〕打開 Claude Code，輸入 /beta，丟一段 code（或一個線上問題）進去。重點不是它會跑，是它的「判斷」長得像我，現場帶大家看兩個地方：
一、**先問 primitive**：它會先往底層追 ── 這是 request / response？一條 certificate chain？連線的生命週期？── 而不是急著給一段 patch。握得住底層，才有那把驗證的尺。
二、**分治本 / 治標**：它會明講這是「治標、只是止血」還是「治本」，不會把繞過問題講成解法 ── 這是我的招牌。
最後它一定收那句關不掉的「我可能錯了，自己去驗」。
（備援：若現場網路／環境出狀況，準備一段預錄的輸出截圖。）

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
<p class="cmd sm">git clone https://github.com/tan9/beta.skill.git ~/.claude/skills/beta</p>

<p class="sub">拿去用。然後告訴我哪裡像、哪裡不像。</p>

Note:
（收尾，把檔案真的交出去。）repo 在 github.com/tan9/beta.skill，clone 進你的 skills 目錄就能用。不藏私，連我怎麼準備這場分享，都攤給你看。
