# Alle Mail-Templates mit Übersetzungen ausgeben

Listet alle englischen E-Mail-Templates auf. Wenn das Feld 'name' nicht gesetzt ist, fehlen diese Einträge in der Datenbank. Das könnte dann zu einem Fehler im E-Mailversand führen.

```
SELECT 

mt.id as m_it,
mtt.technical_name,
mtrans.language_id,
lang.name as Sprache,
mtrans.subject,
mtrans.content_html,
mttt.`name`,
mttt.language_id

FROM mail_template mt
LEFT JOIN mail_template_type mtt ON mtt.id=mt.mail_template_type_id
LEFT JOIN mail_template_translation mtrans on mtrans.mail_template_id=mt.id
LEFT JOIN `language` lang on mtrans.language_id=lang.id
LEFT JOIN mail_template_type_translation mttt on mtt.id=mttt.mail_template_type_id and lang.id=mttt.language_id

having Sprache="English"



```
