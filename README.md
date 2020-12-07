# 国际咖啡品牌网站CSS样式修复, 修复移动端导航无法点击.

## 方案一(调用《andkinV2响应式风格》模板的移动端导航栏) :

### 1. 在 footer.html 文件中渲染移动端导航栏内容

```html
<div id="tm-offcanvas" class="uk-offcanvas">
 <div class="uk-offcanvas-bar">
  <ul class="uk-nav uk-nav-offcanvas uk-nav-parent-icon" data-uk-nav="{multiple:true}">
   <li class="uk-nav-header">栏目导航</li>



   <!-- 移动端导航栏内容在此渲染 -->
   {pc:content action="category" catid="0" num="4" siteid="$siteid" order="listorder ASC"}
   {loop $data $r}
   <li class="uk-parent{if $catid==$r[catid] || $top_parentid==$r[catid]} uk-active{/if}">< a href=" "><i class="uk-icon-folder-open"></i> {$r[catname]}</ a>
    {pc:content action="category" catid="$r[catid]" num="25" siteid="{$siteid}" order="listorder ASC"}
    {if $data}
    <ul class="uk-nav-sub">
     {loop $data $v}
     <li>< a href="{$v[url]}">{$v[catname]}</ a></li>
     {/loop}
    </ul>
    {/if}
    {/pc}
   </li>
   {/loop}
   {/pc}
   <!-- 移动端导航栏内容渲染结束 -->



   <li class="{if $catid==10 || $top_parentid==$r[catid]} uk-active{/if}">< a href="{$CATEGORYS[10][url]}"><i class="uk-icon-folder-open"></i> {$CATEGORYS[10][catname]}</ a></li>
   <li class="{if $catid==29} uk-active{/if}">< a href="{$CATEGORYS[29][url]}"><i class="uk-icon-folder-open"></i> {$CATEGORYS[29][catname]}</ a></li>
   <li class="{if $catid==3} uk-active{/if}">< a href="{$CATEGORYS[3][url]}"><i class="uk-icon-folder-open"></i> {$CATEGORYS[3][catname]}</ a></li>
  </ul>
  <form class="uk-search" data-uk-search action="{APP_PATH}index.php" method="get" target="_blank">
   <input type="hidden" name="m" value="search"/>
   <input type="hidden" name="c" value="index"/>
   <input type="hidden" name="a" value="init"/>
   <input type="hidden" name="typeid" value="1" id="typeid"/>
   <input type="hidden" name="siteid" value="{$siteid}" id="siteid"/>
   <input class="uk-search-field" type="search" name="q" placeholder="输入要搜索的关键字...">
   <button class="uk-search-close" type="reset"></button>
  </form>
  <div class="uk-panel">
   <h3 class="uk-panel-title">微信订阅</h3>
   打开微信，点击底部的“通讯录”，点击右上角的 “添加” 搜号码 < a href="{siteurl($siteid)}/assets/images/getqrcode.jpg" title="安妮导刊微信二维码" target="_blank">andk_in</ a> 或查找公众号 安妮导刊 即可。
  </div>
 </div>
</div>
```

---

## 方案二 :

### 1. 在 footer.html 文件添加如下 js 代码

```html
<script>
    var cls = 'mobile-client';
    var style = '';
    style += '<style type="text/css">';
    style += '  @media (max-width: 767px) {';
    style += '      ul.uk-navbar-nav {';
    style += '          background: #fff;';
    style += '          width: 30%;';
    style += '          margin-top: 40px;';
    style += '          position: absolute;';
    style += '          right: 0;';
    style += '      }';
    style += '      ul.uk-navbar-nav > li {';
    style += '          display: block;';
    style += '          width: 100%;';
    style += '          margin-left: 0;';
    style += '      }';
    style += '      div.uk-navbar-flip {';
    style += '          position: absolute;';
    style += '          top: 0;';
    style += '          right: 10px;';
    style += '      }';
    style += '  }';
    style += '</style>';
    $(document).on('click', '.uk-navbar-flip', function()
    {
        if (!$(this).hasClass(cls))
        {
            $(this).addClass(cls);
            $('head').append($(style));
            console.log('yes');
            $('.uk-parent > div.uk-dropdown-navbar').remove();
        }

        $('.uk-navbar-nav').toggle();
    });
</script>
```
