---
title: Simple ajax
position: 1
parameters:
  - name:
    content:
content_markdown: |-
  Simple ajax send data
  
left_code_blocks:
  - code_block: |-
        window.onload = function () {
            $form = $('#contactForm');
            $form.submit(function (e) {
                e.preventDefault();
                if (grecaptcha.getResponse() == "") {
                    $("#success").fadeOut(50);
                    $("#error").fadeIn();
                } else {
                    $url = "/wp-content/themes/terminal/email/send.php";
                    $.ajax({
                        type: "POST",
                        url: $url,
                        data: $("#contactForm").serialize(),
                        success: function () {
                            $form[0].reset();
                            window.location.href = "/thank-you-page/";
                        }
                    });
                }
            });
        };
    title: JS 
    language: javascript
---