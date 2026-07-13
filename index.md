---
# layout: home
# articles:
#   excerpt_type: html

layout: article
title: Luis Ortega Palacios | Software Engineer
cover: /assets/headshot-photo-trimmed.jpg
---

Hi, I'm Luis, a Computer Engineering graduate from the University of Granada (2026) specialized in Software Engineering and with a passion for Graphics Programming. This is my portfolio where you can see the more impressive [projects](/archive2.html) I've done. 


<!--more-->

<center>
    <h1>About Me</h1>
</center>

I'm an avid programmer who enjoys the problem-solving challenge that comes with learning skills on my own. In my free time, I like to engage with creative activities such as writing, drawing, video editing and more. 

<center>
<div class="mt-5">
    <div class="mb-0">
        <img class="image image--xl" src="/assets/headshot-photo-trimmed.jpg">
    </div>
</div>
</center>
<!--more-->

{%- assign _site_author = site.author -%}
{%- if _site_author.type == 'organization' -%}
    {%- assign _site_author_itemtype = 'http://schema.org/Organization' -%}
{%- else -%}
    {%- assign _site_author_itemtype = 'http://schema.org/Person' -%}
{%- endif -%}

<center>
    <h1>Contact me</h1>
</center>


<center>{%- include author-links.html author=_site_author -%}<center></center>