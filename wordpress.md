wp_nav_menu 和自定义菜单
wordpress学习
============================

## 主题文件说明
* index.php  ---- 首页 （必需）
* style.css  ---- 样式表及主题说明文件 （必需）
* single.php ---- 文章详细页 displaying all single posts
* page.php   ---- 创建的页面
* archive.php
* search.php ---- 搜索页
* 404.php

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
    $field : name, description, admin_email, version, stylesheet_url

#### 获取作者信息
    the_author_meta( $field, $userID )

    $field : user_login, user_pass, user_nicename, user_email, user_url, user_registered, user_status, display_name, nickname, first_name, last_name, description, user_level, user_firstname, user_lastname, user_description, ID

#### query_posts
    query_posts('cat=4');
    query_posts('category_name=Codex');
    query_posts('cat=2,6,17');
    query_posts('cat=-3');  // 排除
    query_posts(array('category_and' => array(2, 6));
    query_posts(array('category_in' => array(6)));
    query_posts(array('category_not_in' => array(2, 6));
    query_posts('tag=cooking');
    query_posts('author=3');
    query_posts('author=-3');
    query_posts('author_name=bob');
    query_posts(array('post_in' => get_option('sticky_posts'));
    query_posts(array('post_not_in' => get_option('sticky_posts'));
    query_posts('cat=6&posts_per_page=3&caller_get_posts=1');
    query_posts('year=2015&monthnum=12&day=20');
    query_posts(array(
        'p' => 20, // 文章编号
        'name' => 'about',
        'page_id' => 7, // 分页编号
        'pagename' => 'about', //
        'showposts' => 6,
        ...
    ));
    !!注意
    结束后使用wp_reset_query()
  
#### wp_get_recent_posts( $args )
     $args = array(
            'numberposts' => 10,  // 文章数量
            'offset' => 0,
            'category' => 0,
            'orderby' => 'post_date',
            'order' => 'DESC',
            'include' => ,        // 要显示文章的ID
            'exclude' => ,        // 要排除文章的ID
            'meta_key' => ,       // 自定义字段名称
            'meta_value' =>,      // 自定义字段的值
            'post_type' => 'post',
            'post_status' => 'draft, publish, future, pending, private',
            'suppress_filters' => true
    );

#### get_terms( $args )
     $args = array(
            'hide_empty' => 0, 
            'offset' => 0,
            'category' => 0,
            'orderby' => 'post_date',
            'order' => 'DESC',
            'slug'  => ,
            'hierarchical' => , // 是否返回层级分类法，默认为true
            'name_like' => ,
            'pad_counts' => ,   // 值为true时将计算包括$terms在内的所有子辈
            'get' => ,          // 默认值为空。可通过为'all'赋值来改写'hide_empty'和'child_of'
            'child_of' => ,     // 默认值为0。获取该term的所有后代
            'parent' => ,       // 默认值为0。获取该term的直系子辈（即上辈明确为该值的term）
    );

#### 显示标题
    if ( is_home() ) {
        bloginfo( 'name' ); echo ' - ';  bloginfo('description');
    } elseif ( is_category() ) {
        single_cat_title();
    } elseif ( is_single() || is_page() ) {
        single_post_title();
    } elseif ( is_search() ) {
        echo '搜索结果'; echo ' - '; bloginfo('name');
    } elseif ( is_404() ) {
        echo '页面未找到';
    } elseif ( is_user_logged_in() ) {
        echo '';
    }else {
        wp_title('', true);
    }
    ?>

#### wp_nav_menu
    主要用于生成菜单
    wp_nav_menu(array(
        'theme_location' => '', // primary|second|''
        'container' => 'nav',
        'container_class' => 'primary',
        'container_id' => '',
        'menu' => 'header-menu', 
        'menu_class' => '',
        'menu_id' => '',
        'before' => '',
        'after'    => '',
        'link_before' => '',
        'link_after'    => '',        
        'fallback_cb' => '',
        'walker' => '',         // 
        'echo' => true,      // 是否打印，false时为赋值使用
        'depth' => 0,        // 显示菜单层数，默认为0，显示所有层
        'items_wrap' => '<ol id="%1$s" class="%2$s">%3$s</ol>',
    ));

#### paginate_links
    分页导航
    global $wp_query;
    paginate_links(array(
          'base' => '%_%',
          'format' => '?page=%#%',
          'total'  => $wp_query->max_num_pages,
          'type'      => 'array',  //array|list|plain
          'current'   => max(1, get_query_var('paged')),
          'show_all'  => false,    // 是否显示所有可用页码
          'prev_next' => true,     // 是否显示上一页和下一页
          'prev_text' => __('<<'),
          'next_text' => __('>>'),
          'end_size'  => 1,        // 页面显示在列表的末尾号
          'mid_size'  => 2,        // 多少个数字到当前页面的两侧
          'add_args'  => false,    // 添加查询字符串参数到链接
          'add_fragment' => '',    // 添加文本追加到每个链接
          'before_page_number' => '', // 在页码前显示的字符串
          'after_page_number'  => '', // 在页码后显示的字符串
    ));

#### 自定义菜单
    function theme_setup()
    {
        if (function_exists('register_nav_menus')) {
            register_nav_menus( array(
                'primary'   => __( 'Navigation Menu', 'mousefinance' ),
                'secondary' => __( 'Page Menu', 'mousefinance' ),
            ) );
        }
    }


#### 日志循环
    <?php
    if ( have_posts() ) : while (have_posts() ) : the_post();
            the_title(); the_author();the_category(', ');
            the_permalink(); the_ID();
               the_content();
            posts_nav_link('in between','before','after');
            comments_popup_link('No Comments »', '1 Comment »', '% Comments »');
            edit_post_link('Edit', ' | ', '');
    endwhile;
    else :
     ..
    endif;
    wp_reset_query();
    ?>

#### 上一篇|下一篇 文章链接
    <?php if (get_previous_post(true) || get_next_post(true)) : ?>
    <div class="conten-col-02">
        <?php if (get_previous_post()) {previous_post_link(' %link ', '%title', true) ; }?>
        <?php if (get_next_post()) {next_post_link(' %link ', '%title', true) ; }?>
    </div>
    <?php endif; ?>
    // next_post_link($format=’%link &raquo;’, $link=’%title’, $in_same_cat =false, $excluded_categories = ”)

#### 根据post_id获取特色图片url
    /**
    * 根据post_id获取特色图片url
    * @param  [type] $post_id [description]
    * @param  string $size    thumbnail:缩略图 medium：中图 large：大图 full：原图
    * @return [type]          [description]
    */
    function get_attachment_image($post_id, $size = 'thumbnail') {
        $default_image = '';
        $attachment_image = wp_get_attachment_image_src( get_post_thumbnail_id( $post_id ), $size );
        $url = ( isset($attachment_image) && !empty($attachment_image) ) ? $attachment_image[0] :  $default_image;
        return $url;
    }

#### 获取参数
    get_query_var()

#### esc_attr()
    依照WordPress 编程规范，属性中出现的文本需要经过esc_attr处理，这样单引号和双引号才不会影响属性值结束，
    否则会导致无效代码和安全问题。一般要检查的地方有 title， alt， 和 value 属性.

#### 分类
    $cate = get_the_category($val['ID']);
    $cate = $cate[0];

#### 分类链接
    wp_list_cats();

#### 检查博客是否有固定链接结构、添加URL后缀斜线
    if ( get_option('permalink_structure') != '' ) { echo 'permalinks enabled' }
    if (!is_admin())  {
        function ppm_fixe_trailingslash($url, $type)
        {
            $permalink_structure = get_option('permalink_structure');
            if (!$permalink_structure || '/' === substr($permalink_structure, -1))
                return;
            if ('single' === $type || 'page' === $type)
                return $url;
            return trailingslashit($url);
        }
        add_filter('user_trailingslashit', 'ppm_fixe_trailingslash', 10, 2);
    }

#### 读取分类
    get_the_category($post->ID);

#### 归档链接
    wp_get_archives('type=monthly');

#### 评论内容
    if ( comments_open() || get_comments_number() ) {
        comments_template();
    }

#### 获取信息
    get_calendar();  // 日历链接
    get_tags();        //
    get_search_query();  // 搜索关键字

#### meta
    wp_register();
    wp_loginout();
    wp_meta();

#### 判断函数
    is_trackback()
    is_search()
    is_comments_popup()
    is_admin()
    !empty($_POST)
    is_preview()
    is_robots()
    $is_IIS && !iis7_supports_permalinks()
    is_ssl()
    is_404()
    is_singular
    is_multisite
    is_front_page
    is_attachment

#### 页面跳转
    wp_redirect( site_url(  '/wp-login.php?action=register' ) );

#### 给默认编辑器添加按钮
    function enable_more_buttons( $buttons )
    {
        $buttons[] = 'hr';
        $buttons[] = 'fontselect';
        $buttons[] = 'fontsizeselect';

        return $buttons;
    }
    add_filter('mce_buttons_3', 'enable_more_buttons'); // 里面的数字是按钮行数
    // bold ,italic ,underline ,strikethrough ,justifyleft ,justifycenter ,justifyright ,justifyfull ,bullist ,numlist ,outdent ,indent ,cut ,copy,paste ,undo ,redo ,link ,unlink ,image ,cleanup ,help ,code ,hr ,removeformat ,formatselect ,fontselect ,fontsizeselect ,styleselect ,sub ,sup ,forecolor ,backcolor ,forecolorpicker ,backcolorpicker ,charmap ,visualaid ,anchor ,newdocument ,block quote

#### 启用特色图片及设置缩略图
    add_theme_support( 'post-thumbnails' );
    add_image_size( 'zero', 70, 70, true );
    add_image_size( 'one', 125, 75, true );
    add_image_size( 'two', 250, 145, true );
    add_image_size( 'three', 500, 290, true );
    
#### 上传图片
    <?php add_thickbox(); ?>
    <script type="text/javascript">
    $('table').delegate('.thickbox', 'click', function(){
        uploadID = $(this).prev('input');
        tb_show('', 'media-upload.php?type=image&TB_iframe=true');
        return false;
    })

    window.send_to_editor = function(html) {
      imgurl = jQuery('img', html).attr('src');
      uploadID.val(imgurl);
      tb_remove();
    }
    </script>

#### 注册管理后台（外观-》小工具+菜单）
    /**
     * Register two widget areas.
     *
     */
    function xxx_widgets_init() {
        register_sidebar( array(
            'name'          => __( 'Main Widget Area', 'xxx' ),
            'id'            => 'sidebar-1',
            'description'   => __( 'Appears in the footer section of the site.', 'xxx' ),
            'before_widget' => '<aside id="%1$s" class="widget %2$s">',
            'after_widget'  => '</aside>',
            'before_title'  => '<h3 class="widget-title">',
            'after_title'   => '</h3>',
        ) );

    }
    add_action( 'widgets_init', 'xxx_widgets_init' );

#### 去除Open San字体
    function remove_open_sans()
    {
        wp_deregister_style('open-sans');
        wp_register_style('open-sans', false);
        wp_enqueue_style('open-sans', '');
    }
    add_action('init', 'remove_open_sans');

#### 自动更新
* Update Types
  - Core updates
  - Plugin updates
  - Theme updates
  - Translation file updates
* 禁用
  - define( 'AUTOMATIC_UPDATER_DISABLED', true ); 或者 add_filter( 'automatic_updater_disabled', '__return_true' ); // wp-config.php, completely disable all types of automatic updates
  - define( 'WP_AUTO_UPDATE_CORE', false );  // wp-config.php, disable core updates
  - define( 'WP_AUTO_UPDATE_CORE', 'minor' ); // 启用小版本核心更新
  - define( 'WP_AUTO_UPDATE_CORE', 'major' ); // 启用大版本核心更新
  - add_filter( 'auto_update_translation', '__return_false' );  // 翻译文件更新
  - add_filter( 'auto_update_theme', '__return_true' );
  - add_filter( 'auto_update_plugin', '__return_true' );

#### $wpdb对象
    global $wpdb;
    $wpdb->query('query'); // select, delete, update
    $wpdb->insert( $table, array $data, array $format); //
    $wpdb->update( $table, $data, $where, $format = null, $where_format)
    $wpdb->prepare( $sql, array('p1', 'p2'))
    $wpdb->get_results('query', output_type)
    $wpdb->get_var( $wpdb->prepare( $sql ) );
    $wpdb->flush();

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
    get_template_directory_uri()

## Plugin
* Acurax Social Icons Options 设置各社交网络链接
* Lightbox Gallery

## 开发插件
    wp-content/plugins/plugin_name
    wp-content/plugins/plugin_name.php
    wp-content/plugins/plugin_name_function.php // 通用方法
    wp-content/plugins/plugin_name_page.php      // html
    /*
    Plugin Name: plugin name
    Description: plugin desc
    Version: 1.0
    Author: author
    License: GPL
    */
    /* 注册激活插件时要调用的函数 */
    register_activation_hook( __FILE__, 'plugin_install');
    /* 注册停用插件时要调用的函数 */
    register_deactivation_hook( __FILE__, 'plugin_remove' );
    function plugin_install() {
        /* 在数据库的 wp_options 表中添加一条记录，第二个参数为默认值 */
        add_option("plugin_text", "", '', 'yes');
    }
    function plugin_remove() {
        /* 删除 wp_options 表中的对应记录 */
        // delete_option('plugin_text');
    }
    if( is_admin() ) {
        /*  利用 admin_menu 钩子，添加菜单 */
        add_action('admin_menu', 'display_plugin_menu');
    }
    function display_plugin_menu() {
        /* add_options_page( $page_title, $menu_title, $capability, $menu_slug, $function);  */
        /* 页名称，菜单名称，访问级别，菜单别名，点击该菜单时的回调函数（用以显示设置页面） */
        add_options_page('Set Recommend', 'plugin_name', 'editor','display_plugin', 'display_plugin_page');
    }
    function display_plugin_page()
    {
    // main function
    }

## FAQ
* 加载Google Fonts导致访问变慢？ 安装Disable Google Fonts插件并启用
* 引用wp-blog-header.php报404？应该引用wp-load.php文件


## 网上资料
[中文文档](http://codex.wordpress.org/zh-cn:Main_Page '中文文档')
[函数参考](http://codex.wordpress.org/zh-cn:%E5%87%BD%E6%95%B0%E5%8F%82%E8%80%83 '函数参考')
[条件标签](http://codex.wordpress.org/zh-cn:%E6%9D%A1%E4%BB%B6%E6%A0%87%E7%AD%BE "条件标签")
[模板标签](http://codex.wordpress.org/zh-cn:%E6%A8%A1%E6%9D%BF%E6%A0%87%E7%AD%BE '模板标签')
[插件API](http://codex.wordpress.org/zh-cn:%E6%8F%92%E4%BB%B6_API '插件API')

[Action Reference](http://codex.wordpress.org/Plugin_API/Action_Reference "Action Reference")
[ifonder主题系列教程](http://www.ifonder.com/287.html "ifonder主题系列教程")
[WordPress.org China](http://cn.wordpress.org/ 'WordPress.org China')
[hook机制](http://www.cnblogs.com/jocobHerbertPage/archive/2012/09/17/2689780.html 'hook机制')
