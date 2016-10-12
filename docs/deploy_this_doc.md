# 이 문서 참고

<https://github.com/mkdocs/mkdocs/blob/master/mkdocs.yml>

# edit

    code . && mkdocs serve -a :10001

# commit

    git add . && git commit -m . &&  git push -u origin master

# deploy

    mkdocs gh-deploy

# all-in-one (commit + deploy)    

    git add . && git commit -m . &&  git push -u origin master && mkdocs gh-deploy