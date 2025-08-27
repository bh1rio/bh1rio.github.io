---
layout: post
title: '[翻译]TechNET上关于Monad Shell(MSH)的一次聊天'
date: 2006-01-11 13:24:00 -0000
categories: dotnet
tags: PowerShell
---

原文位置：http://www.microsoft.com/technet/community/chats/trans/windowsnet/wnet_120704.mspx

请注意: 这个抄本的一部分经过编辑。

介绍

MSFT Don (Moderator):  
欢迎来今天的聊天。我们今天的主题是微软将发布的叫做Monad(或MSH)的命令行shell。

MSFT Don (Moderator):  
我们有请今天的专家。 我请他们先介绍一下自己。

MSFT Kenneth (Expert):  
我是命令行shell的程序经理。我主要负责API、类型系统和cmdlet供给器(provider)。

MSFT Jeffrey Snover (Expert):  
你好。我是Jeffrey Snover，Monad的架构师[并且是这个项目的负责人]。

MSFT James Truher (Expert):  
嘿，我是James Truher，Monad组的一个程序经理。我负责语言、错误报告和许多其他的特殊函数。

MSFT Don (Moderator):  
我是主持人Don Spencer。我是Windows Platform SDK(WinFX)的一名编辑。

聊天开始

MSFT James Truher (Expert):  
问: 是不是MSH V1.0努力要在Longhorn之前完成？  
A: Monad首先将作为一个功能搭载进入目标在2H06（06第二季度？）发布的Exchange 12。之后Monad将在那之后搭载进入Windows。发布手段还没有确定。Monad将支持Win2003 SP1、XP SP2 和Longhorn。

MSFT Kenneth (Expert):  
问: 你们打算什么时候发布VS.NET的项目模板？  
A: 这是一项很棒的功能，我们很多人都希望能拥有它。不过，我们无法在第一个版本中实现该功能。对于后续版本，我目前无法发表评论。

MSFT James Truher (Expert):  
问: Monad将作为Exchange的一个功能发布？你能提供一些MSH和Exchange整合在一起的详细内容吗？  
A: 是的，没错——MSH与Exchange 12的集成方式为：Exchange的命令行管理将通过Cmdlets完成，而图形化管理则是建立在这些Cmdlets之上的一个层级。

MSFT Jeffrey Snover (Expert):  
问: 历史性问题——Monad项目实际上是从何时开始的？  
A: Monad 的根源是 WMIC（Windows 管理规范命令行接口）。这一工具由我发明，当时我便意识到，若能实现通用对象反射，所能释放的能力与价值将十分巨大。2001 年夏天，我在学习 .NET 技术时意识到，我们完全可以借助 .NET 实现同样的功能 —— 这便是该项目的起点。起初，没人能理解我所阐述的想法，因此我不得不开发一个详尽的演示程序来进行说明。而当我完成演示后，所有人都表现出了浓厚的兴趣，项目也自此正式启动。

MSFT James Truher (Expert):  
问: 微软会不会把SSH服务器搭载进入远程Monad？  
A: 我们目前没有推出 SSH 服务器的计划。我知道微软内部其他团队正在研究安全远程访问相关事宜，但目前没有具体细节可以提供。

MSFT James Truher (Expert):  
问: 我们何时能看到下一个 MSH 版本发布？
A: 我们尚未安排下一次版本发布，因此目前不清楚下一次版本发布何时进行，也不确定是否会有下一次版本发布。

MSFT Jeffrey Snover (Expert):  
问: 我听说 Monad 有 VMS 的渊源…… 我们是否会推出一款类似 VERB 的工具或功能，以便创建我们自己的动词命令和参数？
A: 我们深受 VMS（以及 AS400）环境的影响。尽管如此，我们并没有一套完全相同的工具。若要定义您自己的命令，需编写一个从我们的基类派生的.NET 类，并为其标记一个 NOUN（名词）和一个 VERB（动词）。该类的属性将成为参数（PARAMETERS）。

