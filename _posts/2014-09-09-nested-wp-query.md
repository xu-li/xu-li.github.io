---
layout: post
title: Nest WP_Querys
category: code
tags: wordpress, WP_Query, loop
---

I googled a lot for *how to nest two WP_Querys*. The closest solution I could find is [Loop within a loop](http://wordpress.stackexchange.com/questions/71724/loop-within-a-loop){:target="_blank"}, but it only says "// restore the global $post from the previously created backup". After digging into the source code, I found the key method: ```$query->reset_postdata();```.

<!--more-->

### How to nest two WP_Querys

~~~ php
$query1 = new WP_Query(array("post_type" => "post"));
$query2 = new WP_Query(array("post_type" => "page"));

while ($query1->have_posts()) {
    $query1->the_post();

    echo "Query1: " . esc_html(get_the_title()) . "<br />";

    while ($query2->have_posts()) {
        $query2->the_post();
        echo "Query2: " . esc_html(get_the_title()) . "<br />";
    }

    // key method, you have to reset_postdata to get back the outer $post
    $query1->reset_postdata();

    // same as the previous one
    echo "Query1: " . esc_html(get_the_title()) . "<br />";
    echo "<hr />";
}

// reset, so that the global wp_query is restored
wp_reset_postdata();
~~~

### How to reset and break out of the loop

~~~ php
while ($query->have_posts()) {
    the_title();

    // if you want to reset and break out of the loop
    if (true) {
        $query->rewind_posts();
        $query->in_the_loop = false;

        break;
    }
}
~~~
