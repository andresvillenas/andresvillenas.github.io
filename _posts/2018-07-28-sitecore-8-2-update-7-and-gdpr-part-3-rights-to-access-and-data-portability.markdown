---
layout: post
title: "Sitecore 8.2 Update 7 and GDPR, part 3 - rights to access and data portability"
date: 2018-07-28 00:59:00 -0500
comments: true
published: true
categories: ["blog", "archives"]
tags: []
permalink: ["/post/sitecore-8-2-update-7-and-gdpr-part-3-rights-to-access-and-data-portability"]
---
<!-- more -->
{% include imported_disclaimer.html %}
<p>Continuing with the series about the Sitecore 8.2 Update 7 and the GDPR, the next topic is the&nbsp;<em>rights to access and data portability.&nbsp;</em>It is described in&nbsp;the article 15 and 20 of the&nbsp;<a href="https://gdpr-info.eu/" target="_blank">General Data Protection Regulation</a>&nbsp;site.</p>
<p>The individuals have the right to access and&nbsp;receive the data concerning him or her. The sites and applications must provide a way to access and move the data to another controller, in a commonly used and machine-readable format.&nbsp;</p>
<p>Sitecore can be configured to enable the individuals to see what personal data is processed and stored. Also, it can be configured to allow the subjects to have a copy of the personal data.</p>
<p>In the following snippet, you can see an example of how to extract the information stored for a specific contact.</p>
<pre class="brush:csharp;auto-links:false;toolbar:false" contenteditable="false">var cursor = _repository.GetInteractionCursor(contactId, visitsToLoadPerBatch, maximumSaveDate);
var interactions = new List&lt;VisitData&gt;();
while (cursor.HasNextBatch)
{
  interactions.AddRange(cursor.GetNextBatch());
}</pre>
<p>That's it for today.</p>
<p>Until the next post!</p>
