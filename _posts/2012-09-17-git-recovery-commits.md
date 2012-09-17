---
layout: default
title: git恢复丢失的提交
published: true
category: git
tags: [git,提交,恢复,找回]
---
<div id="detail" class="detail" style="line-height: 1.3;">
# [转载](http://www.programblings.com/2008/06/07/the-illustrated-guide-to-recovering-lost-commits-with-git "To be translated") 
<p> Git is one hell of a powertool.</p>

<p>Like with any such tool, as soon as you get to know it enough, you start pushing the boundaries. Git gives you a lot of control over your repository:</p>

<ul>
    <li>trivial branching and merging (even with long lived branches);</li>
    <li>rebasing as a cleaner alternative to merging;</li>
    <li>stashing aside your changes for a quick fix elsewhere;</li>
    <li><a href="http://tomayko.com/writings/the-thing-about-git">extracting logical, distinct commits from a multi-hours coding spree</a>;</li>
</ul>


<p>The list goes on…</p>

<p>More traditional version control systems don’t give you as much power as Git by any stretch of the mind. They are like taking a walk in the woods with your parents, at age 14.</p>

<p>You’re probably gonna see and do neat stuff, but you sure ain’t gonna get lost or anything.</p>

<!-- more -->


<p>Using Git on the other hand is more akin to being handed a cool motocross to go play alone in the woods… Also at age 14.</p>

<p><a title="Insane motocross shit" href="/uploads/2008/06/insane_motocross_shit.jpg"><a rel="gallery0" class="fancybox" title="Insane motocross shit" href="http://www.programblings.com/uploads/2008/06/insane_motocross_shit.jpg"><img width="426" height="336" alt="Insane motocross shit" src="/uploads/2008/06/insane_motocross_shit.jpg"></a><span class="caption">Insane motocross shit</span></a></p>

<p>We all know what’s bound to happen, right?</p>

<p>You’ll smash into a tree.</p>

<p>The source control equivalent to slamming into a tree is losing commits. Getting all of Git’s power and flexibility at once can be somewhat dangerous.  You’ll find it so easy and helpful to branch and merge that you’ll start doing it way more often. On the other hand &ndash; especially in the beginning &ndash; you’ll misunderstand or plainly miss some important warnings, and make errors. Or you may just end up in weird merging situations you never thought of, and don’t necessarily understand. These situations can often result in losing commits or whole branches.</p>

<p>My goal with this article is to make sure you understand the situation you’re really in: you have <em>temporarily</em> lost commits or branches.</p>

<h3>Disclaimer</h3>


<p>This article assumes a basic knowledge of how git works, e.g. committing, branching and merging.</p>

<h3>My first time</h3>


<p>The first time I lost a commit was a good while ago. I can’t remember the details, but basically I got bit by the fact that under the covers, Git uses hard links liberally. Which means that copy / pasting your code directory as a recovery solution isn’t going to save your ass <a rel="gallery0" class="fancybox" title="A nice poney" href="http://www.programblings.com/uploads/2008/06/ass.jpg"><img alt="A nice poney" style="vertical-align: middle" src="/uploads/2008/06/ass.jpg"></a><span class="caption">A nice poney</span> when you attempt a potentially damaging operation you don’t fully understand.</p>

<p>Note that compressing your code directory will, though.</p>

<p>So there I was, after attempting an operation I didn’t really understand. I knew I had failed what I attempted and I knew I had lost my last commit. Ironically, I still had Gitk open, displaying that very commit. As long as I didn’t refresh the Gitk view with F5 I could see the lost commit.</p>

<p>Here’s a fun fact: under OSX (not sure about Linux) you cannot select and copy text from Gitk’s interface, except for the SHA1 field [1]. I knew Git probably had a way to recover from that… But you know, I just wanted to get back to work and NOT search documentation and blog posts endlessly.</p>

<p>So I took screenshots, passed them real quick through <a href="http://jocr.sourceforge.net/">GOCR</a>, just to see how far it would get.</p>

<p>The result: GOCR doesn’t like the font Monaco :-)</p>

<h2>How to (really) recover lost commits with Git</h2>


<p>Recently I lost a commit again. This time however, Gitk was not up to date. I knew I’d just lost something I wouldn’t necessarily remember in its entirety. It was a commit an hour old, touching many files. And I have a crappy memory.</p>

