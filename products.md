### Produkte mit Basis-Informationen

Liefert alle Produkte mit den Basisinformationen aus Sicht eines konfigurierbaren Produkts zurück. Als Argument muss in der `where in condition` jeweils eine Liste an konfigurierbaren Produkten übergeben werden. 

```
SELECT 

configurable.id,
configurable.product_number,
CASE
	WHEN configurable.child_count > 0 THEN 'configurable'
	ELSE 'simple'
END as type,
configurable.active,
configurable.stock,
configurable.available,
JSON_EXTRACT(configurable.price -> '$.*.gross[0]', '$[0]') as price,
configurable.child_count,

children.product_number,
children.stock,
children.available,
JSON_EXTRACT(children.price -> '$.*.gross[0]', '$[0]') as price,

shop_visibility.visibility as shop_visibility,
club_visibility.visibility as club_visibility


FROM product configurable

LEFT JOIN product as children on configurable.id=children.parent_id
LEFT JOIN product_visibility as club_visibility on configurable.id=club_visibility.product_id and club_visibility.sales_channel_id=X'51e32d6cdcad4310887a989bd533ce9b'
LEFT JOIN product_visibility as shop_visibility on configurable.id=shop_visibility.product_id and shop_visibility.sales_channel_id=X'98432def39fc4624b33213a56b8c944d'

WHERE configurable.product_number in ("132101 00-0060-B", "132101 00-0060", "132101 00-0002");
```

Test