MSFT Bruce Payette (Expert):  
Q: Monad 的主要特性有哪些？能否详细说明它与现有的 Windows 脚本环境（如 Windows 外壳脚本、WSH 等）之间的区别？
A: Monad 的目标是提供一套功能强大的命令行管理解决方案。它既是一种语言，也是一个便于创建命令以管理 Windows 平台的框架。因此，与 WSH（Windows 脚本宿主）相比，它更偏向命令行操作，但同时具备 WSH 系列语言的诸多脚本编写能力。相较于 VBScript（Visual Basic 脚本）等语言，它在某种程度上属于更高级的语言。另一个相当显著的区别是，它是一个交互式环境。

MSFT James Truher (Expert):  
Q: Will there be more command-line tools for Windows, so that we can actually do stuff in Monad?  
A: With regard to the Exchange release, we are working closing with Exchange to ensure that all of their management is possible via cmdlets.

MSFT Kenneth (Expert):  
Q: Is there any support for command line completion beyond builtin commands and file names (as in bash)?  
A: As your question implies, monad has the architecture in place to perform tab-completion on parameters and other elements. However, we will not be able to implement and test tab-completion beyond mshpaths (cmdlet providers) in version1.

MSFT Jeffrey Snover (Expert):  
Q: As SSHD is indeterminate, how is remote script execution coming in Monad  
A: Monad will be leveraging the WS-MGMT protocol for remote execution. WS-MGMT is an emerging industry standard that will provide a common protocol to manage servers in both the PRE-OS environment (e.g. talking to the base motherboard controller) and the OS-resident environment. It's pretty awesome stuff.

MSFT Bruce Payette (Expert):  
Q: Will Monad include cmdlets to programmatically access Office and/or other clientside applications?  
A: Probably not in version 1 as our focus is on server management. Now - we do support COM/ActiveX objects directly in msh so you can do most of the same things you do in VBscript. There have been a number of examples of what can be done posted to the Betaplace list.

MSFT James Truher (Expert):  
Q: What language is the API and shell language based on?  
A: The shell language is based generally on 3 different sources. sh/ksh, perl and C#. I wanted to be sure that the language was expressive enough to ensure parity with the unix shells, but wanted to not use the same syntax as the unix shells as they are somewhat irregular and provide a glide path to C#. The shell itself is written in C#.

