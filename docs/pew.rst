Referenz zur PewPew-Bibliothek
******************************

.. module:: pew

.. function:: init()

    Initialisiert das Modul.

    Diese Funktion schaltet das Display ein und macht die Bibliothek
    betriebsbereit.


.. function:: brightness(level)

    Setzt die Display-Helligkeit, von 0 (minimal) bis 15 (maximal). Auf Geräten,
    welche die Helligkeit nicht ändern können, hat die Funktion keinen Effekt.


.. function:: show(pix)

    Zeigt das übergebene Bild auf dem Display, in der oberen linken Ecke
    platziert. Du wirst das ein Mal pro Frame aufrufen wollen.


.. function:: keys()

    Gibt eine Zahl zurück, die angibt, welche Tasten seit dem letzten Aufruf
    gedrückt wurden oder immer noch gedrückt sind. Diese Zahl kann dann mit dem
    Operator ``&`` und den Konstanten ``K_X``, ``K_DOWN``, ``K_LEFT``,
    ``K_RIGHT``, ``K_UP`` und ``K_O`` gefiltert werden, um zu sehen, ob eine
    bestimmte Taste gedrückt war.


.. function:: tick(delay)

    Wartet, bis ``delay`` Sekunden vergangen sind seit dem letzten Aufruf. Du
    kannst das in jedem Frame aufrufen, um eine konstante Frame-Rate zu
    erreichen.


.. class:: Pix(width=8, height=8, buffer=None)

    Ein Pix ist eine Zeichenfläche (ein Bild), ``width`` Pixel breit und ``height`` Pixel
    hoch.

    Wenn kein ``buffer`` angegeben wird, um die Bilddaten zu speichern, wird
    automatisch ein passender angelegt.

    .. classmethod:: from_iter(cls, lines)

        Macht ein neues Pix und initialisiert seinen Inhalt, indem über die
        Zeilen ``lines`` und dann über einzelne Pixel innerhalb jeder Zeile
        iteriert wird. Alle Zeilen müssen mindestens so lang sein wie die erste.

    .. classmethod:: from_text(cls, text, color=None, background=0, colors=None)

        Macht ein neues Pix und schreibt den angegebenen Text hinein. Es erhält
        genau die Grösse, die für den Text nötig ist. Zeilenumbrüche und andere
        Spezialzeichen werden als Leerzeichen dargestellt.

        Wenn keine Farbe ``color`` angegeben ist, werden die Buchstaben aus
        verschiedenfarbigen Pixeln bestehen. Ansonsten wird die angegebene Farbe
        verwendet, mit ``background`` als Hintergrundfarbe.

        Alternativ kann als ``colors`` ein 4-Tupel von Farben angegeben werden,
        die Argumente ``color`` und ``background`` werden dann ignoriert und
        stattdessen diese vier Farben verwendet.

    .. method:: pixel(self, x, y, color=None)

        Falls ``color`` angegeben ist, wird das Pixel an der Position ``x``,
        ``y`` auf diese Farbe gesetzt. Ansonsten wird die aktuelle Farbe dieses
        Pixels zurückgegeben.

        Falls die Position ausserhalb der Zeichenfläche liegt, wird 0
        zurückgegeben.

    .. method:: box(self, color, x=0, y=0, width=self.width, height=self.height)

        Zeichnet ein gefülltes Rechteck in der Farbe ``color`` mit oberer linker
        Ecke bei ``x``, ``y``, Breite ``width`` und Höhe ``height``. Wenn keine
        Position und Grösse angegeben sind, wird die gesamte Zeichenfläche
        ausgefüllt.

    .. method:: blit(self, source, dx=0, dy=0, x=0, y=0, width=None, height=None, key=None)

        Kopiert die Zeichenfläche ``source`` auf diese Zeichenfläche an der
        Position ``dx``, ``dy``.

        Wenn ``x``, ``y``, ``width`` und ``height`` angegeben sind, wird nur
        dieser Ausschnitt des Quell-Bildes kopiert, ansonsten das gesamte Bild.

        Wenn eine Farbe ``key`` angegeben ist, wird diese Farbe im Quell-Bild
        als transparent betrachtet und nicht auf diese Zeichenfläche kopiert.
