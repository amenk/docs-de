.. _rst_cookbook_symfony_mm-2-1-tips:

Symfony und MM 2.1 Tipps
========================

Für die Arbeit mit MM 2.1 unter Symfony einige Tipps für den Start
oder als "Merkzettel".

Die Aufrufe auf der Konsole gehen immer vom Installationsverzeichnis von
Contao aus - also da, wo die composer.json liegt, d.h. vor allen Aufrufen
erstmal in das Verzeichnis wechseln:

``cd /var/www/mein-contao``

Composer-Update auf der Konsole - der Pfad zu PHP wird z.B. beim Systemcheck des
Contao-Managers mit angezeigt.

``/usr/bin/php71 web/contao-manager.phar.php composer update -v``

oder mit Speicher- und Laufzeitzuweisung

``/usr/bin/php71 -d memory_limit=1G -d max_execution_time=900 web/contao-manager.phar.php composer update -v``

Nach einem Update ggf. das Installtool aufrufen, damit Datenbankänderungen
durchgeführt werden (wird gern vergessen :D).

Die composer.phar sollte regelmäßig aktualisiert werden - dazu folgenden Befehl aufrufen:

``/usr/bin/php71 web/contao-manager.phar.php self-update``

Bei Anpassungen den Contao-Cache leeren.

``rm -rf var/cache/``

Während der Entwicklung sollte man unbedingt Zugriff auf die Entwicklungsumgebung
per `app_dev` haben - der Seitenaufruf ist dann "domain.tld/app_dev.php/...".
Dazu muss ein Zugang für app_dev eingerichtet werden über

``vendor/bin/contao-console contao:install-web-dir --user=ichbins --password=totalgeheim``

Für den app_dev-Zugang kann aber nur ein User angelegt werden.

Achtung: sofern der Zugang zur Seite über htaccess geschützt ist, müssen user+passwort
für htaccess und app_dev die selben sein!

Mit dem Seitenaufruf per app_dev wird auch das Caching von Contao unterbunden und man muss
den Cache nicht so häufig leeren - bedeutet aber auch, dass die Seite ohne app_dev ggf. "anders
aussieht" => Cache löschen. Zudem wird die Debug-Toolbar von Symfony im Browser eingeblendet.

|img_symfony-toolbar|

Muss im Quelltext mal was debugt werden, die Debug-Funktion ``debug()`` von Symfony verwenden
- die Ausgabe erfolgt dann in der Debug-Toolbar und kann über das "Fadenkreuz-Icon" eingesehen
werden.

Für das Debugging der Templates gibt es hier eine Beschreibung: :ref:`rst_cookbook_debug_templates`

Möchte man die SQL-Aufrufe z.B. einer Filterregel "Eigenes SQL" untersuchen, so kann man auf der
Debug-Toolbar auf "Doctrine" gehen - dort werden alle SQL-Aufrufe aufgelistet. Über die Suche im
Browser und einigen Bestandteilen wie der Tabellenname o.ä. ist das Query meist schnell gefunden.
Die Toolbar bietet den SQL-Code in verschiedenen Formatierungen an, so dass das Query einfach in
phpMyAdmin übernommen und getestet werden kann.


.. |img_symfony-toolbar| image:: /_img/screenshots/cookbook/debug/symfony-toolbar.jpg