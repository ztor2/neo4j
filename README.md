### Neo4j

- 모든 노드 삭제
**MATCH (n) DETACH DELETE n**
<br>
- Undirected graph 개체 만들기
**CALL gds.graph.create(
    'graph1',
    'Place',
    {EROAD: {orientation: 'UNDIRECTED'}},
    {   
       nodeProperties: ['latitude', 'longitude', 'population'],
        relationshipProperties: 'distance'
     }
)**

<br>

- Shortest path

**MATCH (a.Place {id: "Amsterdam"}), (b.Place {id: "London"})
CALL algo.shortestPath.stream(a, b, null)
YIELD nodeId, cost
RETURN algo.getNodebyId(nodeId).id AS place, cost**