<p>This time I had to do it the right way. I found out it’s really easy (once you figure it out), but I found no really clear explanation anywhere. So here goes.</p>

<h3>Initial setup</h3>


<p>If you wanna follow along &ndash; and I strongly recommend it &ndash; here’s the boring few steps to create a dummy repo and bring it up to speed with for the rest of this article. We’re going to beat the hell out of this repo and it’s going to be fun.</p>

<p>So just paste the following into a console:</p>

<pre><strong>mkdir recovery;cd recovery
git init
touch file
git add file
git commit -m "First commit"
echo "Hello World" &gt; file
git add .
git commit -m "Greetings"git branch cool_branch
git checkout cool_branch
echo "What up world?" &gt; cool_file
git add .
git commit -m "Now that was cool"
git checkout master
echo "What does that mean?" &gt;&gt; file</strong></pre>


<p>Ok, let’s look at where we’re at:</p>

<pre><strong>gitk &ndash;&ndash;all &amp;</strong></pre>


<p>The &ndash;&ndash;all option lets you see all branches at the same time, as well as your stashes.</p>

<p>Click here to enlarge your picture!!1</p>

<p><a title="Initial setup - Recovering git commits" href="/uploads/2008/06/initial_setup.png"><a rel="gallery0" class="fancybox" title="Initial setup - Recovering git commits" href="http://www.programblings.com/uploads/2008/06/initial_setup.png"><img width="353" height="272" alt="Initial setup - Recovering git commits" src="/uploads/2008/06/initial_setup.png"></a><span class="caption">Initial setup - Recovering git commits</span></a></p>

<p>We can see the cool_branch as well as some yet uncommitted changes over the master branch.</p>

<pre><strong>mathieu@ml recovery (master)$ <font color="#6666ff">ls -l</font>
total 16
-rw-r--r--  1 mathieu  staff    15B  7 Jun 18:19 cool_file
-rw-r--r--  1 mathieu  staff    33B  7 Jun 18:19 file</strong></pre>


<p>Got my 2 files, I’m good to go.</p>

<h3>Let’s make a mistake</h3>


<p>Let’s say I decide I want to bring in these cool changes in master. I’ll do it with a rebase. I know there’s no big risk of conflicts so that’s a no-brainer.</p>

<table width="100%">
<tbody><tr>
<td width="50%">
<pre><strong>mathieu@ml recovery (master)$ <font color="#6666ff">git rebase cool_branch</font>
file: needs update</strong></pre>
</td>
<td width="50%">
<p style="margin: 0pt" class="center"><a rel="gallery0" class="fancybox" title="My ugly mug" href="http://www.programblings.com/uploads/2008/06/my_ugly_mug.jpg"><img width="41" height="41" alt="My ugly mug" src="/uploads/2008/06/my_ugly_mug.jpg"></a><span class="caption">My ugly mug</span></p>
</td>
</tr>
</tbody></table>


<p>Now if you look carefully you’ll notice I wasn’t paying attention when Git gave me a feeble complaint about ‘file’.</p>

<p>Everything’s well, so I think “Ok, I don’t need cool_branch anymore”.</p>

<pre><strong>mathieu@ml recovery (master)$ <font color="#6666ff">git branch -d cool_branch</font>
error: The branch 'cool_branch' is not an ancestor of your current HEAD.
If you are sure you want to delete it, run 'git branch -D cool_branch'.</strong></pre>


<p>Huh? Whatever you say, Linus. Let’s get on with it.</p>

<pre><strong>mathieu@ml recovery (master)$ <font color="#6666ff">git branch -D cool_branch</font>
Deleted branch cool_branch.</strong></pre>


<p>Ahh, it feels good to be a Git ninja. Now let’s see where we’re at and refresh Gitk with F5.</p>

<p><a title="Gitk - oh shit moment" href="/uploads/2008/06/gitk_oh_shit.png"><a rel="gallery0" class="fancybox" title="Gitk - oh shit moment" href="http://www.programblings.com/uploads/2008/06/gitk_oh_shit.png"><img width="353" height="271" alt="Gitk - oh shit moment" src="/uploads/2008/06/gitk_oh_shit.png"></a><span class="caption">Gitk - oh shit moment</span></a></p>

