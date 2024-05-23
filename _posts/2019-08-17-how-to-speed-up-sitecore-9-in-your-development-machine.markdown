---
layout: post
title: "How to speed up Sitecore 9 in your development machine."
date: 2019-08-17 20:00:00 -0500
comments: true
published: true
categories: ["blog", "archives"]
tags: ["Sitecore", "Speed up", "Initial load"]
permalink: ["/post/how-to-speed-up-sitecore-9-in-your-development-machine"]
---
<!-- more -->
{% include imported_disclaimer.html %}
<p>Recently, I had to upgrade a Sitecore 8.1 instance to Sitecore 9.1. After some changes in the code, including the updating of the GlassMapper calls, the site showed up and everything seems to be working fine.&nbsp;However, I noticed that every time that a DLL was deployed, making Sitecore restart, the application took like 5 minutes to load.</p>
<p>Initially, I thought that something was going on with one or more components that I just installed. After checking the logs, I didn't find any ERROR or WARN lines that suggest the cause of the problem, although I saw some INFO lines regarding a job that started multiple times</p>
<pre class="brush:html;auto-links:false;toolbar:false">INFO Job started: Sitecore.ListManagement.Operations.UpdateListOperationsAgent</pre>
<p>After taking a look for that job at the configuration files, I found that&nbsp;it is being executed every 10 seconds by default(!). Therefore, the solution was obvious, increase the time and set it to 30 minutes. With that configuration, the application only took a few seconds to load instead of 5 minutes.</p>
<p>This is a partial configuration file that I included in my project.</p>
<pre class="brush:xml;auto-links:false;toolbar:false" contenteditable="false">&lt;?xml version="1.0"?&gt;
&lt;configuration xmlns:patch="http://www.sitecore.net/xmlconfig/" xmlns:role="http://www.sitecore.net/xmlconfig/role/"&gt;
    &lt;sitecore&gt;
        &lt;scheduling&gt;
            &lt;agent type="Sitecore.ListManagement.Operations.UpdateListOperationsAgent, Sitecore.ListManagement"&gt;
                &lt;patch:attribute name="interval"&gt;00:30:00&lt;/patch:attribute&gt;
            &lt;/agent&gt;
        &lt;/scheduling&gt;
    &lt;/sitecore&gt;
&lt;/configuration&gt;x</pre>
<p>I hope this helps someone else to avoid waiting for Sitecore to load after a single DLL deployment.</p>
<p>That's it for today.</p>
<p>Until the next post!</p>
<p>&nbsp;</p>
