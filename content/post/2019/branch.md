---
date: 2019-08-15
title: 分支管理
sidebar: false
categories: [技术文档]
description: Git强大的分支、合并管理功能使得制定各类分支策略和工作流更加灵活。但是，许多组织最终采用的工作流要么没有明确定义，要么过于复杂，要么就是未能与问题追踪系统集成。许多从其他版本控制系统转向git的组织经常会发现很难开发出有效的工作流。本文介绍一些常用的Git分支管理策略，为具体项目中提供规范性的指导。
tags: [Git]
---

### 建议规范
#### Git flow  

Git flow是一个定义良好的标准，但其复杂性引入了两个问题。  
一是开发人员必须使用开发分支而不是主干分支，主干分支是为要发布到生产的代码保留的。将master设置为您默认分支的名称是一种惯例，绝大多数的其他分支来源于此，并最终合并于此。由于大多数工具会自动使用master分支作为默认分支，因此老是切换到另一个分支是很烦人的。     
二是补丁和发布分支引入的复杂性。这些分支对于某些组织来说可能是一个好主意，但对绝大多数组织来说都是过度的。如今大多数组织都在实施持续交付，这意味着我们可以部署默认分支。这样就可以避免使用补丁和发布分支，包括他们引入的所有流程。 

![image >](/img/git_flow.png "git flow")

#### GitHub flow 

此工作流仅具有特性分支和主干分支。非常简单和干净，许多组织已经采用它并取得了巨大的成功。 Atlassian建议采用类似的策略，尽管他们会修改功能分支。将所有内容合并到主干分支和部署通常意味着您最大限度地减少“库存”中的代码量，这与精益和持续交付最佳实践一致。但是这个流程仍然存在很多关于部署、环境、发布和issue集成的问题。 

![image](/img/github_flow.png#left "github flow")  


#### GitLab flow

##### 带生产分支  
![image](/img/gitlab_flow1.png)   
GitHub Flow 确实假设您每次合并功能分支时都可以部署到生产环境。这对于SaaS应用程序是可行的，但在许多情况下这是不可能的。一种情况是您无法控制确切的发布时刻，例如需要通过AppStore验证的iOS应用程序。另一个例子是当你有部署窗口时（工作日从上午10点到下午4点，当运营团队满负荷运转时），你也可以在其他时间合并代码。在这些情况下，您可以创建一个反映已部署代码的生产分支。您可以通过将master合并到生产分支来部署新版本。如果您需要知道生产中的代码，您可以检出生产分支以查看。在版本控制系统中，合并提交很容易看到部署的大致时间。如果您自动部署生产分支，则此时间非常准确。如果您需要更准确的时间，则可以让部署脚本在每个部署上创建标记。此流程可避免git flow中常见的释放，标记和合并开销。  
##### 带环境分支 
![image](/img/gitlab_flow2.png)   
拥有一个自动更新到主干分支的环境可能是个好主意。仅在这种情况下，此环境的名称可能与分支名称不同。假设您有一个临时环境，一个预生产环境和一个生产环境。在这种情况下，主干分支部署在临时环境上。当有人想要部署到预生产时，他们会创建从主干分支到预生产分支的合并请求。而将预生产分支合并到生产分支则会触发代码的上线。这种变更提交（commits）只向下游流动的工作流可确保所有变更在所有环境中都经过测试。如果您需要cherry-pick一个包含修补程序的提交，通常做法是在功能分支上开发它并使用合并请求将其合并到master中，不要删除该功能分支。如果主干分支自动测试通过（如果你正在实行持续交付，那么它就应如此），之后你就可以把它合并到其他分支。在某些情况下，可能需要执行更多的手工测试（这导致无法执行上述的主干->预生产->生产合并的标准流程），那么您可以从特性分支发送合并请求到下游分支。环境分支的“极端”版本正在为Teatro创建每个功能分支的环境。  

##### 带发布分支  
![image](/img/gitlab_flow3.png)   
只有在您需要向外界发布软件时，才需要使用发布分支。在这种情况下，每个分支包含次要版本（2-3-stable，2-4-stable等）。 stable分支使用master作为起点，并尽可能晚地创建。通过尽可能晚地创建分支，您可以最大限度地减少将bug fixes应用于多个分支所花费的时间。在一个发布分支被公布后，仅有严重错误的修复能被包括在该分支中。如果可能的话，这些bug fixes应首先合并到master中，然后cherry-pick到发布分支中。这样你就不会忘记将它们cherry-pick到master中，以避免在后续版本中遇到相同的bug。这被称为“上游优先”策略，也是谷歌和红帽实施的策略。每次在发布分支中包含错误修复时，都会通过设置新标记来增加补丁的版本号（以符合语义版本控制）。有些项目还有一个稳定的分支，指向与最新发布的分支相同的提交。在此流程中，拥有生产分支（或git flow 的master分支）并不常见。 

### 实践方案  
常设三个分支：
- dev：开发分支，开发人员日常使用，push和merge不受限制。  
- master：测试环境的稳定分支，用于构建测试环境。push仅限于bug修改，merge需要审核。
- prod：生产稳定分支，用于同步生产版本。除了从master分支进行merge，不接受任何其它修改。
  
平时开发工作中，根据需要由开发人员创建两类临时分支：
- feature-*：为了开发某个特定功能，从develop分支上面分出来的。开发完成后，要merge到develop分支。功能分支的命名，采用feature-*形式命名(*为任务单号)
- fixbug-*：Bug修复分支，为了修复某个bug，从常设分支上面分出来的，一般从生产稳定分支分出来。修复完成后，再merge到其他的分支。采用fixbug-*的形式命名（*为bug单号）

![image](/img/sample-flow.png)