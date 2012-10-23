bootstrap 标签集
============================

## Scaffolding

### Grid system

	basic:
        div.row>div.span4+div.span8
    offset: 
        div.row>div.span4.offset4
    nesting:
        div.row>div.span9>div.row>div.span6+div.span4

### Fluid grid system

    fluid:
    	div.row-fluid>span4+span8

### Layouts

	basic:
		div.container
	fluid:
		div.container-fluid

### Enabling responsive features

	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link href="assets/css/bootstrap-responsive.css" rel="stylesheet">

  Responsive utility classes

    * .visible-phone
    * .visible-tablet
    * .visible-desktop
    * .hidden-phone
    * .hidden-tablet
    * .hidden-desktop

## Base CSS

### Typography

  Emphasis classes

    p.lead
    p.muted
    p.text-warning
    p.text-error
    p.text-info
    p.text-success

    address>br+br+br

    .pull-right

    ul.unstyled

    dl.dl-horizontal>dt+dd

### Code

    pre.pre-scrollable

### Tables 

    table.table
    table.table.table-striped //添加条纹
    table.table-bordered
    table.table.table-hover
    //更紧凑
    table.table.table-condensed

    tr.success
    tr.error
    tr.warning
    tr.info

### Forms

    basic:
      form>legend+label+input:text+span+label>input:checkbox
    search form:
      form.form-search>input:text.input-medium.search-query
    inline form:
      form.form.form-inline>input*2+label>input
    horizontal form:
      form.form-horizontal>div.control-group*3>label.control-label+div.controls>input

  input

      inline checkboxes:
        label.checkbox.inline*3>input.checkbox

  extending form controls

      prepended:
        div.input-prepend>span.add-on+input
      append:
        div.input-append>input+span.add-on
      combined:
        div.input-prepend.input-append>span.add-on+input+span.add-on
      buttons instead of text:
        input.input-append>input+button.btn*2

  control sizing

      input.mini
      input-small
      input-medium
      input-large
      input-xlarge
      input-xxlarge

  grid sizing

      .span1 - .span12
  	  div.controls.controls-row>input.span4+input.span1

  uneditable inputs  

      span.uneditable-input

  form actions

      form-actions>button.btn.btn-primary+button.btn //自动设置样式

  help text

      input+span.help-inline	  
      input+span.help-block

  validation states

      div.control-group.info>label.control-label+div.controls>input+span.help-inline
      div.control-group.warning>label.control-label+div.controls>input+span.help-inline
      div.control-group.error>label.control-label+div.controls>input+span.help-inline
      div.control-group.success>label.control-label+div.controls>input+span.help-inline

### Button

    style:
      button.btn
      button.btn.btn-primary
      button.btn.btn-info
      button.btn.btn-success
      button.btn.btn-warning
      button.btn.btn-danger
      button.btn.btn-inverse
      button.btn.btn-link
    size:
      button.btn.btn-large
      button.btn.btn-small
      button.btn.btn-mini
    block:
      button.btn-large.btn-block
    disable:
      button.btn.disabled
      a.btn.btn.disabled

### Images

    img.img-rounded
    img.img-circle
    img.img-polaroid

### Icons by Glyphicons

    icon-glass;icon-music;icon-search;icon-envelope;icon-heart;
    icon-star;icon-star-empty;icon-user;icon-film;icon-th-large;
    icon-th;icon-th-list;icon-ok;icon-remove;icon-zoom-in;
    icon-zoom-out;icon-off;icon-signal;icon-cog;icon-trash;
    icon-home;icon-file;icon-time;icon-road;icon-download-alt;
    icon-download;icon-upload;icon-inbox;icon-play-circle;icon-repeat;
    icon-refresh;icon-list-alt;icon-lock;icon-flag;icon-headphones;
    icon-volume-off;icon-volume-down;icon-volume-up;icon-qrcode;icon-barcode;
    icon-tag;icon-tags;icon-book;icon-bookmark;icon-print;
    icon-camera;icon-font;icon-bold;icon-italic;icon-text-height;
    icon-text-width;icon-align-left;icon-align-center;icon-align-right;icon-align-justify;
    icon-list;icon-indent-left;icon-indent-right;icon-facetime-video;icon-picture;
    icon-pencil;icon-map-marker;icon-adjust;icon-tint;icon-edit;
    icon-share;icon-check;icon-move;icon-step-backward;icon-fast-backward;
    icon-backward;icon-play;icon-pause;icon-stop;icon-forward;
    icon-fast-forward;icon-step-forward;icon-eject;icon-chevron-left;icon-chevron-right;
    icon-plus-sign;icon-minus-sign;icon-remove-sign;icon-ok-sign;icon-question-sign;
    icon-info-sign;icon-screenshot;icon-remove-circle;icon-ok-circle;icon-ban-circle;
    icon-arrow-left;icon-arrow-right;icon-arrow-up;icon-arrow-down;icon-share-alt;
    icon-resize-full;icon-resize-small;icon-plus;icon-minus;icon-asterisk;
    icon-exclamation-sign;icon-gift;icon-leaf;icon-fire;icon-eye-open;
    icon-eye-close;icon-warning-sign;icon-plane;icon-calendar;icon-random;
    icon-comment;icon-magnet;icon-chevron-up;icon-chevron-down;icon-retweet;
    icon-shopping-cart;icon-folder-close;icon-folder-open;icon-resize-vertical;icon-resize-horizontal;
    icon-hdd;icon-bullhorn;icon-bell;icon-certificate;icon-thumbs-up;
    icon-thumbs-down;icon-hand-right;icon-hand-left;icon-hand-up;icon-hand-down;
    icon-circle-arrow-right;icon-circle-arrow-left;icon-circle-arrow-up;icon-circle-arrow-down;icon-globe;
    icon-wrench;icon-tasks;icon-filter;icon-briefcase;icon-fullscreen;

    i.icon-search.icon-white
    example:
      div.btn-group>a*4>i.icon-align-left
    dropdown
      //!!todo
      div.btn-group>a.btn.btn-primary>i.icon-user.icon-white
                    a.btn.dropdown-toggle>span.caret
                    ul.dropdown-menu>li*3>a>i.icon-pencil
    small button:
      a.btn.btn-small>i.icon-star

