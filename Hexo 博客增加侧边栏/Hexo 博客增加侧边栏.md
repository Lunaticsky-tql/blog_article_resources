---
title: Hexo 博客增加侧边栏
categories: 博客搭建
tags: [Hexo, 前端]
---
### Hexo 博客增加侧边栏

根据https://github.com/qixa/hexo-theme-fluid-mod修改

#### 修改主题配置文件

color下新增属性

```css
  # 侧边栏颜色
  sidebar_text_color: "#3c4858"
  sidebar_background_color: "rgba(246, 248, 250, 0.82)" #f6f8fad1
  sidebar_button_color: "#99a9bf"
  sidebar_button_shift_color: "#ffffff"
  sidebar_button_shift_shadow: "0.1rem 0.1rem 0.5rem #3e3e3e"
  sidebar_about_link_color: "#3c4858"
  sidebar_about_link_hover_color: "#57A7D9"
  sidebar_avatar_border: "5px solid #ffffff"
  sidebar_subtitle_color: "#999999"
  sidebar_friend_title: "#ffffff"
  sidebar_friend_title_background: "#8FABD7"
  sidebar_friend_link: "#3c4858"
  sidebar_friend_link_hover: "#ffffff"
  sidebar_friend_li_border: "1px dashed #bdbdbd"
  sidebar_friend_li_hover: "#57A7D9"
  sidebar_friend_ico: "#bfbfbf"
```

新增全局属性

```css
sidebar:
    enable: true
    name: Lunatic sky
    introduce:  # 支持 HTML，留空则使用网站subtitle
    icons: 
        "fab fa-github": https://github.com/Lunaticsky-tql
        "fas fa-envelope": mailto:******

#---------------------------
# 侧边栏链接
# Links
#---------------------------    
sidebar_links:
  "my repository": https://github.com/Lunaticsky-tql?tab=repositories
```



#### 新增侧边栏模板文件

新建layout/_partial/sidebar.ejs

