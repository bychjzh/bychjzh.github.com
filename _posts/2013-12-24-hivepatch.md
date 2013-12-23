---
layout: post
title: "Hive打patch步骤"
description: ""
category: "Hive"
tags: ['Hive']
---
{% include JB/setup %}

##一、浏览官方JIRA
找到解决相应问题的JIRA ISSUE编号，如[HIVE-4513][1] 

***注意：如果同时需打多个patch，需先分析各个patch之间的依赖关系。***

##二、创建新分支

    git checkout -b hive-0.11-HIVE-4513
##三、打上patch
首先切换到trunk分支通过git log找到对应JIRA任务编号的commit SHA1值。

    [bychjzh@localhost:hive(trunk)]$ git log
 
    commit 519077e50bb3477dc101d26e35a10a62d0bf2b64
    Author: Ashutosh Chauhan <hashutosh@apache.org>
    Date:
    Tue Aug 13 11:57:49 2013 +0000
    HIVE-4513 : disable hivehistory logs by default (Thejas Nair via Ashutosh Chauhan)
    git-svn-id: https://svn.apache.org/repos/asf/hive/trunk@1513445
    13f79535-47bb-0310-9956-ffa450edef68
 
在需要打上patch的分支上执行`git cherry-pick`

    [bychjzh@localhost:hive(hive-0.11-HIVE-4513)]$ git cherry-pick -x
    519077e50bb3477dc101d26e35a10a62d0bf2b64
提交当前分支

    [bychjzh@localhost:hive(hive-0.11-HIVE-4513)]$ git push origin
    hive-0.11-HIVE-4513:hive-0.11-HIVE-4513 
将当前分支合并到测试分支

    [bychjzh@localhost:hive(hive-0.11-dev)]$git merge hive-0.11-HIVE-4513
##四、在jenkins执行测试并构建
##五、合回主干，并上线
  [1]: https://issues.apache.org/jira/browse/HIVE-4513