MSFT Jeffrey Snover (Expert):  
Q: How is security addressed in Monad?  
A: This is a very board topic. We spend a lot of time on security. One of the common questions is "are we reintroducing script attacks?". We are doing a number of things to mitigate those exposures. 1) we will not have a doc handler for .msh files (this means that you won't be able to double-click a .msh file and have it run). 2) We'll have a policy that only allows signed scripts (from people you trust) to run (we'll then make it easy for you to sign scripts).

MSFT Kenneth (Expert):  
Q: How are other teams buying into Monad? Exchange obviously seems on-board. What about IIS? SQL?  
A: A number of teams have created prototype cmdlets and cmdlet providers - this has been very helpful in improving the API and validating the model. however, our first focus is on the exchange release. these other teams have not dropped off our focus, but we can't commit to any other partners' cmdlets at this time.

MSFT Kenneth (Expert):  
Q: Thanks Kenneth, but I don't quite get it. Does it mean I can write a cmdlet which provides tab completion for parameters? I.e. what else in addition to mshpaths would you consider?  
A: in version1 tab-completion we will only handle mshpaths.

MSFT James Truher (Expert):  
Q: What cmdlet providers (or libraries) will be available (e.g. database access, file access, regular expressions)?  
A: The providers that will be a part of the Exchange release are filesystem, registry, function, variable, certificate, alias, environment.

MSFT Jeffrey Snover (Expert):  
Q: Will there be any backward compatibility issues with scripts and cmdline tools?  
A: As a general rule, MSH runs all existing command and scripts. That said, MSH does NOT interpret .bat files, it passes them to cmd.exe to run them. There are certain scripts that are written to modify the environmental variables to affect subsequent scripts. That particular semantic (of .bat scripts) will not work in MSH. That is the only compatibility issue that we are aware of.

MSFT James Truher (Expert):  
Q: Will V1 have support for tee-ing the pipe?  
A: yes, we will provide a tee-object cmdlet

MSFT Bruce Payette (Expert):  
Q: any resolution on the elseif / else if debate?  
A: We've decided to leave it as elseif.

MSFT James Truher (Expert):  
Q: Will MSH V1.0 be done before Longhorn?  
A: MSH will ship as part of Exchange 12

MSFT James Truher (Expert):  
Q: When can we expect the next drop of MSH bits?  
A: I believe that this question was answered earlier

MSFT Jeffrey Snover (Expert):  
Q: Will the monad command line parsing be extensible? (i.e. write a cmdlet which implements 'vi' type command line editing?)  
A: Monad has a clear separation between the ENGINE and the HOST. The HOST is the thing that provides a UI. Hosts can be CLI-based or GUI-based (e.g. MMC could provide a host for Monad). The V1 CLI host that MSH provides will not provide an extensible command line parsing capability. We expect 3rd parties to add value in this area by providing this sort of function. This may be something that we do in later releases. Thanks.

MSFT Kenneth (Expert):  
Q: ..."filesystem, registry, function, variable, certificate, alias, environment"; what about AD? Pretty hard to manage Exchange without that?  
A: Exchange cmdlets will implicitly manage active directory as required. We will continue to work with AD, WMI and other groups for later releases.

MSFT Kenneth (Expert):  
Q: hmmm - no AD (and no Wmi) provider at time of Ex12 release ? Seems a little strange with the Ex melding into AD.  
A: Exchange cmdlets will implicitly manage active directory as required. We will continue to work with AD, WMI and other groups for later releases to create desired providers.

MSFT James Truher (Expert):  
Q: (Question from Christa) Any chance for per-session support in Monad? Last I saw, it assumed a single session.  
A: I think that you're asking about logging - we will be providing a logging mechanism which will allow you to determine what a session is doing

MSFT Kenneth (Expert):  
Q: Do you guys know when it might be possible to get on the Exchange 12 beta, or if that is a possibility for us at all?  
A: you'll have to contact your exchange representative for an exchange12 beta.

MSFT Jeffrey Snover (Expert):  
Q: Scripters are often used to deploying "windowless" solutions - scripts that run without a console or GUI. Is that going to be possible with MSH?  
A: We are looking at modifications to our CLI host to address this issue.

MSFT James Truher (Expert):  
Q: How deep will monad go as far as exchange management? e.g. Will I be able to mount/dismount the information store from monad?  
A: We working with Exchange to ensure that the entire management can be done via Monad, but I can't speak authoritatively about this specific feature.

MSFT James Truher (Expert):  
Q: ..."yes, we will provide a tee-object cmdlet " \- what about a way to merge back together?  
A: You will be able to script a solution to this, but we will not be exposing of the data flow engine in v1, so it won't be possible to do this, other than manually aggregating results (e.g., via variables, etc)

MSFT James Truher (Expert):  
Q: Do you still plan on supporting casting to void to throw away results (or better yet, not ask for ToString in the first place) e.g. [void]myStringBuilder.Append("MSH - don't force copy on write yet")?  
A: yes! we will support [void]

MSFT Bruce Payette (Expert):  
Q: Will there be if not now but eventually a converter tool to migrate or convert existing scripts to Monad Shell scripts ?  
A: We've experimented with a tool to convert VBscript to msh and it was pretty successful but it's not in scope for v1. Alex has also written a set of "VB personality" scripts that help in conversion. However - when and if we release a tool is not something we can speak to at this time unfortunately.

MSFT James Truher (Expert):  
Q: How does one use runspaces with the current drop ?  
A: runspaces are not surfaced in the current drop

MSFT James Truher (Expert):  
Q: I should have said... Will there be a distributable version of the Monad shell that will be release with Exchange?  
A: the shell that releases with Exchange will be targeted at Exchange management. The schedule for a general shell release is to be determined.

MSFT Jeffrey Snover (Expert):  
Q: At a Windows XPSP2 (pre-release) event earlier in the year, we were advised that Monad was the replacement of VBScript / WScript ... do you have any views on that?  
A: We are working to ensure a path forward for VBScript/WSH users. There are 2 directions to that. One the one hand, Monad will provide VBSCRIPT-style scripting in that you’ll be able to access COM object and invoke methods and access their prosperities. On the opposite direction, we are looking at providing a COM interface to Monad so that VBScript users will have access to all of it's functionality. This is NOT a booked plan but should give you a feel for how we are thinking about the issue (so let's just keep this info between those of us with access to the internet ;) ) . We are working to get a booked plan and then make it public.

