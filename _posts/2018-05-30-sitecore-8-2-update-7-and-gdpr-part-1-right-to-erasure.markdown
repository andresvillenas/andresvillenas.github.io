---
layout: post
title: "Sitecore 8.2 Update 7 and GDPR, part 1 - right to erasure"
date: 2018-05-30 23:02:00 -0500
comments: true
published: true
categories: ["blog", "archives"]
tags: []
permalink: ["/post/sitecore-8-2-update-7-and-gdpr-part-1-right-to-erasure"]
---
<!-- more -->
{% include imported_disclaimer.html %}
<p>As you probably know, the European Data Protection Regulation is applicable since May 25th, 2018 in all member states to harmonize data privacy laws across Europe. All the sites and applications that collect any data from users MUST compliant the new regulations described at&nbsp;<a href="https://gdpr-info.eu/" target="_blank">General Data Protection Regulation</a>&nbsp;site.</p>
<p>In general terms, GDPR for software vendors is about to apply all strategies available to understand what personal data is being collected, protect the privacy of that information, and provide ways to empower the end users to have control of their own data.</p>
<p>Most of the Sitecore vendors have started to take some actions to cover the new regulations.&nbsp;The initial step is to deeply understand the regulation, and then, the client and the vendor should asses what actions&nbsp;should be done to compliant the regulation.</p>
<p>From the software perspective, there are several actions that can be done to cover the most critical aspects described in the regulation. Sitecore has recently released&nbsp;<a href="https://dev.sitecore.net/Downloads/Sitecore_Experience_Platform/82/Sitecore_Experience_Platform_82_Update7.aspx">Sitecore XP 8.2 Update 7</a>&nbsp;that&nbsp;brings some new features around the regulation. Sitecore 9 brings additional and built-in features around GDRP that will be covered in another post(s).</p>
<p>One of the aspects&nbsp;covered with the update is the&nbsp;<a href="https://gdpr-info.eu/art-17-gdpr/" target="_blank">right to erasure</a>, also know as the right to be forgotten. Sitecore xDB stores the interactions of the contacts in the database. This release allows executing a new pipeline,&nbsp;removeContactPiiSensitiveData,&nbsp;to find and remove an individual's data from xDB.&nbsp;</p>
<p>The pipeline executes the following tasks:</p>
<ul>
<li>It locks the contact so that no edits can be made</li>
<li>It removes all the contact personal&nbsp;and sensitive facets</li>
<li>It removes the contact identifier</li>
<li>It removes the device last known contact ID</li>
<li>It sets the&nbsp;<em>Contact.GdprStatus.ExecutedRightToBeForgotten</em> flag to <em>true</em></li>
<li>It saves the contact</li>
<li>It removes personal and sensitive data from the interactions</li>
<li>It unlocks the contact</li>
</ul>
<p>In order to execute this pipeline, you can use the following code lines:</p>
<pre class="brush:csharp;auto-links:false;toolbar:false" contenteditable="false">var args = new Sitecore.Analytics.Pipelines.RemoveContactPiiSensitiveData.RemoveContactPiiSensitiveDataArgs(contactId)
{
  RemoveInteractionPiiSensitiveData = true
};

Sitecore.Pipelines.CorePipeline.Run("removeContactPiiSensitiveData", args); </pre>
<p>That's all for now. Next part will include some real examples of all the new pipelines applied over the Habitat example site.&nbsp;</p>
<p>Until the next post!&nbsp;</p>
<p>&nbsp;</p>
