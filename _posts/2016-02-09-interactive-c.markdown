---
layout: post
title: "Interactive C#"
date: 2016-02-09 19:10:00 -0500
comments: true
published: true
categories: ["blog", "archives"]
tags: ["C#", "Interactive"]
permalink: "/post/interactive-c"
---
<!-- more -->

{% include imported_disclaimer.html %}

<p>Probably as a DotNet developer, you have worked in a portion of code that you wanted to test separately, so you can&nbsp;check if it will work as you think. Unfortunately, DotNet languages have been known as languages that need compilation prior to be executed, therefore the results are obtained after the project is compiled and run.</p>
<p>However, a set of new features of the DotNet Compiler Platform (codename Roslyn) allow to execute portions of c# code directly in the new compiler. This new interactive compiler (csi.exe) is a REPL (read-eval-print-loop) environment that processes expressions you enter to it, line by line.</p>
<p>There are two ways to use the interactive compiler:&nbsp;</p>
<ul>
<li>In the command line interpreter (cmd, powershell or <a title="cmder" href="http://cmder.net/" target="_blank">cmder</a>), type csi.exe or,&nbsp;</li>
<li>In&nbsp;Visual Studio 2015, go to View, Other Windows, and select&nbsp;C# Interactive,&nbsp;</li>
</ul>
<p>The main difference between both is that csi.exe won't add the default references to DotNet libraries and neither "using" directives to the compilation session. It means that you will have, for instance, enter the&nbsp;following statement</p>
<pre class="brush:csharp;auto-links:false;toolbar:false" contenteditable="false">using System;</pre>
<p>in order to use&nbsp;&nbsp;</p>
<pre class="brush:csharp;auto-links:false;toolbar:false" contenteditable="false">Console.WriteLine()</pre>
<p><img style="margin-right: auto; margin-left: auto; display: block;" src="/image.axd?picture=/Posts/Interactive-C/1. Using in Console.gif" alt="" /></p>
<p>Visual Studio, in the other hand, will add that for you automatically.&nbsp;</p>
<p><img style="margin-right: auto; margin-left: auto; display: block;" src="/image.axd?picture=/Posts/Interactive-C/2. CSharp_Interactive_VS.gif" alt="" /></p>
<p>&nbsp;</p>
<p>Once you've started, you can test whatever you need. Let's try something more interesting. Let's say you want to remove all the numbers at the end of&nbsp;the&nbsp;strings in a list&nbsp;using regular expressions. There are some alternatives to do this, however, let's do it directly in the compiler.</p>
<p>&nbsp; <img style="margin-right: auto; margin-left: auto; display: block;" src="/image.axd?picture=/Posts/Interactive-C/3. Test 2.gif" alt="" /></p>
<p>&nbsp;</p>
<p>Further information about the Interactive C# Window can be found <a href="https://github.com/dotnet/roslyn/wiki/Interactive-Window">here</a>.</p>
<p>That's it for today.</p>
<p>See you soon in the digital neighborhood!</p>
