---
title: Recaptcha
position: 2
parameters:
  - name:
    content:
content_markdown: |-
  Goolge https://www.google.com/recaptcha/intro/android.html
  
left_code_blocks:
  - code_block: |-
        $formRestaurant = $('#formRestaurant');
        $formRestaurant.submit(function (e) {
            e.preventDefault();
            if (grecaptcha.getResponse() == "") {
                $("#success").fadeOut(50);
                $("#error").fadeIn();
            } else {
                $url = "/grillo/email/send_restaurant.php";
                $.ajax({
                    type: "POST",
                    url: $url,
                    data: $("#formRestaurant").serialize(),
                    success: function () {
                        $formRestaurant[0].reset();
                        window.location.href = "/grillo/thankyou.php";
                    }
                });
            }
        });
    title: JS 
    language: javascript
- code_block: |-
      use PHPMailer\PHPMailer\PHPMailer;
        require ( "lib/PHPMailer.php" );
        require ( "lib/SMTP.php" );
        $mail = new PHPMailer(true);
        $recaptcha_secret = "6LdUWFAUAAAAADIilCZ-gjXJQLaSzQHX6ox9jEfd";
        $response = file_get_contents("https://www.google.com/recaptcha/api/siteverify?secret=".$recaptcha_secret."&response=".$_POST['g-recaptcha-response']);
        $response = json_decode($response, true);

        if ( $response["success"] === true ) {
            $message = "<p><b>First Name: </b>" . strip_tags($_POST['fname']) . "</p>" .
                "<p><b>Last Name: </b>" . strip_tags($_POST['lname']) . "</p>" .
                "<p><b>Email: </b>" . strip_tags($_POST['email']) . "</p>" .
                "<p><b>Phone: </b>" . strip_tags($_POST['phone']) . "</p>" .
                "<p><b>City: </b>" . strip_tags($_POST['city']) . "</p>" .
                "<p><b>State: </b>" . strip_tags($_POST['state']) . "</p>" .
                "<p><b>Zipcode: </b>" . strip_tags($_POST['zipcode']) . "</p>" .
                "<p><b>Quote: </b>" . strip_tags($_POST['quote']) . "</p>" .
                "<p><b>Comments/Questions: </b>" . strip_tags($_POST['comments']) . "</p>";
            $mail->isHTML(true);
            $mail->IsSMTP();
            $mail->SMTPDebug = 1;
            $mail->SMTPAuth = true;
            $mail->SMTPSecure = 'ssl';
            $mail->Host = "smtp.gmail.com";
            $mail->Port = 465;
            $mail->Username = "website.email.smtp@gmail.com";
            $mail->Password = "QF49z#826V^t";
            $mail->setFrom('website.email.smtp@gmail.com', 'Grillo & Associates');
            $mail->addAddress('taras@bowenmedia.com', "Taras");
            $mail->Subject = "Grillo & Associates";
            $mail->Body = $message;
            $mail->send();
        }
    title: PHP
    language: php    
---