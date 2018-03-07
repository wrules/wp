---
title: Attachment Pages Redirect
position: 2
parameters:
  - name:
    content:
content_markdown: |-
  Attachment Pages Redirect

  This rules need add in function.php file.
left_code_blocks:
  - code_block: |-
        /* Redirect attachment URLs to parent post URL */
        add_action( 'template_redirect', 'wpsites_attachment_redirect' );
        function wpsites_attachment_redirect(){
            global $post;
            if ( is_attachment() && isset($post->post_parent) && is_numeric($post->post_parent) && ($post->post_parent != 0) ) :
                wp_redirect( get_permalink( $post->post_parent ), 301 );
                exit();
                wp_reset_postdata();
            endif;
        }          
    title: PHP 
    language: php
---