<p>Oops, my cool commit is gone! That thing can’t be right. Let’s panic:</p>

<pre><strong>mathieu@ml recovery (master)$ <font color="#6666ff">ls</font>
file

mathieu@ml recovery (master)$ <font color="#6666ff">git status</font>
# On branch master
# Changed but not updated:
#   (use "git add &lt;file&gt;..." to update what will be committed)
#
#    modified:   file
#
no changes added to commit (use "git add" and/or "git commit -a")

mathieu@ml recovery (master)$ <font color="#6666ff">git diff</font>
diff --git a/file b/file
index 557db03..f2a8bf3 100644
--- a/file
+++ b/file
@@ -1 +1,2 @@
 Hello World
<font color="#008000">+What does that mean?</font></strong></pre>


<p><a rel="gallery0" class="fancybox" title="Oh shit face" href="http://www.programblings.com/uploads/2008/06/oh_shit.jpg"><img width="61" height="83" alt="Oh shit face" src="/uploads/2008/06/oh_shit.jpg"></a><span class="caption">Oh shit face</span>
Oh sh!t</p>

<p>So the ‘file: needs update’ message back there meant that the rebase didn’t happen, because I had pending changes.</p>

<p>Helpful.</p>

<h2>Recovering a lost commit</h2>


<p>Since I don’t think my uncommitted work is complete, I’ll just stash it instead of committing it. Then I’ll hunt down my lost work.</p>

<pre><strong>mathieu@ml recovery (master)$ <font color="#6666ff">git stash save "Questioning the universe"</font>
Saved working directory and index state "On master: Questioning the universe" HEAD is now at 6da726f... Greetings</strong></pre>


<p>In the name of paranoïa, let’s make sure this got in right:</p>

<p><a title="In a paranoïa moment, we make sure the stash is saved correctly" href="/uploads/2008/06/gitk_check_out_that_stash.png"><a rel="gallery0" class="fancybox" title="In a paranoïa moment, we make sure the stash is saved correctly" href="http://www.programblings.com/uploads/2008/06/gitk_check_out_that_stash.png"><img width="364" height="285" alt="In a paranoïa moment, we make sure the stash is saved correctly" src="/uploads/2008/06/gitk_check_out_that_stash.png"></a><span class="caption">In a paranoïa moment, we make sure the stash is saved correctly</span></a></p>

<p>Ok, let’s get on with our rescue mission:</p>

<pre><strong>mathieu@ml recovery (master)$ <font color="#6666ff">git fsck −−lost-found</font>
dangling commit 93b0c51cfea8c731aa385109b8e99d19b38a55be</strong></pre>


<p>That sounds right, exactly one commit in the lost and found.</p>

<p>Let’s just make sure:</p>

<pre><strong>mathieu@ml recovery (master)$ </strong><font color="#6666ff"><strong>git show 93b0c51cfea8c731aa385109b8e99d19b38a55be | mate</strong></font></pre>


<p><a title="We see in textmate that this is our lost commit" href="/uploads/2008/06/show_lost_found.png"><a rel="gallery0" class="fancybox" title="We see in textmate that this is our lost commit" href="http://www.programblings.com/uploads/2008/06/show_lost_found.png"><img width="266" height="168" alt="We see in textmate that this is our lost commit" src="/uploads/2008/06/show_lost_found.png"></a><span class="caption">We see in textmate that this is our lost commit</span></a></p>

<p>Bingo!</p>

<h3>Different ways to recover the commit</h3>


<p>There are a few different ways to recover that commit. Obviously we can just copy and paste that snippet, but in the case of a bigger commit, that approach will just amount to a lot of error-prone busywork.</p>

<p>I’ll reclaim my Git ninja status and try it a few different ways.</p>

<h4>Recover it with rebase</h4>


<p>Let’s just replay this change on top of master:</p>

<pre><strong>mathieu@ml recovery (master)$ <font color="#6666ff">git rebase 93b0c51cfea8c731aa385109b8e99d19b38a55be</font>
First, rewinding head to replay your work on top of it...
HEAD is now at 93b0c51... Now that was cool
Fast-forwarded master to 93b0c51cfea8c731aa385109b8e99d19b38a55be.</strong></pre>


