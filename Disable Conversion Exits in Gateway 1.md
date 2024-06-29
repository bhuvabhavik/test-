objective: **Disable Conversion Exits in Gateway



Steps:** 


1\. Redefine the define method in \*MPC\_EXT class. Call the parent define.

2\. Get reference of the entity-> getproperties-> get reference of the property of your interest

3\. Call method DISABLE\_CONVERSION of the property

You can also get reference of the model and call method SET\_NO\_OCNVERSION, so that conversion is disabled for entire model.



Code example:

class ZCL\_ZITD\_COSTPLAN\_MPC\_EXT definition

`  `public

`  `inheriting from ZCL\_ZITD\_COSTPLAN\_MPC

`  `create public .

public section.

` `METHODS define REDEFINITION.

protected section.

private section.

ENDCLASS.



CLASS ZCL\_ZITD\_COSTPLAN\_MPC\_EXT IMPLEMENTATION.

METHOD define.

`    `" Call parent class's define method

`    `super->define( ).

`    `" Get reference to the entity

`    `DATA(lo\_entity\_type) = model->get\_entity\_type( iv\_entity\_name = 'ZPRPS\_CONVERTED' ).

`    `" Get reference to the properties of the entity

`    `DATA(lt\_properties) = lo\_entity\_type->get\_properties( ).



`   `" Loop through the properties to find the specific property

`    `LOOP AT lt\_properties INTO DATA(lo\_property).

`      `IF lo\_property-name = 'PSPNR\_U'. " Replace field name  with the actual Field name

`            `lo\_property-property->disable\_conversion(  ).

`        `EXIT.

`      `ENDIF.

`    `ENDLOOP.

`  `ENDMETHOD.

ENDCLASS.

