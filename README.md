A Knowledge Graph (KG), or any type of graph, is composed of nodes and edges. In a KG, each node represents a concept, while each edge defines a relationship between two such concepts. In this article, I’ll explain a practical approach to transforming any text corpus into a Graph of Concepts (GC) — a term I use interchangeably with Knowledge Graph to more clearly describe the concept we’ll be demonstrating.
All the components required for this implementation can be set up locally, allowing you to run the project easily on a personal computer. I’ve intentionally taken a no-GPT approach, preferring to use lightweight open-source models instead. Specifically, I’ll be using the Mistral 7B OpenOrca Instruct and Zephyr models, both of which can be run locally using Ollama.
While databases like Neo4j provide a convenient way to store and query graph data, to keep things simple, this demonstration will rely on in-memory Pandas DataFrames and the NetworkX Python library.
The objective is to convert a given text corpus into a Graph of Concepts (GC) and visualize it interactively — similar to the visually engaging banner image in this article. We’ll be able to explore the graph dynamically by dragging nodes, adjusting edges, zooming in and out, and modifying the physics of the network.

Here’s how this can be approached:

Divide the text into smaller chunks and assign each chunk a unique chunk_id.

For each text segment, use a language model to extract concepts and identify the semantic relationships between them. Assign a weight (W1) to each relationship. Since multiple relationships can exist between the same pair of concepts, each is treated as a separate edge.

Recognize that concepts appearing within the same text chunk are contextually connected due to their proximity. Assign a secondary weight (W2) to represent this contextual relationship. Note that the same pair of concepts may appear in multiple chunks.

Aggregate similar pairs by summing up their weights and combining their relationship descriptions. This ensures that each unique pair of concepts is represented by a single edge, which carries a cumulative weight and a list of combined relations as its label.
