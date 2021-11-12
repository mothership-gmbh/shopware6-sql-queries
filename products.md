### Produkte mit Basis-Informationen

Liefert alle Produkte mit den Basisinformationen zurück. 

```
SELECT 

p.id,
p.product_number,
CASE
	WHEN p.child_count > 0 THEN 'configurable'
	ELSE 'simple'
END as type,
p.active,
p.stock,
p.available,
JSON_EXTRACT(p.price -> '$.*.gross[0]', '$[0]') as net,
p.child_count

FROM product p
WHERE product_number in ("132101 00-0060-B", "132101 00-0060", "132101 00-0002")
```
