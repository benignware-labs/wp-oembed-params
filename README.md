# wp-oembed-params

Manipulate oembed provider params


## Example: Don't show info with youtube-videos in OEmbed widgets

```php
function my_dynamic_sidebar_params( $sidebar_params ) {
  if ( is_admin() ) {
    return $sidebar_params;
  }
  foreach($sidebar_params as $index => $widget_params) {
    $widget_name = isset($widget_params['widget_name']) ? sanitize_title($widget_params['widget_name']) : '';
    if ($widget_name === 'oembed') {
      $sidebar_params[$index] = array_merge_recursive(
        $widget_params,
        array(
          'oembed' => array(
            'params' => array(
              'youtube' => array(
                'showinfo' => 0
              )
            )
          )
        )
      );
    }
  }
}

add_filter( 'dynamic_sidebar_params', 'my_dynamic_sidebar_params' );
```
