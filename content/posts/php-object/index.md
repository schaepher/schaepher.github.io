---
title: PHP 对象
date: 2020-03-30 12:49:00
updated: 2020-03-30 12:49:00
tags: 
- PHP
- 对象
---


创建对象：  

`zend_objects.c`

```c
ZEND_API zend_object* ZEND_FASTCALL zend_objects_new(zend_class_entry *ce)
{
	zend_object *object = emalloc(sizeof(zend_object) + zend_object_properties_size(ce));

	_zend_object_std_init(object, ce);
	object->handlers = &std_object_handlers;
	return object;
}
```

<!-- more -->

`zend_object_handlers.c`  

```c
ZEND_API const zend_object_handlers std_object_handlers = {
	0,										/* offset */

	zend_object_std_dtor,					/* free_obj */
	zend_objects_destroy_object,			/* dtor_obj */
	zend_objects_clone_obj,					/* clone_obj */

	zend_std_read_property,					/* read_property */
	zend_std_write_property,				/* write_property */
	zend_std_read_dimension,				/* read_dimension */
	zend_std_write_dimension,				/* write_dimension */
	zend_std_get_property_ptr_ptr,			/* get_property_ptr_ptr */
	NULL,									/* get */
	NULL,									/* set */
	zend_std_has_property,					/* has_property */
	zend_std_unset_property,				/* unset_property */
	zend_std_has_dimension,					/* has_dimension */
	zend_std_unset_dimension,				/* unset_dimension */
	zend_std_get_properties,				/* get_properties */
	zend_std_get_method,					/* get_method */
	NULL,									/* call_method */
	zend_std_get_constructor,				/* get_constructor */
	zend_std_get_class_name,				/* get_class_name */
	zend_std_compare_objects,				/* compare_objects */
	zend_std_cast_object_tostring,			/* cast_object */
	NULL,									/* count_elements */
	zend_std_get_debug_info,				/* get_debug_info */
	zend_std_get_closure,					/* get_closure */
	zend_std_get_gc,						/* get_gc */
	NULL,									/* do_operation */
	NULL,									/* compare */
	NULL,									/* get_properties_for */
};
```