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
JSON_EXTRACT(children.price -> '$.*.gross[0]', '$[0]') as price


FROM product configurable

LEFT JOIN product as children on configurable.id=children.parent_id

WHERE configurable.product_number in ("132101 00-0060-B", "132101 00-0060", "132101 00-0002");
```
