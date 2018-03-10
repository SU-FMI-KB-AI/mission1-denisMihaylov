CREATE (you:Person {name:"Denis"})
RETURN you;

MATCH  (you:Person {name:"Denis"})
CREATE (you)-[like:LIKE]->(neo:Database {name:"Neo4j" })
RETURN you,like,neo;

MATCH (you:Person {name:"Denis"})
FOREACH (name in ["Karizma","Karamba","Kazarma","Ema"] |
  CREATE (you)-[:FRIEND]->(:Person {name:name}));
  
MATCH (you {name:"Denis"})-[:FRIEND]->(yourFriends)
RETURN you, yourFriends

MATCH (neo:Database {name:"Neo4j"})
MATCH (karizma:Person {name:"Karizma"})
CREATE (karizma)-[:FRIEND]->(:Person:Expert {name:"Amanda"})-[:WORKED_WITH]->(neo);

MATCH (you {name:"Denis"})
MATCH (expert)-[:WORKED_WITH]->(db:Database {name:"Neo4j"})
MATCH path = shortestPath( (you)-[:FRIEND*..5]-(expert) )
RETURN db,expert,path;
