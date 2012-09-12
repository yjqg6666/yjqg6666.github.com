---
layout: default
title: crontab定时运行git命令-更新代码库
published: true
category: Linux
tags: [git,crontab]
---
<div id="detail" class="detail" style="line-height: 1.3;"><p>Q： &nbsp;<a href="http://stackoverflow.com/questions/7994663/git-push-via-cron" target="_blank" target="_blank">http://stackoverflow.com/questions/7994663/git-push-via-cron</a><div>&nbsp;&nbsp;&nbsp;I'm trying to run a git push from cron. When I 
do the command interactively on the shell it's going through fine. When 
running the command from my user's crontab, cron delivers the error 
message<div class="post-text" itemprop="description">
        

Permission denied (publickey).


<p>I presume it hasn't to do with finding or reading my ~/.ssh/id_rsa, 
as I can cat the file from cron alright. UID and EUID are set fine in 
the cron job. - Any ideas?</p>

<p>UPDATE</p>

<p>I got it working when supplying the environment key SSH_AUTH_SOCK to 
my cron job, but I'm concerned that this is only valid as long as I'm 
logged in. I'm looking for a solution that works independent of 
interactive logins.</p><p>A：</p><p></p><div class="vote"><a class="vote-up-off" title="This answer is useful (click again to undo)"></a>
    <span class="vote-count-post">1</span>
    <a class="vote-down-off" title="This answer is not useful (click again to undo)">down vote</a>
<span class="vote-accepted-on" title="The question owner accepted this as the best answer Nov 3 '11 at 14:49">accepted</span> 
</div>

        



    <div class="post-text"><p>As <a href="http://serverfault.com/questions/92683/execute-rsync-command-over-ssh-with-an-ssh-agent-via-crontab/92689#92689" target="_blank" target="_blank">explained here, </a>it can be due to the lack of knowledge from the cron session shell of the ssh agent.<br>
If that is the case (ie if you are using private ssh keys with a passphrase), <a href="http://oceanpark.com/notes/howto_ssh_keychain_public_key_authentication_forwarding.html" target="_blank" target="_blank"><strong>keychain</strong> i</a>s the usual solution (as <a href="http://serverfault.com/questions/92683/execute-rsync-command-over-ssh-with-an-ssh-agent-via-crontab/236437#236437" target="_blank" target="_blank">mentioned here</a>).<br>
More details in this example: "<a href="http://oceanpark.com/notes/howto_ssh_keychain_public_key_authentication_forwarding.html" target="_blank" target="_blank">Passwordless connections via OpenSSH using public key
authentication, keychain and AgentForward</a>".</p><p><br></p><p></p><p><br></p><p>Very brief synopsis</p><p><br></p><p>1. Generate private/public key pair (id_dsa and id_dsa.pub).</p><p>Save private key in ~/.ssh/id_dsa on trusted hosts you will ssh from.</p><p>Append public key to ~/.ssh/authorized_keys on hosts you will ssh to.</p><p>Do not use ~/.ssh/authorized_keys2. &nbsp;If you see that file, remove it</p><p>and upgrade to a recent version of SSH.</p><p><br></p><p>2. Set ForwardAgent yes in ssh_config on all hosts you ssh</p><p>from. &nbsp;Set PubkeyAuthentication yes in sshd_config on all</p><p>hosts you ssh to. &nbsp;Maybe set StrictModes no in sshd_config.</p><p><br></p><p>3. Install keychain then configure by adding the following lines</p><p>to your $HOME/.bash_profile:</p><p><br></p><p>&nbsp; &nbsp; /usr/local/bin/keychain $HOME/.ssh/id_dsa</p><p>&nbsp; &nbsp; source $HOME/.keychain/${HOSTNAME}-sh</p><p><br></p><p>4. For crontab scripts that use ssh, add the following line in</p><p>order to avoid having to manually enter a passphrase:</p><p><br></p><p>&nbsp; &nbsp; source $HOME/.keychain/${HOSTNAME}-sh</p><p><br></p><p>5. ssh from host to host without needing to enter passwords. &nbsp;Where</p><p>you can ssh, you can also scp, sftp, etc., all securely but without</p><p>having to enter your passwords on the various hosts you use.</p><p></p></div><p></p></div></div></p></div>
