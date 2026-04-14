# Projekt TSwR – Ramię robotyczne do gry w tenisa stołowego
*Opisane założenia projektu są wstępne.*
## Rezultat:
Ramię robota z zamontowaną paletką będzie odbijać piłeczki do tenisa stołowego w celu odwzorowania gry w niego.

## Dlaczego to jest fajne:
Bo ping-pong jest fajny!

<!---
[//]: <> ## Co i jak:

[//]: <> ## W jaki sposób:
-->

## Kamień milowy:
Środowisko oddziałujące z agentem. W środowisku będą znajdować się takie obiekty jak stół, piłeczki pingpongowe i osadzone w nim będzie ramię robota z paletką.

## Wejścia:
– obraz z kamery

## Wyjścia:
– momenty lub przyśpieszenia przegubów robota

## Model
Projekt opiera się na dwóch modelach wirtualnych:
1. **Model Robota:** Zastosujemy 7-osiowe ramię **Franka Emika Panda**. Zamiast tworzyć model od zera, wykorzystamy dostrojony model w formacie MJCF (XML) z oficjalnego repozytorium *MuJoCo Menagerie*. Gwarantuje to poprawne odwzorowanie mas, bezwładności oraz fizycznych limitów przegubów (prędkości i momentów sił). Do efektora końcowego ramienia zostanie wirtualnie "przymocowana" paletka do tenisa stołowego.
2. **Model Piłeczki:** Najważniejszym elementem modelu piłeczki będzie dostrojenie parametru *restitution* (współczynnik sprężystości), aby zjawisko odbicia od blatu oraz od paletki zachowywało się zgodnie z prawami fizyki świata rzeczywistego.

## Symulator
W projekcie wykorzystywany jest silnik fizyczny **MuJoCo**. Wybór ten podyktowany jest specyfiką tenisa stołowego – MuJoCo charakteryzuje się wyjątkowo dokładnym i szybkim rozwiązywaniem równań dynamiki kontaktów, co jest kluczowe przy modelowaniu sprężystych odbić małej piłeczki z dużą prędkością.

## Wizualizacja
Zanim wprowadzony zostanie algorytm Reinforcement Learningu, środowisko musi przejść  przez walidację fizyczną i kinematyczną.
* **Wizualizacja:** Do podglądu symulacji wykorzystywany będzie natywny moduł `mujoco.viewer`. Pozwala on na renderowanie sceny 3D w czasie rzeczywistym oraz interaktywne sprawdzanie limitów przegubów z poziomu interfejsu graficznego.
* **Sposób walidacji:** Poprawność modelu zostanie zweryfikowana poprzez wymuszenie ruchu ramienia za pomocą prostych, deterministycznych skryptów w Pythonie (bez udziału AI). Skrypt wygeneruje trajektorię (np. ruch harmoniczny wybranego przegubu), która doprowadzi do uderzenia w spadającą piłeczkę. Udana wizualizacja realistycznego toru lotu piłki po zderzeniu z paletką (brak zjawiska "przenikania" obiektów) będzie dowodem na stabilność modelu.

## Biblioteki:
- NumPy
- SymPy
- PyBullet
- MuJoCo

## Literatura:
https://ieeexplore.ieee.org/document/11127501
