### iTerm2插件git的缩写大全

<table>
<thead>
<tr>
<th style="text-align:left">Alias</th>
<th style="text-align:left">Command</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left">g</td>
<td style="text-align:left">git</td>
</tr>
<tr>
<td style="text-align:left">ga</td>
<td style="text-align:left">git add</td>
</tr>
<tr>
<td style="text-align:left">gaa</td>
<td style="text-align:left">git add --all</td>
</tr>
<tr>
<td style="text-align:left">gapa</td>
<td style="text-align:left">git add --patch</td>
</tr>
<tr>
<td style="text-align:left">gau</td>
<td style="text-align:left">git add --update</td>
</tr>
<tr>
<td style="text-align:left">gb</td>
<td style="text-align:left">git branch</td>
</tr>
<tr>
<td style="text-align:left">gba</td>
<td style="text-align:left">git branch -a</td>
</tr>
<tr>
<td style="text-align:left">gbda</td>
<td style="text-align:left">git branch --merged | command grep -vE "^(*|\s<em>master\s</em>$)" | command xargs -n 1 git branch -d</td>
</tr>
<tr>
<td style="text-align:left">gbl</td>
<td style="text-align:left">git blame -b -w</td>
</tr>
<tr>
<td style="text-align:left">gbnm</td>
<td style="text-align:left">git branch --no-merged</td>
</tr>
<tr>
<td style="text-align:left">gbr</td>
<td style="text-align:left">git branch --remote</td>
</tr>
<tr>
<td style="text-align:left">gbs</td>
<td style="text-align:left">git bisect</td>
</tr>
<tr>
<td style="text-align:left">gbsb</td>
<td style="text-align:left">git bisect bad</td>
</tr>
<tr>
<td style="text-align:left">gbsg</td>
<td style="text-align:left">git bisect good</td>
</tr>
<tr>
<td style="text-align:left">gbsr</td>
<td style="text-align:left">git bisect reset</td>
</tr>
<tr>
<td style="text-align:left">gbss</td>
<td style="text-align:left">git bisect start</td>
</tr>
<tr>
<td style="text-align:left">gc</td>
<td style="text-align:left">git commit -v</td>
</tr>
<tr>
<td style="text-align:left">gc!</td>
<td style="text-align:left">git commit -v --amend</td>
</tr>
<tr>
<td style="text-align:left">gca</td>
<td style="text-align:left">git commit -v -a</td>
</tr>
<tr>
<td style="text-align:left">gcam</td>
<td style="text-align:left">git commit -a -m</td>
</tr>
<tr>
<td style="text-align:left">gca!</td>
<td style="text-align:left">git commit -v -a --amend</td>
</tr>
<tr>
<td style="text-align:left">gcan!</td>
<td style="text-align:left">git commit -v -a -s --no-edit --amend</td>
</tr>
<tr>
<td style="text-align:left">gcb</td>
<td style="text-align:left">git checkout -b</td>
</tr>
<tr>
<td style="text-align:left">gcf</td>
<td style="text-align:left">git config --list</td>
</tr>
<tr>
<td style="text-align:left">gcl</td>
<td style="text-align:left">git clone --recursive</td>
</tr>
<tr>
<td style="text-align:left">gclean</td>
<td style="text-align:left">git clean -df</td>
</tr>
<tr>
<td style="text-align:left">gcm</td>
<td style="text-align:left">git checkout master</td>
</tr>
<tr>
<td style="text-align:left">gcd</td>
<td style="text-align:left">git checkout develop</td>
</tr>
<tr>
<td style="text-align:left">gcmsg</td>
<td style="text-align:left">git commit -m</td>
</tr>
<tr>
<td style="text-align:left">gco</td>
<td style="text-align:left">git checkout</td>
</tr>
<tr>
<td style="text-align:left">gcount</td>
<td style="text-align:left">git shortlog -sn</td>
</tr>
<tr>
<td style="text-align:left">gcp</td>
<td style="text-align:left">git cherry-pick</td>
</tr>
<tr>
<td style="text-align:left">gcpa</td>
<td style="text-align:left">git cherry-pick --abort</td>
</tr>
<tr>
<td style="text-align:left">gcpc</td>
<td style="text-align:left">git cherry-pick --continue</td>
</tr>
<tr>
<td style="text-align:left">gcs</td>
<td style="text-align:left">git commit -S</td>
</tr>
<tr>
<td style="text-align:left">gd</td>
<td style="text-align:left">git diff</td>
</tr>
<tr>
<td style="text-align:left">gdca</td>
<td style="text-align:left">git diff --cached</td>
</tr>
<tr>
<td style="text-align:left">gdt</td>
<td style="text-align:left">git diff-tree --no-commit-id --name-only -r</td>
</tr>
<tr>
<td style="text-align:left">gdw</td>
<td style="text-align:left">git diff --word-diff</td>
</tr>
<tr>
<td style="text-align:left">gf</td>
<td style="text-align:left">git fetch</td>
</tr>
<tr>
<td style="text-align:left">gfa</td>
<td style="text-align:left">git fetch --all --prune</td>
</tr>
<tr>
<td style="text-align:left">gfo</td>
<td style="text-align:left">git fetch origin</td>
</tr>
<tr>
<td style="text-align:left">gg</td>
<td style="text-align:left">git gui citool</td>
</tr>
<tr>
<td style="text-align:left">gga</td>
<td style="text-align:left">git gui citool --amend</td>
</tr>
<tr>
<td style="text-align:left">ggf</td>
<td style="text-align:left">git push --force origin $(current_branch)</td>
</tr>
<tr>
<td style="text-align:left">ghh</td>
<td style="text-align:left">git help</td>
</tr>
<tr>
<td style="text-align:left">ggpull</td>
<td style="text-align:left">ggl</td>
</tr>
<tr>
<td style="text-align:left">ggpur</td>
<td style="text-align:left">ggu</td>
</tr>
<tr>
<td style="text-align:left">ggpush</td>
<td style="text-align:left">ggp</td>
</tr>
<tr>
<td style="text-align:left">ggsup</td>
<td style="text-align:left">git branch --set-upstream-to = origin/$(current_branch)</td>
</tr>
<tr>
<td style="text-align:left">gpsup</td>
<td style="text-align:left">git push --set-upstream origin $(current_branch)</td>
</tr>
<tr>
<td style="text-align:left">gignore</td>
<td style="text-align:left">git update-index --assume-unchanged</td>
</tr>
<tr>
<td style="text-align:left">gignored</td>
<td style="text-align:left">git ls-files -v | grep "^[[:lower:]]"</td>
</tr>
<tr>
<td style="text-align:left">git-svn-dcommit-push</td>
<td style="text-align:left">git svn dcommit &amp;&amp; git push github master:svntrunk</td>
</tr>
<tr>
<td style="text-align:left">gk</td>
<td style="text-align:left">\gitk --all --branches</td>
</tr>
<tr>
<td style="text-align:left">gke</td>
<td style="text-align:left">\gitk --all $(git log -g --pretty = format:%h)</td>
</tr>
<tr>
<td style="text-align:left">gl</td>
<td style="text-align:left">git pull</td>
</tr>
<tr>
<td style="text-align:left">glg</td>
<td style="text-align:left">git log --stat --color</td>
</tr>
<tr>
<td style="text-align:left">glgg</td>
<td style="text-align:left">git log --graph --color</td>
</tr>
<tr>
<td style="text-align:left">glgga</td>
<td style="text-align:left">git log --graph --decorate --all</td>
</tr>
<tr>
<td style="text-align:left">glgm</td>
<td style="text-align:left">git log --graph --max-count = 10</td>
</tr>
<tr>
<td style="text-align:left">glgp</td>
<td style="text-align:left">git log --stat --color -p</td>
</tr>
<tr>
<td style="text-align:left">glo</td>
<td style="text-align:left">git log --oneline --decorate --color</td>
</tr>
<tr>
<td style="text-align:left">glog</td>
<td style="text-align:left">git log --oneline --decorate --color --graph</td>
</tr>
<tr>
<td style="text-align:left">glol</td>
<td style="text-align:left">git log --graph --pretty = format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)&lt;%an&gt;%Creset' --abbrev-commit</td>
</tr>
<tr>
<td style="text-align:left">glola</td>
<td style="text-align:left">git log --graph --pretty = format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)&lt;%an&gt;%Creset' --abbrev-commit --all</td>
</tr>
<tr>
<td style="text-align:left">glp</td>
<td style="text-align:left">_git_log_prettily</td>
</tr>
<tr>
<td style="text-align:left">gm</td>
<td style="text-align:left">git merge</td>
</tr>
<tr>
<td style="text-align:left">gmom</td>
<td style="text-align:left">git merge origin/master</td>
</tr>
<tr>
<td style="text-align:left">gmt</td>
<td style="text-align:left">git mergetool --no-prompt</td>
</tr>
<tr>
<td style="text-align:left">gmtvim</td>
<td style="text-align:left">git mergetool --no-prompt --tool = vimdiff</td>
</tr>
<tr>
<td style="text-align:left">gmum</td>
<td style="text-align:left">git merge upstream/master</td>
</tr>
<tr>
<td style="text-align:left">gp</td>
<td style="text-align:left">git push</td>
</tr>
<tr>
<td style="text-align:left">gpd</td>
<td style="text-align:left">git push --dry-run</td>
</tr>
<tr>
<td style="text-align:left">gpoat</td>
<td style="text-align:left">git push origin --all &amp;&amp; git push origin --tags</td>
</tr>
<tr>
<td style="text-align:left">gpristine</td>
<td style="text-align:left">git reset --hard &amp;&amp; git clean -dfx</td>
</tr>
<tr>
<td style="text-align:left">gpu</td>
<td style="text-align:left">git push upstream</td>
</tr>
<tr>
<td style="text-align:left">gpv</td>
<td style="text-align:left">git push -v</td>
</tr>
<tr>
<td style="text-align:left">gr</td>
<td style="text-align:left">git remote</td>
</tr>
<tr>
<td style="text-align:left">gra</td>
<td style="text-align:left">git remote add</td>
</tr>
<tr>
<td style="text-align:left">grb</td>
<td style="text-align:left">git rebase</td>
</tr>
<tr>
<td style="text-align:left">grba</td>
<td style="text-align:left">git rebase --abort</td>
</tr>
<tr>
<td style="text-align:left">grbc</td>
<td style="text-align:left">git rebase --continue</td>
</tr>
<tr>
<td style="text-align:left">grbi</td>
<td style="text-align:left">git rebase -i</td>
</tr>
<tr>
<td style="text-align:left">grbm</td>
<td style="text-align:left">git rebase master</td>
</tr>
<tr>
<td style="text-align:left">grbs</td>
<td style="text-align:left">git rebase --skip</td>
</tr>
<tr>
<td style="text-align:left">grh</td>
<td style="text-align:left">git reset HEAD</td>
</tr>
<tr>
<td style="text-align:left">grhh</td>
<td style="text-align:left">git reset HEAD --hard</td>
</tr>
<tr>
<td style="text-align:left">grmv</td>
<td style="text-align:left">git remote rename</td>
</tr>
<tr>
<td style="text-align:left">grrm</td>
<td style="text-align:left">git remote remove</td>
</tr>
<tr>
<td style="text-align:left">grset</td>
<td style="text-align:left">git remote set-url</td>
</tr>
<tr>
<td style="text-align:left">grt</td>
<td style="text-align:left">cd $(git rev-parse --show-toplevel || echo ".")</td>
</tr>
<tr>
<td style="text-align:left">gru</td>
<td style="text-align:left">git reset --</td>
</tr>
<tr>
<td style="text-align:left">grup</td>
<td style="text-align:left">git remote update</td>
</tr>
<tr>
<td style="text-align:left">grv</td>
<td style="text-align:left">git remote -v</td>
</tr>
<tr>
<td style="text-align:left">gsb</td>
<td style="text-align:left">git status -sb</td>
</tr>
<tr>
<td style="text-align:left">gsd</td>
<td style="text-align:left">git svn dcommit</td>
</tr>
<tr>
<td style="text-align:left">gsi</td>
<td style="text-align:left">git submodule init</td>
</tr>
<tr>
<td style="text-align:left">gsps</td>
<td style="text-align:left">git show --pretty = short --show-signature</td>
</tr>
<tr>
<td style="text-align:left">gsr</td>
<td style="text-align:left">git svn rebase</td>
</tr>
<tr>
<td style="text-align:left">gss</td>
<td style="text-align:left">git status -s</td>
</tr>
<tr>
<td style="text-align:left">gst</td>
<td style="text-align:left">git status</td>
</tr>
<tr>
<td style="text-align:left">gsta</td>
<td style="text-align:left">git stash save</td>
</tr>
<tr>
<td style="text-align:left">gstaa</td>
<td style="text-align:left">git stash apply</td>
</tr>
<tr>
<td style="text-align:left">gstd</td>
<td style="text-align:left">git stash drop</td>
</tr>
<tr>
<td style="text-align:left">gstl</td>
<td style="text-align:left">git stash list</td>
</tr>
<tr>
<td style="text-align:left">gstp</td>
<td style="text-align:left">git stash pop</td>
</tr>
<tr>
<td style="text-align:left">gstc</td>
<td style="text-align:left">git stash clear</td>
</tr>
<tr>
<td style="text-align:left">gsts</td>
<td style="text-align:left">git stash show --text</td>
</tr>
<tr>
<td style="text-align:left">gsu</td>
<td style="text-align:left">git submodule update</td>
</tr>
<tr>
<td style="text-align:left">gts</td>
<td style="text-align:left">git tag -s</td>
</tr>
<tr>
<td style="text-align:left">gunignore</td>
<td style="text-align:left">git update-index --no-assume-unchanged</td>
</tr>
<tr>
<td style="text-align:left">gunwip</td>
<td style="text-align:left">git log -n 1 | grep -q -c "--wip--" &amp;&amp; git reset HEAD~1</td>
</tr>
<tr>
<td style="text-align:left">gup</td>
<td style="text-align:left">git pull --rebase</td>
</tr>
<tr>
<td style="text-align:left">gupv</td>
<td style="text-align:left">git pull --rebase -v</td>
</tr>
<tr>
<td style="text-align:left">glum</td>
<td style="text-align:left">git pull upstream master</td>
</tr>
<tr>
<td style="text-align:left">gvt</td>
<td style="text-align:left">git verify-tag</td>
</tr>
<tr>
<td style="text-align:left">gwch</td>
<td style="text-align:left">git whatchanged -p --abbrev-commit --pretty = medium</td>
</tr>
<tr>
<td style="text-align:left">gwip</td>
<td style="text-align:left">git add -A; git rm $(git ls-files --deleted) 2&gt; /dev/null; git commit -m "--wip--"</td>
</tr>
</tbody>
</table>