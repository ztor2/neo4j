### Neo4j/Cypher Basic
<br>

- 모든 노드 삭제


**MATCH (n) DETACH DELETE n**

<br>

- Undirected graph 개체 만들기

**CALL gds.graph.create(<br>
    'graph1',<br>
    'Place',<br>
    {EROAD: {orientation: 'UNDIRECTED'}},<br>
    {   <br>
       nodeProperties: ['latitude', 'longitude', 'population'],<br>
        relationshipProperties: 'distance'<br>
     })**

<br>

- Shortest path

**MATCH (a.Place {id: "Amsterdam"}), (b.Place {id: "London"})<br>
CALL algo.shortestPath.stream(a, b, null)<br>
YIELD nodeId, cost<br>
RETURN algo.getNodebyId(nodeId).id AS place, cost**<br>

<br>

- Random walk

**CALL gds.beta.randomWalk.stream(<br>
  'graph1',<br>
  {<br>
    walkLength: 4,<br>
    walksPerNode: 1,<br>
    randomSeed: 42,<br>
    concurrency: 1<br>
  }<br>
)<br>
YIELD nodeIds, path<br>
RETURN nodeIds, [node IN nodes(path) | node.id ] AS pages**

<br>

- Degree centrality

**CALL gds.degree.stream('graph1')<br>
YIELD nodeId, score<br>
RETURN gds.util.asNode(nodeId).id AS place, score AS followers<br>
ORDER BY followers DESC, place DESC**

<br>

- Betweenness centrality

**CALL gds.betweenness.stream('graph1')<br>
YIELD nodeId, score<br>
RETURN gds.util.asNode(nodeId).id AS place, score AS betweenness_cen<br>
ORDER BY betweenness_cen DESC, place DESC**

<br>



