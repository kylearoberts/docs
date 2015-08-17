---
layout: page
weight: 450
title: Whitelabel
navigation:
   show: true
---

All Whitelabel records that are successfully created on the parent account are available here. These can be attached to one or more subusers. <code>mail_domain</code> and <code>url_domain</code> should be the same in almost all cases.

{% warning %}
If your whitelabel was created after 07/06/2015 you will want to use Web API v3 to associate a whitelabel with a subusers.
<ul>
  <li>[Domain Whitelabel](https://sendgrid.com/docs/API_Reference/Web_API_v3/Whitelabel/domains.html)</li>
  <li>[Link Whitelabel](https://sendgrid.com/docs/API_Reference/Web_API_v3/Whitelabel/links.html)</li>
</ul>
{% endwarning %}

{% warning %}
Take note that IPs have records in line with Whitelabel records, but are not assigned with these commands. Subusers can be assigned to a mismatched whitelabel and IP, but should not be. There is no call at this time to note the whitelabeled rDNS record on the IP, DNS commands can be used to query these public records.
{% endwarning %}

* * * * *

{% anchor h2 %}
List 
{% endanchor %}

{% parameters list %}
 {% parameter task Yes 'Must be set to <code>list</code>' 'Task to list existing whitelabel records on the account' %}
{% endparameters %}


{% apiexample list POST https://api.sendgrid.com/apiv2/customer.whitelabel api_user=your_sendgrid_username&api_key=your_sendgrid_password&task=list %}
  {% response json %}
[
  {
    "mail_domain": "em.domain1.com",
    "url_domain": "em.domain1.com"
  },
  {
    "mail_domain": "em.domain2.com",
    "url_domain": "em.domain2.com"
  }
]
  {% endresponse %}
  {% response xml %}
<whitelabels>
   <whitelabel>
      <mail_domain>em.domain1.com</mail_domain>
      <url_domain>em.domain1.com</url_domain>
   </whitelabel>
   <whitelabel>
      <mail_domain>em.domain2.com</mail_domain>
      <url_domain>em.domain2.com</url_domain>
   </whitelabel>
</whitelabels>

  {% endresponse %}
{% endapiexample %}

* * * * *

{% anchor h2 %}
Attach 
{% endanchor %}

Attaching a new whitelabel record to a subuser also removes any previously-attached whitelabel. This does not affect already-sent messages.

{% parameters append %}
 {% parameter task Yes 'Must be set to <code>append</code>' 'Task to attach subuser to existing whitelabel record' %}
 {% parameter user Yes 'Subuser must be under your account' 'Subuser to modify whitelabel association of' %}
 {% parameter mail_domain Yes '<code>sub.domain.com</code> format' 'Existing whitelabel record to attach to subuser' %}
{% endparameters %}

{% apiexample append POST https://api.sendgrid.com/apiv2/customer.whitelabel api_user=your_sendgrid_username&api_key=your_sendgrid_password&task=append&user=subuser_username&mail_domain=em.domain1.com %}
  {% response json %}
{
  "message": "success"
}
  {% endresponse %}
  {% response xml %}
<result>
   <message>success</message>
</result>

  {% endresponse %}
{% endapiexample %}
