---
title: 自建gitlab和drawio，并同步到github
date: 2024-05-08 12:49:54
tags: IaC
---

{% plantuml %}
skinparam componentStyle rectangle
cloud {
cloud "let's encrypt" as le

cloud cloudflare  as cf

cloud github 
}
node FW{
    
    () "1443 for drawio" as 1443    
    () "8018 git https" as 8018
    () "2424 git ssh" as 2424
 
}



node NAS{
component gitlab{
   () "https" as githttps
   () "ssh" as gitssh
}
 
component "nginx" as ng {
     ()  "https" as nghttps
}
component drawio {
     ()  "http" as drawiohttp
}

 
component certbot as cb{
        database "SSL \ncertificates" as ssl
        database "cloudflare \ncredentials"
}
 }

cf-d->FW:lich.tech
cf-d->1443:ng.lich.tech

le-l->cf:验证域名
github<-d-gitlab:镜像同步

8018-d->githttps
2424-d->gitssh
1443-d->nghttps

ng-d->drawiohttp

nghttps-r->githttps#green

ng-d->ssl
gitlab-d->ssl

cb-u->cf

{% endplantuml %}


<!-- draw.io diagram -->
<div class="mxgraph" style="max-width:100%;border:1px solid transparent;" data-mxgraph="{&quot;highlight&quot;:&quot;#0000ff&quot;,&quot;nav&quot;:true,&quot;resize&quot;:true,&quot;toolbar&quot;:&quot;zoom layers tags lightbox&quot;,&quot;edit&quot;:&quot;https://lich.tech:1443/#Alich.wang%2Fhome-nas%2Fmain%2FHomeNetwork.drawio#%7B%22pageId%22%3A%22e-LJE6VTRzdldm77Gw4b%22%7D&quot;,&quot;xml&quot;:&quot;&lt;mxfile host=\&quot;lich.tech\&quot; modified=\&quot;2024-05-08T15:02:05.418Z\&quot; agent=\&quot;Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36 Edg/124.0.0.0\&quot; etag=\&quot;3n1U-SLlbh0Qb4rT9sAE\&quot; version=\&quot;24.3.1\&quot; type=\&quot;gitlab\&quot;&gt;\n  &lt;diagram name=\&quot;第 1 页\&quot; id=\&quot;e-LJE6VTRzdldm77Gw4b\&quot;&gt;\n    &lt;mxGraphModel dx=\&quot;2258\&quot; dy=\&quot;867\&quot; grid=\&quot;1\&quot; gridSize=\&quot;10\&quot; guides=\&quot;1\&quot; tooltips=\&quot;1\&quot; connect=\&quot;1\&quot; arrows=\&quot;1\&quot; fold=\&quot;1\&quot; page=\&quot;1\&quot; pageScale=\&quot;1\&quot; pageWidth=\&quot;827\&quot; pageHeight=\&quot;1169\&quot; math=\&quot;0\&quot; shadow=\&quot;0\&quot;&gt;\n      &lt;root&gt;\n        &lt;mxCell id=\&quot;0\&quot; /&gt;\n        &lt;mxCell id=\&quot;1\&quot; parent=\&quot;0\&quot; /&gt;\n        &lt;mxCell id=\&quot;TakU2glmTCrqVlv05UEU-4\&quot; value=\&quot;FW\&quot; style=\&quot;shape=umlFrame;whiteSpace=wrap;html=1;pointerEvents=0;recursiveResize=0;container=1;collapsible=0;width=160;\&quot; vertex=\&quot;1\&quot; parent=\&quot;1\&quot;&gt;\n          &lt;mxGeometry x=\&quot;230\&quot; y=\&quot;240\&quot; width=\&quot;340\&quot; height=\&quot;180\&quot; as=\&quot;geometry\&quot; /&gt;\n        &lt;/mxCell&gt;\n      &lt;/root&gt;\n    &lt;/mxGraphModel&gt;\n  &lt;/diagram&gt;\n&lt;/mxfile&gt;\n&quot;}"></div>
<script type="text/javascript" src="https://lich.tech:1443/js/viewer.min.js"></script>
