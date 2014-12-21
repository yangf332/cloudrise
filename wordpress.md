wordpress学习
============================

## 文件说明

## 相关函数

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
    

## 网上资料