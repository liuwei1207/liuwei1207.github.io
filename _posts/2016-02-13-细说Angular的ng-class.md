---
layout:     post
title:      "细说Angular ng-class"
subtitle:   "转载"
date:       2016-02-13
author:     "lewis L"
header-img: "img/post-bg-walking.jpg"
tags:
    - Angular
---
<p>
在前面Angularjs开发一些经验总结中我们说到在angular开发中angular controller never 包含DOM元素（html/css），在controller需要一个简单的POJO（plain object javascript object），与view完全的隔离（交互angularjs框架的职责。但在某些项目中看见controller涉及DOM的元素最多的是在controller scope上定义某变量，其值为class name，形如：
</p>
<pre>
<code>
function ctr($scope){
   $scope.test =“classname”;
}
&lt;div class=”{{test}}”&gt;&lt;/div&gt;
</code>
</pre>
<p>
这种方式完全没错，是angular提供的一种改变class的方式，但是在controller涉及了classname在我看来是乎总是那么诡异，我希望的是controller是一个干净的纯javascript意义的object。
</p>
<p>
在angular中为我们提供了3种方案处理class：
</p>
1. scope变量绑定，如上例。（不推荐使用）
2. 字符串数组形式。
3. 对象key/value处理。
<p>
我们继续其他两种解决方案：
</p>
<p>
1字符串数组形式是针对class简单变化，具有排斥性的变化，true是什么class，false是什么class，其形如;
</p>
<pre>
<code>
function Ctr($scope) { 
    $scope.isActive = true;
}

&lt;div ng-class="{true: 'active', false: 'inactive'}[isActive]"&gt;
&lt;/div&gt;
</code>
</pre>
<p>
其结果是2中组合，isActive表达式为true，则 active，负责inactive。
</p>
<p>
2对象key/value处理主要针对复杂的class混合，其形如：
<pre>
<code>
function Ctr($scope) { 

}

&lt;div ng-class {'selected': isSelected, 'car': isCar}"&gt;
&lt;/div&gt;
</code>
</pre>
<p>
当 isSelected = true 则增加selected class，
</p>
<p>
当isCar=true,则增加car class，
</p>
<p>
所以你结果可能是4种组合。
</p>
<p>
个人推荐用2，3两种方式，不建议将class放入controller scope之上，scope需要保持纯洁行，scope上的只能是数据和行为。
</p>

<p>（完）</p>

### 著作权声明

本文摘录自 [博客园](http://www.cnblogs.com/)，如有转载请注明出处。