<p><a rel="gallery0" class="fancybox" title="Commit recovered with rebase" href="http://www.programblings.com/uploads/2008/06/gitk_recovered_with_rebase.png"><img alt="Commit recovered with rebase" src="/uploads/2008/06/gitk_recovered_with_rebase.png"></a><span class="caption">Commit recovered with rebase</span></p>

<p>Neat! Now I feel like a ninja worthy of the title again.</p>

<p>So let’s rewind one commit and try it another way.</p>

<pre><strong>mathieu@ml recovery (master)$ <font color="#6666ff">git reset --hard head^</font>
HEAD is now at 6da726f... Greetings</strong></pre>


<p><a rel="gallery0" class="fancybox" title="Rewinding to a state where we’ve lost our commit" href="http://www.programblings.com/uploads/2008/06/gitk_rewinding_to_lost_commit.png"><img alt="Rewinding to a state where we’ve lost our commit" src="/uploads/2008/06/gitk_rewinding_to_lost_commit.png"></a><span class="caption">Rewinding to a state where we’ve lost our commit</span></p>

<p>Ok, the commit’s gone.</p>

<p>(Don’t tell anyone but my inner ninja is feeling queasy again.)</p>

<h4>Recover it with merge</h4>


<p>There are cases where rebase is not powerful enough. For example when you expect to face a lot of conflicts. In this case merge is a better solution:</p>

<pre><strong>mathieu@ml recovery (master)$ <font color="#6666ff">git merge 93b0c51cfea8c731aa385109b8e99d19b38a55be</font>
Updating 6da726f..93b0c51
Fast forward
 cool_file |    1 +
 1 files changed, 1 insertions(+), 0 deletions(-)
 create mode 100644 cool_file</strong></pre>


<p><a rel="gallery0" class="fancybox" title="Commit recovered with merge" href="http://www.programblings.com/uploads/2008/06/gitk_recovered_with_merge.png"><img alt="Commit recovered with merge" src="/uploads/2008/06/gitk_recovered_with_merge.png"></a><span class="caption">Commit recovered with merge</span></p>

<p>Too easy… Rewind!</p>

<pre><strong>mathieu@ml recovery (master)$ <font color="#6666ff">git reset --hard head^</font>
HEAD is now at 6da726f... Greetings</strong></pre>


<h4>Recover it with cherry-pick</h4>


<p>If  instead you had a few commits one after another but you just want to pick the last one, rebase and merge won’t do. They would bring the whole branch back in master. That’s a situation for cherry-pick.</p>

<pre><strong>mathieu@ml recovery (master)$ <font color="#6666ff">git cherry-pick 93b0c51cfea8c731aa385109b8e99d19b38a55be</font>
Finished one cherry-pick.
Created commit f443703: Now that was cool
 1 files changed, 1 insertions(+), 0 deletions(-)
 create mode 100644 cool_file</strong></pre>


<p><a rel="gallery0" class="fancybox" title="Commit recovered with cherry-pick" href="http://www.programblings.com/uploads/2008/06/gitk_recovered_with_cherry_pick.png"><img alt="Commit recovered with cherry-pick" src="/uploads/2008/06/gitk_recovered_with_cherry_pick.png"></a><span class="caption">Commit recovered with cherry-pick</span></p>

<p>Insane!</p>

<p>This only leaves one open question: WHO’S YOUR DADDY NOW, GIT?</p>

<p>Now that we’ve established the answer to that question, let’s get back to work!</p>

<h3>Let’s make a second mistake</h3>


<pre><strong>mathieu@ml recovery (master)$ <font color="#6666ff">git stash clear</font></strong></pre>


<p>Or was it Git stash apply?</p>

<p><a rel="gallery0" class="fancybox" title="Oops! Accidentally lost the stash" href="http://www.programblings.com/uploads/2008/06/gitk_accidental_stash_clear.png"><img alt="Oops! Accidentally lost the stash" src="/uploads/2008/06/gitk_accidental_stash_clear.png"></a><span class="caption">Oops! Accidentally lost the stash</span></p>

<p>Oh jeez, there we go again…</p>

