#include <iostream>
#include <vector>
#include <string>

class Player {
protected:
    std::string name;
    int playerID;

public:
    Player(std::string name, int playerID) : name(name), playerID(playerID) {}

    virtual std::string getPlayerPosition() const = 0;
    virtual void play() const = 0;

    std::string getName() const {
        return name;
    }

    int getPlayerID() const {
        return playerID;
    }

    virtual std::string toString() const = 0;
};

class Offense : public Player {
public:
    Offense(std::string name, int playerID) : Player(name, playerID) {}

    std::string getPlayerPosition() const override {
        return "Offense";
    }

    void play() const override {
        std::cout << "Participates in offensive plays.\n";
    }

    std::string toString() const override {
        return "Offense Player: " + name + " (#" + std::to_string(playerID) + ")";
    }
};

class DefenseLineman : public Player {
public:
    DefenseLineman(std::string name, int playerID) : Player(name, playerID) {}

    std::string getPlayerPosition() const override {
        return "Defense Lineman";
    }

    void play() const override {
        std::cout << "Participates in defensive plays.\n";
    }

    std::string toString() const override {
        return "Defense Lineman: " + name + " (#" + std::to_string(playerID) + ")";
    }
};

class Quarterback : public Player {
public:
    Quarterback(std::string name, int playerID) : Player(name, playerID) {}

    std::string getPlayerPosition() const override {
        return "Quarterback";
    }

    void play() const override {
        std::cout << "Throws passes and manages offensive plays.\n";
    }

    std::string toString() const override {
        return "Quarterback: " + name + " (#" + std::to_string(playerID) + ")";
    }
};

class Team {
private:
    std::vector<Player*> players;

public:
    void addPlayer(Player* player) {
        players.push_back(player);
    }

    void displayTeam() const {
        for (const auto& player : players) {
            std::cout << player->toString() << " - " << player->getPlayerPosition() << "\n";
        }
        std::cout << "Total players on the team: " << players.size() << "\n";
    }
};

int main() {
    Team myTeam;

    // Add players to the team
    myTeam.addPlayer(new Offense("Quarterback1", 1));
    myTeam.addPlayer(new DefenseLineman("DefensiveLineman1", 2));
    myTeam.addPlayer(new Quarterback("Quarterback2", 3));

    // Display team information
    myTeam.displayTeam();

    return 0;
}
