# GIT command
###PULL
<code>git pull origin develop</code>

###FETCH
<code>git fetch</code>

###STASH
<code>git stash</code>

###POP
<code>git stash pop</code>

###COMMIT
<code>git add .</code>
<code>git commit -m "comment"</code>

###PUSH
<code>git push origin develop</code>

###PULLプッシュした時のミスを消す
<code>git revert -m 1 commitId</code>



###RESET (delete commit)
<code>git add .</code>
<code>git reset --soft HEAD^</code>

###RESET (hard)
<code>git add .</code>
<code>git reset --hard HEAD^</code>

###GIT CLONE
<code>git clone http://~~</code>

###OTHER
<code>git status</code>
<code>git branch</code>
<code>git log</code>
<code>git checkout -b "branchName"</code>


###NOT TRIED
<code>git diff</code>

### TAR
tar -zcvf. xxxx.tar.gz directory
tar -zxvf. xxxx.tar.gz



git branch -a
git checkout
make
git branch 

git tag
push
git pull merge

#ECLIPSE
###BUILD
mvn clean install -Dmaven.test.skip=true -P UT


#WILDFLY

#file operations
###scp command リモートTOローカル
scp root@address:serverlist.txt ~/materials
<For example>
scp root@10.157.99.36:/var/lib/jenkins/workspace/tor-PR/materials.tar.gz ~/materials
###必要なフォルダを一気に作ってくれる。
mkdir -p /usr/local/sb/weir

service wildfly_01 restart
cd /etc/init.d/ にwildflyが入っているため使える。

psql -h 10.157.17.171 -U user_training -d db_training

ssh root@10.157.82.101

chownコマンド

gitlab origin 変更

telnetコマンド
telnet ip port
ex: telnet 10.157.16.207 8823

mvn -s /usr/local/sb/mvn/conf/settings_Jedi.xml clean install -Dmaven.test.skip=true -X