<pre><strong>mathieu@ml recovery (master)$ <font color="#6666ff">git fsck −−lost-found</font>
dangling commit 24e3752f7a73ae98b361ce1c260e1f285d653447
dangling commit 93b0c51cfea8c731aa385109b8e99d19b38a55be</strong></pre>


<p>Ok, we still see the one we lost earlier, 93b0c51… Let’s look at the other one.</p>

<pre><strong>mathieu@ml recovery (master)$ <font color="#6666ff">git show 24e3752f7a73ae98b361ce1c260e1f285d653447</font>
commit 24e3752f7a73ae98b361ce1c260e1f285d653447
Merge: 6da726f... c90f079...
Author: Mathieu Martin &lt;webmat@gmail.com&gt;
Date:   Sat Jun 7 16:02:57 2008 -0400

On master: Questioning the universe

diff --cc file
index 557db03,557db03..f2a8bf3
--- a/file
+++ b/file
@@@ -1,1 -1,1 +1,2 @@@
Hello World
<font color="#008000">++What does that mean?</font></strong></pre>


<p>Spot on. Let’s try something wild, while we’re here.</p>

<pre><strong>mathieu@ml recovery (master)$ <font color="#6666ff">git checkout 24e3752f7a73ae98b361ce1c260e1f285d653447</font>
Note: moving to "24e3752f7a73ae98b361ce1c260e1f285d653447" which isn't a local branch
If you want to create a new branch from this checkout, you may do so
(now or later) by using -b with the checkout command again. Example:
  git checkout -b &lt;new_branch_name&gt;
HEAD is now at 24e3752... On master: Questioning the universe

mathieu@ml recovery (24e3752...)$</strong></pre>


<p>As you may have noticed, my console always indicates which branch I’m in, so far [2]. But now I seem to be in some kind of twilight zone, which Gitk confirms.</p>

<p><a rel="gallery0" class="fancybox" title="Oops! Accidentally lost the stash" href="http://www.programblings.com/uploads/2008/06/gitk_accidental_stash_clear.png"><img alt="Oops! Accidentally lost the stash" src="/uploads/2008/06/gitk_accidental_stash_clear.png"></a><span class="caption">Oops! Accidentally lost the stash</span></p>

<p>Let’s follow Git’s suggestion and make that a branch.</p>

<pre><strong>mathieu@ml recovery (24e3752...)$ <font color="#6666ff">git checkout -b recovery</font>
Switched to a new branch "recovery"

mathieu@ml recovery (recovery)$</strong></pre>


<p><a rel="gallery0" class="fancybox" title="Stash recovered as a branch" href="http://www.programblings.com/uploads/2008/06/gitk_stash_recovered_as_a_branch.png"><img alt="Stash recovered as a branch" src="/uploads/2008/06/gitk_stash_recovered_as_a_branch.png"></a><span class="caption">Stash recovered as a branch</span></p>

<p>Looks weird, like stashed items always do, but at least we have our commit.</p>

<p>After fiddling around with what’s been recovered from the stash, I recommend NOT keeping it as a commit.</p>

<p>If you try to replay the change in the recovery branch over master’s most recent commit, you lose the “Questioning the universe” commit. Probably because a stash is a weird kind of commit, or maybe because of a bug. I don’t know.</p>

<p><font color="#ff0000">(Don’t follow this one in your console) </font></p>

<pre><strong>mathieu@ml recovery (recovery)$ <font color="#000000">git rebase master  #I said don't do this one</font>
First, rewinding head to replay your work on top of it...
HEAD is now at 93b0c51... Now that was cool
Nothing to do.</strong></pre>


<p><a rel="gallery0" class="fancybox" title="Rebasing the recovered stash over master doesn’t work" href="http://www.programblings.com/uploads/2008/06/gitk_rebasing_over_master_doesnt_work.png"><img alt="Rebasing the recovered stash over master doesn’t work" src="/uploads/2008/06/gitk_rebasing_over_master_doesnt_work.png"></a><span class="caption">Rebasing the recovered stash over master doesn’t work</span></p>

<p>If instead I checkout master and then rebase its last change over the ‘recovery’ branch it seems to work.</p>

<p><a rel="gallery0" class="fancybox" title="Recovered stash back in master" href="http://www.programblings.com/uploads/2008/06/gitk_recovered_stash_back_in_master.png"><img alt="Recovered stash back in master" src="/uploads/2008/06/gitk_recovered_stash_back_in_master.png"></a><span class="caption">Recovered stash back in master</span></p>

