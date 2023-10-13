# Matrix_to_Graph_converter
import java.util.*;

class Graph {
    private int vertices;
    private LinkedList<Integer>[] adjacencyList;

    public Graph(int vertices) {
        this.vertices = vertices;
        this.adjacencyList = new LinkedList[vertices];
        for (int i = 0; i < vertices; i++) {
            adjacencyList[i] = new LinkedList<>();
        }
    }

    public void addEdge(int u, int v) {
        adjacencyList[u].add(v);
    }

    public void bfs(int start) {
        boolean[] visited = new boolean[vertices];
        Queue<Integer> queue = new LinkedList<>();
        visited[start] = true;
        queue.offer(start);

        while (!queue.isEmpty()) {
            int current = queue.poll();
            System.out.print(current + " ");

            for (Integer neighbor : adjacencyList[current]) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.offer(neighbor);
                }
            }
        }
    }
}

public class MatrixToGraphConverter {
    public static Graph matrixToGraph(int[][] matrix) {
        int rows = matrix.length;
        int cols = matrix[0].length;
        int vertices = rows * cols;
        Graph graph = new Graph(vertices);

        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                int currentNode = i * cols + j;

                // Connect with right neighbor
                if (j < cols - 1) {
                    int rightNeighbor = i * cols + (j + 1);
                    graph.addEdge(currentNode, rightNeighbor);
                }

                // Connect with bottom neighbor
                if (i < rows - 1) {
                    int bottomNeighbor = (i + 1) * cols + j;
                    graph.addEdge(currentNode, bottomNeighbor);
                }
            }
        }

        return graph;
    }

    public static void main(String[] args) {
        int[][] matrix = {
            {1, 2, 3},
            {4, 5, 6},
            {7, 8, 9}
        };

        // Convert the matrix into a graph
        Graph graph = matrixToGraph(matrix);

        // Print the adjacency list representation of the graph
        for (int i = 0; i < graph.vertices; i++) {
            System.out.print(i + " -> ");
            for (Integer neighbor : graph.adjacencyList[i]) {
                System.out.print(neighbor + " ");
            }
            System.out.println();
        }

        // Run BFS starting from a specific node (e.g., node 0)
        int startNode = 0;
        System.out.print("BFS traversal starting from " + startNode + ": ");
        graph.bfs(startNode);
    }
}