MSFT James Truher (Expert):  
Q: Will there be a distributable version of the Monad that will be available with Exchange?  
A: this question has been answered

MSFT Bruce Payette (Expert):  
Q: Will the new Exchange System Manager MMC console support generation of MSH code, as demonstrated at PDC?  
A: The next release of MMC will be in R2 before the exchange release so it won't include any Monad support. When Exchange and msh are released the Exchange snapin will be using msh. End-user use of msh in snapins (i.e. writing your own msh based snapins) will be sometime after that.

MSFT Kenneth (Expert):  
Q: The HOST APIs(at least the formatting and output APIs) are heavily geared towards a CLI. Will there be anything done to allow non-CLI hosts to take advantage of the F&O features of the engine?  
A: I’m not sure which part of the infrastructure... the host API itself should be very implementable by a GUI Host. the format/output cmdlets are focused on outputting to some line-oriented device (CLI, printer, file) - they also should write to any host implementing the MshHost class.

MSFT James Truher (Expert):  
Q: Does the scripting language work for a C++ guy? :-) I.e. Is there some strict syntax/semantic check that can be used _before_ the code path is hit? Do we get a debugger?  
A: We are thinking about providing the feature that allows you to single step through a script. We don't currently have plans to supply a more rigorous syntax checker in V1

MSFT Jeffrey Snover (Expert):  
Q: Will there be a way to restrict operations for MSH and provide audit, logging  
A: There will be a bunch of policies that you'll be able to tweak to restrict the running of MSH. We have a pluggable security manager. This allows a NEW host to provide a security manager which can control which commands are run. It also gets called for every ShouldProcess() call which means that it can control things on a per-object level. This is pretty awesome stuff. We also will providing logging of the internal state of the engine. This includes both health-level type information and AUDIT level information (who did what to what when). You'll have policies to control which types of events get emitted.

MSFT Kenneth (Expert):  
Q: What's the latest on support for flattening objects into text? For instance, I want to a set-clipboard cmdlet where the normal console output of "get-process" is what gets put in the clipboard when I type "get-process | set-clipboard".  
A: you can do a ToString on the object results, you may also use the -f operator to explicitly format your objects. if you wanted it formatted using our formatxml then we would need an out-string cmdlet. we do not currently have this cmdlet in our version1 plans. the work around is to use out-file and get-content.

MSFT James Truher (Expert):  
Q: Hosting - is there plans on exposing some of this capability in the beta or is it still too adaptive for the work with Ex team?  
A: we do have a set of hosting APIs, but we won't be releasing an SDK with the Exchange release

MSFT Kenneth (Expert):  
Q: For Longhorn, you should convince Microsoft to spin up a ScriptPad project to create a decent text editor for MSH scripts. One that provides simple completion and color syntaxing. Notepad is getting long in the tooth. :-)  
A: this would be nice. however it is not in the scope of the monad project.

