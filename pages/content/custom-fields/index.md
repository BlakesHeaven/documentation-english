# Custom fields
<!-- position: 7 -->

<div class="note">
<div class="title">Under construction</div>
The following section is under construction, and is only available for Bludit beta (Github version).
</div>

## Introduction
Custom fields allow the user to add fields to the content database; the custom fields appear in the user interface when you create or edit content.

## Structure
The structure is defined in the JSON format, and supports the following keys:
- (required) `type`: Type of the custom field, supported values (`string`, `bool`).
- (optional) `label`: The label for the custom field.
- (optional) `tip`: Small text for the user to describe the custom field.
- (optional) `default`: Default value for the custom field.
- (optional) `placeholder`: Small text inside the field.
- (optional) `position`: Position in the editor, supported values (`top`, `bottom`). If the position option is not used, the Custom field appears on the `Options` `Custom` tab.

## Add custom fields
To add custom fields go to:
```
Settings > General > Custom fields
```

To define custom field, you need to generate a JSON structure. Check out the following examples:

Custom field as `string` and the key name `youtube`:
```
{
    "youtube": {
        "type": "string",
        "label": "YouTube",
        "tip": "Write the YouTube URL."
    }
}
```

Custom field as `boolean` and the key name `inStock`:
```
{
    "inStock": {
        "type": "bool",
        "label": "In Stock",
        "tip": "Select this field if you have stock."
    }
}
```

Two custom fields with different types.
```
{
    "product": {
        "type": "string",
        "label": "Product",
        "tip": "Write the product name."
    },
    "inStock": {
        "type": "bool",
        "label": "In Stock",
        "tip": "Select this field if you have stock."
    }
}
```

Three custom fields with different types and different position in the editor.
```
{
    "product": {
        "type": "string",
		"placeholder": "Product name",
		"position": "top"
    },
    "inStock": {
        "type": "bool",
        "tip": "Select this field if you have stock.",
		"position": "top"
    },
    "imageURL": {
        "type": "string",
		"placeholder": "Image URL",
		"position": "bottom"
    }
}
```

## Get custom field
The class page provides the method `custom()`, which returns the value of the field.

The following example prints the value of the field `youtube` from the above example.
```
<?php
    echo $page->custom('youtube');
?>
```

Check the boolean value from the field `inStock` from the above example.
```
<?php
    if ($page->custom('inStock')) {
        echo "There is stock!";
    } else {
        echo "No more products";
    }
?>
```

## Delete custom field
To delete a custom field you just need to remove the entry from the JSON structure. The custom fields are not completely deleted from the database when you do this, but they are invalidated.

If you want to remove all custom fields, just set an empty JSON in the textarea, as following:
```
{}
```

## Get Custom Fields array options
To get the options for a custom field, pass in true as a second parameter, to return an array of the field options, eg `Label`.
```
<?php
$options = $page->custom('test', true);
echo $options['label'];
?>
```