## Components

### Dropdowns
    
  require: dropdowns javascript plugin

    basic:
      ul.dropdown-menu>li*3>a
                       li.divider
    markup:
      div.dropdown>ul.dropdown-menu>li*3>a
    options:
      ul.dropdown-menu.pull-right
    sub menus: 
      ul.dropdown-menu>li.dropdown-submenu>ul.dropdown-menu

### Button groups

    basic:
      div.btn-group>button.btn*3
    multiple button groups:
      div.btn-toolbar>div.btn-group
    vertical button groups:
      div.btn-group.btn-group-vertical

### Button dropdown menu

    basic:
      div.btn-group>a.btn.dropdown-toggle+ul.dropdown-menu

  Dropup menus

    div.btn-group.dropup>button.btn+button.btn.dropdown-toggle+ul.dropdown-menu

### Navs

    basic:
      ul.nav.nav-tabs>li.active+li*2
    basec pills:
      ul.nav.nav-pills>li.active+li*2
    disabled state:
      li.disabled
    stackable:
      ul.nav.nav-tabs.nav-stacked>li.active+li*2
    stacked pills:
      ul.nav.nav-pills.nav-stacked>li.active+li*2

  Nav lists

    ul.nav.nav-list>li.nav-header+li.active+li*3
    ul.nav.nav-list>li.divider+li.active+li*3

  Tabbable nav - require: jq plugin

    div.tabbable>ul.nav.nav-tabs>li.active+li
                 div.tab-content>div.tab-pane.active>p
                                >div.tab-pane>p
    .fade   

  Tabbable in any direction

    bottom:
      div.tabbable.tabs-below>div.tab-content+ul.nav.nav-tabs
    left:
      div.tabbable.tabs-left>ul.nav.nav-tabs+div.tab-content
    right:
      div.tabbable.tabs-right>ul.nav.nav-tabs+div.tab-content

### Navbar

    basic:
      div.navbar>div.navbar-inner>a.brand+ul.nav>li.active+li*2
    ...

### Breadcrumbs

    ul.breadcrumb>li*2>a+span.divider
                  li.active

### Pagination

    div.pagination>ul>li*6>a
                      li.disabled
                      li.active
    div.pagination.pagination-center>
    div.pagination.pagination-right>

### Pager

    basic:
      ul.pager>li*2>a
    aligned links:
      ul.pager>li.previous+li.next>a
  
### Labels and badges

    span.label
    span.label.label-success
    span.label.label-warning
    span.label.label-important
    span.label.label-info
    span.label.label-inverse

    span.badge
    span.badge.badge-success
    span.badge.badge-warning
    span.badge.badge-important
    span.badge.badge-info

### Typography

    div.hero-unit>h1+p+p>a.btn.btn-primary.btn-large

    span.label.label-inverse

  Page header

    div.page-header>h1+small

### Thumbnails

### Alerts

    default:
      div.alert>button.close+strong
    options:
      div.alert.alert-block
      div.alert.alert-error
      div.alert.alert-warning
      div.alert.alert-info

### Progress bars

    basic:
      div.progress.progress-striped>div.bar (style="width:40%")
    animated:
      div.progress.progress-striped.active>div.bar
    stacked:
      div.progress>div.bar.bar-success+div.bar.bar-warning+div.bar.bar-danger
    additional colors:
      div.progress.progress-info>div.bar
      div.progress.progress-success>div.bar
      div.progress.progress-warning>div.bar
      div.progress.progress-danger>div.bar
    striped bars:
      div.progress.progress-info.progress-striped>div.bar
      div.progress.progress-success.progress-striped>div.bar
      div.progress.progress-warning.progress-striped>div.bar
      div.progress.progress-danger.progress-striped>div.bar




  	  	

  