MSFT Jeffrey Snover (Expert):  
Q: Will there be a way to create a GUI for MSH scripts using Monad?  
A: Superstar Jim Truher created a set of cmdlets which provide TK-type function. It worked pretty well but this is not something we are planning to release in V1 because we don’t' have the bandwidth. We all fully grok why TK is so cool for customers so that may be in our future. That said, it should be pretty easy for a 3rd party to deliver this functionality.

MSFT James Truher (Expert):  
Q: Do you have a speculation model yet of how your releases will go? Specifically will we be even close to seeing a Monad version 2 by the Longhorn Server release, as an integrated feature of that product?  
A: Our plans are still in flux, so rather than speculating here, it would be better for us to solidify our plans so we don't set the wrong expectation

MSFT Bruce Payette (Expert):  
Q: On the depth of integration... is Monad to replace current management mechanisms? MMC? WMI? what's the idea?  
A: All of these elements will continue to work together but in a layered way. MMC provides the GUI built on top of msh. Msh provides the cmdlets which are based on .NET, WMI, ADSI etc, which provide the APIS, etc.

MSFT James Truher (Expert):  
Q: How close are you to a release candidate version? Do you think that there will be significant changes between now and the release, or is it more fine tuning?  
A: We continue to fine tune the release, some of that tuning may result in a significant change, but architecturally, we are making fewer and fewer changes.

MSFT James Truher (Expert):  
Q: In fact, TextPad already makes a great integrated development tool for MSH scripting - edit and run... :)  
A: question?

MSFT Jeffrey Snover (Expert):  
Q: Have you thought about providing some sort of XPath or XQuery support for providers e.g. get-children c:/foo[@size > 1000000]?  
A: Yes we have. The issue is that by and large we leave the namespace syntax to the namespace provider. FOr instance, AD puts children to the left and uses "," to separate path elements. So we don't do much manipulation of the name itself. That leaves us with trying to do something with parameters but the how point of XPATH is that integration of the namespace with the expression syntax. If you have some good ideas about how to make this all work please post them on our betaplace site and we'll eagerly review them.

MSFT James Truher (Expert):  
Q: Thanks for the answer on audit, I dig further. If there is an answer on who did what to what, the next question will be: any rollable transactions? :$  
A: Just to clarify on auditing - auditing in the strictest sense of the word isn't provided (as AUDIT implies a security model that we won't provide), but we will be able to provide audit-like information. As for transaction support, that will not be part of the Exchange release

