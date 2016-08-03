---
layout: post
title: Get current order object in email footer template
category: wordpress
tags: wordpress, woocommerce
---

The current order object is not available in ```email-footer.php```.

## Analysis

If you check out the [email_footer](https://github.com/woothemes/woocommerce/blob/2.6.4/includes/class-wc-emails.php#L194) function in [class-wc-emails.php](https://github.com/woothemes/woocommerce/blob/2.6.4/includes/class-wc-emails.php#L194), you will find it does not pass the order object into the template, which makes sense. The ```email-footer.php``` is used in all the email templates including [customer-new-account.php](https://github.com/woothemes/woocommerce/blob/2.6.4/templates/emails/customer-new-account.php#L37).

Digging deeper, you will find that in the order template files, they do have pass the email object(```WC_Email```) to the ```woocommerce_email_footer``` action hook. For example, [admin-new-order.php](https://github.com/woothemes/woocommerce/blob/2.6.4/templates/emails/admin-new-order.php#L53), and the order object is available at ```$email->object```.

## Solution

### Step 1

Set a global variable ```wc_email```(You may name it whatever you want) to reference the current email object in the ```woocommerce_email_footer``` action hook. Be sure to set the priority less than 10, so that it runs before woocommerce's ```email_footer``` function.

~~~
// In your theme's functions.php

/**
 * Make sure the email instance is available in email-footer template
 */
add_action('woocommerce_email_footer', function ($email) {
    if (!isset($GLOBALS['wc_email'])) {
        $GLOBALS['wc_email'] = $email;
    }
}, 5, 1);
~~~


### Step 2

Reference it in your ```email-footer.php```

~~~
// In your theme's woocommerce/emails/email-footer.php

$order = null;

if (isset($GLOBALS['wc_email']) && $GLOBALS['wc_email']->object && $GLOBALS['wc_email']->object instanceof WC_Order) {
    $order = $GLOBALS['wc_email']->object;
}

~~~

Happy hacking!