<p>However since I just saw a commit disappear when rebasing the other way around, I get the feeling that this isn’t a normal commit and it may come back to haunt me later.</p>

<h4>Recover it by applying a diff</h4>


<p>Let’s just apply the diff to master. I’ll do as if it actually was a substantial commit, involving lots of modifications on lots of files, and apply it automatically with ‘git apply’.</p>

<p>First let’s visualize where we’re at, again:</p>

<p><a rel="gallery0" class="fancybox" title="Stash recovered as a branch" href="http://www.programblings.com/uploads/2008/06/gitk_stash_recovered_as_a_branch.png"><img alt="Stash recovered as a branch" src="/uploads/2008/06/gitk_stash_recovered_as_a_branch.png"></a><span class="caption">Stash recovered as a branch</span></p>

<p>A diff against master is not what we want since master includes a new (very cool) commit.</p>

<p>Instead we just want to see the changes introduced by the current commit. To do this we can compare it with the common ancestor between the master and recovery branches. So let’s start by finding it’s ID.</p>

<p><a rel="gallery0" class="fancybox" title="Finding the ID of the common ancestor" href="http://www.programblings.com/uploads/2008/06/gik_find_common_ancestor.png"><img alt="Finding the ID of the common ancestor" src="/uploads/2008/06/gik_find_common_ancestor.png"></a><span class="caption">Finding the ID of the common ancestor</span></p>

<pre><strong>mathieu@ml recovery (recovery)$ <font color="#6666ff">git diff 6da726f37683c83947d54314cd32ca1ee9d490e0</font>
diff --git a/file b/file
index 557db03..f2a8bf3 100644
--- a/file
+++ b/file
@@ -1 +1,2 @@
Hello World
<font color="#008000">+What does that mean?</font></strong></pre>


<p>Looks good. Now we throw that diff upstairs.</p>

<pre><font color="#6666ff"><strong>git diff 6da726f37683c83947d54314cd32ca1ee9d490e0 &gt; ../recovery.diff</strong></font></pre>


<p>Then get apply it to our master branch.</p>

<pre><strong>mathieu@ml recovery (recovery)$ <font color="#6666ff">git checkout master</font>
Switched to branch "master"

mathieu@ml recovery (master)$ <font color="#6666ff">git apply ../recovery.diff</font></strong></pre>


<p>And we finally confirm that everything’s under control.</p>

<pre><strong>mathieu@ml recovery (master)$ <font color="#6666ff">git status</font>
# On branch master
# Changed but not updated:
#   (use "git add &lt;file&gt;..." to update what will be committed)
#
#    modified:   file
#
no changes added to commit (use "git add" and/or "git commit -a")

mathieu@ml recovery (master)$ <font color="#6666ff">git diff</font>
diff --git a/file b/file
index 557db03..f2a8bf3 100644
--- a/file
+++ b/file
@@ -1 +1,2 @@
Hello World
<font color="#008000">+What does that mean?</font></strong></pre>


<p>This change was first stashed rather than committed because I felt it was not complete. Applying it with Git apply only introduces it as an unstaged change, which works perfectly for this situation. Now I can keep banging at the code until I feel this actually deserves to be committed.</p>

<pre><strong>mathieu@ml recovery (master)$ <font color="#6666ff">echo "I don't know" &gt;&gt; file</font>

mathieu@ml recovery (master)$ <font color="#6666ff">git commit -a -m "Conversation of staggering depth"</font>
Created commit 65a4794: Conversation of staggering depth
 1 files changed, 2 insertions(+), 0 deletions(-)</strong></pre>


<h3>Cleaning up the crud</h3>


<p>Ok, so now I still have this weird looking recovery branch.</p>

<p><a rel="gallery0" class="fancybox" title="Now we want to get rid of this weird recovery branch" href="http://www.programblings.com/uploads/2008/06/gitk_useless_recovery_branch.png"><img alt="Now we want to get rid of this weird recovery branch" src="/uploads/2008/06/gitk_useless_recovery_branch.png"></a><span class="caption">Now we want to get rid of this weird recovery branch</span></p>

