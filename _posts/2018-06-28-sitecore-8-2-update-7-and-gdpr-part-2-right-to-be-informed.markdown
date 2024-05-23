---
layout: post
title: "Sitecore 8.2 Update 7 and GDPR, part 2 - right to be informed"
date: 2018-06-28 11:10:00 -0500
comments: true
published: true
categories: ["blog", "archives"]
tags: []
permalink: ["/post/sitecore-8-2-update-7-and-gdpr-part-2-right-to-be-informed"]
---
<!-- more -->
{% include imported_disclaimer.html %}
<p>Continuing with the series about the Sitecore 8.2 Update 7 and the GDPR, the next topic is the&nbsp;<em>right to be informed. </em>It is described in&nbsp;the article 12 and 13 at&nbsp;<a href="https://gdpr-info.eu/" target="_blank">General Data Protection Regulation</a>&nbsp;site.</p>
<p>The individuals have the right to be informed about the collection and use of their personal data. The sites and applications must provide individuals with information including&nbsp;the purpose for processing their personal data, retention periods for that personal data, and who it will be shared with.</p>
<p>Sitecore can be configured by a developer to track the efforts to inform the users about the data collected through the privacy policy defined for the site. xDB can be extended to include a collection facet named&nbsp;<em class="scemphasis">Privacy Policy Acknowledgement.&nbsp;</em></p>
<p>When&nbsp;a user acknowledges the privacy policy, the xDB will store the Agreement Date and the Policy Identifier. This process can be done using the following classes and methods.</p>
<pre class="brush:csharp;auto-links:false;toolbar:false" contenteditable="false">IContact contact = GetContact(); // Method to get the contact
IGdprStatus gdprStatus = contact.GetFacet&lt;IGdprStatus&gt;("GdprStatus");
IPrivacyPolicyAcknowledgementElement privacyPolicyAcknowledgementElement = gdprStatus.PrivacyPolicyAcknowledgement.Values.Create();
privacyPolicyAcknowledgementElement.AgreementDate = System.DateTime.UtcNow;
privacyPolicyAcknowledgementElement.PolicyIdentifier = "2.0.1"; // Version of the privacy policy</pre>
<p>That's it for today, next time the post will be about the rights of access and data portability.</p>
<p>Until the next post!</p>
