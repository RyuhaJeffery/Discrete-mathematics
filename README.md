# 21600223_WoonseonYu_hw5(Discrete-mathematics)

hw5

dijkstra.c source code

```c

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include "graph.h"

void d_matrix(graph_t *g)
{
    FILE *fp1;
    int edge;
    int b[3];
    int i, j;

    fp1 = fopen("graph1.txt", "r");

    fscanf(fp1, "%d %d\n", &g->n_vertices, &edge);

    for (i = 0; i < edge; i++)
    {
        fscanf(fp1, "%d %d %d\n", &b[0], &b[1], &b[2]);

        if (g->w[b[0]][b[1]][0] > 0)
        {
            if (g->w[b[0]][b[1]][0] > b[2])
            {
                g->w[b[0]][b[1]][0] = b[2];
            }
        }
        else
        {
            g->w[b[0]][b[1]][0] = b[2];
        }

        g->m[b[0]][b[1]]++;
    }
    fclose(fp1);

    for (i = 0; i < g->n_vertices; i++)
    {
        for (j = 0; j <= i; j++)
        {
            g->w[i][j][0] = g->w[j][i][0];
            g->m[i][j] = g->m[j][i];
        }
    }

    for (i = 0; i < g->n_vertices; i++)
    {
        g->w[i][i][0] = 0;
    }
}

int bfs(graph_t *g, int start)
{
    int n_queue = 0;
    int queue[64];
    int head = 0;
    int tail = 0;
    int length[64] int visited[64];

    memset(visited, 0, sizeof(int) * 64);
    for (int i = 0; i < g->n_vertices; i++)
    {
        length[i] = g->w[0][i][0];
    }

    queue[tail++] = start;
    n_queue++;
    visited[start] = 1;
    while (n_queue > 0)
    {
        int curr = queue[head++];
        n_queue--;
        printf("%d\n", curr);

        for (int neighbor = 0; neighbor < g->n_vertices; neighbor++)
        {
            if (g->w[curr][neighbor][0] > 0)
            {
                if (visited[neighbor] == 0)
                {
                    queue[tail++] = neighbor;
                    n_queue++;
                    visited[neighbor] = 1;
                }
            }
        }
    }

    printf("The shortest paths connecting two vertices are %d", length[g->n_vertices]);
    return 1;
}

int main(int argc, char **args)
{
    graph_t *g;

    g = graph_read_stdin();

    if (argc != 3)
    {
        fprintf(stderr, "Too few arguments\n");
        return 1;
    }

    int start, end;

    start = atoi(args[1]);
    end = atoi(args[2]);

    if (start < 0 || g->n_vertices <= start ||
        end < 0 || g->n_vertices <= end)
    {
        fprintf(stderr, "Wrong arguments\n");
        return 1;
    }

    d_matrix(g);
    bfs(g, start);

    graph_free(g);
    return 0;
}
```


euler.c source code

```c
#include <stdio.h>
#include <stdlib.h>
#include "graph.h"

/*TODO: you can add functions as you want */
void d_matrix(graph_t *g)
{
    FILE *fp1;
    int edge;
    int b[3];
    int i, j;

    fp1 = fopen("graph1.txt", "r");

    fscanf(fp1, "%d %d\n", &g->n_vertices, &edge);

    for (i = 0; i < edge; i++)
    {
        fscanf(fp1, "%d %d %d\n", &b[0], &b[1], &b[2]);

        if (g->w[b[0]][b[1]][0] > 0)
        {
            if (g->w[b[0]][b[1]][0] > b[2])
            {
                g->w[b[0]][b[1]][0] = b[2];
            }
        }
        else
        {
            g->w[b[0]][b[1]][0] = b[2];
        }

        g->m[b[0]][b[1]]++;
    }
    fclose(fp1);

    for (i = 0; i < g->n_vertices; i++)
    {
        for (j = 0; j <= i; j++)
        {
            g->w[i][j][0] = g->w[j][i][0];
            g->m[i][j] = g->m[j][i];
        }
    }
}

void take_a_tour(graph_t *g, int start)
{
    int n_edges, next;
    int curr = start;
    int path[129] = {
        130,
    };
    i = 0;
    path[i] = curr;
    do
    {
        for (next = 0; next < g->n_vertices; next++)
        {
            if (g->m[curr][next] > 0)
                break;
        }
        if (next < g->n_vertices)
        {
            graph_remove_edge(g, curr, next);
            curr = next;
            path[++i] = 
        }
    } while (next != g->n_vertices);
    
    i = 0;
    printf("a sequence of vertex identifiers is ") do
    {
        printf("%d ", path[i]);
    }
    while (path[++i] < 130)
        ;
}

int main()
{
    graph_t *g;

    g = graph_read_stdin();

    /* TODO: implement here */
    d_matrix(g);
    take_a_tour(g, 0);

    graph_free(g);
    return 0;
}
```

[Presentation Video Link]()
