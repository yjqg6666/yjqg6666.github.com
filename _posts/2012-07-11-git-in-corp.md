---
layout: default
title: git在公司内部的使用实践
published: true
category: git
tags: [git,公司,开发,流程]
---
<div id="detail" class="detail" style="line-height: 1.3;"><p>自&nbsp;http://zeroq.me/p/451 &nbsp;作者: zeroq<div class="vimiumReset vimiumHUD" style="right: 150px; opacity: 0; display: none; "></div><div><br></div><div><p>从2011.10月左右，开始在后台组推行git版本控制，到现在也差不多半年了，也形成了一套基于git flow的副官模式工作流程：</p>
版本定义：
<p>版本号使用x.x.x进行定义，第一个x代表大版本只有在项目有重大变更时更新<br>
第二个x代表常规版本有新需求会更新<br>
第三个x代表紧急BUG修正<br>
一个常见的版本号类似于：0.11.10</p>
分支定义：
<ul>
<li>master分支对应线上版本，上线都使用master；</li>
<li>develop是开发分支，用于生成提测分支release，始终保持最新；</li>
<li>hotfix是紧急分支，从master生成，bug修正后自动合并到master和develop并且生成tag；</li>
<li>feature是私有分支，用于开发新需求和需要较长时间的BUG修改</li>
<li>release是提测分支也即常规分支，测试并且bug修改结束后生成该版本tag，后续可以使用git show tagname来查看版本信息或者回滚</li>
</ul>
工程师：
&nbsp;&nbsp;&nbsp;&nbsp; <strong>clone版本库后，首先git flow init初始化工作目录。</strong>
&nbsp; 开发工作流程：
<ol>
<li>git flow feature start xxxxx（开始新需求）</li>
<li>在feature/xxxxx分支下进行开发</li>
<li>git flow feature finish xxxxx（开发完成后等待研发经理确认可以完成时执行）</li>
<li>git push origin develop（发布develop分支）</li>
</ol>
<ul>
<li><span style="color: #ff0000;">每天工程师都需要git pull origin develop来更新develop分支，然后将develop分支合并到你正在开发得feature/xxxxx分支上来保持代码最新</span></li>
<li><span style="color: #ff0000;">切记不能直接在develop上进行开发</span></li>
</ul>
&nbsp; 常规分支debug流程：
<ol>
<li>由研发经理通知相关工程师release版本x.x</li>
<li>git fetch</li>
<li>git checkout -b release/x.x origin/release/x.x（拉回release版本）</li>
<li>git pull release/x.x（更新该分支）</li>
<li>修改测试中发现的BUG</li>
<li>git push origin release/vx.x（修改完后提交分支）</li>
<li>循环4-5</li>
</ol>
&nbsp; 紧急debug流程：
<ol>
<li>由研发经理通知相关工程师hotfix分支名称x.x.x</li>
<li>git fetch</li>
<li>git checkout -b hotfix/x.x.x origin/hotfix/x.x.x（拉回hotfix分支）</li>
<li>git pull hfx.x（更新hotfix分支）</li>
<li>在热修复分支下修改bug</li>
<li>git push origin hfx.x（修改完成，提交分支）</li>
</ol>
&nbsp; <span style="color: #ff0000;">在日常工作中不能修改master分支下得代码</span>
研发经理：
&nbsp; <span style="color: #ff0000;">开发和DEBUG流程同工程师流程</span>
&nbsp; 常规分支debug流程：
<ol>
<li>git pull origin develop（更新develop分支为最新）</li>
<li>git checkout develop（切换到develop分支）</li>
<li>git flow release start x.x（生成一个release分支）</li>
<li>通知测试和相关得工程师分支名称</li>
<li>git pull origin release/x.x（最终测试完成后拉回分支最新代码）</li>
<li>git flow release finish x.x（最终修改和测试完成后，结束release版本以供发布）</li>
<li>git push origin develo (发布最新的develop)</li>
<li>git push origin master（发布最终得master分支）</li>
</ol>
&nbsp; 紧急debug流程：
<ol>
<li>&nbsp;git pull origin master（更新master分支为最新）</li>
<li>&nbsp;git checkout master（切换到master分支）</li>
<li>&nbsp;git flow hotfix start x.x.x（生成一个hotfix分支）</li>
<li>&nbsp;通知相关得工程师和测试人员hotfix分支名称</li>
<li>&nbsp;git pull origin hotfix/x.x.x（最终测试完成后拉回分支最新代码）</li>
<li>&nbsp;git flow hot fix finish x.x.x（最终修改和测试完成后，结束hot fix以供发布）</li>
<li>&nbsp;git push origin master（发布最终得master分支）</li>
</ol>
<p>&nbsp;</p>
<p>在全部的流程中，工程师必须维护自己的feature分支保证代码最新，减少合并时的冲突。<br>
研发经理必须维护release分支，将最新的hotfix都合并进去，保证代码最新，减少合并时的冲突。<br>
在提交代码时还要注意判断对代码的修改是否是自己的，多用diff工具，多查看log，防止代码回溯</p></div></p></div>
