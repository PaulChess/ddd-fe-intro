---
# try also 'default' to start simple
theme: default
# random image from a curated Unsplash collection by Anthony
background: https://fastly.jsdelivr.net/gh/slidevjs/slidev-covers@main/static/gKmpcDQWPmY.webp
# some information about your slides, markdown enabled
title: ddd-fe-intro
keywords: ddd,frontend
# apply any unocss classes to the current slide
class: text-center
# https://sli.dev/custom/highlighters.html
highlighter: shiki
selectable: true
presenter: true
remoteAssets: false
# https://sli.dev/guide/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/guide/syntax#mdc-syntax
mdc: true
layout: cover
hideInToc: true
---

# DDD 在前端应用中的一些思考

<div class="abs-br mr-16 mb-20 text-left gap-2">
  <p class="leading-10">分享: 沈佳棋</p>
  <p class="leading-10">日期: 2024.09.27</p>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
layout: center
hideInToc: true
---

# 大纲

<Toc maxDepth="1"></Toc>

---
transition: fade-out
layout: center
---

# 一、什么是 DDD?

---
layout: center
---

### DDD 核心概念：

<div mb="6"></div>

DDD（领域驱动设计）是一种面向对象的软件设计方法。旨在解决 <ColorfulText>业务逻辑的复杂性</ColorfulText>，其目的是将软件系统的<ColorfulText> 核心业务领域（Domain）</ColorfulText>抽象出来，并以此为基础进行设计和实现。  
  
领域驱动设计的核心思想是将 <ColorfulText>领域模型</ColorfulText> 作为软件设计的中心，领域模型是描述业务领域中 <ColorfulText>重要概念</ColorfulText>、<ColorfulText>实体</ColorfulText>、<ColorfulText>关系</ColorfulText> 和 <ColorfulText>操作</ColorfulText> 的一组对象和方法的抽象表示。

---
layout: center
---

## 讨论：同花顺的业务领域有哪些？

--- 
transition: fade-out
layout: center
---

# 二、DDD 适用于前端吗?

---
layout: center
---

### DDD 是否适用于前端的一个核心要素：

<div mb="6"></div>

<v-clicks at="1">

<ColorfulText :bold="false">复杂的核心业务逻辑是否存在于前端？</ColorfulText>

</v-clicks>

---
layout: center
---

### 观点：

<div mb="6"></div>

<v-clicks at="1">

我认为大部分情况下复杂的业务逻辑是不在前端的，即 DDD 大部分情况下是不适合前端业务的。  
  
业务逻辑是 <ColorfulText>高层级的策略</ColorfulText>，其他所有东西都依赖于它；  
  
而前端通常被视为一个 <ColorfulText>低层级的细节</ColorfulText>，相对而言比较易变。

</v-clicks>

---
layout: center
---

## 前端技术的特点：

<div mb="6"></div>

<v-clicks at="1">

- 前端是低层级细节
- 前端很难具备稳定性
- 前端很难符合开闭原则

</v-clicks>

---
transition: fade-out
---

## 1. 前端是低层级细节

<div mb="6"></div>

<div v-click="1">

### 什么是细节？

细节指的是如何实现原则，也就是执行原则的方式，细节是原则的实现。要确定你正在编写的代码是原则还是细节的一种简单方法是问下自己：<ColorfulText>这段代码是否是强制执行有关我的业务领域中规则的实现，还是只是使一些事情得以执行？</ColorfulText>

</div>

<div v-click="2">

### 什么是策略？

策略是指我们正在编写的代码应该遵循什么样的规则和原则。<ColorfulText>主要涉及在我们编写代码的领域中存在的业务逻辑、规则和抽象概念</ColorfulText>。

</div>

<div v-click="3">

### 什么是高层次策略？

高层次策略（high-level policy）通常指的是在应用程序中贯穿各个模块和组件的核心业务逻辑和规则，<ColorfulText>这些逻辑和规则是应用程序的核心价值所在，而且通常是不会轻易改变的</ColorfulText>。

</div>

---
transition: fade-out
layout: center
---

<img src="/assets/1.jpg" />

---

## 2. 前端很难具备稳定性

<div mb="6"></div>

<ColorfulText>领域层是具备了最高级别的稳定性和策略</ColorfulText>。通常来说当前业务模型不会发生重大的变化，稳定性最高。

依据 <ColorfulText>稳定依赖原则</ColorfulText>，稳定的模块是我们可以依赖的，将不易变的模块组织成依赖于稳定模块的结构是有意义的，但永远不要让稳定模块依赖于不稳定的模块。

