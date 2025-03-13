import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";

export default function LadderCompetitie() {
  const [players, setPlayers] = useState([
    { name: "Speler 1", score: 0 },
    { name: "Speler 2", score: 0 },
    { name: "Speler 3", score: 0 },
  ]);
  const [newScore, setNewScore] = useState({ name: "", score: "" });

  const updateScore = () => {
    if (!newScore.name || newScore.score === "") return;
    setPlayers((prev) => {
      const updated = prev.map((p) =>
        p.name === newScore.name ? { ...p, score: parseInt(newScore.score) } : p
      );
      return updated.sort((a, b) => b.score - a.score);
    });
    setNewScore({ name: "", score: "" });
  };

  return (
    <div className="max-w-lg mx-auto p-4">
      <h1 className="text-xl font-bold mb-4">Laddercompetitie</h1>
      <Card className="p-4 mb-4">
        <h2 className="font-semibold mb-2">Score invoeren</h2>
        <Input
          placeholder="Naam speler"
          value={newScore.name}
          onChange={(e) => setNewScore({ ...newScore, name: e.target.value })}
          className="mb-2"
        />
        <Input
          placeholder="Nieuwe score"
          type="number"
          value={newScore.score}
          onChange={(e) => setNewScore({ ...newScore, score: e.target.value })}
          className="mb-2"
        />
        <Button onClick={updateScore}>Score bijwerken</Button>
      </Card>
      <Card>
        <CardContent>
          <h2 className="font-semibold mb-2">Ranglijst</h2>
          <ul>
            {players.map((p, index) => (
              <li key={index} className="mb-1">
                {index + 1}. {p.name} - {p.score} punten
              </li>
            ))}
          </ul>
        </CardContent>
      </Card>
    </div>
  );
}
