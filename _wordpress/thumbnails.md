---
title: HTTPS
position: 1
parameters:
  - name:
    content:
content_markdown: |-
  Add theme support post-thumbnails;

  This rules need add in function.php file.
left_code_blocks:
  - code_block: |-
      // Function.php
      add_theme_support( 'post-thumbnails' );

      // In theme
      $postImageUrl = get_the_post_thumbnail_url(get_the_ID(),'full'); 
      echo $postImageUrl;           
    title: PHP 
    language: php
---