import express from "express";
import fetch from "node-fetch";

const app = express();
const PORT = 3000;

app.get("/musicbrainz", async (req, res) => {
  const query = req.query.q;
  if (!query) return res.status(400).send({ error: "Missing query" });
  const url = `https://musicbrainz.org/ws/2/artist/?query=${encodeURIComponent(query)}&fmt=json`;
  const response = await fetch(url, {
    headers: { "User-Agent": "MITAppInventorExample/1.0 ( your_email@example.com )" }
  });
  const data = await response.json();
  res.json(data);
});

app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
