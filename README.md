# QueryCrate
A fun &amp; creative Q&amp;A study tool
import React, { useState } from 'react';
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";

const qaPairs = [
  { question: "What is the formula of water?", answer: "H₂O" },
  { question: "Who is the founder of Pakistan?", answer: "Quaid-e-Azam Muhammad Ali Jinnah" },
  { question: "What is the boiling point of water?", answer: "100°C or 212°F at 1 atm pressure" },
];

function App() {
  const [index, setIndex] = useState(0);
  const [showAnswer, setShowAnswer] = useState(false);
  const [filter, setFilter] = useState("");

  const filteredQAs = qaPairs.filter(pair =>
    pair.question.toLowerCase().includes(filter.toLowerCase())
  );

  const currentQA = filteredQAs[index] || {};

  const next = () => {
    if (index < filteredQAs.length - 1) {
      setIndex(index + 1);
      setShowAnswer(false);
    }
  };

  const prev = () => {
    if (index > 0) {
      setIndex(index - 1);
      setShowAnswer(false);
    }
  };

  return (
    <div className="p-6 max-w-xl mx-auto space-y-6">
      <h1 className="text-2xl font-bold text-center">📦 QueryCrate</h1>

      <Input
        placeholder="Search questions..."
        value={filter}
        onChange={e => {
          setFilter(e.target.value);
          setIndex(0);
        }}
      />

      <Card>
        <CardContent className="p-4 space-y-4">
          <p className="font-semibold">Q: {currentQA.question || "No question found."}</p>

          {showAnswer && <p className="text-green-700">A: {currentQA.answer}</p>}

          <div className="space-x-2">
            <Button onClick={() => setShowAnswer(!showAnswer)}>
              {showAnswer ? "Hide Answer" : "Show Answer"}
            </Button>
            <Button variant="outline" onClick={prev} disabled={index === 0}>Previous</Button>
            <Button variant="outline" onClick={next} disabled={index >= filteredQAs.length - 1}>Next</Button>
          </div>
        </CardContent>
      </Card>
    </div>
  );
}

export default App;
