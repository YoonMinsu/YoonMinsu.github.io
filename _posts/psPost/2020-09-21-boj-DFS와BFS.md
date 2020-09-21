---
title   : "[BOJ] 1260번: DFS와 BFS"
excerpt : "PS"
categories : 
    - boj
tags : 
    - ps
    - dfs
    - bfs
sidebar:
    title: "BaekJoon"
    nav : sidebar-posts
---  

DFS와 BFS를 공부하는데 기초가 되는 문제다.  


``` java
import java.io.*;
import java.util.*;

class BaekJoon_1260 {
    private ArrayList<ArrayList<Integer>> list;
    private boolean[] visited;


    private void DFS(int v) {
        visited[v] = true;
        System.out.print(v + " ");
        for (int value : list.get(v)) {
            if (!visited[value]) {
                DFS(value);
            }
        } // end for
    }

    private void BFS(int v) {
        Queue<Integer> q = new LinkedList<>();

        visited[v] = true;
        q.offer(v);

        while (!q.isEmpty()) {
            int value = q.poll();
            System.out.print(value + " ");
            for (int vv : list.get(value)) {
                if (!visited[vv]) {
                    visited[vv] = true;
                    q.offer(vv);
                }
            }
        } // end while
    }

    public void run() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] line = br.readLine().split(" ");
        int n = Integer.parseInt(line[0]);
        int m = Integer.parseInt(line[1]);
        int v = Integer.parseInt(line[2]);

        visited = new boolean[n + 1];
        list = new ArrayList<>();
        for (int i = 0; i < n + 1; ++i) {
            list.add(new ArrayList<>());
        }

        for (int i = 0; i < m; ++i) {
            line = br.readLine().split(" ");
            int v1 = Integer.parseInt(line[0]);
            int v2 = Integer.parseInt(line[1]);

            list.get(v1).add(v2);
            list.get(v2).add(v1);
        } // end for

        for (int i = 1; i <= n; ++i) {
            Collections.sort(list.get(i));
        }

        DFS(v);
        Arrays.fill(visited,false);
        System.out.println();
        BFS(v);
    }
}

public class Main {
    public static void main(String[] args) throws IOException {
        new BaekJoon_1260().run();
    }
}

```