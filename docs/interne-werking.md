## Interne werking ##

Je bestanden worden opgeslaan in een repository. Deze repository bevat informatie over de inhoud van de bestanden, hun naam, locatie en de historiek.

* de inhoud van bestanden wordt opgeslaan in blob objecten
* de historiek wordt bijgehouden in commit objecten
* de structuur wordt bijgehouden in tree objecten

Wanneer je meerdere files hebt met dezelfde inhoud, dan zal in de tree meerdere keren verwezen worden naar hetzelfde blob object, waardoor er plaats bespaard wordt.