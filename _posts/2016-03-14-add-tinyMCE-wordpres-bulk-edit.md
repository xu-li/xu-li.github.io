---
layout: post
title: Add tinyMCE to Wordpress bulk edit
category: wordpress
tags: wordpress, tinyMCE, WYSIWYG
---

When adding the tinyMCE using wp_editor to bulk edit form, the Visual tab does not work.

<!--more-->

According to [Codex](https://codex.wordpress.org/Function_Reference/wp_editor):

> Once instantiated, the WYSIWYG editor cannot be moved around in the DOM. What this means in practical terms, is that you cannot put it in meta-boxes that can be dragged and placed elsewhere on the page. Instead use 'edit_page_form' (for pages) or 'edit_form_advanced' (for other post types):

To overcome this issue, you may remove and add the editor back when the bulk edit form is open.

~~~
var editor_id = 'test';
tinymce.EditorManager.execCommand('mceRemoveEditor', true, editor_id);
tinymce.EditorManager.execCommand('mceAddEditor', true, editor_id);
~~~

## A working example

~~~
// Here, I used the 'woocommerce_product_bulk_edit_end' hook.
// It doesn't mean this will only work in woocommerce. 
add_action('woocommerce_product_bulk_edit_end', function () {
    ?>
        <div class="inline-edit-group">
            <span class="title"><?php _e('Test', 'woocommerce'); ?></span>

            <span class="input-text-wrap">
                <?php wp_editor('', 'test'); // the editor id is 'test'?>
            </span>
        </div>

        <script>
        jQuery(function () {
            // We use "on" instead of "click",
            // because we want this callback to be fired
            // after inlineEditPost.setBulk() in inline-edit-post.js
            jQuery(document).on('click', '#doaction, #doaction2', function(e) {
                var n = jQuery(this).attr('id').substr(2);
                if ('edit' === jQuery('select[name="' + n + '"]').val()) {
                    e.preventDefault();

                    // Remember to use the same editor id as the one used in wp_editor
                    tinymce.EditorManager.execCommand('mceRemoveEditor', true, 'test');
                    tinymce.EditorManager.execCommand('mceAddEditor', true, 'test');
                }
            });
        });
        </script>

    <?php
});
~~~
