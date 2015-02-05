PHP Simple HTML DOM Parser
====================

### 快速开始
    $html = file_get_html($url);
    foreach ($html->find('img') as $elem)
        echo $elem->src . '<br />';

### 查找
    $ret = $html->find('a')
    $ret = $html->find('a', 0);
    $ret = $html->find('div[id=foo]')
    $ret = $html->find('#div1', 0);
    $ret = $html->find('a, img');

### 获取内容
    $ret = $html->find('div.title', 0)->plaintext;

### 修改内容
    $html->find('div', 1)->class = 'bar';
    $html->find('div', 1)->innertext = 'bar';

## 网上资料
[中文文档](http://www.ecartchina.com/php-simple-html-dom/manual.htm '中文文档')



