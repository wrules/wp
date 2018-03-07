---
title: PHPMailer
position: 1
parameters:
  - name:
    content:
content_markdown: |-
  PHPMailer https://github.com/PHPMailer/PHPMailer
  
left_code_blocks:
  - code_block: |-
        use PHPMailer\PHPMailer\PHPMailer;
        require ( "lib/PHPMailer.php" );
        require ( "lib/SMTP.php" );
        $mail = new PHPMailer(true);

        $recaptcha_secret = '6LcKtEcUAAAAAERSzSOQ8WIWOVTFHVZtjBeYaHkM';
        $response = file_get_contents("https://www.google.com/recaptcha/api/siteverify?secret=".$recaptcha_secret."&response=".$_POST['g-recaptcha-response']);
        $response = json_decode($response, true);

        if ( $response["success"] === true ) {
            $message = "<p><b>Name: </b>"        .     strip_tags($_POST['name'])      . "</p>" .
                    "<p><b>Email Address: </b>"  .     strip_tags($_POST['email'])     . "</p>" .
                    "<p><b>Subject: </b>"        .     strip_tags($_POST['subject'])   . "</p>" .
                    "<p><b>Message: </b>"        .     strip_tags($_POST['message'])   . "</p>" ;

            $mail->isHTML(true);
            $mail->IsSMTP();
            $mail->SMTPDebug = 1;
            $mail->SMTPAuth = true;
            $mail->SMTPSecure = 'ssl';
            $mail->Host = "smtp.gmail.com";
            $mail->Port = 465;
            $mail->Username = "website.email.smtp@gmail.com";
            $mail->Password = "QF49z#826V^t";
            $mail->setFrom('no-reply@elisadistefano.com', 'ElisaDiStefano');
            $mail->addAddress('taras@bowenmedia.com',"Taras");
            $mail->addAddress('elaine@winkpr.com',"Elisa");
            $mail->Subject  =  "ElisaDiStefano";
            $mail->Body     =  $message;
            $mail->send();
        }      
    title: PHP 
    language: php
---