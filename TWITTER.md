# 推特文案 — 分享 Architect Then Build 方法与 prompt

配套 skill 和 prompt 全文见: https://github.com/billypku/architect-then-build

---

## A. 中文主推

分享个我天天在用的方法,专治"Fable 太贵、token 不经烧"。

一句话:别让最贵的模型写代码,让它只写架构。

我把一个大任务拆成几个闸。前面的架构设计全程用 Fable,只出文档,我一条条审;定稿之后交给 GPT-5.5 照着一项项执行,每步跑测试卡着。Fable 几千 token 的架构,能管住后面一整晚的执行。它最强的判断力全用在最值钱的地方,代码那种又多又便宜的活,交给便宜量大的模型。

(执行这步我自己还做成了能通宵无人值守的 driver,碰危险操作就急停;但那部分跟我的实盘交易绑太死、不通用,就不分享了,只分享前面这套设计方法。)

prompt 和 Codex skill 我都整理好了 👇
https://github.com/billypku/architect-then-build

---

## B. English 主推

A workflow I use every day, for when your best model is too expensive to let loose.

One line: don't let your priciest model write code. Let it only write the architecture.

I split a big task into gates. The design gates run entirely on Fable — documents only, which I review line by line. Once the design is locked, GPT-5.5 executes it item by item with tests gating every step. A few thousand tokens of Fable-grade architecture steer a whole night of cheap execution, so the expensive model spends its judgment only where it actually pays off.

(I've also turned the execution stage into a driver that runs unattended overnight and hard-stops on anything dangerous — but that part is wired too tightly to my live trading setup to be general, so I'm only sharing the design method above, not that code.)

Copy-paste prompts and the Codex skill are here 👇
https://github.com/billypku/architect-then-build

---

## C. Thread 版(每条 280 内)

1/
分享个我天天用的方法,专治"最强的模型太贵、token 不经烧"。
一句话:别让最贵的模型写代码,让它只写架构。🧵

2/
为什么:架构定错,后面写得再对也白干;架构定对,执行就是体力活。
而设计恰恰最吃判断力、最省 token——一份想清楚的架构也就几千 token,却能管住一整晚的执行。所以最贵的模型只押在这一步。

3/
我把一个大任务拆成几个闸:
S1A 定方向
→ S1B 写到签名级
→ S1B 复审
→ S2 生成 build packet
→ S3 照清单单项执行
两条铁律:设计没定稿不进执行;转清单不许新增设计。

4/
S1A:先让 Fable 把一堆想法收敛成"方案对不对、缺什么、谁拍板"的文档。只谈方向、机制、取舍、风险,不许写接口、不许写代码。我不看代码就能审方向。

5/
S1B:再让 Fable 把方案细化到"别人照着能搭出同一套"——接口签名、数据结构、在哪个文件哪一行插进去、什么情况报错、动刀顺序。还是不写代码,写的是契约。

6/
S1B 复审:最好新开一个会话,让 Fable 当"对抗审查者",假设要证明这份架构不能交给 AI 照着写,逐条挑漏,把洞补进正文。这一关过了、我审了,设计才算定死。

7/
S2:把定稿架构喂给便宜的 GPT-5.5,机械转成 build packet:带验证命令的任务清单 + 执行契约 + blocker 列表。只转写,不做新设计;哪里不够细,回去补架构,不在清单里现编。

8/
S3:GPT-5.5 照清单一项项跑。守三条——一轮一项;测试你自己跑,别信它嘴上说"通过";每轮 git 提交一次,早上 git log 就是一整夜的账,哪轮歪了直接 revert。

9/
补一句:我自己有全自动 driver,内部版里 S2 compile、S3 arm/preflight、S4 run。但这块不 share——它围着我自己的实盘系统长的,大半是"在真钱旁边跑"的安全机制,不通用。公开版知道 S2 产包、S3 单项执行就够。

10/
说白了:方向和设计人 + 最强模型定死,后面的力气活交给便宜量大的模型。
prompt 和 Codex skill 在这 👇
https://github.com/billypku/architect-then-build

---

## D. 一句话(自己改口味)

别让最贵的模型写代码。让它只写架构,几千 token 的设计管住一整晚,代码交给便宜量大的模型执行。
