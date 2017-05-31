---
layout:     post
title:      贝叶斯网络
date:       2015-06-24
---

<style type="text/css">
p{
	text-indent: 2em;
}
.post img {
  margin-bottom: 0rem;
}
</style>

<p class="intro">
	<span class="dropcap">贝</span>叶斯网络（Normal distribution）又名信念网络
</p>


<p>贝叶斯网络（Bayesian network），又称信念网络（belief network）或是有向无环图模型（directed acyclic graphical model），是一种概率图型模型，借由有向无环图（directed acyclic graphs, or DAGs）中得知一组随机变数{X_1,X_2,...,X_n}及其n组条件概率分配（conditional probability distributions, or CPDs）的性质。举例而言，贝叶斯网络可用来表示疾病和其相关症状间的概率关系；倘若已知某种症状下，贝叶斯网络就可用来计算各种可能罹患疾病之发生概率。
</p>
<p>一般而言，贝叶斯网络的有向无环图中的节点表示随机变数，它们可以是可观察到的变量，抑或是隐变量、未知参数等。连接两个节点的箭头代表此两个随机变数是具有因果关系或是非条件独立的；而两个节点间若没有箭头相互连接一起的情况就称其随机变数彼此间为条件独立。若两个节点间以一个单箭头连接在一起，表示其中一个节点是“因（parents）”，另一个是“果（descendants or children）”，两节点就会产生一个条件概率值。比方说，我们以X_i表示第i个节点，而X_i的“因”以P_i表示，X_i的“果”以C_i表示；图一就是一种典型的贝叶斯网络结构图，依照先前的定义，我们就可以轻易的从图一可以得知：

<p>P_2=\left\{X_4,X_5\right\},C_2=\left\{X_1\right\},P_4=\empty,C_4=\left\{X_2,X_5\right\},P_1=\left\{X_2,X_3\right\}，以及C_1=\empty<p>
</p>

<p>大部分的情况下，贝叶斯网络适用在节点的性质是属于离散型的情况下，且依照P(X_i|P_i)此条件概率写出条件概率表（conditional probability table, or CPT），此条件概率表的每一行（row）列出所有可能发生的P_i，每一列（column）列出所有可能发生的X_i，且任一行的概率总和必为1。写出条件概率表后就很容易将事情给条理化，且轻易地得知此贝叶斯网络结构图中各节点间之因果关系；但是条件概率表也有其缺点：若是节点X_i是由很多的“因”所造成的“果”，如此条件概率表就会变得在计算上既复杂又使用不便。下图为图一贝叶斯网络中某部分结构图之条件概率表。
</p>