MSFT James Truher (Expert):  
Q: RE: HOST APIs and format/output. I meant that there is currently information (such as default F&O fields for each type of object) that is not exposed with the current HOST APIs. The HOST APIs assume you are using a rectangular text box for output. :(  
A: The formatting object model is not going to be published in the Exchange release, sorry.

MSFT Kenneth (Expert):  
Q: Kenneth: Yeah I was think something like this would be nice "get-process | out-string | set-clipboard". But I guess I'll have to wait on that one and use the workaround for now.  
A: yes. we'll take this feedback to our planning meetings :-).

MSFT Bruce Payette (Expert):  
Q: Have you thought about providing some sort of XPath or XQuery support for providers e.g. get-children c:/foo[@size > 1000000]?  
A: Providers are allowed to support filtering in anyway they want. It's entirely possible for a provider to interpret the filter string as an arbitrary query. This makes sense when the repository you're using supports native queries and filters. It makes less sense in something like the file systems so we do get-children | where {$_.length -gt 100000} instead and leverage the existing msh language facilities instead of building this into the provider itself. It may also be possible to allow filtering in providers using script blocks in the future but I’m not sure it would significantly improve things: get-children -filter {$_.length -gt 100k}

MSFT Jeffrey Snover (Expert):  
Q: MSH introduces some big changes to the way we think about working - the verb-noun model, database-like tabulation and querying... what are some of the long-range possibilities you see coming from this?  
A: Great question. Clearly we are trying to reproduce the AS400/VMS-DCL model where you send a while learning the syntax and then you have it for life. Pull on that thread some more and you can see that if there is enough consistency, it should be possible to write meta-programs or programs which drive programs. This is one of the reasons why we love the namespace model. There we said, you provide the information and we'll provide a set of common commands. These commands are then VERY consistent which allows us to write generic programs against them and have them work with everything.

MSFT Kenneth (Expert):  
Q: Did I get it right that Exchange MMC will internally be based on MSH? Will there be a way to view the script traffic for Exchange MMC in such a case?  
A: We have looked at doing this a few times, but E12 version one is not currently planning on implementing this feature.

MSFT Bruce Payette (Expert):  
Q: Is there some sort of collector cmdlet that can be used in a pipe? In the old pipe days, everything (all text) got passed from one stage of the pipe to another. With MSH multiple records are passed. Can you collect these records into one record to pass on  
A: You could do "function gather { ,$input}" and use it like: "1,2,3,4,5 | gather | foreach {$_.length}" which would print out 5. Is this the sort of thing you're looking for?

MSFT James Truher (Expert):  
Q: Will there be a facility in Monad to encrypt streams?  
A: We will not be providing any cmdlets for encryption in the Exchange release

MSFT Jeffrey Snover (Expert):  
Q: It seems we are way far behind in the current drop from what you folks run. It was said earlier there is no timeframe for a drop update. Is this really the best way for the tech beta to help you ? Any thought on exposing runspaces, info on hosting, etc  
A: This is merely a resource issue. Betaplace feedback has been great and we look forward to getting more.

MSFT Kenneth (Expert):  
Q: I wonder if I will be able to have default MSH behavior based on my AD user profile.  
A: this is not currently in version one.

MSFT Bruce Payette (Expert):  
Q: Re XPath/XQuery: yeah my thinking was to learn one powerful query language and be able to apply it to multiple places. It's good to hear you've at least considered it.  
A: That is exactly our reasoning. We already have a language (msh) so we decided to leverage it as much as possible.

MSFT Jeffrey Snover (Expert):  
Q: As MSH evolves, it 'feels' more and more like a database front end environment sometimes - something that deals with extracting and correlating information from a large store. Where is this taking us?  
A:  
YES - the big difference is that with SQL, you had to put things in a SQL database to get those capabilities. Our big contribution, is the insight that you can provide the same sort of functions against live objects. Those live objects can then be anything - they can be transitory objects, they can be front-ends to data-stores, they can be front-ends to anything. e.g.

msh> notepad  
msh> $g = gps  
msh> stop-process notepad  
msh> $g |where {$_.hasexited}

MSFT Bruce Payette (Expert):  
Q: My question on replacing WMI with MSH was to be ready as such: is the supposed way to go is to lock down the direct usage of WMI and allow anything only via MSH? If not so, how does my MSH restriction policy restrict those, who know what is WMI?  
A: We expect that this will be handled through role-based security and delegated administration. So - if you are authorized to run the msh command then it can access WMI but you won't be able to access it directly.

MSFT Don (Moderator):  
For a schedule of other chats that you might be interested in, go to [http://www.microsoft.com/technet/community/chats/default.mspx](http://blog.zhangchi.com.cn/ct.ashx?id=86cc32bc-578e-4a98-ad48-cdcddb896e82&url=http%3a%2f%2fwww.microsoft.com%2ftechnet%2fcommunity%2fchats%2fdefault.mspx).

MSFT Don (Moderator):  
To download a preview of Monad technology go to [http://beta.microsoft.com/content/bphome.asp](http://blog.zhangchi.com.cn/ct.ashx?id=86cc32bc-578e-4a98-ad48-cdcddb896e82&url=http%3a%2f%2fbeta.microsoft.com%2fcontent%2fbphome.asp). The GuestID is mshPDC.
