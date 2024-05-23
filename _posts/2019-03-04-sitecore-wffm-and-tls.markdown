---
layout: post
title: "Sitecore WFFM and TLS"
date: 2019-03-04 01:29:00 -0500
comments: true
published: true
categories: ["blog", "archives"]
tags: []
permalink: ["/post/sitecore-wffm-and-tls"]
---
<!-- more -->
{% include imported_disclaimer.html %}
<p>Some weeks ago, the infrastructure team in charge of monitoring security&nbsp;issues in the servers of one company alerted us about that TLS 1.0 and 1.1 was still enabled in some Windows Servers. The description of this issue is at&nbsp;<a href="https://docs.microsoft.com/en-us/security/solving-tls1-problem">https://docs.microsoft.com/en-us/security/solving-tls1-problem</a>.</p>
<p>In those servers, there were two Sitecore 8.2 (.Net 4.5.2) applications running. One of them uses the <a href="https://dev.sitecore.net/Downloads/Web_Forms_For_Marketers.aspx" target="_blank">Web Forms For Marketers</a> module&nbsp;to enable two forms that stopped to work after the TLS 1.0 and TLS 1.1 were disabled in the servers.</p>
<p>After checking the logs, the following exception was found:</p>
<pre class="brush:html;auto-links:false;toolbar:false">Exception: System.ComponentModel.Win32Exception
Message: The client and server cannot communicate, because they do not possess a common algorithm
Source: System
  at System.Net.SSPIWrapper.AcquireCredentialsHandle(SSPIInterface SecModule, String package, CredentialUse intent, SecureCredential scc)
  at System.Net.Security.SecureChannel.AcquireCredentialsHandle(CredentialUse credUsage, SecureCredential&amp; secureCredential)
  at System.Net.Security.SecureChannel.AcquireClientCredentials(Byte[]&amp; thumbPrint)
  at System.Net.Security.SecureChannel.GenerateToken(Byte[] input, Int32 offset, Int32 count, Byte[]&amp; output)
  at System.Net.Security.SecureChannel.NextMessage(Byte[] incoming, Int32 offset, Int32 count)
  at System.Net.Security.SslState.StartSendBlob(Byte[] incoming, Int32 count, AsyncProtocolRequest asyncRequest)
  at System.Net.Security.SslState.ForceAuthentication(Boolean receiveFirst, Byte[] buffer, AsyncProtocolRequest asyncRequest)
  at System.Net.Security.SslState.ProcessAuthentication(LazyAsyncResult lazyResult)
  at System.Threading.ExecutionContext.RunInternal(ExecutionContext executionContext, ContextCallback callback, Object state, Boolean preserveSyncCtx)
  at System.Threading.ExecutionContext.Run(ExecutionContext executionContext, ContextCallback callback, Object state, Boolean preserveSyncCtx)
  at System.Threading.ExecutionContext.Run(ExecutionContext executionContext, ContextCallback callback, Object state)
  at System.Net.TlsStream.ProcessAuthentication(LazyAsyncResult result)
  at System.Net.TlsStream.Write(Byte[] buffer, Int32 offset, Int32 size)
  at System.Net.ConnectStream.WriteHeaders(Boolean async)</pre>
<p>With this information, it was clear that disabling TLS 1.1 in the server caused the&nbsp;client, and the server&nbsp;was not able to interchange information because there was not another alternative, like TLS 1.2. To fix this, we had to enabled&nbsp;TLS 1.1 and TLS 1.2 explicitly in the application using the following code:</p>
<pre class="brush:csharp;auto-links:false;toolbar:false">ServicePointManager.SecurityProtocol = SecurityProtocolType.Tls11 | SecurityProtocolType.Tls12</pre>
<p>The previous line of code was required because depending on the .Net Framework version, TLS 1.2&nbsp;may not be enabled and also some old web browsers&nbsp;don't support it.</p>
<ol>
<li><strong>.NET 4.6 and above</strong>. TLS 1.2, it is supported by default.</li>
<li><strong>.NET 4.5.</strong>&nbsp;TLS 1.2, it is supported, but it&rsquo;s not a default protocol.&nbsp;You need to enable it using the following line in the Global.asax file, in the Application_Start event.
<pre class="brush:csharp;auto-links:false;toolbar:false">ServicePointManager.SecurityProtocol = SecurityProtocolType.Tls12</pre>
</li>
<li><strong>.NET 4.0.</strong>&nbsp;TLS 1.2, it is not supported, but if you have .NET 4.5+ installed, then you still can activate it with the following line.
<pre class="brush:csharp;auto-links:false;toolbar:false">ServicePointManager.SecurityProtocol = (SecurityProtocolType)3072;</pre>
</li>
</ol>
<p>I hope this use useful if you have the same issue.</p>
<p>That's it for today.</p>
<p>Until the next post!</p>
