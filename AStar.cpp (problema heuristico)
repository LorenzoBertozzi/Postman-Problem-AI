#include <iostream>
#include <vector>
#include <queue>
#include <unordered_set>
#include <unordered_map>
#include <cmath>

using namespace std;

// Define a estrutura para representar um estado
struct State {
    string city;
    int cost;
    vector<string> path; // Caminho até o estado atual

    State(string _city, int _cost, const vector<string>& _path)
        : city(_city), cost(_cost), path(_path) {}

    bool operator>(const State& other) const {
        // Prioriza estados com menor custo total (custo acumulado + heurística)
        return cost > other.cost;
    }
};

// Função heurística: distância em linha reta até Bucareste (h)
unordered_map<string, int> heuristic = {
    {"Arad", 366}, {"Bucharest", 0}, {"Craiova", 160},
    {"Drobeta", 242}, {"Eforie", 161}, {"Fagaras", 176},
    {"Giurgiu", 77}, {"Hirsova", 151}, {"Iasi", 226},
    {"Lugoj", 244}, {"Mehadia", 241}, {"Neamt", 234},
    {"Oradea", 380}, {"Pitesti", 100}, {"Rimnicu Vilcea", 193},
    {"Sibiu", 253}, {"Timisoara", 329}, {"Urziceni", 80},
    {"Vaslui", 199}, {"Zerind", 374}
};

// Função de custo: custo entre duas cidades (g)
unordered_map<string, unordered_map<string, int>> cost = {
    {"Arad", {{"Zerind", 75}, {"Timisoara", 118}, {"Sibiu", 140}}},
    {"Zerind", {{"Arad", 75}, {"Oradea", 71}}},
    {"Oradea", {{"Zerind", 71}, {"Sibiu", 151}}},
    {"Timisoara", {{"Arad", 118}, {"Lugoj", 111}}},
    {"Lugoj", {{"Timisoara", 111}, {"Mehadia", 70}}},
    {"Mehadia", {{"Lugoj", 70}, {"Drobeta", 75}}},
    {"Drobeta", {{"Mehadia", 75}, {"Craiova", 120}}},
    {"Craiova", {{"Drobeta", 120}, {"Rimnicu Vilcea", 146}, {"Pitesti", 138}}},
    {"Rimnicu Vilcea", {{"Sibiu", 80}, {"Craiova", 146}, {"Pitesti", 97}}},
    {"Sibiu", {{"Arad", 140}, {"Oradea", 151}, {"Rimnicu Vilcea", 80}, {"Fagaras", 99}}},
    {"Fagaras", {{"Sibiu", 99}, {"Bucharest", 211}}},
    {"Pitesti", {{"Rimnicu Vilcea", 97}, {"Craiova", 138}, {"Bucharest", 101}}},
    {"Bucharest", {{"Fagaras", 211}, {"Pitesti", 101}, {"Giurgiu", 90}, {"Urziceni", 85}}},
    {"Giurgiu", {{"Bucharest", 90}}},
    {"Urziceni", {{"Bucharest", 85}, {"Hirsova", 98}, {"Vaslui", 142}}},
    {"Hirsova", {{"Urziceni", 98}, {"Eforie", 86}}},
    {"Eforie", {{"Hirsova", 86}}},
    {"Vaslui", {{"Urziceni", 142}, {"Iasi", 92}}},
    {"Iasi", {{"Vaslui", 92}, {"Neamt", 87}}},
    {"Neamt", {{"Iasi", 87}}}
};

//definir destino da viagem
bool isGoalState(const State& state) {
    return state.city == "Bucharest";
}

void printPath(const vector<string>& path) {
    for (const auto& city : path) {
        cout << city << " -> ";
    }
    cout << "Goal\n";
}

int astar() {
    priority_queue<State, vector<State>, greater<State>> pq;
    unordered_set<string> visited;

    // Estado inicial
    State initialState("Arad", 0, {});

    pq.push(initialState);

    while (!pq.empty()) {
        // Pegar o estado com menor custo na fila de prioridade
        State currentState = pq.top();
        pq.pop();

        // Verificar se já visitou esse estado
        if (visited.find(currentState.city) != visited.end()) {
            continue;
        }

        // Adicionar estado à lista de visitados
        visited.insert(currentState.city);

        // Verificar se é o estado objetivo
        if (isGoalState(currentState)) {
            printPath(currentState.path);
            return currentState.cost;
        }

        // Expandir o estado
        for (const auto& neighbor : cost[currentState.city]) {
            int newCost = currentState.cost + neighbor.second;
            int heuristicCost = heuristic[neighbor.first];

            vector<string> newPath = currentState.path;
            newPath.push_back(currentState.city);

            // Adicionar vizinho à fila de prioridade
            pq.push(State(neighbor.first, newCost + heuristicCost, newPath));
        }
    }

    return -1; // Não encontrou uma solução
}

int main() {
    int cost = astar();

    if (cost != -1) {
        cout << "Custo total do caminho: " << cost << endl;
    } else {
        cout << "Não foi possível encontrar uma solução." << endl;
    }

    return 0;
}