然而，<ColorfulText>UI 层的复用性通常较差</ColorfulText>。不同的用户心智、设计语言、业务背景、以及业务服务，都会对前端 UI 逻辑造成非常大的影响。举个例子，不同业务线的后端服务请求响应数据结构差异化可能直接导致数据处理逻辑无法复用（<ColorfulText>逻辑适配层</ColorfulText>）。

---

## 3. 前端很难符合开闭原则

<div mb="6"></div>

<ColorfulText>通常而言当需要更改某个功能时，前端开发人员通常需要直接修改代码，而不是添加新的功能或模块。</ColorfulText>

对于基础组件来说，通常是做了高度抽象的，相对来说比较稳定。但是，在不同的业务场景中，可能需要对页面进行一些定制化的展示，<ColorfulText>而这些业务规则属于易变的低层级细节，但是往往在业务量比较小、低层级的业务规则没法隐藏到稳定层的时候，这部分工作量往往就会落在前端身上，最后前端视图层和业务组件层会有大量的业务规则逻辑判断</ColorfulText>。通常而言这种方式违反了开闭原则，因为它需要修改现有的代码来实现新的功能，而不是扩展功能模块，这就是因为我们将所有高层级策略放在后端并确保前端不包含高层级策略时所做的工作。

<ColorfulText>策略一：底层稳定组件增加扩展配置来支持定制需求；策略二：基于稳定组件来封装定制化的插件</ColorfulText>

---
layout: center
---

但是，我们也不能完全排除在前端使用 DDD 的可能性。  
在一些复杂的应用中，前端可能需要处理一些业务逻辑，比如业务表单校验规则、权限控制规则等。  

<div mb="6"></div>

在这种情况下，DDD 的一些思想和方法可能有助于组织前端代码，使其更易于理解和维护。  

---
transition: fade-out
layout: center
---

# 三、前端业务复杂度主要在哪?

---
layout: center
---

## 前端业务复杂度：

<div mb="6"></div>

<v-clicks at="1">

- 技术栈的复杂度
- 业务逻辑的复杂度
- UI 交互的复杂度

</v-clicks>

---

## 1. 技术栈的复杂度

<div mb="6"></div>

前端框架解决的问题：

- 定义状态 （data、state）
- 状态变化检测 （Object.defineProperty、Proxy、React reconcilliation）
- 对状态更改做出反应 （Observable、hooks、单向数据流）

---

## 1. 技术栈的复杂度

<div mb="6"></div>

页面开发模式：

- Page = Compose(ComponentA + ComponentB + Fusion/Antd)
- Component = Compose(Fusion/Antd + React hooks + Events + State)

这种组合的特性在业务层如果没有一个比较好的 <ColorfulText>组件依赖原则</ColorfulText>的话，当系统内的各种"组件"的依赖关系越来越复杂的时候，甚至“组件”之间的依赖出现环的时候，业务系统的复杂度就跟着线性递增了。

---

## 1. 技术栈的复杂度

<div mb="6"></div>

![alt text](/assets/2.jpg)

---

## 1. 技术栈的复杂度

<div mb="6"></div>

前端应用中技术栈的复杂度主要体现在以下方面：

<v-clicks at="1">

- <ColorfulText>组件和模块的组织</ColorfulText>：在组件化和模块化设计中，如何组织组件和模块，使得它们的依赖关系合理、清晰，以保证代码的可维护性和可扩展性。
- <ColorfulText>状态逻辑的组织和管理</ColorfulText>：在大型前端应用中，状态管理是一个重要的问题。状态管理需要考虑状态的一致性和可变性，以及如何处理状态的变化。
- <ColorfulText>异步数据处理</ColorfulText>：现代前端应用需要处理大量的异步数据请求和处理。异步数据处理需要考虑异步数据的请求和响应、数据缓存、数据更新和状态管理等问题。

</v-clicks>

---

## 2. 业务逻辑的复杂度

<div mb="6"></div>

- 业务逻辑的复杂度通常来自于业务需求本身，例如业务规则、流程、数据处理等
- 在前端开发中，业务逻辑复杂度可能表现为需要进行大量的数据处理、业务规则的验证、复杂的页面流程设计等

---

## 3. UI 交互的复杂度

<div mb="6"></div>

UI 交互的复杂度主要体现在：

<v-clicks at="1">

- 用户体验设计
- 跨端兼容性
- 性能优化。

</v-clicks>


---
transition: fade-out
layout: center
---

