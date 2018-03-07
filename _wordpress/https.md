---
title: HTTPS
position: 1
parameters:
  - name:
    content:
content_markdown: |-
  Best-practice HTTPS configurations for WordPress to fix mixed-content browser warnings and excessive redirects.

  This rules need add in wp-config.php file.
left_code_blocks:
  - code_block:
      if (isset($_ENV['PANTHEON_ENVIRONMENT']) && php_sapi_name() != 'cli') {
        // Redirect to https://$primary_domain in the Live environment
        if ($_ENV['PANTHEON_ENVIRONMENT'] === 'live') {
          $primary_domain = 'websitename.com';
        }
        else {
          // Redirect to HTTPS on every Pantheon environment.
          $primary_domain = $_SERVER['HTTP_HOST'];
        }
        if ($_SERVER['HTTP_HOST'] != $primary_domain || !isset($_SERVER['HTTP_USER_AGENT_HTTPS']) || $_SERVER['HTTP_USER_AGENT_HTTPS'] != 'ON' ) {
          # Name transaction "redirect" in New Relic for improved reporting (optional)
          if (extension_loaded('newrelic')) {
            newrelic_name_transaction("redirect");
          }
          header('HTTP/1.0 301 Moved Permanently');
          header('Location: https://'. $primary_domain . $_SERVER['REQUEST_URI']);
          exit();
        }
      }            
    title: PHP 
    language: php
---