# 开发中产品的各版本定义(beta,alpha,rc,release...)

###  alpha：

    Alpha是内部测试版,一般不向外部发布,会有很多Bug.除非你也是测试人员,否则不建议使用.是希腊字母的第一位,表示最初级的版本，alpha 就是α，beta 就是β ，alpha 版就是比beta还早的测试版，一般都是内部测试的版本。

### beta:

​                 该版本相对于α版已有了很大的改进，消除了严重的错误，但还是存在着一缺陷，需要经过多次测试来进一步消除。这个阶段的版本会一直加入新的功能。        

### RC：(Release Candidate)

​                  Candidate是候选人的意思，用在软件上就是候选版本。Release.Candidate.就是发行候选版本。和Beta版最大的差别在于Beta阶段会一直加入新的功能，但是到了RC版本，几乎就不会加入新的功能了，而主要着重于除错!  RC版本是最终发放给用户的最接近正式版的版本，发行后改正bug就是正式版了，就是正式版之前的最后一个测试版。

### GA：（general availability）

​            比如：Apache Struts 2 GA这是Apache Struts 2首次发行稳定的版本，GA意味着General Availability，也就是官方开始推荐广泛使用了。

### Release:

             该版本意味“最终版本”，在前面版本的一系列测试版之后，终归会有一个正式版本，是最终交付用户使用的一个版本。该版本有时也称为标准版。一般情况下，Release不会以单词形式出现在软件封面上，取而代之的是符号(R)。



### build:

        指的是单元测试或者是功能测试




这里对说两句，在Maven仓库的library中，除了以上的几个版本定义，还有一个定义：

    SnapShot , Release .

### 什么时候用Snapshot版本？

        依赖库中的jar正处于开发的阶段，会被经常被更新，这种情况下，如果使用Release，会频繁增加版本号，导致版本号的滥用。



        版本的阶段分类知识版本分类的一部分，版本还可以按照面向对象，业务版本，所处环境等等对一个产品定义。版本定义，有时版本学的一个分支部分。我也是慢慢感觉到，版本里面的别有洞天。