# 四、怎么降低前端业务复杂度?

---
layout: center
---

领域驱动设计的主要目的是为了解决业务逻辑的复杂性。  
  
领域驱动设计的核心思想是将领域模型作为我们业务架构设计的中心。   
  
目前前端开发者在以 UI 层为中心进行开发，而如果我们切换视角以 ViewModel、Model 为中心来构建我们的前端业务的话，整体系统设计思路会发生变化。

---

## 1. 领域模型

<div mb="6"></div>

大部分前端代码与实际业务领域无关，这部分前端主要专注在表单验证、API 请求、事件响应、列表渲染等等，然而也有部分业务的前端也确确实实跟业务领域相关，领域业务模型也确实会影响到 UI 层。领域模型通常是一组具有业务含义的类或者对象，它们通过方法、属性等方式封装了系统的关键业务逻辑。无论如何，只要它能被系统中的其他不同应用复用就可以。  
  
通常来说我们可以通过手动创建或者抽象工厂方法构造出模型数据，把这些数据响应式地映射到视图层，再根据视图层触发的事件调用模型层里的函数或方法来更新模型层数据。

---

## 2. 状态管理

<div mb="6"></div>

状态管理主要分两个部分：一个是管理对业务模型层的可变状态和不可变状态，一个管理视图层的可变状态和不可变状态。  
  
视图层上有些状态不是从模型层数据里来的，是纯粹的页面状态，比如数据正在加载的标志、下拉框的联动，等等，这些和模型层无关，且随着需求的变化而动态变化。  
  
在基于 React 渲染方案中，我们既可以利用 React 原生的响应方案也可以借助三方库(mobx)的方案来实现这部分状态管理，选择的方案不同可能会带来在编程范式的差异（FP、OOP）。

---

## 3. 视图层

<div mb="6"></div>


视图层是最不稳定的一层，UI 组件的实现通常受到业务需求的影响，随着需求的变化，UI 组件的实现也需要进行相应的调整和变更。同时，为了保持软件的稳定性和可维护性，需要遵循稳定依赖原则，确保其他基础组件不会依赖于视图层。  
  
基于 React 的视图层又会有伴随着事件响应、生命周期等等副作用。Hooks 实际上只是视图层的东西，背后都是依赖于 React 的响应原理，因此，在我看来，Hooks 会通过合并同类项进入视图层。

---

## 4. 架构分层

<div mb="6"></div>

首先，在互联网行业中，很难一开始就完成完美的系统设计。相反，系统往往需要逐步发展，通过不断迭代和引入新的功能模块来逐步成型。对于现有系统，通过一次大规模的重构难以解决所有问题。好的系统设计需要不断投入工作并逐步积累细节，最终才能获得完善的系统。因此，在日常工作中需要高度重视设计和细节改进。  
  
其次，专业化分工和代码复用是提高软件生产率的重要手段，此外，同一领域服务可以支持不同的上层应用逻辑。这种分工和复用背后的思想是将系统分为多个水平层，并明确定义每个层的角色和任务，以降低单个层的复杂性。同时，每个层只需向相邻层提供一致的接口，可以使用不同的方法进行实现，这为软件重用提供了支持。因此，分层是解决复杂性问题的重要原则。  

---

推荐的文件目录：

```plain
├── shared
│   ├── components // 公用基础组件, 组件之间不能互相耦合
│   ├── constants // 全局变量
│   │   ├── page.ts
│   ├── domains // 领域层
│   │   ├── page
│   │   │   ├── page.model.ts // 实体
│   │   │   └── page.service.ts // 领域Service服务
│   │   ├── ...
│   └── util // 公用函数
│       └── http.ts
├── components // 公共业务组件，业务组件之间不能互相耦合，但是可以依赖公共基础组件
├── modules // 模块视图，模块可以是compose(公共业务组件, 公共基础组件)
└── page // 页面视图层
    ├── index
    │   ├── index.tsx
    │   ├── components
    ├── ...
```

---
transition: fade-out
layout: center
---

# 五、总结



---

### 前端业务工程上深度应用领域驱动设计思想进行实践的几个前提：

<div mb-6></div>

<v-clicks at="1">

- 前提一：开发者需要站在领域模型层为中心的视角来进行系统设计
- 前提二：开发者需要对业务领域模型足够理解，前后端的业务领域模型要对齐
- 前提三：后端能提供业务领域的标准化 CRUD 接口
  
</v-clicks>

---
transition: fade-out
layout: center
hideInToc: true
---

# THX！