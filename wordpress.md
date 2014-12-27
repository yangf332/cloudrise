wordpress学习
============================

## 主题文件说明
    index.php
    single.php
    page.php
    archive.php
    search.php
    404.php

## style.css
    /*
    Theme Name: Theme Name
    Theme URI: http://wordpress.org/themes/themename
    Author: the WordPress team
    Author URI: http://wordpress.org/
    Description: 
    Version: 1.1
    License: GNU General Public License v2 or later
    License URI: http://www.gnu.org/licenses/gpl-2.0.html
    Tags: black, green, white, light, dark, two-columns, three-columns, left-sidebar, right-sidebar, fixed-layout, responsive-layout, custom-background, custom-header, custom-menu, editor-style, featured-images, flexible-header, full-width-template, microformats, post-formats, rtl-language-support, sticky-post, theme-options, translation-ready, accessibility-ready
    Text Domain: themename

    This theme, like WordPress, is licensed under the GPL.
    Use it to make something cool, have fun, and share what you've learned with others.
    */


## 相关函数

#### bloginfo($field)
    $field : name, description, admin_email, version, 

#### 获取作者信息
    the_author_meta( $field, $userID )
    $field : user_login, user_pass, user_nicename, user_email, user_url, user_registered, user_status, display_name, nickname, first_name, last_name, description, user_level, user_firstname, user_lastname, user_description, ID

#### wp_nav_menu
    主要用于生成菜单
    wp_nav_menu(array(
        'menu' => 'header-menu',
        'container' => 'nav',
        'container_class' => 'primary',
        'container_id' => '',
        'menu_class' => '',
        'menu_id' => '',
        'echo' => true,      // 是否打印，false时为赋值使用
        'depth' => 0,        // 显示菜单层数，默认为0，显示所有层
    ));

#### 日志循环
    <?php 
    if (have_posts()) {
        while (have_posts()) {
            the_title(); the_author();the_category(’, ‘);

            the_permalink(); the_ID();
            the_content();
            the_post();

            posts_nav_link(‘in between’,’before’,’after’);
            comments_popup_link(’No Comments »’, ‘1 Comment »’, ‘% Comments »’);
            edit_post_link(’Edit’, ‘ | ‘, ”);
        }
    }
        
    ?>

#### 分类链接
    wp_list_cats();

#### 归档链接
    wp_get_archives('type=monthly');

#### 日历链接
    get_calendar();

#### meta
    wp_register();
    wp_loginout();
    wp_meta();
    
## 文件拆分
    header.php, sidebar.php, footer.php
    get_header(), get_sidebar(), get_footer();
    get_template_part();

## WP的目录
    home_url()
    site_url()
    admin_url() 管理目录URL http://www.example.com/wp-admin
    includes_url() 包含目录URL http://www.example.com/wp-includes
    content_url()  文章目录URL http://www.example.com/wp-content
    plugins_url() 插件目录URL http://www.example.com/wp-content/plugins
    theme_url() 主题目录URL http://www.example.com/wp-content/themes
    wp_upload_dir() 上传目录URL (返回一个数组) http://www.example.com/wp-content/uploads

## 网上资料

[ifonder主题系列教程](http://www.ifonder.com/287.html "ifonder主题系列教程")