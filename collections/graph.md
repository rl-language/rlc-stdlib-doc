# graph.rl

## cls Edge

### Fields


### Methods

* fun `get_target_id()  -> Int`
* fun `get_source_id()  -> Int`
* fun `get_label()  -> ref EdgeLabel`

## cls Node

### Fields


### Methods

* fun `add_edge(Node<NodeLabel, EdgeLabel> other) `
* fun `add_edge(Node<NodeLabel, EdgeLabel> other, EdgeLabel label) `
* fun `get_outgoing(Int index)  -> ref Edge<EdgeLabel>`
* fun `get_size_outgoing()  -> Int`
* fun `get_size_incomming()  -> Int`
* fun `get_incomming(Int index)  -> Int`
* fun `get_label()  -> ref NodeLabel`
* fun `get_id()  -> Int`

## cls Graph

### Fields


### Methods

* fun `add_node(Node<NodeLabel, EdgeLabel> n) `
* fun `add_node() `
* fun `remove_edge(Node<NodeLabel, EdgeLabel> node, Int edge_id) `
* fun `erase_outgoing_edges(Node<NodeLabel, EdgeLabel> n) `
* fun `erase_incomming_edges(Node<NodeLabel, EdgeLabel> n) `
* fun `remove_node(Node<NodeLabel, EdgeLabel> n) `
* fun `get_node(Int node_id)  -> ref Node<NodeLabel, EdgeLabel>`
* fun `get_nodes_size()  -> Int`
* fun `add_node(Int source, Int to) `
* fun `add_node(Node<NodeLabel, EdgeLabel> source, Node<NodeLabel, EdgeLabel> to) `
* fun `get_size_successors(Node<NodeLabel, EdgeLabel> n)  -> Int`
* fun `get_successors(Node<NodeLabel, EdgeLabel> n, Int index_successor)  -> Node<NodeLabel, EdgeLabel>`
* fun `get_size_predecessors(Node<NodeLabel, EdgeLabel> n)  -> Int`
* fun `get_predecessor(Node<NodeLabel, EdgeLabel> n, Int index_successor)  -> Node<NodeLabel, EdgeLabel>`

