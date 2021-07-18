# Dynamic Tags Categories

When controls are created, developers can define whether the [control can accept dynamic data](/controls/control-settings#dynamic-tags) or not. If the control accepts dynamic data, it need to set which data type they accept (i.e. text values, colors, images etc.). Dynamic tags, on the other hand, need the define what data type they return to the control.

This is where categories come in handy. Elementor has a list of predefined data type categories returned by the dynamic tag to the control.

## Available Category Constants

Elementor comes with the following pre-defined dynamic tag category constants:

| Constant             | Value       | Info                                 |
|----------------------|-------------|--------------------------------------|
| `NUMBER_CATEGORY`    | `number`    | Dynamic tags for number controls.    |
| `TEXT_CATEGORY`      | `text`      | Dynamic tags for text controls.      |
| `URL_CATEGORY`       | `url`       | Dynamic tags for URL controls.       |
| `COLOR_CATEGORY`     | `color`     | Dynamic tags for color controls.     |
| `IMAGE_CATEGORY`     | `image`     | Dynamic tags for image controls.     |
| `MEDIA_CATEGORY`     | `media`     | Dynamic tags for media controls.     |
| `GALLERY_CATEGORY`   | `gallery`   | Dynamic tags for gallery controls.   |
| `POST_META_CATEGORY` | `post_meta` | Dynamic tags for post meta controls. |

::: warning Please Note
In older Elementor versions you could define the returned value as simple text like `url`, `number`, `text`, `media` etc. As Elementor evolved, it replaced the text based values with predefined uppercase `constants`. We strongly recommend to replace old text base values with new category constants.
:::

## Applying Categories on Dynamic Tags

When creating new dynamic tags, you need to define what data type the tag will return, for that you can use the `get_categories()` method:

```php
Class Elementor_Test_Tag extends \Elementor\Core\DynamicTags\Tag {

	public function get_categories() {
		return [ \Elementor\Modules\DynamicTags\Module::TEXT_CATEGORY ];
	}

}
```

The method returns an array, meaning that the dynamic tag can return several data types to the control:

```php
Class Elementor_Test_Tag extends \Elementor\Core\DynamicTags\Tag {

	public function get_categories() {
		return [
			\Elementor\Modules\DynamicTags\Module::URL_CATEGORY,
			\Elementor\Modules\DynamicTags\Module::TEXT_CATEGORY,
			\Elementor\Modules\DynamicTags\Module::NUMBER_CATEGORY
		];
	}

}
```

## Using Categories in Controls

On the other hand, when you create [Controls](/controls/) you need to support dynamic tags when defining [Control Settings](/controls/control-settings) thorough the `get_default_settings()` method and choose the category to display.

```php {13-19}
class Elementor_Test_Control extends \Elementor\Base_Control {

	public function get_type() {}

	public function content_template() {}

	protected function get_default_settings() {

		return [
			'show_label' => true,
			'label_block' => true,
			'separator' => 'after',
			'dynamic' => [
				'active' => true,
				'categories' => [
					\Elementor\Modules\DynamicTags\Module::TEXT_CATEGORY,
					\Elementor\Modules\DynamicTags\Module::NUMBER_CATEGORY
				],
			],
		];

	}

}
```