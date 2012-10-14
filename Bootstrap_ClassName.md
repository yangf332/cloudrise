bootstrap 标签集
============================

## Scaffolding

### grid 

	basic:
        div.row>div.span4+div.span8
    offset: 
        div.row>div.span4.offset4
    nesting:
        div.row>div.span9>div.row>div.span6+div.span4
    fluid:
    	div.row-fluid>span4+span8

### layouts

	basic:
		div.container
	fluid:
		div.container-fluid

### Enabling responsive features

	<meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="assets/css/bootstrap-responsive.css" rel="stylesheet">

### Responsive utility classes

    * .visible-phone
    * .visible-tablet
    * .visible-desktop
    * .hidden-phone
    * .hidden-tablet
    * .hidden-desktop

## Base CSS

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

  table 

    table.table
    table.table.table-striped
    table.table-bordered
    table.table.table-hover
    //更紧凑
    table.table.table-condensed

    tr.success
    tr.error
    tr.warning
    tr.info

  forms

    base:
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

  form actions //这个没看明白

      form-actions>button*2

  help text

      input+span.help-inline	  
      input+span.help-block

  validation states

      div.control-group.info>label.control-label+div.controls>input+span.help-inline
      div.control-group.warning>label.control-label+div.controls>input+span.help-inline
      div.control-group.error>label.control-label+div.controls>input+span.help-inline
      div.control-group.success>label.control-label+div.controls>input+span.help-inline

  button

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

  images

    img.img-rounded
    img.img-circle
    img.img-polaroid

  icons

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


  navigation

    


  	  	

  





