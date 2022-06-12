# neo4j2
1.	Znajdź trasy którymi można dostać się z Darjeeling na Sandakphu, mające najmniejszą ilość etapów 

MATCH route = allShortestPaths(({name: "Darjeeling"}) -[*]-> ({name: "Sandakphu"})) RETURN route

2.	Znajdź mające najmniej etapów trasy którymi można dostać się z Darjeeling na Sandakphu i które mogą być wykorzystywane zimą 

MATCH route = allShortestPaths(({name: "Darjeeling"}) -[*]-> ({name: "Sandakphu"})) WHERE ALL (season in relationships(route) where season.winter = "true") RETURN route;

3.	Uszereguj trasy którymi można dostać się z Darjeeling na Sandakphu według dystansu 

MATCH route = ({name: "Darjeeling"}) -[*]-> ({name: "Sandakphu"}) RETURN route, length(route) ORDER BY length(route);

4.	Znajdź wszystkie miejsca do których można dotrzeć przy pomocy roweru (twowheeler) z Darjeeling latem

MATCH route = ({name: "Darjeeling"}) -[t:twowheeler*]-> () WHERE ALL (r in relationships(route) where r.summer = "true")  RETURN route;

Część 2 – Połączenia lotnicze
Zaimportuj dane uruchamiając skrypt task3.cypher. Napisz następujące zapytania:
5.	Uszereguj porty lotnicze według ilości rozpoczynających się w nich lotów

MATCH (:Flight)-[:ORIGIN]->(air:Airport) RETURN air, count(*) as cnt order by cnt desc;

6.	Znajdź wszystkie porty lotnicze, do których da się dolecieć (bezpośrednio lub z przesiadkami) z Los Angeles (LAX) wydając mniej niż 3000 
7.	Uszereguj połączenia, którymi można dotrzeć z Los Angeles (LAX) do Dayton (DAY) według ceny biletów 
8.	Znajdź najtańsze połączenie z Los Angeles (LAX) do Dayton (DAY) 
9.	Uszereguj linie lotnicze według ilości miast, pomiędzy którymi oferują połączenia (unikalnych miast biorących udział w relacjach :ORIGIN i :DESTINATION węzłów typu Flight obsługiwanych przez daną linię) 
10.	Znajdź najtańszą trasę łączącą 3 różne porty lotnicze
