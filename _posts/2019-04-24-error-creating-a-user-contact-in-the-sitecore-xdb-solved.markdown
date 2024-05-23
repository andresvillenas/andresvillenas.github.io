---
layout: post
title: "Error creating a user contact in the Sitecore XDb - solved"
date: 2019-04-24 12:20:00 -0500
comments: true
published: true
categories: ["blog", "archives"]
tags: []
permalink: ["/post/error-creating-a-user-contact-in-the-sitecore-xdb-solved"]
---
<!-- more -->
{% include imported_disclaimer.html %}
<p>Recently, I had to deal with an issue related to the creation of a user's contact in the Sitecore XDb, and wanted to share more details on how the problem was solved.</p>
<p>For some reason, the&nbsp;user creation process failed the first time, then,&nbsp;when the user tried to register again, the process failed at the following lines.</p>
<pre class="brush:csharp;auto-links:false;toolbar:false" contenteditable="false">ERROR Error Happened while creating a user
Exception: System.InvalidOperationException
Message: An element with the specified key already exists.
Source: Sitecore.Analytics.Model
   at Sitecore.Analytics.Model.Framework.ModelDictionaryMember`1.Create(String key)
   at Sitecore.Analytics.Model.Framework.ModelDictionaryMember`1.ElementDictionary.Create(String key)
   at Sitecore.Commerce.Pipelines.Customers.CreateContact.CreateContactInXDb.AddFacets(Contact contact, CreateUserResult createUserResult)
   at Sitecore.Commerce.Pipelines.Customers.CreateContact.CreateContactInXDb.Process(ServicePipelineArgs args)
   at (Object , Object[] )
   at Sitecore.Pipelines.CorePipeline.Run(PipelineArgs args)
   at Sitecore.Pipelines.DefaultCorePipelineManager.Run(String pipelineName, PipelineArgs args, String pipelineDomain)
   at Sitecore.Commerce.Pipelines.PipelineService.RunPipeline[TArgs](String pipelineName, TArgs args)
   at Sitecore.Commerce.Services.ServiceProvider.RunPipeline[TRequest,TResult](String pipelineName, TRequest request)</pre>
<p>Initially, I checked the Contacts collection in the MongoDb, but the user with the reported email was not there. At that point, I started to suspect that the issue was actually something related to how the user sessions are handled by Sitecore.</p>
<p>I tried to look for more information in the Sitecore Knowledge Base site, and I found this article&nbsp;<a href="https://kb.sitecore.net/articles/373937">https://kb.sitecore.net/articles/373937</a>.&nbsp;Inside there is a patch file (it works now, when I tried to get the file, it was not working and I contacted Sitecore Support, and they updated the file).</p>
<p>This patch replaces the original CreateContactInXDb method that actually checks if the contact exists first. With the patch applied in the production site, the problem was solved.</p>
<p>That's it for today.</p>
<p>Until the next post!</p>