<p>Since it’s now useless we can get rid of it.</p>

<pre><strong>mathieu@ml recovery (master)$ <font color="#6666ff">git branch -d recovery</font>
error: The branch 'recovery' is not an ancestor of your current HEAD.
If you are sure you want to delete it, run 'git branch -D recovery'.</strong></pre>


<p>Aha! This time everything’s committed correctly, so I know I can delete it for real. Git is complaining because that commit was not included through its normal merge or rebase commands. So it warns me that I may be about to lose something. However I know I got everything through the diff I made and re-applied.</p>

<pre><strong>mathieu@ml recovery (master)$ <font color="#6666ff">git branch -D recovery</font>
Deleted branch recovery.</strong></pre>


<p>Now that I’m aware that commits are reachable even if they’re not in a branch anymore, I wonder about my repo’s size.</p>

<p><a rel="gallery0" class="fancybox" title="Repository size with a few dangling commits: 224kb" href="http://www.programblings.com/uploads/2008/06/repo_size_fat.png"><img alt="Repository size with a few dangling commits: 224kb" src="/uploads/2008/06/repo_size_fat.png"></a><span class="caption">Repository size with a few dangling commits: 224kb</span></p>

<pre><strong>mathieu@ml recovery (master)$ <font color="#6666ff">git gc</font>
Counting objects: 22, done.
Compressing objects: 100% (14/14), done.
Writing objects: 100% (22/22), done.
Total 22 (delta 7), reused 0 (delta 0)

mathieu@ml recovery (master)$ <font color="#6666ff">git prune</font></strong></pre>


<p><a rel="gallery0" class="fancybox" title="Repo size after cleaning up the crud: 152kb" href="http://www.programblings.com/uploads/2008/06/repo_size_slim.png"><img alt="Repo size after cleaning up the crud: 152kb" src="/uploads/2008/06/repo_size_slim.png"></a><span class="caption">Repo size after cleaning up the crud: 152kb</span></p>

<p>Fair enough. I would expect the unused commits to now be unreachable, but strangely enough:</p>

<pre><strong>mathieu@ml recovery (master)$ <font color="#6666ff">git fsck −−lost-found</font>
dangling commit 49ed65cdea22443af3f1fd400754fe1517421b24
dangling commit 4b1bf4792cba929e88114379d7d5e86a2dc9990f
dangling commit 6cdf88318109dede7bd3c1a75be76c7255708ded
dangling commit 715a6b2cfe797383216d0f9b04fe8f50e90e779f
dangling commit f443703e5060d9f3b4d97504bda5f97e5a0b31e8</strong></pre>


<p>If anyone finds out what that’s all about, please let me know!</p>

<p>Maybe Git’s just refusing to do any work unless it’s going to actually save a considerable amount of space? I have no idea.</p>

<h2>Conclusion</h2>


<p>Once you know how to recover from bad mistakes, you’ll find that Git is not only a very powerful tool, but also a very forgiving one. As opposed to a motocross.</p>

<p>The following commands will help you figure you way out of most bad situations:</p>

<ul>
    <li>git show</li>
    <li>git fsck −−lost-found</li>
    <li>git diff</li>
</ul>


<p>And these ones will actually get out of these bad situations:</p>

<ul>
    <li>git rebase</li>
    <li>git cherry-pick</li>
    <li>git merge</li>
    <li>git apply</li>
</ul>


<p>As I think I demonstrated, Git gives you the ability to recover from most bad mistakes. The fact that any single commit can be cherry-picked, checked out, rebased or merged makes it really easy to recover from hairy situations.</p>

<p>The only case where you might actually lose information is when something has not been committed or stashed yet, which I think is perfectly reasonable.</p>

<p>So if you take only one thing away from this article, let it be this. Git is much safer than a motocross.</p>

<h3>Footnotes</h3>


<p>[1] At the time I didn’t know that just having the SHA1 id was enough to save me.</p>

<p>[2] See how to configure your console in the same manner and also get auto-completion for Git <a title="Various Tips For Setting Up Git: Improve Gitk Look And Get Bash Completion" href="http://jfcouture.com/2007/12/18/various-tips-for-setting-up-git-improve-gitk-look-and-get-bash-completion/">here</a>.</p>
</div>