```javascript
&lt;% if(theme.sidebar.enable){ %&gt;
</p>, <div class="sidebar-hide" id="sidebar">
<span class="sidebar-button sidebar-button-shift" id="toggle-sidebar">
<i aria-hidden="true" class="fa fa-arrow-right on"></i>
</span>
<div class="sidebar-overlay"></div>
<div class="sidebar-intrude">
<div class="sidebar-avatar">
<img alt="avatar" src="&lt;%- url_for(theme.avatar) %&gt;" srcset="&lt;%- url_for(theme.avatar) %&gt;"/>
</div>
<div class="text-center sidebar-about">
<p class="h3 sidebar-author">&lt;%= theme.sidebar.name || config.title %&gt;</p>
<p class="sidebar-subtitle">&lt;%- theme.sidebar.introduce || config.subtitle %&gt;</p>
      &lt;% for(var i in theme.sidebar.icons) { %&gt;
        <a class="h4" href="&lt;%- theme.sidebar.icons[i] %&gt;" target="_blank">
<i aria-hidden="true" class="&lt;%- i %&gt;"></i>
</a>
          
      &lt;% } %&gt;
    </div>
<div class="sidebar-friend">
<p class="h6 sidebar-friend-title">
<span class="sidebar-label-left"><i class="fas fa-user-friends"></i></span>
<span class="sidebar-label">相关链接</span>
</p>
<ul class="list-group">
        &lt;% for(var i in theme.sidebar_links) { %&gt;
          <a href="&lt;%- theme.sidebar_links[i] %&gt;" target="_blank">
<li class="list-group-item">
<i class="fas fa-quote-left"></i> 
              &lt;%- i %&gt;
            </li>
</a>
        &lt;% } %&gt;
    </ul>
</div>
</div>
</div>, '\n<% } %>\n```\n\nlayout.ejs中引入\n\n![image-20220919235231945](https://raw.githubusercontent.com/Lunaticsky-tql/my_picbed/main/Hexo%20%E5%8D%9A%E5%AE%A2%E5%A2%9E%E5%8A%A0%E4%BE%A7%E8%BE%B9%E6%A0%8F/20220920002715526487_276_image-20220919235231945.png)\n\n```javascript\n<%- partial(\'_partials/sidebar.ejs\') %>\n```\n\n#### 修改CSS文件\n\nsource/css/_variables/base.styl\n\n增加侧边栏相关变量\n\n```css\n//toc\n$tocbot-link-shadow = theme-config("color.tocbot_link_shadow", "0.1em 0.1em 0.2em #ffffff")\n$tocbot-active-link-shadow = theme-config("color.tocbot_active_link_shadow", "0.1em 0.1em 0.2em #ffbcbc")\n\n//sidebar\n$sidebar-text-color = theme-config("color.sidebar_text_color", "#3c4858")\n$sidebar-background-color = theme-config("color.sidebar_background_color", "#f6f8fad1")\n$sidebar-button-color = theme-config("color.sidebar_button_color", "#99a9bf")\n$sidebar-button-shift-color = theme-config("color.sidebar_button_shift_color", "#ffffff")\n$sidebar-button-shift-shadow = theme-config("color.sidebar_button_shift_shadow", "0.1rem 0.1rem 0.5rem #3e3e3e")\n$sidebar-about-link-color = theme-config("color.sidebar_about_link_color", "#3c4858")\n$sidebar-about-link-hover-color = theme-config("color.sidebar_about_link_hover_color", "#fe4365")\n$sidebar-avatar-border = theme-config("color.sidebar_avatar_border", "5px solid #ffffff")\n$sidebar-subtitle-color = theme-config("color.sidebar_subtitle_color", "#999999")\n$sidebar-friend-title = theme-config("color.sidebar_friend_title", "#ffffff")\n$sidebar-friend-title-background = theme-config("color.sidebar_friend_title_background", "#fe91b4")\n$sidebar-friend-link = theme-config("color.sidebar_friend_link", "#3c4858")\n$sidebar-friend-link-hover = theme-config("color.sidebar_friend_link_hover", "#ffffff")\n$sidebar-friend-li-border = theme-config("color.sidebar_friend_li_border", "1px dashed #bdbdbd")\n$sidebar-friend-li-hover = theme-config("color.sidebar_friend_li_hover", "#fe91b4")\n$sidebar-friend-ico = theme-config("color.sidebar_friend_ico", "#bfbfbf")\n```\n\nlayout/_partials/css.ejs\n\n引入需要的图标字体\n\n```javascript\n<%- css_ex(theme.static_prefix.font_awesome, "css/all.min.css") %>\n```\n\n#### JS 文件\n\nsource/js/main.js\n\n增加[侧边栏](https://github.com/qixa/hexo-theme-fluid-mod#侧边栏模板文件)相关控制代码\n\n```javascript\n/* Sidebar */\nvar toggleSidebar = function(){\n  $("#sidebar").toggleClass(\'sidebar-hide\');\n  $("#toggle-sidebar").toggleClass(\'sidebar-button-shift\');\n}\nvar hideSidebar = function(){\n  $("#sidebar").addClass(\'sidebar-hide\');\n  $("#toggle-sidebar").addClass(\'sidebar-button-shift\');\n}\n$("#toggle-sidebar").on("click",toggleSidebar);\n$("header").on("click",hideSidebar);\n$("#mainContent").on("click",hideSidebar);\n$("#footerContent").on("click",hideSidebar);\n```\n\nlayout/_partials/scripts.ejs中进行引用\n\n![image-20220920000758138](https://raw.githubusercontent.com/Lunaticsky-tql/my_picbed/main/Hexo%20%E5%8D%9A%E5%AE%A2%E5%A2%9E%E5%8A%A0%E4%BE%A7%E8%BE%B9%E6%A0%8F/20220920002717155064_217_image-20220920000758138.png)\n\n```javascript\n<%- js_ex(theme.static_prefix.internal_js, \'main.js\') %>\n